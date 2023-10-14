# HTTP security

## Content Security Policy (CSP)

- added layer of security that helps to detect and mitigate certain types of attacks
- to enable `CSP` set configuration of web server to return `Content-Security-Policy` HTTP header
- &lt;meta&gt; element can be used to configure a policy
  ```html
  <meta
    http-equiv="Content-Security-Policy"
    content="default-src 'self'; img-src https://*; child-src 'none';"
  />
  ```

### Threats

#### Mitigating cross-site scripting

- primary goal of CSP is to mitigate and report XSS attacks (`Cross-Site Scripting`)
  - victim's browser executes the malicious script because of source trust
  - allow to execute scripts loaded in source files received from allowed domains, ignoring all other scripts
  - sites that want to never allow scripts to be executed can opt to globally disallow script execution

#### Mitigating packet sniffing attacks

- `HTTPS`
- marking all cookies with the `secure` attribute
- `Strict-Transport-Secuirty` HTTP header
  - browsers are connected only over an encrypted channel

### Common use cases

```http
Content-Security-Policy: default-src 'self'
```

- allows content to come from the site's own origin
- excludes subdomains

```html
Content-Security-Policy: default-src 'self' example.com *.example.com
```

- trusted domain and all its subdomains

```html
Content-Security-Policy: default-src 'self'; img-src *; media-src example.org
example.net; script-src userscripts.example.com
```

- allows users of a web application to include images from any origin in their own content, but to restrict audio or video media to trusted providers, and all scripts only to a specific server that hosts trusted code.

<hr>

## Strict-Transport-Security

- HTTP `Strict-Transport-Security` response header informs browsers that the site should only be accessed using HTTPS
- The `Strict-Transport-Security` header is ignored by the browser when your site has only been accessed using HTTP. Once your site is accessed over HTTPS with no certificate errors, the browser knows your site is HTTPS capable and will honor the `Strict-Transport-Security` header. Browsers do this as attackers may intercept HTTP connections to the site and inject or remove the header.

## HTTP cookies

[HTTP cookies](https://github.com/GeneralSting/Frontend-documentation/blob/main/JavaScript/Client-side%20storage.md#using-http-cookies)

<hr>

## X-Content-Type-Options

- response header is a marker used by the server to indicate the `MIME types` adverised in the `Content-Type` headers should be followed and not be changed
- header allows to avoid `MIME type sniffing`

<hr>

## X-Frame-Options

- reponse header can be used to indicate wheater or not a browser should be allowed to render a page in &lt;`frame`&gt; &lt;`iframe`&gt; &lt;`embed`&gt; or &lt;`object`&gt;
  - sites can use this to avoid `click-jacking` attacks, by ensuring their content is not embedded into the other siets
  - two possible directives
    ```http
    X-Frame-Options: DENY
    X-Frame-Options: SAMEORIGIN
    ```
