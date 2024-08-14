# Client-side storage
- JavaScript APIs that allows to store data on the client, user's machine and retrieve it when needed

## Using HTTP cookies
- `HTTP cookie` (web cookie, browser cookie) is msall piece of data that a server sends to a web browser
  - used to tell if two requests come from the same browser
  - remembers stateful information for the `stateless HTTP protocol`

### Creating cookies
1. after receiving an HTTP request, server sends one or more `Set-Cookie` headers in the response
2. browser stores the cookie and sends it with request made to the same server inside a `Cookie` HTTP header
  - specify expiration date
  - specify additional restrictions

#### Set-Cookie & Cookie headers
- HTTP: Set-Cookie: &lt;cookie-name&gt;=&lt;cookie-value&gt;
- `HTTP` server response with instructs to tell the client to store a pair of cookies
  ```
  HTTP/2.0 200 OK
  Content-Type: text/html
  Set-Cookie: name1=value1
  Set-Cookie: name2=value2

  [page content]
  ```
  - browser sends all previously stored cookies back to the server using `Cookie` header
    ```
    GET/sample_page-html HTTP/2.0
    Host: www.example.org
    Cookie: name1=value1; name2=value2
    ```

#### Define the lifetime of a cookie
- `session cookies`
  - deleted when session ends
  - browsers can use session restoring when restarting - causing session cookies to last indefinitely
- `permanent cookies`
  - deleted at a specified date by the `Expires` attribute, or after a period of time specified by the `Max-Age` attribute
    ```
    Set-Cookie: id=13f"a; Expires=Thu, 31 Oct 2024 07:28:99 GTM;
    ```
    - expiring cookie is set on client not the server

#### Restrict access to cookies
- `Secure` attribute
  - encrypted request over the HTTPS protocol
  - disables man-in-the-middle attackers
- `HttpOnly` attribute
  - inaccessible to the JavaScript `Document.cookie API`
  - only sent to the server
    - persists in server-side sessions
    - don't need to be available to JavaScript
    - mitigage cross-site-scripting (`XSS`) attacks
  ```
  Set-Cookie: id=13f"a; Expires=Thu, 31 Oct 2024 07:28:99 GTM; Secure; HttpOnly
  ```

#### Define where cookies are sent
- `Domain` attribute
  - not specified means default domain is the same host, excluding subdomains
- `Path` attribute
  - URL path that must exist in the requested URL in order to send the `Cookie` header
- `SameSite` attribute 
  - lets servers to specify wheather/when cookies are sent with cross-site requests

#### JavaScript access using Document.cookie
- `Document.cookie` property
- can access existing cookies from JavaScript if the `HttpOnly` flag is not set
- cookies created via JavaScript can't include `HttpOnly` flag

<hr>

## Web Storage API
- provides mechanisms by which browsers can store key/value pairs
- `sessionStorage`
  - available for the duration of the page session
  - data stored until the browser or tab is closed
  - data is never transfered to the server
  - storage limit is 5MB
- `local storage`
  - persists even when the browser is closed and reopened
  - gets cleared through JavaScript, or clearing the browser cache / Locally Stored Data

- mechanisms are available via the `Window.sessionStorage` and `Window.localStorage` properties 
  - `Window` object implements `WindowLocalStorage` and `WindowSessionStorage`
  - calling creates an instance of the `Storage` object
    - different Storage object for `sessionStorage` and `localStorage`

## IndexedDB API
- low-level API with significant amounts of structured data
  - files/blobs
- uses indexes to enable high-performance data search
- useful for storing larger amounts of structured data

### Key concepts
- transactional database system, like RDBMS SQL but orienterd on JavaScript-based object-oriented database
- operations are done asynchronously

### Interfaces
- `open()`
  - get access to a database on the indexedDB attribute of a `window` object
  - returns `IDBRequest` object
  - async operations communicate to the calling app by firing events on `IDBRequest` objects

<hr>

## Cache API
- designed for storing HTTP responses to specific requests
  - storing assets offline