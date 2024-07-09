# useDebugValue

## Reference

```jsx
useDebugValue(value, format?)
```

- Hooks allows to add a label to a custom Hook in React DevTools
- `value` parameter is the value we want to display in React DevTools. Can have any type
- optional `format` is a formating function. When the component is inspected, React DevTools will call the formatiing funciton with the value as the argument, and then display the returned formatted value (which may have any type). If we don't specify the formatting funciton, the original `value` itself will be displayed

  - React calls `format` function only when React DevTools is inspected - skips potentially expensive formatting calculations on every render

- Hook does not return anything

## Usage

### Adding label to a custom Hook

- displays a readable **debug value** for **React DevTools**

```jsx
function useOnlineStatus() {
  // ...
  useDebugValue(isOnline ? "Online" : "Offline");
  // ...
}
```

- in the example above, code gives components calling `useOnlineStatus` a label like `OnlineStatus: "Online"` when we inspect component
  - without the `useDebugValue` call, only the underlying data would be displayed, in this case: `true`

### Deferring formatting of a debug value

- we cal also pass a formatting function as the second arguemnt to `useDebugValue` (`fromat` parameter)

  - `format` function is called only when React DevTools are inspected

  ```jsx
  useDebugValue(date, (date) => date.toDateString());
  ```
