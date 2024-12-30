# flushSync

## Pitfall

- **using `flushSync` is uncommon and can hurt the performance of your app**

## Reference

- forces React to flush any updates (any pending work) inside the provided callback synchronously
  - this ensures that the DOM is updated immediately
  - use it as last resort
- reference: `flushSync(callback)`
  - parameters:
    - **callback** - function that React will immediately call and flush any updates it contains synchronously
      - flush any pending updates or effects or updates inside the effect
        - if any update suspends as a result of the `flushSync` call, the fallbacks may be re-shown
  - returns:
    - returns `undefined`

### Caveats

- `flushSync` can significantly hurt performance. Use sparingly.
- `flushSync` may force pending `Suspense` boundaries to show their fallback state
- `flushSync` may run pending effects and synchronously apply any updates they contain before returning
- `flushSync` may flush updates outside the callback when necessary to flush the updates inside the callback
  - for example, if there are pending updates from a click, React may flush those before flushing the updates inside the callback

## Usage

### Flushing updates for third-party integrations

- ensures that, by the time the next line of code runs, React has already updated the DOM

  ```jsx
  flushSync(() => {
    setSomething(123);
  });
  // By this line, the DOM is updated.
  ```

  - Using `flushSync` is uncommon, and using it often can significantly hurt the performance of app.
    - if app only uses React APIs, and does not integrate with third-party libraries, `flushSync` should be unnecessary
    - however, it can be helpful for integrating with third-party code like browser APIs
      - some browser APIs expect results inside of callbacks to be written to the DOM synchronously, by the end of the callback, so the browser can do something with the rendered DOM. In most cases, React handles this automatically. But in some cases it may be necessary to force a synchronous update.
