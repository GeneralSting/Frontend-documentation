# useInsertionEffect

## Pitfall

- `useInsertionEffect` is for **CSS-in-JS library authors**
  - unless you are working on a **CSS-in-JS library** and need a place to inject the styles, you probably want `useEffect` or `useLayoutEffect` instead.

## Reference

```jsx
useInsertionEffect(setup, dependencies?)
```

- `useInsertionEffect` allows inserting elements into the DOM before any layout effects fire
- reference: `useInsertionEffect(setup, dependencies?)`
  - parameters
    - **setup** - function with effect's logic
    - optional **dependencies** - The list of all reactive values referenced inside of the **setup** code
  - returns
    - returns `undefined`

### Caveats

- effects only run on the client. They don’t run during server rendering
- cannot update state from inside `useInsertionEffect`
- by the time `useInsertionEffect` runs, refs are not attached yet.
- `useInsertionEffect` may run either before or after the DOM has been updated.
  - shouldn’t rely on the DOM being updated at any particular time.
- Unlike other types of Effects, which fire cleanup for every Effect and then setup for every Effect, `useInsertionEffect` will fire both cleanup and setup one component at a time
  - results in an “interleaving” of the cleanup and setup functions.

## Usage

### Exposing a custom ref handle to the parent component

- there are three common approaches to CSS-in-JS:

  1. static extraction to CSS files with a compiler
  2. Iiline styles, e.g. `<div style={{ opacity: 1 }}>`
  3. runtime injection of `<style>` tags

  - If CSS-in-JS is used, it is recommended that a combination of the first two approaches (CSS files for static styles, inline styles for dynamic styles). it is not recommended runtime `<style>` tag injection for two reasons:
    1. runtime injection forces the browser to recalculate the styles a lot more often.
    2. runtime injection can be very slow if it happens at the wrong time in the React lifecycle.
    - the first problem is not solvable, but `useInsertionEffect` helps you solve the second problem.

- call `useInsertionEffect` to insert the styles before any layout Effects fire:
- similarly to `useEffect`, `useInsertionEffect` does not run on the server
  - fi we need to collect which CSS rules have been used on the server, we can do it during rendering
