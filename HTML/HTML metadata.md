# HTML metadata

- head of an HTML document is the part that is not displayed in the web browser when the page is loaded.

## HTML head
- content inside &lt;`head`&gt; element
- contains `metadata` about the document

### Metadata
- &lt;`meta`&gt;
- describes data, of a document
  - attribute charset: specifying document's character encoding
    ```js
    <meta charset="utf-8" />
    ```

  - attrbiute <b>name</b>: specifies the type of meta element it is, what type of information it contains
  - attribute <b>content</b>: specifies the actual meta content
    ```js
    <meta name="description" content="keywords">
    ```
  - attribute author
  - attribute <b>description</b>: includes keywords relating the content of page
    - can make page to appear higher in relevant searches - `SEO, Search Engine Optimization`

- metadatas <b>Open Graph Data</b> and <b>Twitter Cards</b> are protocol developed to provide richer metadata for websites
  - richer user experience
  - on Twitter and Facebook users can se for example: website's image and description

### Applying CSS and JavaScript to HTML
- &lt;`link`&gt; element should always go isnide the head of document
  - attribute <span style="color:#ffc75f">rel</span>, with value stylesheet - document is stylesheet
  - attribute <span style="color:#ffc75f">href</span>, contains path to styleseet file
  ```js
  <link rel="stylesheet" href="path-to-document" />
  ```

- &lt;`script`&gt; element should go into the head element
  - attribute <span style="color:#ffc75f">src</span> - path to JS file
  - attribute <span style="color:#ffc75f">defer</span> which instructs the browser to load the JavaScript after the page has finished parsing the HTML
  - `script` element is not void element, needs a closing tag
  ```js
  <script src="path-to-document" defer><script>
  ```

## Setting the primary language of the document
- `lang` attribute
  - document will be indexed more effectively by search engines, allowing it to to appear correctly in language-specific results
  ```js
  <html lang="en-US">
  ...
  </html>
  ```