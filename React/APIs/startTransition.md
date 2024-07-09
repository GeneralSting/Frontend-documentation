# startTransition

## Reference

```jsx
startTransition(scope);
```

- `scope` parameter is a function that updates some state by calling onr or more `set` functions
  - React immediately calls `scope` with no arguments and marks all state updates scheduled synchronously during the `scope` function call as Transitions - non-blocking and will not display unwanted loading indicators
- API does not return anything

### Caveats

- `startTransition` does not provide a way to track whether a Transition is pending - `useTransition` Hook required
- we can wrap an update into a Transition only if we have to access to the `set` function of that state
  - if we want to start a Transition in response to some prop or custom Hook return value - use `useDeferredValue` instead
- function passed to `startTransition` must be synchronous
  - React immediately executes this funciton, marking all state updates as Transitions
  - perform more state updates later (e.g. timeout), they won't be marked as Transitions
- state update marked as a Transition will be interrupted by other state updates
- Transition updates can't be used to control text inputs

## Usage

### Marking a state update as a non-blocking Transition

- `startTransition` is very similar to `useTransition`, except that it does not provide the `isPending` flag to track whether a Transition is ongoing
  - `startTransition` works outside of component
