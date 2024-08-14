# Fetch API

- provides an interface for fetching resources (including across the network)
  - more powerful and flexible replacement form `XMLHttpRequest`

## Concepts and usage

- API uses `Request` and `Response` objects and other things involved with network requests, as well as related concepts such as **CORS** and **HTTP Origin** header semantics

- for making request and fetching a resource, `fetch()` method is used

  - it is global method in both `Window` and `Worker` contexts

- fetch() method takes one mandatory argument, the path to the resource we want to fetch.

  - returns a `Promise` that resolves to the `Response` to that request - as soon as the server responds with headers - event if the server response is an HTTP error status
  - optional `init` options object as second argument for Request object

- once a Response is retrieved, there are a number of methods available to define what the body content is and how it shoudl be handled

## Fetch interfaces

- fetch()
- Headers
  - represents response/request headers, allowing to query them and take different actions depending on the result
- Request
- Response

## Using the Fetch API

- making HTTP requests and processing the responses
- replacement for XMLHtppRequest which uses callbacks

  - fetch is `promise-based` and is integrated with features of the modern web such as **service workers** and **Cross-Origin Resource Sharing (CORS)**

- minimal function that uses fetch() to retrieve some JSON data from a server:

  ```js
  async function getData() {
    const url = "https://example.org/products.json";
    try {
      const response = await fetch(url);
      if (!response.ok) {
        throw new Error(`Response status: ${response.status}`);
      }

      const json = await response.json();
      console.log(json);
    } catch (error) {
      console.error(error.message);
    }
  }
  ```

- fetch() function will reject the promise on some errors, but not if the server responds with an error status like `404` - so we also check the response status and throw if it is not OK
  - otherwise we fetch the response body content as JSON by calling the `json()` method of Response object
    - **like fetch() itself, json() is asynchronous, as are all other methods to access the response body content**

### Making a request

#### Setting a body

- the request body is the payload of the request
- supply the body as an instance of any of the following types:

  - string
  - ArrayBuffer
  - TypedArray
  - DataView
  - Blob
  - File
  - URLSearchParams
  - FormData

- just like response bodies, request bodies are streams, and making the request reads the stream, so if a request contains a body we cannot make it twice - cannot be cosumend twice
  - instead we should **create a clone** of the request before sending it
    - `clone()` method of the Request interface creates a copy of the current Request object
    - clone() throws **TypeError** if the request body has already been used - main reason the clone() exists is to allow multiple uses of body objects, when they are onse-use only

#### Making cross-origin requests

- whether a request can be made cross-origin or not is determined by the value of the `mode` option, values can be:
  - `cors` - by default, meaning if the request is cross-origin then it will use the CORS mechanism
    - if the request is a `simple request` then the request will always be sent, but the server must respond with the correct `Access-Control-Allow-Origin` header or the browser will not share the response with the caller
    - if the request is not a simple request, then the browser will send a preflighted request to check that the server understands CORS and allows the request, real request won't be sent unless the server responds to the preflighted request with the appropiate CORS headers
  - `same-origin` disallows cross-origin requests completely
  - `no-cors` means the request must be a simple request, which restricts headers that may be set, and restricts methods to `GET`,`hEAD` AND `POST`

#### Including credentials

- credentials are cookies, TLS client certificates, or authentication headers containing a username and password
- to control whether or not the browser sends credentials, as well as whether the browser respects any `Set-Cookie` response headers, set the credentials option, which can have values:
  - `omit` - never send credentials in the request or include credentials in response
  - `same-origin` - by default
  - `include` - always include credentials, even cross-origin

### Canceling a request

- create AbortController object and assign its AbortSignal to the request's `signal` property
  - call the controller's `abort()` method - rejects promise with an `AbortError` xception

### Handling the response

#### Checking the response type

- Responses have a `type` proeprty that can be:
  - `basic`: the request was a same-origin request
  - `cors`: the request was a cross-origin CORS request
  - `opaque`: the request was a cross-origin simple request made with **no-cors mode**
  - `opaqueredirect`: the request set the `redirect` option to `manual` and the server returned a `redirect status`

#### Reading the response body

- Response interface provides a number of methods to retrieve the entire body contents in a variety of different formats - all are async methods, returning a Promise which will be fulfilled with the body content
  - Response.arrayBuffer()
  - Response.blob()
  - Response.formData()
  - Response.json()
  - Response.text()

#### Streaming the response body

- request and response bodies are actually `ReadableStream` objects, and whenever we read them, we are streaming the content

  - **ReadableStream** interface of the `Streams API` represents a readable stream of byte data

  - good for memory efficiency, because the browser does not have to buffer the entire response in memory before the caller retrieves it using a method like json()
  - this means that the caller can process the content incrementally as it is received - process chunks of the body as they are received from the network

    - iterate asynchronously over the stream, processing each chunk as it arrives

      ```js
      const url = "https://www.example.org/a-large-file.txt";

      async function fetchTextAsStream(url) {
        try {
          const response = await fetch(url);
          if (!response.ok) {
            throw new Error(`Response status: ${response.status}`);
          }

          const stream = response.body.pipeThrough(new TextDecoderStream());
          for await (const value of stream) {
            console.log(value);
          }
        } catch (e) {
          console.error(e);
        }
      }
      ```

- when we access the body directly, we get the raw bytes of the reponse and must transform it yourself - call `ReadableStream.pipeThrough()` to pipe the response through a `TextDecoderStream` which decodes the UTF-8-encoded body data as text
