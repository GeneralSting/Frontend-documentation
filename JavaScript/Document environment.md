# Document environment

`DOM API`

- JavaScript have limitations with manipulating web browser
  - centered around security
  - web APIs gives access to a lot of functionality

## Parts of a web browser

- `Window` is the browser tab that a web page is loaded into, `Window` object

  - `Window.innerWidth` & `Window.innerHeight`
  - event handlers can be attached to the current window

- `Navigator` represents the state and identity of the browser, `Navigator` object

  - can retreive things like the user's preferred language...

- `DOM` is actual page loaded into the window and is represented in `Document` object

### Document object model

- each entry in tree is called a `node`

#### Node

- `DOM Node` interface is an astract base class upon which many other DOM API objects are based by letting those object types to be used similarly and often interchangeably

  - there is no plain `Node` object, all objects that implement Node functionality are based on one of its subclasses

    - `Document`

    - `Element`

      - the most general base from which all element objects (objects that represent elements) in a `Document` inherit
      - `HTMLElement` interface is the base interface for HTML elements
        - `SVGElement` interface is the basis for all SVG elements
      - <b>Element -> Node -> EventTarget</b>

    - `DocumentFramgnet`
      - represents a minimal document object that has no parent
      - lightweight version of `Document` that stores a segment of a document structure comprised of nodes just like standard document
        - not part of the active document tree structure, changes made to the fragment do not affect the document
      - <b>DocumentFragment -> Node -> EventTarget</b>

- every kind of DOM node is represented by an iterface based on `Node`
- particular property/feature of the base `Node` interface may not apply to one of its child interfaces, inheriting node may return null or throw an exception
  <b>Node -> EventTarget</b>

##### Nodelist

- collections of `nodes` usually returned by properties such as `Node.childNodes` and methods such as `document.querySelectorAll()`

  - it is not an Array, it is possible to iterate over it with forEach()
    - it can be converted to a real Array using Array.from()

- `Live NodeLists`
  - changes in the DOM automatically update the collection
    - `Node.childNodes`
    ```js
    const parent = document.getElementById("parent");
    let childNodes = parent.childNodes;
    console.log(childNodes.length); // let's assume "2"
    parent.appendChild(document.createElement("div"));
    console.log(childNodes.length); // outputs "3"
    ```
- `Static NodeLists`
  - changes in the DOM do not affect the content of the collection
    - `document.querySelectorAll` returns a static NodeList

#### EventTarget

- interface implemented by objects that can receive events and may have listeners for them
- any target of events implements the three methods associated with this interface
  - `EventTarget.addEventListener()`
  - `EventTarget.removeEventListener()`
  - `EventTarget.dispatchEvent()`
- many events targets (elements, documents, windows...) also support setting event handlers via onevent properties and attributes
