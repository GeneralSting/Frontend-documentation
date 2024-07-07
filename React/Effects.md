# Effects

## Synchronizing with Effects

### What are Effects

- `Effects` let you specify side effects that are caused by rendering itself, rather than by a particular event
- Effects run at the end of a commit after the screen updates

### How to write an Effect

#### Declare an Effect

- by default, Effects will run after every commit
- to declare an Effect we need to import and use `useEffect Hook`
- `useEffect` delays a piece of code from running until that render is reflected on the screen
- Effects run after every render, code can produce an infinite loop

#### Specify the Effect dependencies

- re-run when needed rather than after every render
- ref does not need to go into dependency array
  - ref as object has a stable indetity: React guarantees that we will always get the same object from the same `useRef` call on every render
  - omitting always-stable dependencies only works when the linter can "see" that the object is stable, if ref was passed from a parent component you would have to specify it in the dependecy array. We can't know whether the parent component always passes the same ref

#### Add cleanup if needed

- React always cleans up the previous render's Effect before the enxt render's Effect
- specify how to stop, undo or clean up for example: disconnect, unsubscribe, cancel, ignore... something
- example cleanup function code, React calls cleanup function each time before the Effect runs again, and one final time when the component unmounts (gets removed)

```jsx
useEffect(() => {
  const connection = createConnection();
  connection.connect();
  return () => {
    // cleanup function
    connection.disconnect();
  };
}, []);
```

### Downsides of data fetching in Effects

- Effects don't run on the server
- fetching directly in Effects make it easy to create "network waterfalls"
- fetching directly in Effects usually mean you don't preload or cache data
- it's not very ergonomic - quite a bit of boilerplate code

## Unnecessary Effetcs

- don't use Effects to transform data for rendering
- don't use Effects to handle user events

```jsx
export default function ProfilePage({ userId }) {
  return <Profile userId={userId} key={userId} />;
}
```

### Caching expensive calculations

- `useMemo Hook` for caching (memoize) instead of Effects
  - tells React that we don't want the `memo` inner function to re-run unless items from dependecy arrays have changed
  - if certain calculation takes **1ms** or more - it should be memoized (cached)

### Reseting all state when a prop changes

```jsx
function Profile({ userId }) {
  // ✅ This and any other state below will reset on key change automatically
  const [comment, setComment] = useState("");
  // ...
}
```

- by passing userId as a key to the Profile component, you’re asking React to treat two Profile components with different userId as two different components that should not share any state. Whenever the key (which you’ve set to userId) changes, React will recreate the DOM and reset the state of the Profile component and all of its children

## Lifecycle of reactive Effects

### The lifecycle of an Effect

- every React component goes through the same lifecycle

  - a component mounts when it is added to the screen
    - `componentDidMount`
  - a component updates when it receives new props or state, in response to an interaction
    - `componentDidUpdate`
  - a component unmounts when it is removed from the screen
    - `componentWillUnmount`

- think about components but not about Effects - each Effect independently from component's lifecycle
  - React wouldn't always start synchronizing when component mounts and stop synchronizing when component unmounts - sometimes it may be necessary to start and stop synchronizing multiple times while the component remains mounted
  - some Effects don't return a cleanup function at all. if we don't return one, React will behave as if you returned an empty cleanup function

#### Effects "react" to reactive values

```jsx
const serverUrl = "https://localhost:1234";

function ChatRoom({ roomId }) {
  useEffect(() => {
    const connection = createConnection(serverUrl, roomId);
    connection.connect();
    return () => {
      connection.disconnect();
    };
  }, [roomId]);
  // ...
}
```

- since `serverUrl` never changes it would't make sense to specify it as a dependecy. if `serverUrl` was a state it should be also specified into dependency array
- all variables declared in the component body are reactive - all reactive variables should be inside of body and non reactive, outside or imported

  - this is why all variables from the component body used by the Effect should be in the Effect dependency list
  - even regular variables (not state or prop) that can be calculated during rendering are reactive variables
  - **all values inside the component (including props, state and variables in component's body) are reactive. Any reactive value can change on a re-render, so you need to include reactive values as Effect's dependencies**

- **global or mutable values shouldn't be dependencies**

  - contradicts React logic
  - chaning mutable value like `ref.current` wouldn't trigger a re-render of component

- in some cases, React knows that a value never changes even though it's declared inside the component. Stable values are not reactive, so we can omit them from the list. Including them is allowed - they won't change so it doesn't matter

#### Avoid to re-synchronize Effect

- Effects are reactive blocks of code - they re-synchronize when the values read inside of them change

  - we can't choose dependencies - they must include every reactive value that is in the Effect

- to fix problems we can:
  - check that Effect represents an independent synchronization process
    - Effect might be unnecessary
    - if it synchronizes several independent things - split it up
  - read latest value of props or state without "reacting" to it and re-synchronizing the Effect
    - split Effect into a reactive part (which will keep in the Effect) and a non-reactive part (which we will extract into something called an **Effect Event**)
  - avoid relying on objects and functions as dependencies
    - if we create a function or object during rendering and then read them from an Effect, they will be different on every render. This will cause Effect to re-synchronize every time
    - this happens because new function and object are created on every render and that will make Effect to also run on every render because the dependency is always considered "changed"
      - `useCallback` and `useMemo` Hooks for caching functions and objects

## Separating Events from Effects

### Reactive values and reactive logic

- event handlers are triggered manually
  - logic inside event handlers is not reactive
- Effects are triggered automatically
  - logic inside Effects is reactive

### Declaring an Effect Event :warning:

- special experimental API, not yet released - Hook `useEffectEvent` extracts non-reactive logic out of Effect
