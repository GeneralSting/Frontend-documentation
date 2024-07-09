# createContext

## Reference

```jsx
const SomeContext = createContext(defaultValue);
```

- API allows to create a **context** that components can provide or read
- `defaultValue` parameter is the value what we wanot the context to have when there is no matching context provider in the tree above the component that reads context
  - default value is meant as a "last resort" fallback, it is static and never changes over time
- returns a context object which does not hold any information. It represents which context other components read or provide
  - `SomeContext.Provider` in components above specifies the context value
  - `useContext(SomeContext)` call in components below to read context
  - context object properties:
    - `SomeContext.Provider` allows to provide the context value to components
    - `SomeContext.Consumer` is an alternative and rarely used way to read the context value
