# useTransition

## Reference

```jsx
const [optimisticState, addOptimistic] = useOptimistic(state, updateFn);
```

- allows optimistically update the UI
- reference: `useOptimistic(state, updateFn)`
  - React Hook that lets us show a different state while an async action is underway
    - it accepts some state as an argument and returns a copy of that state that can be different during the duration of an async action such as a network request
    - we provide a function that takes the current state and the input to the action, and returns the optimistic state to be used while the action is pending
    - state is called the “optimistic” state because it is usually used to immediately present the user with the result of performing an action, even though the action actually takes time to complete
  - parameters:
    - **state** - the value to be returned initially and whenever no action is pending
    - **updateFn(currentState, optimisticValue)** - function that takes the current state and the optimistic value passed to addOptimistic and returns the resulting optimistic state
      - it must be a pure function
  - returns:
    - **optimisticState** - the resulting optimistic state, equal to the **state** unless an action is pending, then equal to the result of the **updateFn**
    - **addOptimistic** - dispatching function to call when we have optimistic update

## Usage

### Optimistically updating forms

- provides a way to optimistically update the user interface before a background operation, like a network request, completes.
  - in the context of forms, this technique helps to make apps feel more responsive
  - when a user submits a form, instead of waiting for the server’s response to reflect the changes, the interface is immediately updated with the expected outcome
