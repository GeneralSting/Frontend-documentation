# preload

```jsx
preload("https://example.com/script.js", { as: "script" });
```

- lets eagerly fetch a stylesheet or external script

## Reference

- provides the browser with a hint that it should start downloading and executing the given resource, which can save time
  - scripts that we `preload` are executed when they finish downloading
  - stylesheets that we `preload` are inserted into the document, which causes them to go into effect right away
- reference: `preload(href, options)`

  - parameters:

    - **href** - string, URL of the resource we want to download and execute
    - **options** - object, contains properties

      - **as** - required string, type of resource, possible values are
        - audio
        - document
        - embed
        - fetch
        - font
        - image
        - object
        - script
        - style
        - track
        - video
        - worker
      - **crossOrigin** - string, `CORS policy` to use
        - possible values are **anonymous** and **use-credentials**
        - required when **as** property is set to "fetch"
      - **referrerPolicy** - string, the `Referrer header` to send when fetching, possible values are **no-referrer-when-downgrade** (default), **no-referrer**, **origin**, **origin-when-cross-origin** and **unsafe-url**
      - **integrity** - string, a cryptographic hash of the resource to verify its authenticity
      - **nonce** - string, a `cryptographic nonce` to allow the resource when using a strict **Content Security Policy**
      - **type** - string, `MIME` type of the resource
      - **fetchPriority** - string, suggests a relative priority for fetching the resource, possible values are **auto** (default), **high** and **low**
      - **imageSrcSet** - string, for use only when **as** has 'image' value
        - specifies the source set of the image
      - **imageSizes** - string, for use only when **as** has 'image' value
        - specifies the sizes of the image

  - returns:
    - returns nothing

### Caveats

- multiple calls to `preload` with the same **href** have the same effect as a single call
  - calls pt `preload` are considered equivalent according to the following rules:
    - two calls are equivalent if they have the same **href** expect if **as** property is set to **image**, two calls are equivalent if they have the same **href**, **imageSrcSet** and **imageSize**
- in the browser, `preload` can be called in any situation
- in server-side rendering or when rendering server components, `preload` only has an effect if we call it while rendering a component or in an async context originating from rendering a component
  - any other calls will be ignored

## Usage

### Preload when rendering

- call it when rendering a component, if we know that its children will use a specific resource

#### Preloading an external script

- if we want the browser to start executing the script immediately (rather than just downloading it), use `preinit` instead
- if we want to load an ESM module, use `preloadModule`

```jsx
import { preload } from "react-dom";

function AppRoot() {
  preload("https://example.com/script.js", { as: "script" });
  return;
}
```

#### Preloading a stylesheet

- if we want the stylesheet to be inserted into the document immediately (which means the browser will start parsing it immediately rather than just downloading it), use `preinit` instead
- preloading a stylesheet, it’s smart to also `preload` any fonts that the stylesheet refers to
  - that way, the browser can start downloading the font before it’s downloaded and parsed the stylesheet

```jsx
import { preload } from "react-dom";

function AppRoot() {
  preload("https://example.com/style.css", { as: "style" });
  preload("https://example.com/font.woff2", { as: "font" });
  return;
}
```

#### Preloading an image

- when preloading an image, the **imageSrcSet** and **imageSizes** options help the browser **fetch the correctly sized image for the size of the screen**

```jsx
import { preload } from "react-dom";

function AppRoot() {
  preload("/banner.png", {
    as: "image",
    imageSrcSet: "/banner512.png 512w, /banner1024.png 1024w",
    imageSizes: "(max-width: 512px) 512px, 1024px",
  });
  return;
}
```

### Preloading in an event handler

- call in an event handler before transitioning to a page or state where external resources will be needed
  - this gets the process started earlier than if you call it during the rendering of the new page or state

```jsx
import { preload } from "react-dom";

function CallToAction() {
  const onClick = () => {
    preload("https://example.com/wizardStyles.css", { as: "style" });
    startWizard();
  };
  return <button onClick={onClick}>Start Wizard</button>;
}
```
