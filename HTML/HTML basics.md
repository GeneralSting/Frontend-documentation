# HTML basics

## HTML: HyperText Markup Language

- most basic building block of the Web.
- defines the meaning and structure of web content
- `"Hypertext"` refers to links that connect web pages to one another.
  - links are a fundamental aspect of the web
- HTML uses `"markup"` to annotate content for display in a Web browser

  - `elements`

    - `void elements`: elements with no content
      - img

  - `tags`

### Anatomy of an HTML document

- &lt;`!DOCTYPE html`&gt;

  - `doctype`: required, preamble found at the top of all documents. Prevents a browser from switching into <b>quirks mode</b> when rendering a document
    - quirks mode
      - <b>quirks mode</b>, layout emulates behaviour in Navigator 4 and Internet Explorer 5
      - <b>no-quirks mode</b>, desired behaviour described by the modern HTML and CSS specifications
      - <b>limited-quirks mode</b>, small number of quirks implemented
    - form HTML documents, browsers use `DOCTYPE` in the beginning of the document to decide wheater to handle it in quirks mode or standards mode
    - only purpose is to activate <b>no-quirks mode</b>
    - the value of document.compatMode in JavaScript will show wheater or not the document is in quirks mode.
      - value: "BackCompat": document is in quirks mode
      - value: "CSS1Compat": document is not in quirks mode

- &lt;`html`&gt;&lt;/`html`&gt;
  - wraps all the content on the entire page
  - root element
  - lang attribute for setting the primary language of the document

- &lt;`head`&gt;&lt;/`head`&gt;
  - container for all the stuff on the HTML page that is not content.
  - keywords and a page description for search results

- &lt;`meta charset="utf-8"`&gt;
  - handles any textual content

- &lt;`meta name="viewport" content="width=device-width"`&gt;
  - <b>viewport element</b> ensure the page renders at the width of viewport, preventing mobiles browsers from rendering pages wider
    - mobile browsers render pages in a virtual window or viewport, generally at 980px, which is usually wider than the screen, and then shrink the rendered result down so it can all be seen at once
    - <b>width</b> property controls the size of the viewport. It should be set to <b>device-width</b>, which is the width of the screen in CSS pixels at scale of 100%. Other properties: <b>maximum-scale</b>, <b>minimum-scale</b> and <b>user-scalable</b>, which control weather users can zoom the page in or out.

- &lt;`title`&gt;&lt;/`title`&gt;
  - title of the page

- &lt;`body`&gt;&lt;/`body`&gt;
  - contains all the content that web shows to users.