# Hooks

## Built-in React Hooks

- allows us to use different React features from our components
  - use either **built-in Hooks** or combine them to build **custom Hooks**

### State Hooks

- **state** lets a component "remember information"

  - form component - stores user input value

- to add state to the component, use these Hooks:
  - `useState` - declares a state variable that you can update directly
  - `useReducer` - declares a state variable with the update logic inside a reducer function

### Context Hooks

- **context** allows component to receive information from distant parent without passing it as props

  - passing UI theme

- to use context, use this Hook:
  - `useContext` - reads and subscribes to the context

### Ref Hooks

- **refs** let a component to hold information that isn't used for rendering

  - DOM node
  - timeout ID

- unlike with state, updating a ref does not re-render your component

  - **refs** are an “escape hatch” from the React paradigm. They are useful when you need to work with non-React systems, such as the built-in browser APIs.

- to use refs, consider these Hooks:
  - `useRef` - declares a ref, can hold any value in it but most often it is DOM node
  - `useImperativeHandle` - lets customize the ref exposed by our component

### Effect Hooks

- **effects** let a component connecet to and synchronize with external systems

  - dealing with network, browser DOM, animations, widgets written using different UI library, and other non-React code.

- effects are an “escape hatch” from the React paradigm

  - don’t use Effects to orchestrate the data flow of your application. If you’re not interacting with an external system, **you might not need an effect**.

- effects Hooks:
  - `useEffect` - connects a component to a external system
    - there are two rarely used variations of `useEffect` with differences in timing
      - `useLayoutEffect` - fires before the browser repaints the screen, measure layout here
      - `useInsertionEffect` - fires before React makes changes to the DOM, libraries can insert dynamic CSS here

### Performance Hooks

- a common way to optimize re-rendering performance is to skip unnecessary work

  - reuse cached calculations

- to skip calculations and unnecessary re-rendering, use one of these Hooks

  - `useMemo` - lets you cache the result of an expensive calculation
  - `useCallback` - lets you cache a function definition before passing it down to an optimized component

- sometimes, you can’t skip re-rendering because the screen actually needs to update.

  - improve performance by separating blocking updates that must be synchronous (like typing into an input) from non-blocking updates which don’t need to block the user interface (like updating a chart)

- to prioritize the rendering, use one of these Hooks:
  - `useTransition` - lets you mark a state transition as non-blocking and allow other updates to interrupt it
  - `useDeferredValue` - lets you defer updating a non-critical part of the UI and let other parts update first

### Other Hooks

- these Hooks are mostly useful to library authors and aren’t commonly used in the application code
  - `useDebugValue` - lets you customize the label React DevTools displays for your custom Hook
  - `useId` - lets a component associate a unique ID with itself. Typically used with accessibility APIs
  - `useSyncExternalStore` - lets a component subscribe to an external store
  - `useActionState` - allows you to manage state of actions

### Custom Hooks

- we can also define our own custom Hooks as JavaScript functions in combination with React Hooks.

## Built-in React DOM Hooks

- the react-dom package contains Hooks that are only supported for **web applications** (which run in the browser DOM environment)
  - these Hooks are not supported in non-browser environments like iOS, Android, or Windows applications

### Form Hooks

- allows creation of the interactive controls for submitting information
- to manage forms in components, use this Hook:
  - `useFormStatus` - allows you to make updates to the UI based on the status of the a form
