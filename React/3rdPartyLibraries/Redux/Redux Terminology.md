# Redux Terminology

## Actions

- plain JS object that has a `type` field
- <b>event that describes something that happened in the application</b>
- `type`˙field should be a string that gives this action a descriptive name - "domain/eventName"
- `action` object can have other fields with additional information about what happened
  - that information is put in a field - `payload`

```js
const addTodoAction = {
  type: "todos/todoAdded",
  payload: "Buy milk",
};
```

## Action Creators

- function that creates and returns an `action` object
  - we do not have to write the `action` object by hand every time

```js
const addTodo = (text) => {
  return {
    type: "todos/todoAdded",
    payload: text,
  };
};
```

## Reducers

- function that receives the current state and an action object
- decides how to update the state if necessary and returns new state
  - (state, action) => newState
  - as event listener which handles events based on the received action (event) type
  - <i>similar to the kind of callback funciton you pass to the Array.reduce() method</i>

### Reducer rules

1. only calculate the new state value absed on the state and action arguments
2. they are not allowed to modify the existing state

- makes immutable updates by copying the existing state and making changes to the copied values

3. they must not do any asynchronous logic, calculate random values or "side effects"

### Reducer logic

1. check to see if the `reducer` cares about this action

- if so - make copy of state...

2. otherwise return the existing state unchanged

- if/else, switch loops

```js
const initialState = { value: 0 };

function counterReducer(state = initialState, action) {
  // Check to see if the reducer cares about this action
  if (action.type === "counter/increment") {
    // If so, make a copy of `state`
    return {
      ...state,
      // and update the copy with the new value
      value: state.value + 1,
    };
  }
  // otherwise return the existing state unchanged
  return state;
}
```

## Store

- application state lives in an object called `store`
- store is created by passing in a `reducer` and has a mehod called `getState` that returns the current state value

```js
import { configureStore } from "@reduxjs/toolkit";

const store = configureStore({ reducer: counterReducer });

console.log(store.getState()); // {value: 0}
```

### Dispatch

- Redux `store` has method called `dispatch` which is the only way to update state - call `store.dispatch()` and pass in an action object
  - `store` will run its reducer function and save the new state value inside - `getState()` retrieves the updated value
  - `dispatching actions` are like triggering an event
    - `reducers` act like event listeners, and when they hear an action they are interested in - they update the state in response

### Selectors

- functions that know how to extract specific pieces of information from a `store` state value.
  - for bigger apps allows to avoid repeating logic as different parts of the app need to read the same data

## Application data flow

- `one-way data flow`
  1. state describes the condition of the app at specific point in time
  2. UI is rendered based on that state
  3. when something happens - state is updated based on what occurred
  4. UI re-renders based on the new state

### In more details

1. initial setup

- Redux store is created using a root reducer function
- store calls root reducer once - saves the return value as its initial state
- when UI is first time rendered - UI components access the current state of the redux store and use that data to decide what to render
  - subscribes to any future store updates

2. updates

- something happens in the app
- the app code dispatches an action to the redux store
- store runs the reducer function again with the previous state and the current action and saves the return value as the new state
- store notifies all parts of the UI that are subscribed
- each UI component checks to see if the parts of the state they need have changed
- each component that sees its data changed forces a re-render with new data
