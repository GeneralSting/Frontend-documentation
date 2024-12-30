# createPortal

- allows rendering some children into a different part of the DOM

## Reference

- a portal only changes the physical placement of the DOM node
  - every other way, rendered JSX into a portal acts as a child node of the React component that renders it
    - for example, the child can access the context provided by the parent tree, and events bubble up from children to parents according to the React tree
- `createPortal(children, domNode, key?)`
  - parameters:
    - **chidlren** - JSX code, string, number, array
    - **domNode** - DOM node, node must already exist
      - updated node will cause the protal content to be recreated
    - optional **key** - a unique string or number to be used as the portal’s key
  - returns:
    - React node that can be included into the JSX or returned from a React component

### Caveats

- events from portals propagate according to the React tree rather than the DOM tree
  - if the parent has `onClick` logic, clicking will fire event handler

## Usage

### Rendering to a different part of the DOM

- **pitfall** - it's important to make sure that your app is accessible when using portals
  - manage keyboard focus so that the user can move the focus in and out of the portal in a natural way
