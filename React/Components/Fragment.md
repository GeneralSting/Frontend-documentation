# Fragment

## Reference

- `<Fragment>` (<>...</>)
- allows to group elements without a wrapper node
- wraps elements in `Fragment` to group them togheter in situations where we need a single element

  - has no effect on the resulting DOM
  - shorthand: `<></>`

- optional key must be explicitly declared with `Fragment`

### Caveats

- React does not reset state when we go from rendering `<><Child /></>` to `[<Child />]` or back, or when we go from rendering `<><Child /></>` to `<Child />` and back.
  - this only works a single level deep: `<><><Child /></></>` to `<Child />` resets the state
