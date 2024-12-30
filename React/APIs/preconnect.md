# preconnect

```jsx
preconnect("https://example.com");
```

- lets eagerly connect to the server that we expect to load resources from

## Reference

- preconnecting speeds up the loading of resource from the server
- reference: `preconnect(href)`
  - parameters:
    - **href** - string, URL of the server we want to connect to
  - returns:
    - returns nothing

### Caveats

- multiple calls to `preconnect` with the same server have the same effect as a single call
- in the browser, `preconnect` can be called in any situation
- in server-side rendering or when rendering server components, `preconnect` only has an effect if we call it while rendering a component or in an async context originating from rendering a component
  - any other calls will be ignored
- if we know the specific resources we will need, we can call other resource loading functions instead that will start loading the resources right away
- **there is no benefit to preconnecting to the same server the webpage itself is hosted from because it’s already been connected to by the time the hint would be given**

## Usage

### Preconnecting when rendering

- call `preconnect` when rendering a component if we know that its children will load external resources from that host

### Preconnecting in an event handler

- call in an event handler before transitioning to a page or state where external resources will be needed
  - this gets the process started earlier than if you call it during the rendering of the new page or state

```jsx
import { preconnect } from "react-dom";

function CallToAction() {
  const onClick = () => {
    preconnect("http://example.com");
    startWizard();
  };
  return <button onClick={onClick}>Start Wizard</button>;
}
```
