# Keeping components pure

## Purity

- pure function follows these characteristics:

  - it minds its own business - does not change any objects or variables that existed before it was called
  - same inputs, same output - should always return the same result

- React assumes that every component is a pure function

### Purity benefits

- components could run in a different environment - for example, on the server
- improve performance by skipping rendering components whose inputs have not changed
  - this is safe because pure functions always return the same results, so they are safe to cache
- if some data changes in the middle of rendering a deep component tree, React can restart rendering without wasting time to finish the outdated render
  - purity makes it safe to stop calculating at any time

### Detecting impure calculations with StrictMode

- three kinds of inputs that you can read whuile rendering: **props**, **state** and **context**
  - **always treat these inputs as read-only**
- change something in response to user input, you should `set state` instead of writing to a variable
- React offers a "Strict Mode" in which it calls each component's function twice during development - calling the component functions twice helps to find components that break rules

### Side effects

- rendering process must always be pure - components should only return their JSX, and not change any object or variable that existed before rendering

  - `mutation` - changing state which is outside of function, pure functions don't mutate state(variables) outside of the function's scope or objects that were created before the call
    - pass state as component's/function's prop
    - it is fine to change variables and objects that are created while rendering - "`local mutation`"

- side effects - updating screen, changing data... they are happening "on the side", not during rendering :heavy_exclamation_mark:
- side effects usually belong inside `event handlers`
  - functions that React runs when you perform some action - button click
  - defined inside component, they do not run during rendering - **event handlers don't need to be pure**
  - `useEffect` as event handler
    - side effect tells React to execute it later, after rendering, when side effects are allowed - **this approach should be last resort**
    - **expressing logic with rendering alone is best solution**
