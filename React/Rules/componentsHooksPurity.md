# Components and Hooks must be pure

- pure functions only perform a calculation and nothing more
  - it makes code easier to understand, debug and allows React to automatically optimaze components and hooks correctly

## Purity

- **React is purity**

### Idempotent

- term popularized in functional programming
  - refers to the idea that we always get the same result every time for the same inputs
- move all non-idempotent calculation outside of rendering

### Has no side effects in render

- code with side effects should run **separately from rendering**
  - React can render components multiple times to create the best possible user experience
    - effects like event handler causes UI to update - run after render
- side effects are broader term then effects
  - effetcs refer to the code that is wrapped in `useEffect, while a side effect is a general term for code that has any observable effect other than its primary result of returning a value to the caller

### does not mutate non-local values

- never modify values that are not created locally in render

#### When is it okay to have mutation

- local mutation
  - locally mutation is not "remembered" when the component is rendered again
    - it only stays around as long as the component does - component with local state is always recreated every time is rendered - always returns the same result
- lazy initialization
  - also fine despite not being fully pure
- changing the DOM
  - side effects are not allowed in the render logic of React components

#### Props and state are immutable

#### Return values and arguments to hooks are immutable

- important principle in React is _local reasoning_ - the ability to understand what a component or hook does by looking at its code in isolation
  - hooks should be treated as "black boxes" when they are called

### How does React run code

- React is declarative: we tell React what to render, and React will figure out how best to display it to user
  - React has few phases where it runs code
    - at high level, code runs at the render and outside of it

#### Rendering

- refers to calculating what the next version of UI should look like
- after rendering, **effects** are flushed (meaning they are run until there are no more left) and may update the calculation if the effects have impacts on layout
  - React takes this new calculation and compares it to the calculation used to create the previous version of UI, then **commits** just the minimum changes needed to the DOM to catch it up to the latest version

##### What code runs in render?

- code written at the top of the level, run during render

  ```jsx
  function Dropdown() {
    const selectedItems = new Set(); // created during render
    // ...
  }
  ```

- event handlers and effects does not run in render

  - handlers code is only run when the user triggers it
  - effects are only run after rendering

  ```jsx
  function Dropdown() {
    const selectedItems = new Set();
    const onSelect = (item) => {
      // this code is in an event handler, so it's only run when the user triggers this
      selectedItems.add(item);
    };
  }
  function Dropdown() {
    const selectedItems = new Set();
    useEffect(() => {
      // this code is inside of an Effect, so it only runs after rendering
      logForAnalytics(selectedItems);
    }, [selectedItems]);
  }
  ```
