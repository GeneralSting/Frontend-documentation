# useTransition

## Reference

```jsx
const [isPending, startTransition] = useTransition();
```

- Hook allows to update the state without blocking the UI
- `isPneding` flag tells whether there is a pending Transition
- `startTransition` function allows us to mark a state update as a Transition

  - parameter `scope` is a function that updates some state by calling one or more `set` functions
  - React immediately calls `scope` with no parameters and marks all state updates scheduled synchronously during the `scope` function call as Transition. They will be non-blocking and will not display unwanted loading indicators
  - `startTransition` does not return anything

    ```jsx
    function TabContainer() {
      const [isPending, startTransition] = useTransition();
      const [tab, setTab] = useState("about");

      function selectTab(nextTab) {
        startTransition(() => {
          setTab(nextTab);
        });
      }
      // ...
    }
    ```

### Caveats

- we can wrap an update into a Transition only if we have access to the `set` function of that state. If we want to start a Transition in response to some prop or a custom Hook value we should use `useDeferredValue` instead
- function passed to `startTransition` must be synchronous. React immediately executes this function, marking all state updates that happen while it executes as Transitions
  - if we try to perform more state updates later (timeout, for example), they won't be marked as Transitions
- state update marked as a Transition will beinterrupted by other state updates
  - example: updating chart component inside a Transition, but then start typing into an input while the chart is in the middle of a re-render, React will restart the rendering work on the chart component after handling the input update
- Transition updates can't be used to control text inputs
- React batches togheter multiple ongoing Transitions
  - :warning: this is currently correct but react announced to remove this limitation :clock10:

## Usage

### Marking a state update as a non-blocking Transition

- Transitions allows user interface to updates responsive even on slow devices
  - UI stays responsive in the middle of a re-render - example: user clicks a tab but then changes mind and click another tab, user can do that without for the first re-render to finish

### Preventing unwanted loading indicators

- Transitions will only "wait" long enough to avoid hiding _already revealed_ content (like the tab container). If the one tab has a nested `<Suspense>` boundary, the Transition would not "wait" for it
