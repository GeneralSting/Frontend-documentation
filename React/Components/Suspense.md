# Suspense

## Reference

- `<Suspense>`
- allows to display a fallback until its children have finished loading
- `children` props is actual UI that is intended to be rendered. If `children` suspends while rendering, the Suspense boundary will switch to rendering `fallback`
- `fallback` props is an alternative UI to render in place of the actual UI if it has not finished loading
  - any valid React node is accepted, though it should be a lightweight placeholder view (loading spinner or skeleton)
  - Suspense automatically switches to `fallback` when `children` suspends, and back to `children` when the data is ready
    - if `fallback` suspends while rendering, it will activate the closest parent Suspense boundary

### Caveats

- React does not preserve any state for render that got suspended before they were able to mount for the first time. When the component has loaded, React will retry rendering the suspended tree from scratch
- again suspended content will be replaced by the `fallback` unless the update causing it was caused by `startTransition` or `useDeferredValue`
- if React needs to hide the already visible content because it suspended again, it will clean up **layout Effects** in the content tree. When the content is ready to be shown again, React will fire the layout Effects again. This ensures that Effects measuring the DOM layout don't try to do this while the content is hidden
  - React hides already visible content - when component that uses Suspense suspends, React might need to hide the content that was previously visible. Hiding the content means React unmounts it from the DOM to show the fallback UI
  - cleaning up layout Effects - when React unmounts/hides the content, it cleans up any layout Effects associtated with that content (`useEffect` and `useLayoutEffect`). This prevents those Effects from trying to read or modify the DOM while the content is hidden (also applies for cleanup functions)
  - firing layout Effects again - when the suspended content is ready, react remounts the content (re-fire the layout Effects)
- React includes under-the-hood optimization like _Streaming Server Rendering_ and _Selective Hydration_ that are integraed with Suspense (Suspense SSR architecture)

## Usage

### Displaying a fallback while content is loading

- only Suspense-enabled data sources will activate the Suspense component
  - data fetching with Suspense-enabled frameworks like Relay and Next.js
  - Lazy-loading component code with `lazy`
  - reading the value of Promise with `use`
- Suspense does not detect when data is fetched inside an Effect or event handler

### Showing stale content while fresh content is loading

- both **deferred values** and **Transitions** let us avoid showing Suspense fallback in favor of inline indicators. Transitions mark the whole update as non-urgent so they are typically used by frameworks and router libraries for navigation. Deferred values, on the other hand, are mostly useful in application code where we want to mark a part of UI as non-urgent and let it "lag behind" the rest of the UI
