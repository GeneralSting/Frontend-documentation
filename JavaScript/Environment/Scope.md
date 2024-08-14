# Scope

- the `scope` is the current context of execution in which values and expressions are "visible" or can be referenced
  - if a variable is not in the current scope, it will not be available to use
  - scopes can also be layered in a hierarchy, so that child scopes have access to parent scopes, but not vice versa

## Global scope

- default scope for all code running in script mode
- contains various properties of code (properties and methods)

  - methods: fetch(), find(), getScreenDetails()...
  - properties: pageXOffset, parent, performance...
  - also contains functions that are declared in below scopes - child's properties and functions

- **`var` declaration variables are stored in global scope**

## Module scope

- scope for code running in module mode

## Funciton scope / Local scope

- scope created with a function

## Block scope

- created with a pair of curly braces (a block)
- in addition, identifiers declared with certain syntaxes including `let`, `const`, `class` (in strict mode) or function can belong to an additional scope - block scope

  - block scope doe not scope the `var` declarations

  ```js
  // var declaration
  {
    var x = 1;
  }
  console.log(x); // 1

  // const/let declaration
  {
    const x = 1;
  }
  console.log(x); // ReferenceError: x is not defined
  ```

## Google's V8 JavaScript engine - script scope

- this scope does not exists in JavaScript but in V8 engine
  - engine calls the part of global environment that holds the new style of lexically-scoped globals created when we use `let`, `const` and `class` at global scope. They are still globals, but they are different from the older style of globals created by `var` and function declarations at global scope - V8 debugger lists the `two types of globals` in those two different places
