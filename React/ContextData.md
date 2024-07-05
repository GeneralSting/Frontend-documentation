# Passing data deeply with context

- "prop drilling" - same data is being sent at almost every level due to requirements in the final level
- lifting up state - sending data from child to parent

- alternatives to consider before using context:

  - start by passing props
  - extract components and pass JSX as `children` to them

- use cases for context:
  - theming
  - current account
  - routing
  - managing state
    - use reducer togheter with context to manage complex state and pass it down to components

## Step 1: create the context

- only argument to `createContext` is the default value

## Step 2: Use the context

- `useContext` is a Hook, reads passed context

## Step 3: Provide the context

- wrap components with a context provider
