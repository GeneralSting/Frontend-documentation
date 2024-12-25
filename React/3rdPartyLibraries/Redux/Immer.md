# Immer

- German - always
- tiny package that allows to work with `immutable` state in a mora convenient way

## Immer simplifies handling immutable data structures

- generally: `immutable` data structures allow for efficient change detection
  - if the reference to an object didn't change, the object itself did not change
    - making cloning cheap
    - unchanged parts of a data tree don't need to be copied and are shared in memory with older versions of the same state
  - but always creates an altered copy instead - can result in code that is cumbersome to write
    1. `Immer` will detect accidental mutations and throw an error
    2. removes typical boilerplate code when creating deep updates to `immutable` objects
    - object copies need to be made by hand at every level
      - lots of ... spread operations
    - `immer` handles changes using `draft` object that records the changes and takes cares of creating the necessary copies
    3. `Immer` uses plain JS data structures, and use the well-known mutable JS APIs
    - relieving programmer of learning this structure paradigm

### code example

- base state - update the second todo and add a third one
  - avoid deep cloning, preserve the first todo

```js
const baseState = [
  {
    title: "Learn TypeScript",
    done: true,
  },
  {
    title: "Try Immer",
    done: false,
  },
];
```

- without `Immer`:

```js
const nextState = baseState.slice(); // shallow clone the array
nextState[1] = {
  // replace element 1...
  ...nextState[1], // with a shallow clone of element 1
  done: true, // ...combined with the desired update
};
// since nextState was freshly cloned, using push is safe here,
// but doing the same thing at any arbitrary time in the future would
// violate the immutability principles and introduce a bug!
nextState.push({ title: "Tweet about it" });
```

- with `Immer`:

```js
import { produce } from "immer";
// leverage the produce function with arguments - state and function called the recipe
// function is passed a draft to which we can apply straightforward mutations
// mutations are recorded and used to produce the next state once the recipe is done
// produce will take care of all the necessary copying
const nextState = produce(baseState, (draft) => {
  draft[1].done = true;
  draft.push({ title: "Tweet about it" });
});
```

- `Redux + Immer`

```js
import { produce } from "immer";

// Reducer with initial state
const INITIAL_STATE = [
  /* bunch of todos */
];

const todosReducer = produce((draft, action) => {
  switch (action.type) {
    case "toggle":
      const todo = draft.find((todo) => todo.id === action.id);
      todo.done = !todo.done;
      break;
    case "add":
      draft.push({
        id: action.id,
        title: "A new todo",
        done: false,
      });
      break;
    default:
      break;
  }
});
```

### How Immer works

- applies all chnages to a temporary draft, which is a proxy of the <i>currentState</i>
  - once all mutations are completed - `Immer` produces the <i>nextState</i> based on the mutations to the draft state
  - modifying data by keeping all benefits of immutable data

### Benefits

- follow the immutable data paradigm
  - JS objects, arrays, JS APIs
- strongly typed, no string based paths selectors...
- structural sharing out of the box
- object freezing out of the box
- deep updates are easier
- boilerplate reduction
- JSON support
- small package
