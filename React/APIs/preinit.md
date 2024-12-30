# preinit

```jsx
preinit("https://example.com/script.js", { as: "script" });
```

- lets eagerly fetch and evaluate a stylesheet or external script

## Reference

- provides the browser with a hint that it should start downloading and executing the given resource, which can save time
  - scripts that we `preinit` are executed when they finish downloading
  - stylesheets that we `preinit` are inserted into the document, which causes them to go into effect right away
- reference: `preinit(href, options)`
  - parameters:
    - **href** - string, URL of the resource we want to download and execute
    - **options** - object, contains properties
      - **as** - required string, type of resource, possible values are **script** or **style**
      - **precedence** - required with stylesheets, says where to insert the stylesheet relative to others
        - stylesheets with higher precedence can override those with lower precedence, possible values are **reset**, **low**, **medium**, **high**
      - **crossOrigin** - string, `CORS policy` to use
        - possible values are **anonymous** and **use-credentials**
        - required when **as** property is set to "fetch"
      - **integrity** - string, a cryptographic hash of the resource to verify its authenticity
      - **nonce** - string, a `cryptographic nonce` to allow the resource when using a strict **Content Security Policy**
      - **fetchPriority** - string, suggests a relative priority for fetching the resource, possible values are **auto** (default), **high** and **low**
  - returns:
    - returns nothing

### Caveats

- multiple calls to `preinit` with the same **href** have the same effect as a single call
- in the browser, `preinit` can be called in any situation
- in server-side rendering or when rendering server components, `preinit` only has an effect if we call it while rendering a component or in an async context originating from rendering a component
  - any other calls will be ignored

## Usage

### Preinit when rendering

- call it when rendering a component, if we know that its children will use a specific resource
  - and it is OK that resource is evaluated and thereby taking effect immediately upon being downloaded

#### Preinitng an external script

- if we want to download the script but to not execute it right away, use `preload` instead
- if we want to load an ESM module, use `preinitModule`

```jsx
import { preinit } from 'react-dom';

function AppRoot() {
  preinit("https://example.com/script.js", {as: "script"});
  return ...;
}
```

#### Preinting a style

- if we want to download the stylesheet but not to insert it into the document right away, use `preload` instead.

```jsx
import { preinit } from "react-dom";

function AppRoot() {
  preinit("https://example.com/style.css", {
    as: "style",
    precedence: "medium",
  });
  return;
}
```

### Preinting in an event handler

- call in an event handler before transitioning to a page or state where external resources will be needed
  - this gets the process started earlier than if you call it during the rendering of the new page or state

```jsx
import { preinit } from "react-dom";

function CallToAction() {
  const onClick = () => {
    preinit("https://example.com/wizardStyles.css", { as: "style" });
    startWizard();
  };
  return <button onClick={onClick}>Start Wizard</button>;
}
```
