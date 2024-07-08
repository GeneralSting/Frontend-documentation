# useState

## Reference

```jsx
const [state, setState] = useState(initialState);
```

- Hook allows to add a state variable to component
- **array destructuring** is used in this Hook
- `initialState` is value we want for state to have initially

  - `initialState` is treated as an initializer function so it should be pure and take no arguments
  - React calls initializer function when initializing component and stores its returned value as the initial state

- `set` function returned by `useState` allows us to update the state to a different value and trigger a re-render
  - we can pass next state directly, or a function that claculates it from the previous state
  - if we pass a function as next state, it will be treated as an **updater function**. It must be pure, should take the pending state as its only argument and return the next state
    - React puts the updater function in a queue and re-render component
  - `set` function does not have return value

### Caveats

- Strict Mode causes calling initializer function twice to help find accidental impurities
  - same applies for calling the **updater function** twice
- `set` function **only updaes the state variable for the next render**
  - reading the state variable after calling `set` function will result in getting the the old value that was on the screen before call
- new values are checked by `Object.is` comparison to determine if re-render is needed
- React batches state updates - updates the screen after all the event handlers have run and have called thier `set` functions
  - to prevent multiple re-render during a single event by forcing React to update the screen earlier we can use **flushSync**
- calling `set` function during renderins is only allowed from within the currently rendering component
  - React discards its output and immediately attempts to render it again with the new state
  - used to store information from the previous renders

## Usage

### Updating state based on the previous state

```jsx
function handleClick() {
  setAge(age + 1); // setAge(42 + 1)
  setAge(age + 1); // setAge(42 + 1)
  setAge(age + 1); // setAge(42 + 1)
}
```

```jsx
function handleClick() {
  setAge((a) => a + 1); // setAge(42 => 43)
  setAge((a) => a + 1); // setAge(43 => 44)
  setAge((a) => a + 1); // setAge(44 => 45)
}
```

- `a => a + 1` is **updater function**
  - it takes the pending state and calculates the next state from it
  - React puts updater function in a queue
- if we can prefer consistency over slightly more verbose syntax, it is reasonable to always write an updater if the state we are setting is calculated from the previous state
  - helps with mutliple updates within the same event

### Updating objects and arrays in state

- state is considered read-only so we should replace state rather then mutate existing objects

```jsx
// ✅ Replace state with a new object
setForm({
  ...form,
  firstName: "Taylor",
});
```

### Resetting state with a key

- `key` attribute when rendering lists - it also servers another purpose:
  - we can reset a component's state by passing a different `key` to a component
