GIPHY serves 10 billion GIFs every day, here's how it beautifully uses different features of CDN.

## What is CDN

Think of CDN as a geographically distributed cache; and just like any regular cache, it sits between the user and the origin.

For any request, if it has the data, it serves the response. If not, it hits the origin to grab the data, cache it, and then responds.

### Geographical Nearness

A key highlight of using a CDN is geographical nearness. Because the CDN servers are distributed worldwide, the request from a user is served from the nearest edge server giving an excellent UX.

## CDN for media content

This is a no-brainer application of CDN. Giphy serves all the media content like images and videos through CDN that sits transparently between the user and the origin (eg: S3).

## CDN for API responses

Apart from the media content, Giphy uses CDN to cache API responses of Search and Discover APIs like

- /v1/gifs/trending
- /v1/search?q=funny

It serves these APIs from CDN because the responses of these APIs do not change often; hence using CDN for this reduces the load on API servers.

## Route-specific TTL

Not all APIs or media objects need to be cached on CDN for the same amount of time. Hence Giphy configures different expirations for different types of APIs.

Media object endpoints are cached longer while trending API is cached for a shorter duration.

## Response-driven TTL

Sometimes, it is the backend server that should dictate for how long the response should be cached.

Hence, Giphy, in the HTTP response from the origin server provides `max-age` headers that tell CDN the TTL for the specific response. This gives finer control over key expiration.

## Cache invalidation by grouping

Giphy uses Surrogate Keys (tags) while caching endpoints on CDN. It helps in smarter cache invalidation, eg:

- invalidate API responses that contain a specific GIF
- invalidate API responses from an API key
- invalidate API responses where the query contains a particular query