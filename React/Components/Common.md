# Common

## Props

- these special React props are supported for all built-in components:
  - **children** - React node (an element, string, number, portal, empty node like `null`, `undefined` and booleans, or an array of other React nodes)
    - specifies the content inside the component
  - **dangerouslySetInnerHTML** - object of the form `{ __html: '<p>some html</p>' }` with a raw HTML string inside
    - overrides the `innerHTML` property of the DOM node and displays the passed HTML inside
    - used with extreme caution - risk of XSS vulnerability
  - **ref** - ref object from `useRef`, `createRef`, or a `ref` callback function, or a string for legacy refs
    - ref will be filled with the DOM element (node)
  - **suppressContentEditableWarning** - boolean, suppresses the warning that React shows for elements that both have **children** and **contentEditable={true}** (which normally do not work together)
    - used with building a text input library that manages the contentEditable content manually
  - **suppressHydrationWarning** - boolean, if server rendering is used, normally there is a warning when the server and the client render different content
    - in some rare cases (like timestamps), it is very hard or impossible to guarantee an exact match
      - if we set `suppressHydrationWarning` to true, React will not warn we about mismatches in the attributes and the content of that element. It only works one level deep, and is intended to be used as an escape hatch. Don't overuse it
  - **style** - an object with CSS styles, similarly to the DOM `style` property
    - CSS property names need to be written as `camelCase`
    - passed number will automatically get `px`, pixels to the value (added by React) unless it's a unitless property
    - use `style` only for dynamic styless where we don't know the styles value ahead - **applying plain CSS classes with `className` is more efficient**
