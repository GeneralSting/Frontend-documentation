# throw

- `throw` statement throws a user-defined exception
- execution of the current function will stop, statements after `throw` won't be executed, and control will be passed to the first `catch` block in the call stack
  - if no `catch` block exists among caller functions, the program will terminate.

```js
throw expression;
```

## Description

- `throw` statement is valid in all contexts where statements can be used
- its execution generates an exception that penetrates through the call stack
- exception should always be an `Error` object or an instance of an `Error` subclass, such as `RangeError`
  - code that catches the error may expect certain properties, such as `message` to be present on the caught value
    - web APIs typically throw `DOMException` instances, which omherit from `Error.prototype`

### Automatic semicolon insertion

- syntax forbids line terminators between the throw keywoed and the expression to be thrown
  ```js
  // invalid code
  throw
  new Error();
  ```
  ```js
  throw; // also invalid, throw must be followed by an expression
  new Error();
  ```
  ```js
  // valid code
  throw (
    new Error()
  );
  ```
