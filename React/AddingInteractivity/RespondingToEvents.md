# Responding to events

- pass it as a prop to the appropriate JSX tag
- event handle functions:
  - usually defined inside components
  - have names that start with _handle_, followed by the name of the event

define inline in the JSX:

```jsx
<button onClick={function handleClick() {
  alert('You clicked me!');
}}>
```

```jsx
<button onClick={() => {
  alert('You clicked me!');
}}>
```

## Pitfall

- functions passed to event handlers must be passed, not called! :warning:

```jsx
<button onClick={handleClick()}>  // calling a function - incorrect
<button onCLick={handleClick}>    // passing a function - correct
```

- passing function as an event handler tells React to remember it and only call your function when the user triggers event
- calling function, the () at the end, fires the function immediately during rendering, without triggering event

  - this is because JavaScript inside the `JSX { and }` executes right away

- define event handler inline, wrap it in anonymous function:

```jsx
// This alert fires when the component renders, not when clicked!
<button onClick={alert('You clicked me!')}> // calling a function - incorrect
<button onClick={() => alert('You clicked me!')}> // passing a function - correct
```

## Event propagtion

- all events propagate in React except `onScroll`, which only woks on the JSX tag you attach it to

### Stopping propagation

- event handlers receive an **event object** as their only argument - that event object also allows propagation to stop
  - `event.stopPropagation()`

## Preventing default behavior

- `event.preventDefault()` - prevents the default browser behavior for the few events that have it
  - _form_ element submit event

## event handlers and side effects

- unlike rendering functions, event handlers don't need to be pure, it is great place to change something
  - change input's value in response to typing
  - in order to change some information, it needs to saved into a store - state, componenet's memory
