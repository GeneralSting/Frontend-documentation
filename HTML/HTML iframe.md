# HTML iframe element
&lt;`iframe`&gt; elements are designed to allow you to embed other web documents into the current document
  - third-party content which cannot be controlled


## Attributes
- <span style="color: #ffc75f">border</span>
  - by default browsers display with surrounding border
- <span style="color: #ffc75f">allowfullscreen</span>
  - fullscreen mode using the `Fullscreen API`
- <span style="color: #ffc75f">src</span>
  - for video and img elements
- <span style="color: #ffc75f">border</span> <span style="color: #ffc75f">height</span> & 
  - iframe width and height
- <span style="color: #ffc75f">sandbox</span>
  - security settings

## Security concerns
- iframes are a common target (`attack vector`)
  - security mechanisms
    - only embed when necessary
    - use HTTPS
      1. reduces the chance that remote content has been tampered with in transit
      2. prevents embedded content from accessing content in document
    - always use the <span style="color: #ffc75f">sandbox</span> attribute
      1. gives only the permissions needed for doing its job
    - configure CSP directives
      - `content security policy` provides a set of HTTP Headers (metadata) designed to improve the security of document.
      - configure your server to send an appropriate `X-Frame-Options` header which prevent other websites from embedding your content in their web pages