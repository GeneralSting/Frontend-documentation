# lazy

## Reference

```jsx
const SomeComponent = lazy(load);
```

- API allows to defer loading component's code until it is rendered for the first time
- `load` parameter is a function that returns a **Promise** or another _thenable_ (a Promise-like object with a `then` method)
  - React will not call `load` until the first time we attempt to render the returned component. After React first calls `load`, it will wait for it to reslove, and then render the resolved value's `.default` as a React component
  - both the returned Promise and the Promise's resolved value will be cached, so React will not call `load` more than once. If the Promise rejects, React will `throw` the rejection reason for the nearest Error Boundary to handle
    `load` function receives no parameters
- API returns a React component what we can render in our tree
  - while the code for the lazy component is still loading, attemptin to render it will suspend - use `<Suspend>`

## Usage

### Lazy-loading components with Suspense

```jsx
const MarkdownPreview = lazy(() => import("./MarkdownPreview.js"));

/*
 * ...
 */

<Suspense fallback={<Loading />}>
  <h2>Preview</h2>
  <MarkdownPreview />
</Suspense>;
```

- code relies on **dynamic** `import()` which might require support from bundler or framework
