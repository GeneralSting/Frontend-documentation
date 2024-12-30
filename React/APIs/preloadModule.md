# preloadModule

```jsx
preloadModule("https://example.com/module.js", { as: "script" });
```

- lets eagerly fetch an ESM module

## Reference

- provides the browser with a hint that it should start downloading and executing the given module, which can save time
  - modules that we `preloadModule` are executed when they finish downloading
- reference: `preloadModule(href, options)`
  - parameters:
    - **href** - string, URL of the module we want to download and execute
    - **options** - object, contains properties
      - **as** - required string, must be **'script'**
      - **crossOrigin** - string, `CORS policy` to use, possible values are **anonymous** and **use-credentials**
      - **integrity** - string, a cryptographic hash of the module to verify its authenticity
      - **nonce** - string, a `cryptographic nonce` to allow the module when using a strict **Content Security Policy**
  - returns:
    - returns nothing

### Caveats

- multiple calls to `preloadModule` with the same **href** have the same effect as a single call
- in the browser, `preloadModule` can be called in any situation
- in server-side rendering or when rendering server components, `preloadModule` only has an effect if we call it while rendering a component or in an async context originating from rendering a component
  - any other calls will be ignored

## Usage

### Preloading when rendering

- call it when rendering a component, if we know that its children will use a specific module

  - and it is OK that module is evaluated and thereby taking effect immediately upon being downloaded

- if we want to download the module and execute it right away, use `preinitModule` instead
- if we want to load the script that is not an ESM module, use `preload`

```jsx
import { preloadModule } from "react-dom";

function AppRoot() {
  preloadModule("https://example.com/script.js", { as: "script" });
  return;
}
```

### Preloading in an event handler

- call in an event handler before transitioning to a page or state where external modules will be needed
  - this gets the process started earlier than if you call it during the rendering of the new page or state

```jsx
import { preloadModule } from "react-dom";

function CallToAction() {
  const onClick = () => {
    preloadModule("https://example.com/module.js", { as: "script" });
    startWizard();
  };
  return <button onClick={onClick}>Start Wizard</button>;
}
```
