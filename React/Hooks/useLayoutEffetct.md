# useLayoutEffect

## Reference

```jsx
useLayoutEffect(setup, dependencies?)
```

- Hook is version of `useEffect` that fires before the browser repaints the screen
- can hurt performance, prefer `useEffect` when possible
- `setup` function with Effect's logic
  - can return cleanup function
  - same logic as `useEffect` Hook
- optionaldependencies - list of all reactive values referenced inside of `setup` code

### Caveats

- same problems as `useEffect` Hook
- code inside `useLayoutEffect` and all state updates scheduled from it block the browser from repainting the screen
  - can make app slow

## Usage

### Measuring layout before the browser repaints the screnn

- most components don't need to know their position and size on the screen to decide what to render, they only return JSX. Browser calculates their layout (position and size) and repaints the screen

  - sometimes that's not enough, we should know elements height and whether it fits at certain poistion - render in two passes

    - render the element anywhere, even with a wrong position
    - measure its height and decide where to place the element
    - render the tooltip again in the correct place

    ```jsx
    function Tooltip() {
      const ref = useRef(null);
      const [tooltipHeight, setTooltipHeight] = useState(0); // You don't know real height yet

      useLayoutEffect(() => {
        const { height } = ref.current.getBoundingClientRect();
        setTooltipHeight(height); // Re-render now that you know the real height
      }, []);

      // ...use tooltipHeight in the rendering logic below...
    }
    ```
