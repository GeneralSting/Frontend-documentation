# HTML element: link

## Attribute: rel

- rel attribute defines the relationship between a linked resource and the current document
  - valid on &lt;link&gt;, &lt;a&gt;, &lt;area&gt;, &lt;form&gt;

### the most important existing keywords

- <span style="color: #ffc75f">author</span>
  - author of the current document or article
- <span style="color: #ffc75f">icon</span>
  - icon representing the current document
- <span style="color: #ffc75f">stylesheet</span>
  - imports a style sheet

## Attribute sizes: :clock1:
  - This attribute defines the sizes of the icons for visual media contained in the resource. It must be present only if the `rel` contains a value of icon or a non-standard
  - values:
    - any: icon can be scaled to any size as it is in a vector format like image/svg+xml
    - white-space separated list of sizes

## Attribute: type
  - used to define the type of the content linked to. 
  - value of the attribute should be a MIME type such as text/html, text/css...