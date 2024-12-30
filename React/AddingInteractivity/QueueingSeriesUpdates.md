# Queueing a series of state updates

- batching updating multiple state variables - even from multiple components - without triggering too many re-renders
- React does not batch across multiple events like clicks - each click is handled separately
  _setNumber(n => n + 1)_ is way to tell React to do something with the state value instead of just replacing it

  - **updater function**
  - setNumber(n => n + 1): n => n + 1 is a function. React adds it to a queue
  - React queues this function to be processed after all the other code in the event handler has run
  - during the next render, React goes through the queue and gives the final updated state

- _setState(5)_ actually works like _setState(n => 5) but \_n_ is unused

```jsx
const [number, setNumber] = useState(0);

return (
  <>
    <h1>{number}</h1>
    <button
      onClick={() => {
        setNumber(number + 5);
        setNumber((n) => n + 1);
        setNumber(42);
      }}
    >
      Increase the number
    </button>
  </>
);
```

| queued update    | n          | returns   |
| ---------------- | ---------- | --------- |
| "replace with 5" | 0 (unused) | 5         |
| n => n + 1       | 5          | 5 + 1 = 6 |
| "replace with 42 | 6 (unused) | 42        |

1. an update function get added to the queue
2. any other value adds number to the queue, ignoring what's already queued

- after the event handler completes, React will trigger a re-render. During re-render, React will process the queue, Updater functions run during rendering, so updater functions must be pure and only return the result
