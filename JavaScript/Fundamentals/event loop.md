# The event loop

- JavaScript is single threaded programming language (single runtime), has single call stack - do one thing at the time

- JavaScript has a runtime model based on an `event loop`, which is responsible for executing the code, collecting and processing events, and executing queued sub-tasks
  - this model is quite different from models in other languages like C and Java

## Runtime concepts

<div style="text-align:center">
  <img src="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Event_loop/the_javascript_runtime_environment_example.svg" alt="runtime concept visual representation" />
</div>

### Stack

- LIFO, last in, first out

- function calls form a `stack of frames`

  ```js
  function foo(b) {
    const a = 10;
    return a + b + 11;
  }

  function bar(x) {
    const y = 3;
    return foo(x * y);
  }

  const baz = bar(7); // assigns 42 to baz
  ```

- calling `bar`, first fame is created containing references to `bar`'s arguments and local variables
- `bar` calling `foo`, a second frame is created and pushed on top of the first one, containing references to `foo`'s arguments and local variables
- returning foo then bar, the stack is empty

- arguments and local variables may continue to exist, as they are stored outside the stack - so they can be accessed by any nested functions long after their outer function has returned

- **main() function is the first that goes at the stack and it represents the file itself, as file is one big main function which then calls all other functions/variables...**

  - first set to the stack so it means main() is last on stack,

- when an error occurs it prints stack trace - whole stack from funciton where error occured to the function that start calling all functions before

### Heap

- memory allocation happens
- objects are allocated in a head which is just a name to denote a large, mostyl unstructured region of memory

### Queue

- used for `API`s - Web API, Ajax, fetch...
  - APIs callback are placed into task queue, callback is eventually transffered to the stack and then run
- `message queue`, which is a list of messages to be processed, each message has an associated function that gets called to handle the message

  - at some point during the `event loop`, the runtime starts handling the messages on the queue, starting with the oldest one - to do so, message is removed from the queue and its corresponding function is called with the message as an input parameter
    - calling a funciton creates a new stack frame for that function's use

- processing of functions continues until the stack is once again empty, then, the event loop will process the next message in the queue if there is one

- **Task queue and Microtask queue**
  - in task queue goes web APIs, on microtask which is prioritized by event loop goes async await tasks
    - when microtask queue is empty then it checks task queue and deals with it

## Event loop

- got its name because of how it is usually implemented, which usually resembles:

  - waits synchronously for a message to arrive, if one is not already available and wainting to be handled

  ```js
  while (queue.waitForMessage()) {
    queue.processNextMessage();
  }
  ```

### Run-to-completion

- each message is processed completely before any other message is processed
  - whenever a function runs, it cannot be preempted and will run entirely before any other code runs - function runs on thread and cannot be stopped at any point by the runtime system to run other code in another thread
    - if message takes too long the web app is unable to process user interactions like click or scroll - browser mitigates the script with "a script is takking too long to run" dialog
      - make message processing short and if possible cut down one message into several messages

### Adding messages

- messages are often added when an event occurs and there is an event listener attached to it
  - if there is no listener, the event is lost
- `setTimeout` does not run immediately after its time expires

### Zero delays

- calling setTimeout with a delay of 0 (milliseconds) does not execute the callback function after the given interval
  - execution depends on the numer of waiting tasks in the queue - needs to wait for all the code for queued messages to complete even though we specified a particular time limit

### Several runtimes communicating togheter

- web worker or a cross-origin `iframe` has its own stack, heap and message queue
  - two distinct runtimes can only communicate through sending messages via `postMessage` method

## Never blocking

- property of the event loop model is that JavaScript never blocks - handling I/O is typically performed via events and callback, so when the application is waiting for query to return or a fetch request it can still process other things like user input

## Rendering DOM

- rendering happends every 16.7 milliseconds ideally (60 frames in second)
  - **first call stack must be cleared to render - render is given a higher priority than our callbacks**
  - if render is blocked we cannot for example press button, select text - we cannot see response!
