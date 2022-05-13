What are Remote Procedure Calls? How were they conceptualized? and Why are people adopting them? Here's why 👇‍

The two services need to communicate with each other so as to get things done. The most common way to do it today is to make a REST call over HTTP to the other service.

With this approach, every service needs to write logic to make HTTP call to the other service and handle things like failures, retries, compression, and security. Can we not abstract these complexities in some way?

RPCs were conceptualized to solve this problem.

# Remote Procedure Calls

RPCs are designed to make remote network calls look and feel like local procedures. They abstract out all the complexities of remote invocations like Marshalling, Unmarshalling, Compressions, Retries, Security, etc.

RPCs achieve this level of coherence using Stubs that sit in between the two services and convert incoming and outgoing packets into native objects.

# Stubs

Stubs are the common piece of auto-generated code that defines the interface, in a given language, exposed by the server, and used by the client to consume the data.

The interface is defined in a common language like Protobuf and holds the information about functions that the server exposes and the request response object types. A generator is shipped with the RPC runtime that would take this interface and generate code in the target language.

For example, if the Auth service is written in Golang, the generator would generate a working code with the interface along with the transport details. This way, we can solely focus on writing the business logic and not worry about the network or other repetitive things.

# Communication RPC

RPC can use any transport protocol for communication - Raw TCP, UDP, HTTP 1.1, or even HTTP 2. The transport is just a way through which the marshaled information will be sent across systems; and depending on the features an RPC runtime plans to support, an appropriate protocol will be chosen.

# Advantages of using RPC

- easy to use
- strong API contract
- remote invocations are just local function calls
- cross language communication is a breeze
- mundane tasks like retries, compression, etc are abstracted
- get performance out-of-the-box - streaming, connection pool
- security is just a plug
- no need to write client libraries, they can be auto-generated

# Concerns while adopting RPC

- stubs need to be re-generated whenever the signature changes
- testing RPC is n trivial for beginners
- getting started can be a little challenging
- browser support for RPC is pretty limited