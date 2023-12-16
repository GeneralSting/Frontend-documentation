# Strict mode

- strict mode makes several changes to normal JavaScript semantics

  1. Eliminates some JavaScript silent errors by changing them to throw errors.
  2. Fixes mistakes that make it difficult for JavaScript engines to perform optimizations: strict mode code can sometimes be made to run faster than identical code that's not strict mode.
  3. Prohibits some syntax likely to be defined in future versions of ECMAScript.

## Invoking strict mode

- applies to entire scripts or to individual functions
- it does not apply to block statements

### Strict mode for scripts

- to invoke strict mode for an entire script requires exact statement `"use strict"`
  ```js
  // Whole-script strict mode syntax
  "use strict";
  const v = "Hi! I'm a strict mode script!";
  ```

### strict mode for functions

- to invoke strict mode for a function requires exact statement `"use strict"` in function's body before any other statements
  ```js
  function myStrictFunction() {
    // Function-level strict mode syntax
    "use strict";
    function nested() {
      return "And so am I!";
    }
    return `Hi! I'm a strict mode function! ${nested()}`;
  }
  function myNotStrictFunction() {
    return "I'm not strict.";
  }
  ```
- to use strict mode can only be applied to the body of functions with simple parameters.

  - using it in functions with `rest`, `default` or `destructed` parameters is a `syntax error`

    - `rest parameter` syntax allows a function to accept an indefinite number or arguments as an array, providing a way to represent `variadic functions` in JS
      ```js
      function sum(...theArgs) {
        let total = 0;
        for (const arg of theArgs) {
          total += arg;
        }
        return total;
      }
      ```
    - `default function parameters` allow named parameters to be initiačized with default values if no value or undefined is passed
      ```js
      function multiply(a, b = 1) {
        return a * b;
      }
      ```
    - `destrcturing assignment` syntax is a JavaScript expression that makes it possible to unpack values from arrays, or properties from objects, into distinct variables

      ```js
      let a, b, rest;
      [a, b, ...rest] = [10, 20, 30, 40, 50];

      console.log(rest);
      // [30, 40, 50]
      ```

### Strict mode fo modules

- the entire contents of JS modules are automatically in strict mode, with no statement needed to initate it

### Strict mode for classes

- all parts of class's body are strict mode code, including class declarations and class expressions

## Changes in strict mode

- converting mistakes into errors (syntax errors or at runtime)
  - changes some previously-accepted mistakes into errors.
  - makes it impossible to accidentally create global variables
  - failing to assign to object properties
    - assignment to non-writable data property
    - assignment to a getter-only accessor property
    - assignment to a new property on a non-existible object
  - failing to delete object properties
  - attempts to delete non-configurable, undeletable property
  - duplicate parameter names
  - legacy octal literals
    - forbids a 0-prefixed octal literal or octal escape esequence
- simplifying how variable references are resolved
- simplifying eval and arguments
- making it easier to write secure JS
  - JS in browsers can access the user's private information, so such JS must be partially transofrmed before it is run, to censor access to foridden functionality. JS flexibility makes it effectively impossible to do this without many runtime checks. Certain language functions are so pervasive that performing runtime checks has a considerable performance cost. a few strict mode tweaks, plus requiring that user-submitted JS be strict mode code and that it will be invoked in a certain manner, sustantially reduce the need for those runtime checks
  - no `this` substitution
    - Thus for a strict mode function, the specified this is not boxed into an object, and if unspecified, this is undefined instead of `globalThis`, `global object`
      - use `call`, `apply`, or `bind` to specify a particular `this`
  - removal of stack-walking properties
- anticipating future ECMAScript evolution
  - extra reserved words
    - identifiers that can't be used as variable names
