# useRef

## Reference

```jsx
const ref = useRef(initialValue);
```

- Hook allows reference a valut that's not needed for rendering
- `initialValue` is the value we want for the ref object's `current` property to be initially

  - value can be any type
  - argument is ignored after the initial render

- Hook returns an object with a single property - `current`
  - ref attribute to a JSX node will make React to add its `current` property

### Caveats

- `ref.current` is mutable
- ref is plain JavaScript object
- do not write or read `ref.current` during rendering, except for initialization
- Strict Mode calls component twice to check purity of the code

## Usage

### Referencing a value with a ref

- can store information between re-renders, unlike regular variables
- information is local to each copy of component

### Manipulating the DOM with a ref

- after React creates the DOM node and puts it on the screen, React will set the **current property** of ref object to the DOM node

  - then we can access the element's DOM node and call methods like `focus()`
  - React will set the current property back to null when the node is removed

  ```jsx
  function handleClick() {
    inputRef.current.focus();
  }
  ```
