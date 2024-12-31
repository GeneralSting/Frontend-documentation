# React compiler

## What does compiler do

- in order to optimize applications, React compiler automatically memoizes code
  - compiler uses its knowledge of JavaScript and React's rules to automatically memoize values or groups of values within components and hooks
    - if it detects breakages of the rules, it will automatically skip over components or hooks and continue safely compiling other code
    - React compiler can statically detect when rules of React are broken, and safely opt-out of optimizing just the affected components or hooks. It is not necessary for the compiler to optimize 100% of your codebase.

### React compiler memoization

1. skipping cascading re-rendering of components - re-rendering `<Parent />` causes many components in its component tree to re-render, even though only `<Parent />` has changed
2. skipping expensive calculation from outside of React

#### Optimizing re-renders

- react compiler automatically applies the equivalent of manual memoization, ensuring that only the relevant parts of an app re-render as state changes, which is sometimes referred to as “fine-grained reactivity”

#### Expensive calculations memoized

- compiler can also automatically memoize for expensive calculations used during rendering

  ```jsx
  // **Not** memoized by React Compiler, since this is not a component or hook
  function expensivelyProcessAReallyLargeArrayOfObjects() {
    /* ... */
  }

  // Memoized by React Compiler since this is a component
  function TableContainer({ items }) {
    // This function call would be memoized:
    const data = expensivelyProcessAReallyLargeArrayOfObjects(items);
    //
  }
  ```

- react compiler only memoizes React components and hooks, not every function
- react compiler's memoization is not shared across multiple components or hooks

## eslint-plugin-react-compiler

- ESLint plugin will display any violations of the rules of React in your editor

  - when it does this, it means that the compiler has skipped over optimizing that component or hook. This is perfectly okay, and the compiler can recover and continue optimizing other components

- **rules of React**

```js
import reactCompiler from "eslint-plugin-react-compiler";

export default [
  {
    plugins: {
      "react-compiler": reactCompiler,
    },
    rules: {
      "react-compiler/react-compiler": "error",
    },
  },
];
```

## use no memo directive

- `use no memo` is a **temporary escape hatch** that lets you opt-out components and hooks from being compiled by the React compiler
  - it is not recommended to reach for this directive unless it’s strictly necessary
