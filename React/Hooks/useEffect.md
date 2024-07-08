# useEffect

## Reference

```jsx
useEffect(setup, dependencies?)
```

- Hook allows us to synchronize a component with an external system
  - `setup` is function with Effect's logic, function may optionally return a cleanup function
    - React runs setup function
    - after every re-render with changed dependencies, React will first run the cleanup function if is provided with the old values, and then run setup function with the new values. After removing component from the DOM, React will run the cleanup function
  - optional dependencies - list of all reactive values referenced inside of the `setup` code
    - React compares each dependency with its previous value using `Object.is` comparison

### Caveats

- if we are not trying to synchronize with some external system, we probably don't need an Effect
  - external system means any price of code that's not controlled by React:
    - time manager: `setInterval()` and `clearInteval()`
    - event subscription: `window.addEvenetListener()` and `window.removeEventListener()`
    - third-party animation library with an API: `animation.start()` and `animation.reset()`
- with **Strict Mode** on, React runs one extra-development-only setup + cleanup cycle before the real setup
- if dependencies are objects or functions defined inside the component, there is a risk that they will cause the Effect to re-run more often then needed
- if we need Effect to do something visual and the delay is noticeable we should replace `useEffect` with `useLayoutEffect`
- Effects only run on the client, they don't run during server rendering

## Usage

### Connecting to an external system

- **setup code** runs when component is added to the page - component mounts
- after every re-render of component where dependencies have changed:
  - first **cleanup code** runs the old props and state
  - then **setup code** runs with the new props and state
- **cleanup code** runs one final time after component is removed from the page

### Fetching data with Effects

- writing data fetching directly in Effects gets repetitive and makes it difficult to add optimizations like caching and server rendering later
- ut us easier to use a custom Hook

#### Fetching data alternatives

- Effects don't run on the server
  - constantly loading data is not efficient
- fetching directly in Effects make it easy to create "network waterfalls"
  - when parent and childs component need to fetch data - it can goes many steps into UI tree to get all data
- fetching directly in Effects usually means we can't preload or cache data
  - when component mounts and unmounts again - data fetch is needed
- not ergonomic - boilerplate code

- recommended the following approaches:
  - framerwork's built-in data fetching mechanism
  - using or building a client-side cache - React Query, useSWR, React Router

### Updating state based on previous state from Effect

- updating reactive value in Effect causes triggering re-render and then running Effect's code - causing infinite loop
  - solution is to pass the `state updater`: `value => value + 1`
