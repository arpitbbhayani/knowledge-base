Can we send the payload in an HTTP GET request? [ in a gist ]

It is a common myth that we could not pass the request body in the HTTP GET request. HTTP 1.1 specification neither enforces nor suggests this behavior.

This means it is up to implementing the application web servers - Flask, uWSGI, etc. - to see if it parses the request body in the HTTP GET request. To do this, just check the request object you would be getting in your favorite framework.

⚡ What can we do with this information?

Say you are modeling an analytics service like Google Analytics in which you are exposing an endpoint that returns you the data point depending on the requirements. The requirements specified here could be a large, complex JSON.

Passing this query in the URL of the GET request as a query param is not convenient as it would require you to serialize and escape the JSON string before passing.

This is a perfect use case where the complex JSON query can be passed as a request body in the HTTP GET request, giving a good user experience.

⚡ So, does any popular tool uses this convention?

Yes. ElasticSearch - one of the most popular search utilities, uses this convention.

The search endpoint of ElasticSearch is a GET endpoint where the complex search queries in JSON format are sent in the request payload.