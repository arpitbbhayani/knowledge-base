Is REST all about just exposing an HTTP endpoint?

REST is an abbreviation that stands for Representational State Transfer. A lot of complex words but stick with me.

REST is a specification that suggests how a client should demand/request information from the server and how the server should respond; it does not enforce anything.

## Everything is a Resource

In REST, everything is a resource. Any actionable entity in your application eg: book, student, customer, or order is a resource for REST. The client can demand action on a resource like get, create, delete, or update.

REST does not put any restriction on how the data is stored in your application, but it allows clients to specify how it wants the data from the server eg: XML, JSON, CSV, etc. So long as the server supports the representation the server would respond in the demanded format.

## Underlying Protocol for REST

REST does not enforce any restriction on the underlying protocol to be used. All it cares about is that we have a defined way to act on a resource. So, we can implement REST over HTTP or even hardware like USB.

## Why REST over HTTP?

The most common implementation of REST is over HTTP and it gels very well together. Why so?

HTTP has verbs like GET, POST, DELETE, and PUT and these become actions on our resource. The resource is specified by the URL of the HTTP request. For example, to get a student's details whose `id = 1` we fire

```
GET /students/1
```

We are representing the student with `id = 1` using the URL `/students/1` and are specifying action `GET` using the HTTP verb `GET`. Similarly to update the student with `id = 1` we could

```
POST /students/1
```

Here we see how REST is resource-oriented and we have a way to specify the action to be taken on it.

### Existing tooling

One very important reason why HTTP is so commonly used in implementation is the availability of existing tooling. We can reuse the existing set of tools to get the job done, which includes.

- using existing HTTP Clients like Postman, cURL, Requests
- use caches like Ngnix, HA Proxy, and Varnish to boost performance
- use monitoring tools like Distributed Tracing
- use load balancers to uniformly distribute the load
- use SSL to get out-of-the-box security

## Downsides of doing REST over HTTP

- all clients would have to serialize and deserialize the HTTP body
- all clients would have to repetitively handle failures and retries
- some web servers might not support verbs like PUT, DELETE
- HTTP payloads are JSON and hence huge
- HTTP would not support switching underlying protocols