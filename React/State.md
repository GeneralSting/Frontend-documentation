# State: component's memory

- local variables don't persist between renders
- changes to local variables won' trigger renders

## useState hook

- provides a state variable to retain the data between renders
- provides a state setter function to update the variable and trigger React to render the component again

### Destructing assignment

- the `[` and `]` syntax is called `array destructing` and it lets you read values from an array

  - array returned by useState always has exactly two items

- destructing assignment is a aspecial syntax that allows us to "unpakc" arrays or objects into a bunch of variables - as sometimes that's more convenient

  - destructuring does not mean destructive
  - destructurizes by copying items into variables, however the array itself is not modified

- array destructing
  - working with variables instead of array members

```js
// we have an array with a name and surname
let arr = ["John", "Smith"];

// destructuring assignment
// sets firstName = arr[0]
// and surname = arr[1]
let [firstName, surname] = arr;

alert(firstName); // John
alert(surname); // Smith
```

## Hooks pitfall

- hooks—functions starting with use—can only be called at the top level of your components or your own Hooks. You can’t call Hooks inside conditions, loops, or other nested functions. Hooks are functions, but it’s helpful to think of them as unconditional declarations about your component’s needs. You “use” React features at the top of your component similar to how you “import” modules at the top of your file.

## How does React know which state to return

- `useState` call does not receive any information about which state variable it refers to - there is no indenifier passed to `useState`
  - hooks rely on a stable call order on every render of the same component - because hooks are at the top level they will always be called in the same order
  - React holds an array of state pairs for every compoennt
    - maintains the current pair index - 0 beofre rendering
    - each `useState` call gives the next state pair and increments the index

## State is isolated and private

- **rendering the same component twice, each copy will have completely isolated state**
