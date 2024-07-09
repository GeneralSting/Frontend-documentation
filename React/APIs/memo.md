# memo

## Reference

```jsx
const MemoizedComponent = memo(SomeComponent, arePropsEqual?)
```

- API allows to skip re-rendering a component when its props are unchanged
- `Component` parameter is the component we want to memoize
  - `memo` does not modify this component, but returns a new, memoized component instead
  - any valid React component including functions and `forwardRef` components is accepted
- optional `arePropsEqual` is a funciton that accepts two arguments - component's previous props and its new props

  - `Object.is` comparison - `true` if the old and new props are equal

- `memo` returns a new React component - component behaves the same except that React will not always re-render it when its parent is bein re-rendered unless its props have changed

## Usage

### Skipping re-rendering when props are unchanged

- rely on `memo` as a performance optimization
- don't use `memo` everywhere

  - there is no significant hard but there is also no benefit to wrap every component

- `Object.is` comparison

### Specifying a custom comparison function

- in rare cases we can add "arePropsEqual" function as the comparison method
  - this will replace React's shallow equality
  - function should return true or false
  - using custom function we must compare every prop, including function - we should avoid deep equality checks (it can slow and freeze the app)
