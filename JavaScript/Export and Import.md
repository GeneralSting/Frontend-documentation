# Export and Import

## Export

- export values from JavaScript module
- to use `export` declaration in a source file, the file must be interpreted by the runtime as a `module`
  - adding `type="module"` to the script tag
  - modules are automatically interpreted in `strict mode`

### Export types

- exporting declarations
  ```js
  export const name = "joe";
  ```
- export list
  ```js
  export { name1, name2 /*...*/ };
  export { name1 as default /*, … */ };
  ```
- default export
  ```js
  export default class {
    /* ... */
  }
  ```
- aggregating modules

  ```js
  export * from "module-name";
  export * as name1 from "module-name";
  ```

### Export descriptions

- every module can have two different types of export, named export and default export. You can have multiple named exports per module but only <b>one</b> default export.
- export does not export empty object `export {}`
- export declarations can be anonymous

<hr>

## Import

- static `import` declaration is used to import read-only live bindings which are `exported` by another module
- to use `export` declaration in a source file, the file must be interpreted by the runtime as a `module`
  - adding `type="module"` to the script tag
  - modules are automatically interpreted in `strict mode`
  - function-like dynamic `import()` which does not require scripts of `type="module"`

```js
import defaultExport from "module-name";
import * as name from "module-name";
import { export1 } from "module-name";
import { export1 as alias1 } from "module-name";
```

### Forms of import declarations

- named import
  ```js
  import { export1, export2 } from "module-name";
  ```
- default import
  ```js
  import defaultExport from "module-name";
  ```
- Namespace import
  ```js
  import * as name from "module-name";
  ```
- Side effect import
  ```js
  import "module-name";
  ```

### Description

- `import` declarations are designed to be syntatically rigid, which allows modules to be statically analyzed and linked before getting evaluated. this is the key to making modules asynchronous by nature, powering features like `top-level await`
