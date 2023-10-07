# Document and website structure

## Basic sections of a document

- `header`
  - &lt;header&gt;
    - global header of parent element
- `navigation bar`
  - &lt;nav&gt;
    - main navigation functionality for the page
- `main content`
  - &lt;main&gt;
    - unique
		- one per page
		- shouldn't be nested
  - &lt;article&gt;
    - block of related content that makes sense on its own without the rest of the page
  - &lt;section&gt;
    - grouping together a single part of the page that constitutes one single piece of functionality
		- more sections in one article
- `sidebar`
  - &lt;aside&gt;
    - content not directly related to the main content
    - provides additional information
- `footer`
  - group of end content for a page

### Non-semantic wrappers
  - &lt;div&gt;
    - block element
  - &lt;span&gt;
    - inline element