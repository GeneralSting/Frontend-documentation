# React APIs

## Built-in React APIs

- in addition to hooks and components, the react package exports a few other APIs that are useful for defining components

### Resource APIs

- resources can be accessed by a component without having them as part of their state
  - reading a message from a **Promise** or read styling information from a **context**
    - `use` lets us to read value of a reasource like **Promise** or **context**

## React DOM APIs

- contains methods that are only supported for the web applications (browser DOM environment)

### APIs

- these APIs can be imported from our components:
  - rarely used
  - `createPortal` - allows rendering child components in a different part of the DOM tree
  - `flushSync` - forces React to flush a state update and update the DOM synchronously

### Resource Preloading APIs

- these APIs can be used to make apps faster by pre-loading resources such as scripts, stylesheets, and fonts as soon as they are needed
  - `prefetchDNS` - prefetch IP address of the DNS domain name
  - `preconnect` - connect to the server
  - `preload` - fetch a stylesheet, font, image or external script
  - `preloadModule` - fetch an ESM module
  - `preinit` - fetch and evaluate an external script or fetch and insert a stylesheet
  - `preinitModule` - fetch and evaluate an ESM module

### Entry Points

- provides two additional entry points
  - `react-dom/client` - contains APIs to render React components on the client (in the browser)
  - `react-dom/server` contains APIs to render React components on the server

### Removed APIs

- APIs removed in the `React 19`
  - `findDOMNode`
  - `hydrate` - use `hydrateRoot` instead
  - `render` - use `createRoot` instead
  - `unmountComponentAtNode` - use `root.unmount()` instead
  - `renderToNodeStream` - use `react-dom/server` APIs instead
  - `renderToStaticNodeStream` - use `react-dom/server` APIs instead
