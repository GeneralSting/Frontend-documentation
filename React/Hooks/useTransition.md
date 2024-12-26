# useTransition

## Reference

```jsx
const [isPending, startTransition] = useTransition();
```

- Hook allows rendering a part of the UI in the background
- reference: `useTransition()`

  - parameters:
    - does not take any parameters
  - returns:

    - `isPending` - flag that tells is there a pending transition
    - `startTransition` - function that marks updates as a transition

### startTransition(action)

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

- functions called in `startTransition` are called **actions**
  - by convention, any callback called inside should be named _action_ or include _action_ suffix
- parameters:
  - **action** - a function that updates state by calling one or more `set functions`
    - React calls **action** immadiately with no params and marks all state updates scheduled synchronously during the **action** function call as transitions
    - any async calls that are awaited in the **action** will be included in the transition, but currently require wrapping any `set` functions after the await in an additional `setTransition`
    - state udpates marked as transitions will be **non-blocking** and will not display unwanted loading indicators
- returns:
  - does not return anything

### Caveats

- Using multiple state updates can cause our component to render more frequently than usual. React triggers a render after all state updates are processed, but if there are several updates, this can lead to additional renders.

  - With `startTransition`, we can mark some state updates as low priority, which may also result in extra renders:
    1. The component first renders after updating "high-priority" states.
    2. React then updates the "low-priority" states, causing another render.

- `useTransition` is a hook, so it can only be called inside components or custom hooks. If we need to start a transition somewhere else (for example, from a data library), use the standalone `startTransition` instead
- we can wrap an update into a transition only if we have access to the set function of that state
  - If we want to start a Transition in response to some prop or a custom Hook value, use `useDeferredValue` instead
- function passed to `startTransition` is called immediately, marking all state updates that happen while it executes as transitions

  - If we try to perform state updates in a setTimeout, for example, they won’t be marked as transitions

- we must wrap any state updates after any async requests in another `startTransition` to mark them as transitions
- `startTransition` function has a stable identity

  - we will often see it omitted from effect dependencies, but including it will not cause the effect to fire
    - If the linter lets us omit a dependency without errors, it is safe to do

- state update marked as a transition will be interrupted by other state updates
  - for example, if we update a chart component inside a transition, but then start typing into an input while the chart is in the middle of a re-render, React will restart the rendering work on the chart component after handling the input update
- transition updates can’t be used to control text inputs
- if there are multiple ongoing transitions, React currently batches them together

## Usage

### Perform non-blocking updates with Actions

### Exposing action prop from components

### Preventing unwanted leading indicators

- transitions only “wait” long enough to avoid hiding already revealed content (like the tab container)
  - If the Posts tab had a nested `<Suspense>` boundary, the transition would not “wait” for it

### Updating an input in a Transition doesn’t work

- this is because transitions are non-blocking, but updating an input in response to the change event should happen synchronously
  - if we want to run a Transition in response to typing, we have two options:
    1. declare two separate state variables: one for the input state (which always updates synchronously), and one that you will update in a transition. This allows to control the input using the synchronous state, and pass the transition state variable (which will “lag behind” the input) to the rest of our rendering logic.
    2. use `useDeferredValue`

### React doesn’t treat async state update as a Transition

### React doesn’t treat state update after await as a Transition
