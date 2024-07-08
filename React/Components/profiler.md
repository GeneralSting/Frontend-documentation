# Profiler

## Reference

- `<Profiler>`
- allows to measure rendering performance of a React tree programmatically
- wrap a component tree in a `Profiler` to measure its rendering performance

  - `id` is a string identifying the part of the IU we are measuring
  - `onRender` is callback that Reacts calls every time components within the profiled tree update. It receives informaiton about what was rendered and how much time it took
    - React calls `onRender` callback with information about what was renderd
    - `id` parameter is string prop of the `<Profiler>` tree that has just commited - lets identify which part of the tree is commited
    - `phase` parameter can have values: **"mount"**, **"update"** or **"nested-update"**. This lets us know whether the tree has just been mounted for the first time, or re-rendered due to a change
    - `actualDuration` parameter is the number of milliseconds spend rendering the `<Profiler>` and its descendants for the current update
      - indicates how well the subtree makes use of memoization
      - ideally this value should decrease significantly after the initial mount (after that only needs to re-render spcific props change while initial render paints whole logic)
    - `baseDuration` parameter is the number of milliseconds estimating how much time it would take to re-render the entire `<Profiler>` subtree without any optimizations - this value estimates a worst-case cost of rendering. Compare with `actualDuration`
    - `startTime` parameter is a numberic timestamp for when React began rendering the current update
    - `commitTime` parameter is a number timestamp for when React commited the current update. This value is shared between all priflers in a commit, enabling them to be grouped if desirable

  ```jsx
  <Profiler id="App" onRender={onRender}>
    <App />
  </Profiler>
  ```

  ```jsx
  function onRender(
    id,
    phase,
    actualDuration,
    baseDuration,
    startTime,
    commitTime
  ) {
    // Aggregate or log render timings...
  }
  ```

### Caveats

- profilling adds some additional overhead, so it is disabled in the production build by default. to opt into production profiling we need to eanble a special production build with profiling enabled

## Usage

### Measuring rendering performance programmatically

- `<Profiler>` allows to gather measurements programmatically
  - if we need an interactive profiler, we nned the Profiler tab in **React Developers Tools** - it exposes similar functionality as a browser extension
- `<Profiler>` is a lightweight component but using it too much makes CPU and memory overhead to an application
