# Updating Objects and Arrays in state

- treat state as read-only
- local mutation is fine because it mutates a fresh object that is just created

## Updating objects

```jsx
const nextPosition = {};
nextPosition.x = e.clientX;
nextPosition.y = e.clientY;
setPosition(nextPosition);
```

- spread syntax `...` is "shallow" - it only copies things one level deep
  - for nested properties it is needed to use it multiple times

```jsx
function handleChange(e) {
  setPerson({
    ...person,
    [e.target.name]: e.target.value,
  });
}
```

- using a single event handler for multiple fields
  - _e.target.name_ refers to the _name_ property given to the input DOM element

### Objects are not really nested

```js
let obj1 = {
  title: "Blue Nana",
  city: "Hamburg",
  image: "https://i.imgur.com/Sd1AgUOm.jpg",
};

let obj2 = {
  name: "Niki de Saint Phalle",
  artwork: obj1,
};

let obj3 = {
  name: "Copycat",
  artwork: obj1,
};
```

- if you were to mutate obj3.artwork.city, it would affect both obj2.artwork.city and obj1.city. This is because obj3.artwork, obj2.artwork, and obj1 are the same object. This is difficult to see when you think of objects as “nested”. Instead, they are separate objects “pointing” at each other with properties.

### Why is mutating state not recommended

- debuginig
  - won't get the more recent state changes
- optimization
  - React **optimization strategies** rely on skipping work if previous props or state are the same as the next ones
  - if **prevObj === obj** - nothing changed
- new features
  - new React features rely on state being treated like a snapshot
- requirement changes
- simpler implementation
  - React does not rely on mutation so it does not need to do anything special with your objects like hijack their properties, wrap them into Proxies...

## Updating arrays in state

- reference table of common array operations and what is needed to avoid the methods

|           | avoid - mutates the array          | prefer - returns a new array       |
| --------- | ---------------------------------- | ---------------------------------- |
| adding    | `push`, `unshift`                  | `concat`, `[...arr] spread syntax` |
| removing  | `pop`, `shift`, `splice`           | `filter`, `slice`                  |
| replacing | `splice`, `arr[i] = ...`assignment | `map`                              |
| sorting   | `reverse`, `sort`                  | copy the array first               |

- **Immer** allows methods from both columns

- even if you copy an array, you can’t mutate existing items inside of it directly. This is because copying is shallow—the new array will contain the same items as the original one

```jsx
const nextList = [...list];
nextList[0].seen = true; // Problem: mutates list[0] list[0] and nextList[0]
//points to the same object
setList(nextList);
```

### Updating objects inside arrays

- objects are not really located inside arrays
- when updating nested state, you need to create copies from the point where you want to update and all the way up to the top level

- use `map` to substitute an old item with its updated version without mutation.
