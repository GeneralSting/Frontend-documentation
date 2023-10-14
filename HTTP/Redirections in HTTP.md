# Redirections in HTTP

- URL forwarding

## Principle

- triggered by a server sending a special redirect response to a request
  - status `codes start` with 3 and a `Location` header holding the URL to redirect to

## Types of redirects

### Permanent redirections

- original URL should no longer be used and replaced with the new one

| Code | Text               | Method handling                                                   | Typical case use            |
| ---- | ------------------ | ----------------------------------------------------------------- | --------------------------- |
| 301  | Moved Permanently  | `GET` methods                                                     | Reorganization of a website |
| 308  | Permanent Redirect | Method and body not changed, created when using non-`GET` methods | Reorganization of a website |

### Temporary redirections

- cannot be accessed from its canonical location, can be accessed from another place

| Code | Text               | Method handling                                                   | Typical case use                                                                                                                   |
| ---- | ------------------ | ----------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| 302  | Found              | `GET` methods                                                     | Temporary unavailable for unforeseen reasons                                                                                       |
| 303  | See Other          | `GET` methods                                                     | Used to redirect after a `PUT` or a `POST` so that refreshing the result page doesn't retrigger the operation                      |
| 307  | Temporary Redirect | Method and body not changed, created when using non-`GET` methods | The Web page is temporarily unavailable for unforeseen reasons. Better than 302 when non-GET operations are available on the site. |

### Special redirections

| Code | Text             | Typical case use                                                                                                                                        |
| ---- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 300  | Multiple Choices | Not many: the choices are listed in an HTML page in the body. Machine-readable choices are encouraged to be sent as `Link` headers with `rel=alternate` |
| 304  | Not Modified     | Sent for revalidated conditional requests. Indicates that the cached response is still fresh and can be used                                            |

- `300` (Multiple Choices) is a manual redirection: the body, presented by the browser as a Web page, lists the possible redirections and the user clicks on one to select it.

## Alternative way of specifying redirections

### HTML redirections

- &lt;`meta`&gt; element with `http-equiv` attribute set to `Refresh`
  - when displaying the page, the browser will go to the indicated URL
  - `content` attribute starts with number indicating how many seconds the browser should wait before redirecting to the given URL
  ```html
  <head>
    <meta http-equiv="Refresh" content="0; URL=https://example.com/" />
  </head>
  ```

### JavaScript redirections

```js
window.location = "https://example.com/";
```

## Order of precendece

1. HTTP redirects - they exist when there is not even a transmitted page
2. HTML redirects - &lt;`meta`&gt;
3. JavaScript redirects
