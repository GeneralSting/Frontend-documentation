# forwardRef

## Reference

```jsx
const SomeComponent = forwardRef(render);
```

- API allows component to expose a DOM node to parent component with a **ref**
- `render` parameter is the render function, React calls this function with the props and `ref` that our component received from its parent
  - returned JSX will be the output of our component
  - React calls render function with `props` and `ref` parameters
    - `props` parameter is passed props by the parent component
    - `ref` parameter is the `ref` attribute passed by the parent component. `ref` can be object or a function, if the parent component has not passed a ref it will be `null`. Pass either `ref` received to another component or pass it to `useImperativeHanle`
- API returns a React component that we can render in JSX

  - unlike a plain defined functions, a component returned by `forwardRef` also can receive a `ref` prop

  ```jsx
  const MyInput = forwardRef(function MyInput(props, ref) {
    return (
      <label>
        {props.label}
        <input ref={ref} />
      </label>
    );
  });
  ```

### Caveats

- in Strict Mode react calls render function twice - impurity check

## Usage

### Exposing a DOM node to the parent component

- by default, each component's DOM nodes are private
  - sometimes is useful to expose a DOM node to the parent, example, to allow focusing it
  - to opt in, wrap component definition into `forwardRef()`
  - render function's second argument is `ref` which needs to be passed to the DOM node

### Exposing an imterpative handle instead of a DOM node

- instead of exposing an entire DOM node, we can expose a custom object, called an **imperative handle**, with a more constrained set of methods - define a separate ref to hold the DOM node

  - pass the `ref` received to `useImperativeHandle` and specify the value we want to expose to the `ref`
  - in the example below: if some component gets a ref to `MyInput`, it will only receive our { focus, scrollIntoView } object insted of the DOM node - limited information exposed about our DOM node

  ```jsx
  const MyInput = forwardRef(function MyInput(props, ref) {
    const inputRef = useRef(null);

    useImperativeHandle(
      ref,
      () => {
        return {
          focus() {
            inputRef.current.focus();
          },
          scrollIntoView() {
            inputRef.current.scrollIntoView();
          },
        };
      },
      []
    );

    return <input {...props} ref={inputRef} />;
  });
  ```

- Pitfall :warning:
  - do not overuse refs. Use it only for imperative behaviors what cannot be expressed as props
    - scrolling to a node
    - focusing a node
    - triggering an animation
    - selecting text...
  - if we can express something as a prop, do not use ref then
    - Effects can help to expose imperative behaviors via props
