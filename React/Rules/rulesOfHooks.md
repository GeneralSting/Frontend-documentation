# Rules of hooks

- hooks are defined using JavaScript functions, but they represent a special type of reusable UI logic with restrictions on where they can be called

## Only call hooks at top level

- 🔴 do not call hooks inside conditions or loops
- 🔴 do not call hooks after a conditional return statement
- 🔴 do not call hooks in event handlers
- 🔴 do not call hooks in class components
- 🔴 do not call hooks inside functions passed to `useMemo`, `useReducer`, or `useEffect`
- 🔴 do not call hooks inside try/catch/finally blocks

- can use the `eslint-plugin-react-hooks` plugin to catch these mistakes

### Only call hooks from React functions

- do not call hooks from regular JavaScript functions instead:
  - call hooks from React function components
  - call hooks from custom hooks
