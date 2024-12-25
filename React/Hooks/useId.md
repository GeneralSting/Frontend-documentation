# useId

## Reference

```jsx
const id = useId();
```

- call Hook to generate a unique ID
- reference: `useId()`
  - returns
    - unique string ID associated with this particular `useId` call in this particular component

### Caveats

- `useId` is a hook, so we can only call it at the top level of your component or our own hooks. We can’t call it inside loops or conditions. If we need that, extract a new component and move the state into it
- **should not be used to generate keys** in the list

## Usage

### Generating unique IDs for accessibility attributes

- **HTML accessibility attributes** like **aria-describedby** let us specify that two tags are related to each other
  - hardcoding IDs like this is not a good practice in React
    - a component may be rendered more than once on the page—but IDs have to be unique - instead of hardcoding an ID, generate a unique ID with `useId`
      - if the component appears multiple times, each will have unique ID and generated IDs will not clash

### Pitfall

- with **server rendering**, `useId` requires an identical component tree on the server and the client
  - if the trees we render on the server and the client don’t match exactly, the generated IDs won’t match

### Why is useId better than an incrementing counter

- the primary benefit of `useId` is that React ensures that it works with server rendering. During server rendering, your components generate HTML output. Later, on the client, hydration attaches your event handlers to the generated HTML. For hydration to work, the client output must match the server HTML
  - this is very difficult to guarantee with an incrementing counter because the order in which the client components are hydrated may not match the order in which the server HTML was emitted. By calling `useId`, we ensure that hydration will work, and the output will match between the server and the client
  - inside React, `useId` is generated from the “parent path” of the calling component. This is why, if the client and the server tree are the same, the “parent path” will match up regardless of rendering order

### Generating IDs for several related elements

- if we need to give IDs to multiple related elements, us can call `useId` to generate a shared prefix for them
  - this lets us avoid calling `useId` for every single element that needs a unique ID.

### Using the same ID prefix on the client and the server

- if we render multiple independent React apps on the same page, and some of these apps are server-rendered, make sure that the **identifierPrefix** we pass to the hydrateRoot call on the client side is the same as the **identifierPrefix** we pass to the server APIs such as _renderToPipeableStream_
