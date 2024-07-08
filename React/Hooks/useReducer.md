# useReducer

## Reference

```jsx
const [state, dispatch] = useReducer(reducer, initialArg, init?)
```

- Hook allows to add a **reducer** to component
- `reducer` function specifies how the state gets updated
  - it must be pure, should take state and action as arguments, and return the next state
  - state and actions can be any types
- `initialArg` value from which the initial state is calculated
  - how the initial state is calculated from it depends on the next `init argument`
- optional `init` initializer function should return the initial state

  - if not specified, initial state is set to `initialArg`, otherwise the initial state is set to the result of calling `init(initialArg)`

- returns an array with exactly two values:
  - the current state, during first render its `init(initialArg)` or `initialArg`
  - the **dispatch function** that allows to update the state to a different value and trigger a re-render

### Caveats

- in Strict Mode React calls reducer and initializer twice to help find accidental impurities - this does not cause problems if the reducer and initializer are pure

## Dispatch function

- `dispatch` function returned by `useReducer` allows to update the state to different value and trigger re-render
  - action as the only argument to the function
  - `action` performed by the user, it can be a value of any type. Action is an object with a `type` property indetifying it and, optionally, other properties with additional information
    . `dispatch` function does not have a return value

### Dispatch function caveats

- function only updates the state variable for the next render
  - reading value after calling the dispatch function will still have the old value
- new values will be checked by `Object.is` comparison and will skip re-rendering the component and its children if values are the same
- React batches state updates - updates the screen after all the event handlers have run and have called their set functions
  - `flushSync` for forcing React to update the screen earlier

## Usage

### Adding a reducer to a component

- the **current state** of this state variable, initially set to the **initial state** that was provided
- the **dispatch function** allows change in response to iteraction

- React will pass the current state and the action to `reducer function`
- `useReducer` is similar to `useState` but allows us to move the state update logic from event handlers into a single function outside of component

### Writing the reducer function

- action type names are local to component
  - each action describes a single ineraction, even if that leads to multiple changes in data
- state is read-only, do not modify any objects or arrays in state
