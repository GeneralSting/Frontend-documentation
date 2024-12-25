# useActionState

## Reference

```jsx
const [state, formAction, isPending] = useActionState(fn, initialState, permalink?);
```

- React Hook that allows to update the state based on the result of the a form action
- reference: `useActionState(action, initialState, permalink)`
  - call Hook at the top level of your component to create component state that is updated when a **form action is invoked**
    - pass an existing form action function as well as an initial state, and it returns a new action that we use in our form, along with the latest form state and whether the action is still pending. The latest form state is also passed to the function we provided
      - the form state is the value returned by the action when the form is last submitted, if not submitted, it is initial value.
      - if used with server functions, hook allows the server’s response from submitting the form to be shown even before hydration has completed
  - parameters:
    - `fn` - the function to be called when the form is submitted or button pressed
    - `initialState` - the value you want the state to be initially
    - optional `permalink` - a string containing the unique page URL that this form modifies
  - returns:
    - array with following values:
      - **the current state**
      - a **new action** that you can pass as the action prop to your form component or formAction prop to any button component within the form
      - the **isPending** flag that tells whether there is pending transition

### Caveats

- when used with a framework that supports React Server Components, `useActionState` lets you make forms interactive before JavaScript has executed on the client. When used without Server Components, it is equivalent to component local state
- the function passed to `useActionState` receives an extra argument, the previous or initial state, as its first argument. This makes its signature different than if it were used directly as a form action without using `useActionState`

## Usage

### Using information returned by a form action

- call `useActionState` at the top level of your component to access the return value of an action from the last time a form was submitted
- when the form is submitted, the action function that you provided will be called. Its return value will become the new current state of the form
