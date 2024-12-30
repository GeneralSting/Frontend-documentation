# use

## Reference

```jsx
const value = use(resource);
```

- API allows to read the value of resource like `Promise` or `context`
- reference: `use(resource)`
  - parameters:
    - **resource** - source of the data that we want to read a value from
  - returns:
    - returns value that was read
- when called with a `Promise` , the `use` API integrates with `Suspense` and `error boundaries`

### Caveats

- must be called inside the component or hook
- when fetching data in a server component, prefer async and await over use
  - async and await pick up rendering from the point where await was invoked, whereas use re-renders the component after the data is resolved
- prefer creating `Promises` in server components and passing them to client components over creating `Promises` in client components
  - `Promises` created in client components are recreated on every render. `Promises` passed from a server component to a client component are stable across re-renders

## Usage

### Reading context with use

- `use` returns **context value** for the passed **context**
  - to determine context value, React searches the component tree and finds the closest context provider above
- **can be called conditionally**
- **pitfall** - does not consider context providers in the component in which is called

### Streaming data from the server to the client

- data streamed from the server to the client by passing the `Promise` as a prop from a server component to a client component
  - resolved value from passed `Promise` must be serializable to pass between server and client
    - data types like functions aren’t serializable and cannot be the resolved value of such a `Promise`

### Resolving Promise in a server or client component

- `Promise` can be passed from a server component to a client component and resolved in the client component with the `use` API. We can also resolve the `Promise` in a server component with await and pass the required data to the client component as a prop
  - using await in a server component will block its rendering until the await statement is finished. Passing a `Promise` from a server component to a client component prevents the `Promise` from blocking the rendering of the server component

### Dealing with rejected Promises

- in some cases a `Promise` passed to `use` could be rejected. You can handle rejected `Promises` by either:

  1. displaying an error to users with an **error boundary**
  2. Providing an alternative value with `Promise.catch`

- **pitfall** - `use` cannot be called in a try-catch block
