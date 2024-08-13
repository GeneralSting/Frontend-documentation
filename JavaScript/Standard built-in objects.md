# Standard built-in objects

- the term `"global objects"` or standard built-in objects here is not to be confused with the `global object`

## Global object

- object which represents the `global scope`
- only one global object per environment - global object is always defined

  - global object's interface depends on the execution context in which the script is running
    - in web browser, any code which the script does not specifically start up as background task has a `Window` as its global object - vast majority of JS code on the Web
    - code running in a `Worker` has `WorkerGlobalScope` object as its global object
    - scripts running under `Node.js` have an object called `global` as their global object

- the `globalThis` global property allows one to access the global object regarless of the current environment
- `var` statements and `function declarations` at the top level of script create properties of the global object
  - **let** and **const** declarations never create properties of the global object
- properties of the global object are automatically added to **global scope**

- global object always holds a reference to itself

  ```js
  console.log(globalThis === globalThis.globalThis); // true (everywhere)
  console.log(window === window.window); // true (in a browser)
  console.log(self === self.self); // true (in a browser or a Web Worker)
  console.log(frames === frames.frames); // true (in a browser)
  console.log(global === global.global); // true (in Node.js)
  ```

## Standard objects by category (built-in objects)

### Value properties

- these global properties returns a simple value, no methods
  - globalThis
  - Infinity
  - NaN
  - undefined

### Function properties

- these global functions - functions which are called globally, rather than on an object - directly return their results to the caller
  - eval()
  - isNaN()
  - parseFloat()
  - parseInt()
  - DecodeURI()

### Fundamental objects

- these objects represent fundamental language constructs
  - Object
  - Function
  - Boolean
  - Symbol
    - built-in object whise constructor returns a `symbol` primitive, also called a **Symbol value** or just a Symbol
    - guaranteed to be unique -> every Symbol() call is guaranteed to return a unique Symbol. Every `Symbol.for("key")` call will always return the same Symbol for a given value of `"key"`. When Symbol.for("key") is called,
    - often used to add unique property keys to an object that won't collide with keys any other code might add to the object - weak encapsulation, form of weak information hiding

### Error objects

- special type of fundamental object, include basic `Error` type as well as several specialized error types
  - Error
  - AggregateError
  - EvalError
  - RangeError
  - ReferenceError
  - SyntaxError
  - TypeError
  - URIError

### Numbers and dates

- base objects representing numbers, dates and mathematical calculations
  - Number
  - BigInt
  - Math
  - Date

### Text processing

- objects represent strings and support manipulating them
  - String
  - RegExp

### Indexed collection

- objects represent collections of data which are ordered by an index value
  - Array
  - Int8Array
  - Uint8Array
  - BigInt64Array
  - Float32Array

### Keyed collections

- represents collections which use keys
  - Map
  - WeakMap
  - Set
  - WeakSet

### Structured data

- objects represents and interact with structure data buffers and data coded using JSON
  - ArrayBuffer
    - represents a generic raw binary data buffer - array of bytes, "byte array"
    - cannot directly manipulate the contents of ArrayBuffer; isntead we must create one fo the `typed array objects` or a `DataView` object which represents the buffer in a specific format and use that ot read and write the contents of the buffer
  - SharedArrayBuffer
  - DataView
    - view provides a low-level interface for reading and writing multiple number types in a binary **ArrayBuffer**, without haveing to carte about the platform's `endianness` (btye-order that describes how computers organizer the bytes that make up numbers)
  - Atomics
  - JSON

### Managing memory

- objects interact with the garbage collection mechanism
  - WeakRef
  - FinalizationRegistry

### Control abstraction objects

- control abstractions can help to structure code, especially async code, without using deeply nested callbacks
  - Iterator
  - AsyncIterator
  - Promise
  - Generator
  - AsyncGenerator
  - AsyncFunction

### Reflection

- Reflect
- Proxy

### Internalization

- additions to the ECMAScript core for language-sensitive functionalities
  - Intl
  - Intl.DateTimeFormat
  - Intl.Locale
  - Intl.NumberFormat
