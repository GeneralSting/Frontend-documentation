# React calls hooks and components

- React is responsible for rendering components and hooks when necessary to optimize the user experience
  - it is declarative - we tell React what to render in component's logic and React will figure out how best to display it

## Never call component functions directly

- letting React orchestrate rendering also allows a number of benefits
  1. components become more than functions - React can augment them with features like local state
  2. component types participate in reconciliation - letting React call components also tells more about the conceptual structure of tree
  3. React can enhance user experience - let the browser do some work between component calls so that re-rendering a large component tree does not block the main thread
  4. better debugging story
  5. more efficient conciliation - React can decide which components in the tree need re-rendering and skip over the ones that don't

## Never pass around hooks as regular values

- they should be called as a function and only be called inside of components and hooks
  - enables _local reasoning_

### Do not dynamically mutate a hook

```jsx
function ChatInput() {
  const useDataWithLogging = withLogging(useData); // 🔴 Bad: don't write higher order Hooks
  const data = useDataWithLogging();
}
```

- hooks should be immutable and not be mutated
  - instead of mutating a hook dynamically, create a static version of the Hook with the desired functionality

```jsx
function ChatInput() {
  const data = useDataWithLogging(); // ✅ Good: Create a new version of the Hook
}

function useDataWithLogging() {
  // ... Create a new version of the Hook and inline the logic here
}
```

### Do not dynamically use hooks
