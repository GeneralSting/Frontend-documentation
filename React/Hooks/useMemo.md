# useMemo

## Reference

```jsx
const cachedValue = useMemo(calculateValue, dependencies);
```

- Hook allows caching the result of a calculation between re-renders
- `calculateValue` function calculating the value that will be cached
  - it should be pure, without arguments, and return a value of any type
  - React calls function during the initial render, on next render we get same value or new result which React stores so it can be reused later (depends on dependencies)
- `dependencies` - list of all reactive values referenced inside of `calculateValue` code
  - React compares each dependency with its previous value using the `Object.is` comparison

### Caveats

- in Strict Mode React calls calculation function twice in order to help find accidental impurities
- React will not throw aray cached value unless there is a specific reason to do that

## Usage

### Skipping expeinsive recalculations

- rely on `useMemo` as a performance optimization only
  - most code is not expensive, but expensive code can be creating or looping over a thousands of objects
  - **1ms** or more is considered code that needs optimization
- Hook won't make first render faster, only helps skip unnecessary work on updates

### Where to add useMemo

- calculation put in `useMemo` is noticeably slow, and its dependencies rarely change
- props is passed to a component wrapped in `memo`
  - memoization allows component to re-render only when dependencies aren't the same
- `useEffect` dependency is `useMemo` calculation value

- code can become less readable, there is not other harm
- unnecessary memoizations:
  - component visually wraps other component, let it accept JSX as children, this way, when wrapper component updates its own state, React knows that its children don't need to re-render
- prefer local state and don't lift state up any further than necessary
- kepp rendering logic pure
- avoid unnecessary Effects that update state
  - most performance problems are caused by chains of updates originating from Effects

### Skipping re-rendering of components

- by default when component re-renders, React re-renders all of its children recusively

### Memoizing individual JSX nodex

```jsx
export default function TodoList({ todos, tab, theme }) {
  const visibleTodos = useMemo(() => filterTodos(todos, tab), [todos, tab]);
  const children = useMemo(() => <List items={visibleTodos} />, [visibleTodos]);
  return <div className={theme}>{children}</div>;
}
```

- example of code above: instead of wrapping `List` in `memo` we can wrap `<List/>` JSX node itself in `useMemo`
  - the behavior would be the same
  - if React sees the same exact JSX as during the previous render, it won't try to re-render component because JSX node are **immutable**. JSX node object could not have changed over time, so React knows it's safe to skip a re-render
    - Node object acutally need to be same object, not look same
  - manually wrapping JSX nodes is not convenient, conditionally wrapping is not possible - wrap components with `memo` instead of wrapping JSX nodes
