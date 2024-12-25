# useImperativeHandle

## Reference

```jsx
useImperativeHandle(ref, createHandle, dependencies?)
```

- `useImperativeHandle` is a React hook that lets we customize the handle exposed as a **ref**
- reference: `useImperativeHandle(ref, createHandle, dependencies?)`
  - parameters
    - **ref** - ref we received as a prop to the our component
      - starting with `React 19`, ref is available a prop. In `React 18` and earlier, it was necessary to get the **ref** from `forwardRef`.
    - **createHandle** - function that takes no argument and returns the ref handle we want to expose
    - optional **dependencies** - the list of all reactive values referenced inside of the **createHandle** code
  - returns
    - returns `undefined`

## Usage

### Exposing a custom ref handle to the parent component

- to expose a DOM node to the parent element, pass in the ref prop to the node.
  - however, we can expose a custom value instead, To customize the exposed handle, call `useImperativeHandle`

### Exposing our own imperative methods

- the methods we expose via an imperative handle don’t have to match the DOM methods exactly

### Pitfall

- do not overuse refs
  - use refs for imperative behaviors that we can’t express as props: for example, scrolling to a node, focusing a node, triggering an animation, selecting text, and so on
