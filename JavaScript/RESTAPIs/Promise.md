# Promise

- `Promise` object represents the eventual completion or failure of an `asynchronous operation` and its resulting value

## Description

- Promise is a proxy for a value not necessarily known when the promise is created

  - it allows us to associate handlers with an asynchronous action's eventual success value or failure reason
  - allows async methods return values like syncronous methods: instead of immediately returning the final value, the async method returns a promise to supply the value at some point in the future

- Promise is in one of these states:

  - pending: initial state, neither fulfilled nor rejected
  - fulfilled: meaning that operation was completed successfully
  - rejected: meaning that the operation failed

- the eventual state of a pending promise can either be fulfilled witrh a value or rejected with a reason (error)

  - when either of these options occur, the associated handlers queued up by a promise's `then` method are called

  ![flowchart showing how the Promise state transitions between states](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/promises.png)

- Promises in JS represent processes that are already happening, which can be chained with callback functions

  - lazy evaluate the expression - using a function with no arguments

- Promise itself has no first-class protocol for cancellation, but we can directly cancel the underlying async operation, typically using `AbortController`

### Term resolved Promise

- this means that the promise is settled or "locked-in" to match the eventual state of another promise, and further resolving or rejecting it has not effect
  - "resolved" promises are often equivalent to "fulfilled"

### Chained Promises

- promise methods `then()`, `catch()` and `finally()` are used to associate further action with a promise that becomes settled. The then() method takes up to two arguments; both are callback functions, one for fulfilled case (first argument) and one for rejected case (second argument)

  - a catch() is really just a then() without passing the fulfillment handler. As these methods return promises, they can be chained

    ```js
    const myPromise = new Promise((resolve, reject) => {
      setTimeout(() => {
        resolve("foo");
      }, 300);
    });

    myPromise
      .then(handleFulfilledA, handleRejectedA)
      .then(handleFulfilledB, handleRejectedB)
      .then(handleFulfilledC, handleRejectedC);
    ```

## Static methods

- `Promise.all()`

  - takes an iterable of promises as input and returns a single Promise, which filfills when all of the input's promises fulfill with an array of fulfillment values
  - rejects when any of input's promises reject, with this first rejection reason

- `Promise.allSettled()`

  - takes an iterable of promises as input and returns a single Promise when all of input's promises settle, with an array of objects that describe the outcome of each promise

- `Promise.any()`

  - this returns promise when any of inputs't promises fulfill, with this first fulfillment value
  - it rejects when all of the input's promises reject with an `AggregateError` containing an array of rejection reasons

- `Promise.race()`

  - returned promise settles with the eventual state of the first promise that settles

- `Promise.reject()`

  - returns a new Promise object that is rejected with the given reason

- `Promise.resolve()`
  - returns a Promise object that is resolved with the given value
    - if the value is a thenable - has a `then()` method, the returned promise will "follow" that thenable, adopting its eventual state; otherwise, the returned promise will be fulfilled with the value

## Instance methods

- `Promise.prototype.then()`

  - appends fulfillment and rejection handlers to the promise, and returns a new promise resolving to the return value of the called handler, or to its original settled value if the promise was not handled

- `Promise.prototype.catch()`

  - appends a rejection handler callback to the promise, and returns a new promise resolving to the return value of the callback if it is called, or to its original fulfillment value if the promise is instead fulfilled

- `Promise.prototype.finally()`
  - appends a handler to the promise, and returns a new promise that is resolved when the original promise is resolved
  - called called when the promise is settled - fulfilled or rejected
