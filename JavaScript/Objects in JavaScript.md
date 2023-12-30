# Objects in JavaScript

## Objects and properties

- Object in javascript is container for other datatypes that is passed via reference and link to a prototype

  - `objects` are containers for other datatypes
  - passed by `reference`

    - primitive datatypes

      ```js
      const myBoolean = false;
      // myBoolean -> false, variable directly applies to variable
      ```

    - objects

      ```js
      const myObj = new Object();
      // myObj -> 0x6a99aa2f, object applies to memory address
      ```

  - link to a `prototype`

## Creating objects

- all objects link to a prototype
- object literal syntax

  - gives a quick way to define object and its properties
  - key-value

  ```js
  const myCourse = {
    title: "Arrays and Objects in JavaScript",
    id: "ps_arr_obj_js",
    author: "Joe Doe",
  };
  ```

- `new` syntax

  - used to create an object of a particular type

  ```js
  const myDate = new Date();
  ```

- `Object.create`
  - allows creation of new object while defining its prototype
  ```js
  const myObj = Object.create(Object.prototype);
  const myObj2 = Object.create(Date.prototype);
  const myObj3 = Object.create(null); // links to no prototype
  ```

## JavaScript Object Prototypes

- objects are predefined
- main/root prototype is `Object.prototype` :exclamation:
  - everything is object because everything inherits the prototype object
- objects link to prototypes which define their behavior
  - calling a property on an object will look through the prototype chain
  ```js
  const myDate = new Date();
  // myDate is empty object with no properties
  // myDate is new object of Date class/prototype
  // so it is linked to Date.prototype which has predefined properties
  // getDate() -> Date.prototype property
  // toString() -> Object.prototype property
  ```
- object vs Object
  - object is the general word for the datatype
  - Object is a standard built-in object, all objects links to `Object.prototype`
- object literals link to `Object.prototype`
- `Object.prototype` sits at the end of prototype
- an object's prototype can be set:
  - with the `new` sytnax
  - by using `Object.create()`

### Creating properties

- can be even objects and functions
- `hasOwn()` property returns true if object has an own property with the given name
  - replaces <b>hasOwnProperty()</b>
  - objectName.hasOwn("property name") -> true
  - objectName.hasOwn("prototype property") -> false

```js
const contentBlockPrototype = {
  id: "No ID",
  title: "No title",
  description: "No description",
};

const contentBlock = Object.create(contentBlockPrototype);

console.log(contentBlock.color); // undefiend
console.log(contentBlock.description); // No description

contentBlock.description = "desc"; // Dot notation
contentBlock[description] = "desc"; // bracket notation

contentBlock.hasOwn("description"); // check if a property exists
if ("description" in contentBlock)
  // check if a property exists

  console.log("hasOwn" in contentBlock); // true
// because it is proeprty of contentBlock
```

| Dot notation                             | Bracket notation                     |
| ---------------------------------------- | ------------------------------------ |
| object.property                          | object&#91;property&#93;             |
| shortest way to access properties        | more flexible                        |
| can't be used for illegal variable names | can compute property name at runtime |

## Anatomy of a property

- property

  - name
  - value
  - `writable`, default true
    - when false:
      - cannot edit :x:
      - cannot delete :x:
      - can change attributes :white_check_mark:
  - `configurable`, default true
    - when false:
      - can editing :white_check_mark:
      - cannot delete :x:
      - cannot change attributes :x:
  - `enumerable`, default true

    - enumerating properties of an object

    ```js
    for (let key in object) {
      // looping through enumerable properties
      console.log(key);
    }
    ```

    - enumerable means be able to be counted of named, one by one
    - enumerable: false means that object property will no longer appear in for...in loop

      ```js
      Object.defineProperty(object, "property", {
        enumerable: false,
      });
      ```

    - ways to iterate through properties

      - for...in loop returns all non-enumerable properties:

        - <b>enumerable</b> :white_check_mark:
        - <e>non-enumerable</b> :x:
        - <b>own</b> :white_check_mark:
        - <b>inherited</b> :white_check_mark:

        ```js
        for (let key in object) {
          console.log(key);
        }
        ```

      - Object.keys access all enumerable own properties

        - <b>enumerable</b> :white_check_mark:
        - <e>non-enumerable</b> :x:
        - <b>own</b> :white_check_mark:
        - <b>inherited</b> :x:

        ```js
        Object.keys(object).forEach((key) => {
          console.log(key);
        });
        ```

      - Object.getOwnPropertyNames access all enumerable and non-enumerable own properties
        - <b>enumerable</b> :white_check_mark:
        - <e>non-enumerable</b> :white_check_mark:
        - <b>own</b> :white_check_mark:
        - <b>inherited</b> :x:
        ```js
        Object.getOwnPropertyNames(object).forEach((key) => {
          console.log(key);
        });
        ```

- editing a property attribute

  ```js
  Object.defineProperty(object, "property", {
    writable: false,
    configurable: false,
  });
  ```

- protecting an entire object from modification, `freeze()`

  - writable: false :x:
  - configurable: false :x:
  - prevents extensions :x:

  ```js
  Object.freeze(object);
  ```

- preventing properties from being configured or added, `seal()`
  - configurable: false :x:
  - prevents extensions :x:
  - properties can still be edited, writable: true :white_check_mark:
  ```js
  Object.seal(object);
  ```
- preventing properties from being added only
  - prevents extensions :x:
  - properties can still be edited, writable: true :white_check_mark:
  - property attributes can still be configured, configurable: true :white_check_mark:
  ```js
  Object.preventExtensions(object);
  ```

## Object references and scope

- reference types defined with `const` cannot be redefined
- objects are `reference` types
- `stack` vs `heap`
  - variables are stored in `stack`
  - `stack` representation:
    - const myvariable 123
    - const myObject 0x3157ff1e
  - objects are stored in `stack` but object value is stored inside `heap` because it cannot be known how big will be object
    - `heap` has dynamic memory allocation while `stack` does not
  - accessing object
    - javascript finds object name, myObject
    - looks for `heap` `reference` (memory allocation)
    - finds object value at `heap` location
  - so referencing object as `const` means that `reference` (memory allocation) cannot be change as `const` variable value cannot be changed
    - we can change object value that is stored in `heap` dynamic memory location but we can't change `reference` stored in `stack`
    - const myvariable (123 :lock:)
    - const myObject (0x3157ff1e :lock:)
    - let myObject2 0x3a57fc2d
      - myObject2 = myObject :white_check_mark: now points on the same `reference`
      - myObject = myObject2 :x: not possible

<br>

![stack and heap](stack_vs_heap.png)

## Comparing and cloning objects

- if two objects has same properties with same values, while comparing them we will get false value
- objects parsed with <b>JSON.parse</b> have a prototype of Object.prototype
- problem with cloning objects :warning:
  ```js
  obj2 = obj1; // obj2 now references on the same memory allocation as obj1
  obj2.newProperty = "new value"; // now even obj1 has newProperty because it changed object value on heap memory location
  // both objects points to the same reference
  ```
- two ways to copy properties
  - `Object.assign`(targetObject, sourceObject);
    - copy all enumerable own properties from one object to another
  - `spread operator`
    - let newObj = {...oldObj};
    - unpacks and returns all enumerable own properties

## Scope in objects

- `this` is a keyword which is used to refer to a particular instance of an object
- objects inside functions

  - primitive types are not modified outside a function, when edited within a function
  - accessing objects within functions gives `reference` to function

    - changing property values affects object because it points to the same `reference`
      ```js
      const fun = function(newObj) {
        newObj.someProperty = "updated"
      }

      fun(myObj)
      console.log(myObj) // myObj with updated someProperty value
      ```
    - giving a function object parameter a new object value will not affect the initial object beacuse new object is `referenced` to new memory location
      ```js
      const fun = function(newObj) {
        newObj = {
          someProperty: "new value"
        };
      }

      fun(myObj)
      console.log(myObj) // myObj unchanged
      ```
## Object wrappers for primitives
- primitive types are kind of objects - `primitive wrappers`
  - a convenient way to get access to object-like functionality on primitives, without need ti instantiate an object
```js
let num = 12.34566;
number.toFixed(2)   // value is created inside heap memory location as object, returns value and delete that object from heap location
```
```js
let num = new Number(12.34565)  // creates new object
```
