# Hoisting

- refers to the process whereby the interpreter appears to move the declaration of functions, variables, classes or imports to the top of their scope, prior to execution of the code
- hositing behaviours:

  - being able to use a variable's value in its scope before the line it is declared - value hoisting
    - `function` declarations
    - import declarations
  - being able to reference a variable in its scope before the line is is declared, without throwing **ReferenceError**, but the value is always `undefined` - declaration hoisting

    - `var` declaration

    ```js
    console.log(b); // Output: undefined
    var b = 20;
    ```

  - the declaration of the variable causes behaviour changes in its scope before the line in which it is declared
    - `let`, `const` and `class` declarations - collectively called lexical declarations
  - the side effects of a declaration are produced before evaluating the rest of the code that contains it
    - `import` declarations

## Temporal dead zone

- `let`, `const` and `class` as non-hoisting because the temporal dead zone strictly forbids any use of the variable before its declaration
