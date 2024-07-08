# useCallback

## Reference

```jsx
const cachedFn = useCallback(fn, dependencies);
```

- React Hook that allows caching a function definition between re-renders
- reference: `useCallback(fn, dependencies)`
  - function value that we want to cache, can take any arguments and return any value
    - React will return, **not call** function back to us during the initial render. On next renders, React will give us the same function again if the dependencies have not changed sinde the last render, otherwise React stores function so it can be reused later. React won't call function, funciton is returned to us so we can decide when and whether to call it
  - dependencies: list of all reactive values referenced inside of the function code
    - React compares each dependency with its previous value using `Object.is` comparison algorithm

### Caveats

- React will not throw away the cached function unless there is specific reson to do that
  - React throws aray the cache if component suspends during the initial mount

## Usage

### Skipping re-rendering of components

- in JavaScript, a `function () {}` or `() => {}` always creates a different function, similar to how the `{}` object literal always creates a new object
  **Hook useCallback should be only used as a performance optimization**

### Usage with useMemo

- both Hooks are useful when we are trying to optimize a child component - they allows us to memoize (cache) something we are passing down
- difference in what we are caching:

  - `useMemo` calls our funciton and caches its result - caches the result of calling our function. When necessary, React will call the passed funciton during rendering to calculate the result
  - `useCallback` caches function itself, unlike `useMemo` it does not call the function we provide. Our function won't run until we call it again

- we can think of `useCallback` as this:

```jsx
// Simplified implementation (inside React)
function useCallback(fn, dependencies) {
  return useMemo(() => fn, dependencies);
}
```

### Where to add useCallback

- caching a function is only valuable in a few cases:

  - passed it as a prop to a component wrappd in `memo`
  - the function we are passing is later used as a dependency of some Hook - another function wrapped in `useCallback` depends on it, or it depends on this function from `useEffect`

- not all memoizaiton is effective (it makes code less readable): a single value that's "always new" is enough to break memoization for an entire component

- practives to make a lot of memoization unnecessary:
  - when component visually wrap other components, let it accept JSX as children. Then, if the wrapper component updates its own state, React knows that its chidlren don't need to re-render
  - prefer local state and don't lift state up any further than necessary
  - keep your rendering logic pure
  - avoid unnecessary Effects that update state, most performance problems are caused by chains of updates orignating from Effects
  - try to remove unnecessary dependencies from Effects - remove the need for a function dependency by moving function isnide the Effect

### Optimizing a custom Hook

- it is recommended to wrap any functions that it returns into `useCallback`

```jsx
function useRouter() {
  const { dispatch } = useContext(RouterStateContext);

  const navigate = useCallback(
    (url) => {
      dispatch({ type: "navigate", url });
    },
    [dispatch]
  );

  const goBack = useCallback(() => {
    dispatch({ type: "back" });
  }, [dispatch]);

  return {
    navigate,
    goBack,
  };
}
```
