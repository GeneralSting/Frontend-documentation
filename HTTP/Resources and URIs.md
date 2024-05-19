# Resources and URIs

## Identifying resources on the Web

- the target of the HTTP request is called a "resource"

### URLs and URNs

#### URLs

- the most common form of `URI` is the `Unifrom Resource Locator` (URL), known as web address
  ```
  https://developer.mozilla.org
  https://developer.mozilla.org/en-US/docs/Learn/
  https://developer.mozilla.org/en-US/search?q=URL
  ```

#### URNs

- `Uniform Resource Name` identifies a resource by name in a particular namespace, without specifying its location or weather it exists
  - `www.example.com`

### Syntax of Uniform Resource Identifiers (URIs)

- http://www.example.com:80/path/to/myfile.html?key1=value1&key2=value2#SomewhereInTheDocument

#### Scheme or protocol

- `http://`

| Scheme     | DescriptionSavings           |
| ---------- | ---------------------------- |
| data       | Data URLs                    |
| file       | Host-specific file names     |
| ftp        | File Transfer Protocol       |
| http/https | Hyper text transfer protocol |
| mailto     | Electronic mail address      |
| ssh        | Secure shell                 |

#### Authority

- `www.example.com`
  - indicates which web server is being requested

#### Port

- `:80`
  - gate used to access the resources on the web server
  - 80 for HTTP
  - 443 for HTTPS

#### Path

- `/path/to/myfile.html`

#### Query

- `?key1=value1&key2=value2`

#### Fragment

- `#SomewhereInTheDocument`
  - "bookmark" inside the resource
  - fragment identifier
  - never sent to the server with the request

<hr>

## MIME types

- `IANA` media type (Multipurpose Internet Mail Extensions)
- Internet Assigned Numbers Authority is responsible for all official `MIME` types

### Structure of a MIME type

- type and subtype
  - type/subtype
  - type presents the general category
  - subtype identifies the exact kind of data of the speicfied type the MIME type represents
  - always has both a type and a subtype
  - optional parameter to provide additional details
    ```
    type/subtype;parameter=value
    text/plain;charset=UTF-8
    ```

#### Types

- discrete
  - single file or medium
  - application
  - audio
  - text
  - ...
- multipart
  - indicate a category of document broken itno pieces, often with different MIME types
  - they represent a composite document
  - multipart types
    - message
      - encapsulate other messages
      - breaking large message into smaller ones
    - multipart
      - multiple components, different MIME types
      - `multipart/form-data`
        - FormData API
        - As a multipart document format, it consists of different parts, delimited by a boundary (a string starting with a double dash --). Each part is its own entity with its own HTTP headers, `Content-Disposition`, and `Content-Type` for file uploading fields.
      - `multipart-byteranges`
        - When the `206 Partial Content` status code is sent, this MIME type indicates that the document is composed of several parts, one for each of the requested ranges. Like other multipart types, the `Content-Type` uses a boundary to separate the pieces. Each piece has a `Content-Type` header with its actual type and a `Content-Range` of the range it represents.

### MIME types

- application/octet-stream
  - default binary files
  - unknown binary file
  - browsers treat it as if the `Content-Disposition` header was set to `attachment`, and propose "Save As" dialog
- text/plain
  - default, unknown textual file
- text/css
- text/html
- text/javascript
  - `charset` parameter isn't valid for JavaScript content, and in most cases will result in a script failing to load

### MIME sniffing

- In the absence of a MIME type, or in certain cases where browsers believe they are incorrect, browsers may perform `MIME sniffing` — guessing the correct MIME type by looking at the bytes of the resource.

<hr>

## WWW

- `domain name`
- `domain name` is hosted on a server where the document resides
- offical domain is called the `canonical name`
  - 301 code error for redirecting
  - &lt;link rel="canonical"&lt;
    - tells search engine crawlers where the page actually lives
