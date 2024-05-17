# HTTP

- `Hypertext Transfer Protocol` is an `application-layer` protcol for trasnmitting hypermedia documents
  - sent over `TCP` or over `TLS`-encrypted TCP connection
- follows a classical `client-server model`
  - client opening a connection to make a request
  - client receives a response from server
- `stateless protocol`
  - server does not keep any data (state) between two requests

## Components of HTTP-based systems

- each individual request is sent to a server, which handles it and provides the response
  - between the client and the server there are numerous entitites, collectively called `proxies`
- layered design of the Web, HTTP is on top, at `applicaiton layer`

### Client

1. requests document that represents the page
2. parses received files
3. make additional requests corresponding to execution scripts, layout information (CSS) to display and sub-resources
4. combines these resources to present the complete document - Web page

- Web page is a hypertext document
  - means that page can lead to other pages, fetch a new Web page
  - browser translates directions into HTTP request and interprets the HTTP response

### Web server

- serves the requested document - response

### Proxies

- can be transparent
- non-transparent
  - changes request in some way before passing it along to the server
- caching
- fitlering
- load balancing (allow multiple servers to serve different requests)
- authentication (control access to different resources)
- logging (storage of historical information)

## Basic aspects

### HTTP is simple

- generally designed to be simple human-readable
  - even with complexity in HTTP/2 by encapsulating HTTP messages into frames

### HTTP is extensible

- `HTTP headers` makes protocol easy to extend

### HTTP is stateless, but not sessionless

- there is no link between two requests on the same connection
- `HTTP cookies` allow the use of stateful sessions
  - sharing same data

### HTTP and connections

- connection is controlled at the transport layer
  - out of scope for HTTP
- `TCP` connection-based transport protocol
  - before exchanging HTTP request/response pair TCP connection must be established
  - HTTP/2 multiplexing messages over a single TCP connection

### What can be controlled by HTTP

- caching
  - how documents are cached
  - server instructs proxies and clients about what to cache
- relaxing the origin constraint
  - enforce strict separation between websites
  - only pages from the <b>same origin</b> can access all the information of a Web page
    - HTTP headers can relax this strcit separation on the server side
- authentication
  - `HTTP cookies`
  - `WWW-Authenticate`
    - response header
    - defines methods called "challenges"
    - server will respond with `401-Unauthorized` for protected resource
    - client sends `Authorization` header to supply the credentials to the server - encoded for the selected "challenge" authentication method.
      -  `WWW-Authenticate` header. This header indicates what authentication schemes can be used to access the resource (protected routes)
    - &lt;auth-scheme&gt;, realm, token68
- proxy and tunneling
  - server and client hides true IP address
    - HTTP goes through proxies to cross this network barrier
    - not all proxies are HTTP proxies
- sessions
  - link requests with the state of the server
  - creates sessions
  - `HTTP cookies`

### HTTP flow

1. open a TCP connection
  - requests-responses
  - open new connection, reuse existing, open several TCP connections
2. send an HTTP message
    ```
    GET / HTTP/1.1
    Host: developer.mozzila.org
    Accept-Language: fr
    ```
3. read the response sent by the server
  ```
  HTTP/1.1 200 OK
  Date: Sat, 09 Oct 2010 14:28:02 GMT
  Server: Apache
  Last-Modified: Tue, 01 Dec 2009 20:18:22 GMT
  ETag: "51142bc1-7449-479b075b2891b"
  Accept-Ranges: bytes
  Content-Length: 29769
  Content-Type: text/html

  <!DOCTYPE html>… 
  ```
4. close or reuse the connection for further requests

### HTTP messages

- HTTP/2 has messages embedded into binary structure
  - frames allowing optimizations like compression of headers and multiplexing

#### Requests

- `HTTP method`
  - defines the operation the client wants to perform
  - `GET`
  - `POST`
  - `OPTIONS`
- `the path of the resource`
  - without protocol (http://), domain (developer.mozzila.org), or TCP port (80)
- `version of the HTTP protocol`
- `optional headers`
  - additional information for the servers
- `body`
    - sent resource

#### Response

- `version of the HTTP protcol`
- `status code`
- `status message`
  - short description of the status code
- `HTTP headers`
  - like those for requests
- `body`
  - containing fetched resource
  - optionally
