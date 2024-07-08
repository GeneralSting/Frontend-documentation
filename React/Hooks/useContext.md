# useContext

## Reference

```jsx
const value = useContext(SomeContext);
```

- Hook allows us to read and subscribe to context from our component
- reference: useContext(SomeContext)
  - context that is previously created with `createContext`. The context itself does not hold the information, it only represents the kind of information we can provide or read from components
  - returns the context value for the calling component. It is determined as the `value` passed to the closest SomeContext.Provider above the calling component in the tree. If there is no such provider, then the returned value will be `defaultValue` passed to `createContext` for that context. Returned value is always up-to-date, React automatically re-renders components that read some context if it changes

### Caveats

- `useContext()` call in a component is not affected by providers returned from the same component - the corresponding `<Context.Provider>` needs to be above the component doing the `useContext()` call
- React automatically re-renders all children that use a particular context
  - previous and next values are compared with the `Object.is` comparison
  - skipping re-renders with `memo` does not prevent the chidlren receiving fresh context values
- if build system produces duplicates modules in the output - this can break context.
  - passing something via context only works if `SomeContext` that is used to provide context and `SomeContext` that is used to read it are exactly the same object, as determined by `===` comparison

## Usage

### Passing data deeply into the tree

- to determine the context value, React searches the component tree and finds the closest context provider above for that particular context
  - pitfall - it searches upwards and does nto consider providers in the component from which is called `useContext()`

```jsx
<ThemeContext.Provider value="dark">
  <Form />
</ThemeContext.Provider>
```

### Specifying a fallback default value

- if React can't find any providers of that particular context in the parent tree, the context value returned will be equal to the `defaultValue` what is specified when creating context

```jsx
const ThemeContext = createContext("light");
```

### Overiding context for a part of the tree

- override the context by wrapping that part in a provider with a different value
  - nest and override providers as many times as needed

### Optimizing re-renders when passing objects and functions

- wrap the function with `useCallback` and wrap the object creation into `useMemo`
