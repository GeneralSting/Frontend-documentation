# Rendering lists

- arrow functions implicitly return the expression right after =>, does not need `return` statement

```js
const listItems = chemists.map(
  (person) => <li>...</li> // Implicit return!
);
```

- `return` must be written explicitly if => is followed by curly brace!

```js
const listItems = chemists.map((person) => {
  return <li>...</li>;
});
```

- arrow functions containing curly braces are said to have a `block body`
  - allows you to write more than a single line of code, but a `return` statement is needed

## Keys

- JSX elements directly inside a map() call always need keys!
- keys tell React which array item each component corresponds to, so that it can match them up later.
- rather than generating keys on fly, they should be included in code's data

- the short <>...</> `Fragment` syntax won't let a key to be passed, slightly longer and more explicit &lt;Fragment&gt; syntax is needed

### Where to get key

- data from database, unique by nature
- locally generated data, incrementing counter
  - crypto.randomUUID()
  - uuid

### Rules

- keys must be unique among siblings, it is okay to use the same keys for JSX nodes in different arrays
- keys must not change, do not generate them while rendering

### Pitfall

- React uses item's index if key is not specified at all

  - order in which items are ordered will change over time if item is inserted, deleted or if array gets reordered - leads to subtle and confusing bugs

- genereting keys on fly, e.g. with key={Math.random()} will cause keys to never match up between renders

  - stable ID is needed

- components won't receive `key` as a prop, it is only used as a hint by React itself

  - if component needs an ID, another prop is needed

  ```jsx
  <Profile key={id} userId={id} />
  ```
