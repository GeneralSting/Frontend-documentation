# Closures

- combination of a function bundled togheter (enclosed) with references to its surrounding state (the `lexical environment`).
- closures are created every time a function is created

## Lexical scoping

```js
function init() {
  var name = "Mozilla"; // name is a local variable created by init
  function displayName() {
    // displayName() is the inner function, that forms the closure
    console.log(name); // use variable declared in the parent function
  }
  displayName();
}
init();
```

- in this particular example, the scope is called a function scope, because the variable is accessible and only accessible withing the function body where it's declared

### Scoping with let and const

- before ES6 there was only two kinds of scopes: `function scope` and `global scope`

  - `var` statements are global variable, blocks don't create scopes for var

  ```js
  if (Math.random() > 0.5) {
    var x = 1;
  } else {
    var x = 2;
  }
  console.log(x); // no error, prints 1 or 2
  ```

- in ES6 `let` and `const` declarations were introduced, which, among other things like `temporal dead zones` allow you to create block-scoped variables. Blocks are treated as scopes

```js
if (Math.random() > 0.5) {
  const x = 1;
} else {
  const x = 2;
}
console.log(x); // ReferenceError: x is not defined
```

- ES6 also intrduced `modules`
  - modules have a separate scope distinct from the global scope - variables, function and other codes defined within a module are not accessible to code in other modules or the global scope unless explicitly exported and imported

## Closure scope chain

- every closure has three scopes:

1. local scope (own scope)
2. enclosing scope (block, function or module scope)
3. global scope
