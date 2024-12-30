# prefetch

```jsx
prefetchDNS("https://example.com");
```

- lets eagerly look up the IP of a server that we expect to load resource from

## Reference

- `prefetchDNS` function provides the browser with a hint that it should look up the IP address of a given server
  - if the browser chooses to do so, this can speed up the loading of resources from that server
- reference: `prefetchDNS(href)`
  - parameters:
    - **href** - string, URL of the server we want to connect to
  - returns:
    - returns nothing

### Caveats

- multiple calls to `prefetchDNS` with the same server have the same effect as a single call
- in the browser, `prefetchDNS` can be called in any situation
- in server-side rendering or when rendering server components, `prefetchDNS` only has an effect if we call it while rendering a component or in an async context originating from rendering a component
  - any other calls will be ignored
- if we know the specific resources we will need, we can call other resource loading functions instead that will start loading the resources right away
- **there is no benefit to prefetching to the same server the webpage itself is hosted from because it’s already been connected to by the time the hint would be given**
- **compared with `preconnect`, `prefetchDNS` may be better if you are speculatively connecting to a large number of domains, in which case the overhead of preconnections might outweigh the benefit**

## Usage

### Prefetching DNS when rendering

- call it when rendering a component, if we know that its children will load external resources from the host

### Prefetching DNS in an event handler

- call in an event handler before transitioning to a page or state where external resources will be needed
  - this gets the process started earlier than if you call it during the rendering of the new page or state

```jsx
import { prefetchDNS } from "react-dom";

function CallToAction() {
  const onClick = () => {
    prefetchDNS("http://example.com");
    startWizard();
  };
  return <button onClick={onClick}>Start Wizard</button>;
}
```
