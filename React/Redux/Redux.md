# Redux

## What is Redux

- pattern and library for managing and updating application state, using events called actions
  - serves as centralized store for state that needs to be used across your entire application
  - state can only be updated in a predictable fashion

## Why use Redux

- helps managing global state
  - pattern and tools provided by `Redux` allows writing code that is predictable and testable

## When to use Redux

- for large amounts of application state that are needed in many places in the app
- app state is updated frequently
- logic to update state is complex
- medium-large codebase size

## Redux libraries and tools

- `Redux` is small standalone JS library

### React-Redux

- integrated with any UI framework
  - most requently is with React

### Redux Toolkit

- recommended with `Redux`
  - simplifies most `Redux` tasks
  - prevents common mistakes

### Redux DevTools Extension

- shows history of the changes to the state in `Redux` store
  - time-travel debugging

## Terms and Concepts

### State management

```js
function Counter() {
  // State: a counter value
  const [counter, setCounter] = useState(0);

  // Action: code that causes an update to the state when something happens
  const increment = () => {
    setCounter((prevCounter) => prevCounter + 1);
  };

  // View: the UI definition
  return (
    <div>
      Value: {counter} <button onClick={increment}>Increment</button>
    </div>
  );
}
```

1. <b>`state`</b> - app data
2. <b>`view`</b> - declarative description of the UI based on the current `state`
3. <b>actions</b> - the events that occur in the app

#### one-way data flow

- `state` describes the condition of the app at a specific point in time
- the UI is rendered based on the `state`
- when something happens - the `state` is updated based on what occurred
- the UI re-renders based on the new `state`

#### Lifting state up

- different components share same `state` - when `state` is updated re-render both UI/components
  - share `state` between components
    - remove `state` from both of them
    - move `state` to their closest common parent and pass `state` via props

#### Complex app logic

- define various concepts involved in `state` management enforcing rules that maintain independence between `views` and `states`
  - code is more structure and maintainable
  - basic ideo behind `Redux` - single centralized place to contain the global `state` in app with specific patterns that follows `state`s updating so we get predicatable code

### Immutability

- "`mutable`" means "changebale"
  - JS objects and arrays
  - mutating the object or array - it is the same object or array reference in memory but the contents inside the object have changed
  - in order to update values immutably - code must make copies of existing objects/arrays and then modify the copies
    - spread operator (...)
  - `Redux` expects that all `state` updates are done immutably
- "`immutable`" means it can never be changed
  - primary values
  - values cannot be changed but variable can re reassigned
