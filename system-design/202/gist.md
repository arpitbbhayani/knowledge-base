Dropbox has to render a lot of thumbnails when we browse a folder containing a bunch of images. Here's how they serve them efficiently at scale.

## Simple approach

Thumbnail is created for each image present in a Dropbox folder and uploaded to a blob store like s3 or hdfs. Each thumbnail thus has a path using which it can be fetched on the client and shown to the end user.

A simple approach to serve thumbnails is to send thumbnail URLs in an API response to the client and as the user scrolls through them, we keep fetching the images and render them.

This sounds good in theory but gives a very sluggish experience in practice; because of the browser limitation. Every browser caps the maximum number of concurrent connections it can make to a domain.

This limit is 6 for chrome and 8 for firefox, which means at max the browser will be able to fetch 6 images at a time (at best). When there are many photos to render, the experience becomes sluggish as the user will need to scroll and wait for the photos to load.

## Dropbox's Solution

> Note: This is HTTP/1.1 based solution; you can do a lot more if you are using HTTP/2

### Batching Requests

Expose an endpoint (GET) that accepts multiple thumbnail paths as query parameters. 

```
GET https://photos.dropbox.com/tbatch?paths=1.png,2.png
```

The server upon receiving this request goes to the blob store and grabs the thumbnails. It then converts the thumbnails in Base64 and puts them in a text response.

The server then sends this response, containing base64 encoded image data of multiple images, back to the client. The client then identifies the image and its base64 data and renders it.

### Chunked Transfer Encoding

The server need not wait to get image data of all the requested images before it can send the response; instead, it uses chunked transfer encoding to stream a partial response to the client.

The server gets the request and it initiates the fetching of thumbnails in parallel. As and when it receives image data, it creates a chunked response and sends it to the client.

A chunked response is a text file that looks like this

```
0: data:image/jpeg;base64, <image data>
2: data:image/jpeg;base64, <image data>
11: data:image/png;base64, <image data>
```

Once it has completed sending the response for all the images, it sends the terminating response informing the client that the entire response is sent, and closes the connection.