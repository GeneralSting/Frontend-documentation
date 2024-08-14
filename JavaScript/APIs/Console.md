# Console interface
- provides access to the browser's debugging console (`web console`)
- `console` object can be accessed from any global object

## Outputting text to the console
- `console.log()`
- console.info()
- console.warn()
- console.error()
- console.debug()

### Using string substitutions
- object's methods that accepts a string (log method)
  - %o or %O
    - outputs object, clicking opens more info
  - %d or %i
    - outputs an integer
  - %s
    - outputs a string
  - %f
    - outputs a floating-point value

  ```js
  for (let i = 0; i < 5; i++) {
    console.log("Hello, %s. You've called me %d times.", "Bob", i + 1);
  }
  /* 
  Hello, Bob. You've called me 1 times.
  Hello, Bob. You've called me 2 times.
  Hello, Bob. You've called me 3 times.
  Hello, Bob. You've called me 4 times.
  Hello, Bob. You've called me 5 times. 
  */
  ```

### Styling console output
- %c directive applies a CSS style
  - text before directive won't be affected
  - %c can be used multiple times
  ```js
  console.log(
    "This is %cMy stylish message",
    "color: yellow; font-style: italic; background-color: blue;padding: 2px",
  );
  ```
  ```js
  console.log(
    "Multiple styles: %cred %corange",
    "color: red",
    "color: orange",
    "Additional unformatted message",
  );
  ```

### Groups
- `console.group()`
- `console.groupCollapsed()`
- `console.groupEnd()`

### Timers
- start a `timer` to calculate the duration of a specific operation
- `console.time()` & `console.timeEnd()`
  - name as the only parameter

### Stack trace
- `console.trace()`
  - showing the call path taken to reach the point where is called `console.trace()`