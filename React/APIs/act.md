# act

## Reference

```jsx
await act(async actFn)
```

- test helper to apply pending React updates before making assertions
  - to prepare a component for assertions, wrap the code rendering it and performing updates inside an `await act()` call. This makes our test run close to how React works in the browser
    - `React Testing Library` helpers are wrapped with `act()`
- reference: `await act(async actFn)`
- it makes sure all updates related to the "units" have been processed and applied to the DOM before we make any assertions

  - the name `act` comes from the `Arrange-Act-Assert` pattern
  - use `act` with `await` and an `async` function
  - parameters:
    - async **actFn** - async function wrapping renders or interactions for components being tested
      - any updates triggered within the actFn, are added to an internal act queue, which are then flushed together to process and apply any changes to the DOM. Since it is async, React will also run any code that crosses an async boundary, and flush any updates scheduled
  - returns:
    - does not return anything`

- in testing frameworks like `React Testing Library`, `IS_REACT_ACT_ENVIRONMENT` is already set for us

  - global setup file for React tests

    ```jsx
    global.IS_REACT_ACT_ENVIRONMENT = true;
    ```

## Usage

- when testing a component, we can use act to make assertions about its output

### Dispatching events in tests

- **pitfall** - don't forget that dispatching DOM events only works when the DOM container is added to the document
  - `React Testing Library` reduces this boilerplate
