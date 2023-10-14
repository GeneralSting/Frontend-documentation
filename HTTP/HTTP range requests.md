# HTTP range requests

- request asks the server to send only a portion of an HTTP message back to a client
- checking if a server supports partial requests - `Accept-Ranges` with value anything other than "none"
  ```http
  HTTP/1.1 200 OK
  …
  Accept-Ranges: bytes
  Content-Length: 146515
  ```

## Single part ranges

- `Content-Length`
  - can indicates the size of the requested range and not the full size of file
- `Content-Range`
  - response header indicates where in the full resource this partial message belongs for

## Multipart ranges

`Range` header allows us to get multiple ranges at once in multipart document

```bash
curl http://www.example.com -i -H "Range: bytes=0-50, 100-150"
```

- `206 Partial Content` status and `Content-Type` header indicates that other multipart follows
- each part contains its own `Content-Type` nad `Content-range`
