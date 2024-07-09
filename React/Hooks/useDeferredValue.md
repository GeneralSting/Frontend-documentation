# useDeferredValue

## Reference

```jsx
const deferredValue = useDeferredValue(value);
```

- Hook allows to defer updating a part of the UI
- `value` parameter is the value we want to defer, can be any type
- :warning: **Canary only** optional `initialValue` parameter is the value to use during the initial render of a component

  - if this parameter is omitted, `useDeferredValue` will not defer during the initial render, because there is no previous version of `value` that it can render instead

- returns `currentValue` - during the initial render, the returned deferred value will be the same as the value that was provided. During updates, React will first attempt a re-render with the old value (so it will return the old value), and then try another re-render in the background with the new value (so it will return the updated value)

- :warning: Canary - in the latest React Canary versions, useDeferredValue returns the initialValue on initial render, and schedules a re-render in the background with the value returned

### Caveats

- when an update is insde a Transition, `useDefferedValue` always returns the new `value` and does not spawn a deferred render, since the update is already deferred
- values passed to `useDeferredValue` should either be primitive values or objects created outside of rendering. If new object is created during rendering and immediately passed it to `useDeferredValue`, it will be different on every render, causing unnecessary background re-renders
- when `useDeferredValue` receives a different value (compared with `Object.is`), in addition to the current render (when it still uses the previous value), it schedules a re-render in the background with the new value. The background re-render is **interruptible**: if there’s another update to the `value`, React will restart the background re-render from scratch. For example, if the user is typing into an input faster than a chart receiving its deferred value can re-render, the chart will only re-render after the user stops typing
- `useDeferredValue` is integrated with `<Suspense>`. If the background update caused by a new value suspends the UI, the user will not see the fallback. They will see the old deferred value until the data loads
- Hook does not by itself prevents extra network requests
- there is no fixed delay caused by Hook itself. As soon as React finishes the original re-render, React will immediately start working on the background re-render with the new deferred value. Any updates caused by events (like typing) will interrupt the background re-render and get prioritized over it
- the background re-render caused ny `useDeferredValue` does not fire Effects until it's commited to the screen. If the background re-render suspends, its Effect wil run after the data loads and the UI updates

## Usage

### Showing stale content while fresh content is loading

- during updates the deferred value will "lag behind" the laters value

  - React tries to re-render without updating the deferred value, and then try to re-render with the newly received value in the background

- Suspense-enabled data source
  - data fetching with Suspense-enabled frameworks like Relay and Next.js
  - lazy-loading component code with `lazy`
  - reading the value of a Promise with `use`

### Deferring re-rendering for a part of the UI

- for optimization is required to have child component wrapped in `memo` when we want to update state in parent component but to have defered value in child component (parent component should immediately get screen update)
  - during re-render React can skip re-rendering child component because there is no changes - **defered value still not updated**

### How is deferring a value vs debouncing and throttling

- two common optimization techniques

  - **Debouncing** means we wait for the user to stop typing (e.g. for a second) before updating
  - **Throttling** means we can update the defered element (e.g. input) (defered value) every once in a while (e.g. at most once a second)

- this techniques are helpful in some cases, `useDeferredValue` is better suited to optimizing rendering because it is deeply integrated with React itself and adapts to the user's device`
  - unlike debouncing or throttling it does not requires to choose any fixed delay
    - React uses logic to chose how big delay will be (it can depend on device we use - faster device, shorter delay)
- `useDeferredValue` Hook's deferred re-renders are **interruptible**
- debouncing and throttling are maybe better in calling a fewer network requests
  - techniques can be combined togheter
