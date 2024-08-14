# try...catch

- statement is comprised of a `try` block and either a `catch` block, a `finally` block or both
  - `try` block is executed first, and if it throws an exception, the code in the `catch` block will be executed
  - code in the `finally` block will always be executed before control flow exits the entire construct
  ```js
  try {
    tryStatements;
  } catch (exceptionVar) {
    catchStatements;
  } finally {
    finallyStatements;
  }
  ```

## Description

- blocks must be blocks, instead of single statements
- if any statement within the `try` block throws an exception, control is immediately shifted to the `catch` block. if no exception is thrown in the `try` block, tha `catch` block is skipped
- you can nest one or more `try` statements. If an inner `try` statement does not have a `catch` block, the enclosing `try` statement's `catch` block is used instead.
- `binding` can be used to get information about the exception that was thrown in the `catch` block
  - `binding` is only available in the `catch` block's scope
  - exception binding is writable
- `finally` block always executes, regardless of whether an exception was thrown or caught.
- `finally` block executes immediately before a control-flow statement (return, throw, break, continue) is executed in the `try` block or `catch` block.
- `finally` block is best used for cleanup code
