# Pro JavaScript Design Patterns

## Ross Harmes and Dustin Diaz

## The essentials of object-oriented JavaScript programming

### Everything in JavaScript is not an Object

- it is a very common misbelief or misstatement that everything in JavaSCript is an object. Objects are the general building blocks which JavaScript is built on but that does not mean that everything is an object
- JS has two main kinds of values:

#### Primitive values

- immutable values
- string
- number, all numbers in JS are floating-point
- boolean
- null, assignment value that means `"no value"`
  - typeof null returning object"" but this is a well-known bug in JS that can't be fixed because it would break existing code. that does not mean that null is actually an object
- undefined, unassigned variables with a default value of undefined

#### Objects

- mutable
- all non primitive values are objects
- wrappers for primitives: `Boolean`, `Number`, `String`
- creatable by literals, produces objects that can also be created via a constructors
  - use literals whenever you can
  - `Array`: [] same as new Array();
  - `Object`: {} same as new Object()
  - `Function`: function(){} same as new Function()
  - `RegExp`: /\s*/ same as new RegExp("\s*")
  - `Date`: new Date("2011-12-24)
  - `Error`: create Error object with intention of raising it using the throw keyword, thwor new Error("error")

```js
var strPrimitive = "This is a string";
typeof strPrimitive; // "string"
strPrimitive instanceof String; // false

var strObject = new String("This is a string");
typeof strObject; // "object"
strObject instanceof String; // true
```

- in the above code-snippet the primitive value "This is a string" is not an object, it's a primitive literal and immutable value. To perform operations on it, such as checking its length, accessing its individual character contents, etc, a String object wrapper is required.

### Encapsulation and information hiding

#### Scope, nested functions and closures

```js
function foo() {
  var a = 10;
  function bar() {
    a *= 2;
    return a;
  }
  return bar;
}

var baz = foo(); // baz is now a reference to function bar.
baz(); // returns 20.
baz(); // returns 40.
baz(); // returns 80.
var blat = foo(); // blat is another reference to bar.
blat(); // returns 20, because a new copy of a is being used.
```

### Inheritance

#### Prototypal inheritance

- in prototypal inheritance, instead of defining the structure through a class, you simply
  create an object. This object then gets reused by new objects, thanks to the way that prototype
  chain lookups work. It is called the prototype object because it provides a prototype for what
  the other objects should look like
- object literal -> prototype object
