# Strict Mode

## Reference

- `<StrictMode>`
- allows to find common bugs in components early during development
- enables additional development-only behaviors and warnings for the component tree insidež

  - components will re-render an extra time to find bugs caused by impure rendering
  - components will re-run Effects and extra time
  - components will be checked for usage of deprecated APIs

- `StrictMode` acceps no props

### Caveats

- there is no way to opt out of Strict Mode inside a tree wrapped in `<StrictMode>`

## Usage

### Fixing bugs found by double rendering in development

- React assumes that every component is a pure function
- Strict Mode calls functions twice in development:

  - component function's body (only top-level logic, so this does nto include code inside event handlers)
  - functions that we pass to `useState`, `set` functions, `useMemo` or `useReducer`
  - some class components mezhods like `constructor`, `render` `shouldComponentUpdate`...

- if we have **React DevTools** installed, any `console.log` calls during the second render vall will appear slightly dimmed
  - tools also offers a setting to suppress them completely which is not turned on by default

#### fixing bugs by re-running Effects

- React also run one extra **setup + cleanup** cycle in development for every Effect
