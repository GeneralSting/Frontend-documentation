# HTTP messages

- `HTTP/2` binary framing mechanism does not require any alteration of the APIs of config files applied
  - broadly transparent to the user
- requests and responses share similar structure
  1. start line describing the request, or status
  - single line
  2. optional set of HTTP headers
  3. blank line indicating all meta-information for the request has been sent
  4. optional body

![HTTP message structure](https://documentation.help/DogeTool-HTTP-Requests-vt/http_responsemessageexample.png)

## HTTP requests

### Start line

1. `HTTP method` that describes the action to be performed
2. `request target` - URL

- absolute path followed by '?' and query string
  - common for GET, POST, HEAD, OPTIONS
- complete URL - absolute path
  - common for GET when connected to a proxy
- setting HTTP tunel - port
  - ':'
  - CONNECT
- '\*' used with OPTIONS representing the server as a whole

3. HTTP version - defines the structure of the remaining message

### Headers

- case-insensitive string
- `General headers`
  - apply to the message as a whole
- `Request headers`
  - that can be used in an HTTP request to provide information about the request context, so that the server can tailor the response
  - `Accept` header idnicate the allowed and preferred formats of the response
- `Representation headers`
  - describe the original format of the message data and any encoding applied
  - `Content-Type`

![request header groups](https://developer.mozilla.org/en-US/docs/Web/HTTP/Messages/http_request_headers3.png)

### Body

- fetching resources
- with `PUT`, `POST` methods
- two categories
  1. single-resource bodies
  - one single file
  - defined by two headers - `Content-Type` and `Content-Length`
  2. multiple-resource bodies
  - multipart body, each containing a different bit of information
  - HTML forms

## HTTP Response

### Status line

1. protocol version
2. status code
3. status text

### Headers

- `General headers`
- `Response headers`
  - additional information about the server which doesn't fit in the status line
  - `Accept-Ranges`
- `Representation headers`
  - describes the original format of the message data and any encoding applied
  - `Content-Type`

### Body

- three categories
  1. single-resource bodies consisting of a single file of known length
  2. single-resource bodies consisting of a single file of unknown lenght
  3. multiple-resource bodies
