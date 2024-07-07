# Custom Hooks

## Reusing logic with custom Hooks

- own Hooks allows us to extract component logic intor eusable functions, making code more modular and easier to maintain
  - custom Hooks leverage the built-in React hooks, allowing to manage state, handle side effects or abstract any reusable logic
  - custom hooks let us share stateful logic, not state itself
- Hook names always start with `use` followed by a capital letter
- they can return arbitrary values

- the code inside of custom Hooks will re-run during every re-render of component, this is why like components, custom Hooks need to be pure

### When to use custom Hooks

- whenever we write an Effect, we should consider whether it would be clearer to also wrap it in a custom Hook
  - we shouldn't need Effects very often, so if we are writing one, it means that we need to "step outside React" to syhncronize with some external system or to do something that React does not have a built-in API for

### Kepp custom Hooks focues on cnncrete high-level use cases

- avoid creating and using custom "lifecycle" Hooks that act as alternatives anc convenience wrappers for the `useEffect` API itself
  - custom “lifecycle” Hooks like useMount don’t fit well into the React paradigm
- **a good custom Hook makes the calling code more declarative by constraining what it does**
- custom Hooks helps to migrate to better patterns
