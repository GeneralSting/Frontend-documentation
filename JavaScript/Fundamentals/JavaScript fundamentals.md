# JavaScript fundamentals

## Data type conversions

### Type conversions

- even though JavaScript leverages dynamic typing, we still need to understand how types work in the language. This includes knowing how to ceonvert one type to another type. The process of changing from one type to another is called conversion.
- using the <span style="color:#ffc75f">typeof</span> function

```js
let strValue = "Hello World";
let numValue = 1;
let boolValue = true;
console.log(typeof strValue); // string
console.log(typeof numValue); // number
console.log(typeof boolValue); // boolean
```

- joining a non-string value with a <span style="color:#ffc75f">string</span>

```js
let age = 41;
let firstName = "David";
let description = `${firsName} is ${age} years old`;
console.log(description); // David is 41 years old
```

- converting a string to a <span style="color:#ffc75f">number</span>
- Number function vs new number created by constructor

```js
let ageString = "41";
let ageNum = Number(ageString);
console.log(typeof ageNum); // number
let ageNewNum = new Number(ageString);
console.log(typeof ageNewNum); // object
```

- <span style="color:#ffc75f">NaN</span>, Not-a-Number

```js
let ageString = "forty-one";
let ageNum = Number(ageString);
console.log(`Age String: ${ageNum}`); //Age String: NaN
let isInvalid = isNan(ageNum);
console.log(isInvalid); //true
```

- converting a value to a <span style="color:#ffc75f">boolean</span>

```js
let num = 1;
let num2 = 0;
let bool = Boolean(num);
let bool2 = Boolean(num2);
console.log(`num: ${bool} num2: ${bool2}`); // num: true num2: false

let str = "Hello";
let bool3 = Boolean(str);
let val; //undefined by default
let bool4 = Boolean(val);
console.log(`str: ${bool3} val: ${bool4}`); // str: true val: false
```

<br>

### JSON

- JavaScript Object Notion(<span style="color:#ffc75f">JSON</span>) enebles developers to cenvert a JavaScript object into a string. This string can be passed between applications, stored on the local file system, or loaded at runtime.
- similar to the object literal syntax
- requires double quotes for property names
- requires any string values to be in double quotes
- won't include undefined properties or functions
- convert object to JSON string

```js
// employee is some object
let jsonValue = JSON.stringify(employee);
let jsonValueClear = Json.stringify(employee, null, 2); // easier to read
```

- convert value back to object

```js
let newEmployee = JSON.parse(jsonValue);
```

- improperly formatted JSON gives syntax error

<br>

### Formatting Numbers

- <span style="color:#ffc75f">locale</span> in computing is a set of parameters that defines the user's language, region and any special variant preferences that the user wants to see in their user interface. Usually a locale identifier consists of at least a language code and a country/region code. Locale is an important aspect of i18n (internationalization)
  - basic locale code -> language-region
    - en-US
    - en-GB
    - fr-FR
- rounding number to an integer

```js
let num = 5.618345;
console.log(`Round: ${Math.round(num)}`); // Round: 6
console.log(`Ceiling: ${Math.ceil(num)}`); // Ceiling 6
console.log(`Floor: ${Math.floor(num)}`); // Floor: 5

let num2 = 5.028345;
console.log(`Round: ${Math.round(num2)}`); // Round: 5
console.log(`Ceiling: ${Math.ceil(num2)}`); // Ceiling 6
console.log(`Floor: ${Math.floor(num2)}`); // Floor: 5

// fixed
let fixed = num.toFixed(3);
console.log(`Fixed type: ${typeof fixed}, Fixed value: ${fixed}`); // Fixed type: string, Fixed value: 5.618
```

- display in locale-specific format

```js
let num = 1_000_000;
console.log(`USA: ${num.toLocaleString("en-US")}`); // USA: 1,000,000
console.log(`Greece: ${num.toLocaleString("el-EL")}`); // Greece: 1.000.000
console.log(`Bangladesh: ${num.toLocaleString("bg-BG")}`); // Bangladesh: 1 000 000
```

- Intl format currency

```js
let salary = 100000;
let monthlySalary = salary / 12;
console.log(`Monthly salary: ${monthlySalary.toFixed(2)}`); // Monthly salary: 83333.33

let formatter = new Intl.NumberFormat("en-US", {
  style: "currency",
  currency: "USD",
});
console.log(`US Dollars: ${formatter.format(monthlySalary)}`); // US Dollars: $8,333.33

let formatter2 = new Intl.NumberFormat("ja-JA", {
  style: "currency",
  currency: "JPY",
});
console.log(`Yen: ${formatter2.format(monthlySalary)}`); // Yen: ¥8,333
```

<br>

### Formatting dates

- create a <span style="color:#ffc75f">date</span>

```js
let date = new Date("2023-01-23T14:23:02-05:00");
console.log(`Date: ${date}`); // Date: Mon Jan 23 2023 14:23:02 GMT-0500 (Eastern Standard Time)

// calendar date
console.log(`Calendar date: ${date.toDateString()}`); // Calendar date: Mon Jan 23 2023

// locale-specific date string
console.log(`Locale en-US: ${date.toLocaleDateString("en-US")}`); // Locale en-US: 1/23/2023
console.log(`Locale ja-JP: ${date.toLocaleString("ja_JP")}`); // Locale ja-JP 2023/1/23

// display just the time
console.log(`Date time: ${date.toTimeString}`); // Date time: 14:23:02 GMT-0500 (Eastern Standard Time)

// locale-specific time string
console.log(`Locale en-US: ${date.ToLocaleTimeString("en-US")}`); // Locale en-US: 2:23:02 PM
console.log(`Locale ja-JP: ${date.ToLocaleTimeString("ja-JP")}`); // Locale ja-JP: 14:23:02
```

- custom date string

```js
let date = new Date("2023-01-23T14:23:02-05:00");

let options = {
  dateStyle: "short",
  timeStyče: "short",
};

console.log(`Custom date: ${date.toLocaleString("en-US", options)}`); // Custom date: 1/23/23, 2:23 PM
```

- Intl.DateTimeFormat() constructor

<hr>

<br>

## Conditional logic and control flow

### falsy values

- a <span style="color:#ffc75f">falsy</span> (sometimes written falsey) value is a value that is considered false when encountered in a Boolean context. JavaScript uses type conversion to coerce any value to a Boolean in contexts that require it, such as conditionals and loops.
- simply function to log out truthyness

```js
const isThruthy = (name, exp) => {
  console.log(`${name}: ${Boolean(exp)}`);
};

// Numbers
isThruthy("val", 0); // val: false
isThruthy("val1", 1); // val1: true
isThruthy("val2", -1); // val2: true
isThruthy("val3", NaN); // val3: false
isThruthy("val4", 0n); // val4: false

// Boolean, null and undefined
isThruthy("val5", undefined); // val5: false
isThruthy("val6", null); // val6: false
isThruthy("val7", false); // val7: false

// Strings -> checks if string has value
isThruthy("val8", ""); // val8: false
isThruthy("val9", "HI"); // val9: true
isThruthy("val10", "false"); // val10: true

// Objects
isThruthy("val11", {}); // val11: true

// Undefined variables -> undefined value
let variable;
isThruthy("val12", variable); // val12: false
```

<br>

### Multiple conditions in 'if' statement

```js
if ((Type == 2 && PageCount == 0) || (Type == 2 && PageCount == "")) {
  // ...
}
// shorten version, taking out same factor
if (Type == 2 && (PageCount == 0 || pageCount == "")) {
  // ...
}
```

<hr>

<br>

## Collections and loops

### Collection types

- <span style="color:#ffc75f">Array</span> in JavaScript is an ordered collection of items. It has a length property and methods for manipulating the list. Arrays should be used for collection where the order matters

  ```js
  var cars = new Array("Saab", "Volvo", "BMW");
  var cars2 = ["Saab", "Volvo", "BMW"];
  // arrays are exactly the same

  var myNumbers = [42]; // creates array with single item, 42
  var myNumbers = new Array(42); // creates array with length 42
  // arrays are not same (in case when there is only one item and it's numeric)

  var myNumbers = [42, 50];
  var myNumbers = new Array(42, 50);
  // arrays are exactly the same
  ```

  - functions

  ```js
  unshift(); // adds value at start of array
  shift(); // removes value at start of array

  // splice(start, deleteCount, item1, item2, ... itemN)
  splice(1, 0, "value"); // adds value at second place, removes 0 items
  ```

  - array of objects

  ```js
  const obj = {
    firstName: "David",
    lastName: "Tucker",
  };

  const obj2 = {
    firstName: "Sarah",
    lastName: "Jenkis",
  };

  const obj3 = {
    firstName: "David",
    lastName: "Tucker",
  };

  const employees = [obj, obj2];
  console.log(`Is identical object in array: ${employees.includes(obj3)}`); // Is identical object in array: false.
  // It is false because obj3 points in different block of memory than obj. obj3 is not included in array

  console.log(`Is same object in array: ${employees.includes(obj1)}`); // Is same object in array: true
  // obj1 is included into array
  ```

- <span style="color:#ffc75f">Map</span> is JavaScript collection type that allows you to use any data type as your key. It has a size property and methods for manipulating the collection

  - values can be arrays, objects and functions

  ```js
  // In JavaScript, the const keyword is used to declare a constant variable, which means its value cannot be reassigned after it has been initialized. However, when you use const with objects like arrays or maps, it doesn't make the contents of the object immutable. You can still modify the properties or values within the object. So, if you have a Map declared as const, you can still add, update, or remove key-value pairs from it.
  const map = new Map();

  // Set a function as the key
  const myFunction = () => "HI!";
  map.set(myFunction, "function");

  // Retrieve the value using the same function reference
  const value = map.get(myFunction);

  console.log(value); // function
  ```

- <span style="color:#ffc75f">Set</span> in JavaScript is a collection type that allows for a <span style="color:#ffc75f">unique</span>set of values. It has a size property and methods for manipulating the set.

<br>

### Loops
- <span style="color:#ffc75f">break</span> exists loop
- <span style="color:#ffc75f">continue</span> skips loop step
- we can specify which loop to break, continue with adding value to loop
  ```js
  employeeLoop: for (let employee of employees) {
    for (let property in employee) {
      if(...) {
        continue employeeLoop   // skips step in first loop
        continue                // skips step in the loop it is in
      }
    }
  }
  ```

<hr>

<br>

## Functions

### Arrow function vs traditional function expression

1. lexical

- arrow functions don't have their own <span style="color:#ffc75f">this</span> or <span style="color:#ffc75f">this</span> binding. Instead, those identifiers are resolved in the lexical scope like any other variable. <b>this</b> and <b>arguments</b> refer to the values of <b>this</b> and <b>arguments</b> in the evironment the arrow function is defined in (outside of the arrow function)

2. arrow functions cannot be called with <b>new</b>

- ES2015 distinguishes between functions that are callable and functions that are constructable. If a function is constructable, it can be called with <b>new</b>, new User(). If a function is callable, it can be called without <b>new</b> (normal function call).

- Functions created through function declarations / expressions are both constructable and callable.
  Arrow functions (and methods) are only callable. class constructors are only constructable.

- If you are trying to call a non-callable function or to construct a non-constructable function, you will get a runtime error.

<br>

### Higher-order functions

- in JavaScript, <span style="color:#ffc75f">higher-order functions</span> are functions that can accept other functions as arguments or return functions as their results.

```js
const bookTitles = books.map((book) => book.title);
// map is higher-order function because it takes the callback function (book) => book.title as an argument.
// the provided callback function (book) => book.title is a simple arrow function that takes each book object from the books array and extracts the title property from it.
// map then applies this callback function to each element in the books array, creating a new array (bookTitles) with the extracted titles.
```

<hr>

<br>

## Asynchronous JavaScript and error handling

### Synchronous vs asynchronous

- <span style="color:#ffc75f">Promise</span> is the object that represents the eventual completion or failure of an asynchronous operation and its resulting value
  - <span style="color:#ffc75f">resolve()</span>
  - <span style="color:#ffc75f">reject()</span>
  - <span style="color:#ffc75f">then()</span>
  - <span style="color:#ffc75f">catch()</span>

### Using callbacks

- <span style="color:#ffc75f">throw</span> statement throws a user-defined exception. Execution of the current function will stop (the statements after throw won't be executed), and control will be passed to the first catch block in the call stack. If no catch block exists among caller functions, the program will terminate.

```js
throw error; // Throws a previously defined value (e.g. within a catch block)
throw new Error("Required"); // Throws a new Error object
```

- <span style="color:#ffc75f">try...catch</span> statement is comprised of a try block and either a catch block, a finally block, or both. The code in the try block is executed first, and if it throws an exception, the code in the catch block will be executed. The code in the finally block will always be executed before control flow exits the entire construct.

```js
try {
  nonExistentFunction();
} catch (error) {
  console.error(error);
  // Expected output: ReferenceError: nonExistentFunction is not defined
  // (Note: the exact output may be browser-dependent)
}
```

<b>

### Using Promises with async and await

- <span style="color:#ffc75f">async</span> function declaration declares an async function where the await keyword is permitted within the function body. The async and await keywords enable asynchronous, promise-based behaviour to be written in a cleaner style, avoding the need to explicitly configure promise chains... Use of async and await enables the use of ordinary try / catch block around asynchronous code

```js
async function loadData() {
  try {
    const data = await // ...
    const dataObj = JSON.parse(data);
    console.log("Complete");
  }
  catch (err) {
    throw err;
  }
}

loadData().then(() => console.log("Promise completed"))
// Complete
// Promise completed
```
- <span style="color:#ffc75f">top-level await</span> enables modules to act as big async functions: With top-level await, ECMAScript Modules (ESM) can await resources, causing other modules who import them to wait before they start evaluating their body.
  - without async keyword on function declaration

<br>

### Event handling

- <span style="color:#ffc75f">Events</span> are things that happen in the system you are programming - the system produces or fires a signal of some kind when an event occurs, and provides a mechanism by which an action can be automatically taken (that is, some code running) when the event occurs
  - system events
  - mouse click
  - key presses
  - async progress events

<hr>

<br>

## Modules

### Using third-party modules
- <span style="color:#ffc75f">Package Manager</span> in terms of software development, a package manager is a tool that enables you to install and manage software written by other developers into your own software projects.
  - package management options
    - package management clients:
      - <span style="color:#ffc75f">npm</span>
      - <span style="color:#ffc75f">yarn</span>
      - pnpm
    - registeres
      - npm

<hr>

<br>

## Code formatting and testing

### Unit testing
- <span style="color:#ffc75f">unit testing</span> is where individual components or units of an application are tested to make sure they behave as the author intended. Tese tests are usually written for a specific unit testing framework. it is common for these tests to get executed every time code is committed to a project to ensure the new code does not break application functionality.
  - Unit testing is just one type of testing that complex software projects may leverage
  - JavaScript testing frameworks
    - Jest
    - Mocha
    - Jasmine
    - AVA
    - Vitest
- code coverage is a metric designed to tell you how much of an application is actually tested by the collection of unit tests that have been written for it. While there are different approaches for calculating this metric, it is generally assumed that a higher code coverage number is better than a lower one as it means more of the application is tested by the unit tests.

<br>

### Code linting
- <span style="color:#ffc75f">linting</span> is the automated checking of your source code for programmatic and stylistic errors. This is done by using a lint tool (otherwise known as <span style="color:#ffc75f">linter</span>). A lint tool is a basic static code analyzer... Linting is important to reduce errors and improve the overall quality of your code. Using lint tools can help you accelerate development and reduce costs by finding errors earlier.