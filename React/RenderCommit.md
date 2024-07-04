# Render and Commit

- requesting and serving UI:

## Step 1: trigger a render

- two reasons for a component to render:
  - it is component's initial render
    - calling `createRoot` with the target DOM node, and then calling its render method with created component
  - the component's or any of its ancestors state has been updated
    - updating state

## Step 2: React renders component

- **Rendering** is React calling certain component
  - on inital render, React will call the root component
  - for subsequent renders, React will call the function compnent whose state update triggered the render
- process is recursive

- rendering must always be a pure calculation :warning:
  - same inputes, same output
  - minds its own business

### State as a snapshot

- rendering means that React is calling component, which is a function. JSX returned from that function is like a snapshot of the UI in a time

  - props, event handlers and local variables were all calculated using its state at the time of the render

- re-rendering a component:

  - React calls function again (component)
  - function returns a new JSX snapshot
  - React then updates the screen to match the snapshot function returned

- as a component's memory, state is nit like a regular variable that disappeears after function returned it - state actually "lives" in React itself

```jsx
const [number, setNumber] = useState(0);

return (
  <>
    <h1>{number}</h1>
    <button
      onClick={() => {
        setNumber(number + 1);
        setNumber(number + 1);
        setNumber(number + 1);
      }}
    >
      +3
    </button>
  </>
);
```

#### State over time

```jsx
const [number, setNumber] = useState(0);

return (
  <>
    <h1>{number}</h1>
    <button
      onClick={() => {
        setNumber(number + 5);
        setTimeout(() => {
          alert(number);
        }, 3000);
      }}
    >
      +5
    </button>
  </>
);
```

- the state stored in React may have changed by the time alert runs, but it was scheduled using a snapshot of the state at the time the user interacted with it
- **a state variable's value never changes within a render**, even if its event handler's code is asynchronous

  - the value of _number_ continues to be 0 even after _setNumber(number + 5)_ was called. Its value was “fixed” when React “took the snapshot” of the UI by calling your component.

- code above is example of state works in React, expected output on button click should be +3 but actually it will return only +1
  - even though _setNumber(number + 1)_ is called three times, in this render's event handler _number_ is always 0 - value of the initial state

## Step 3: React commits changes to the DOM

- after rendering (calling) components, React will modify the DOM
  - for the initial render, React will use the appendCHild() DOM API to put all the DOM nodes it has created
  - for re-renders, React will apply the minimal necessary operations to make the DOM match the laters rendering output
