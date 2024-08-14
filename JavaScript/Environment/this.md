# this

- keyword refers to the context where a piece of code, such as a function's body, is supposed to run.
  - used in object methods, where `this` refers to the object that the method is attached to
- the value of `this` inJS depends on how a function is invoked (`runtime binding`), not how it is defined

## Global object

## Value

- non-strict mode: reference to an object
- strict mode: any value
- the value of `this` depends on in which context it appears: function, class or global

### function context

- when invoked as a standalone function (not attached to an object: func()), `this` typically refers to the `global object` in non-strict mode or `undefined` in strict mode.
  - Function.prototype.bind() method can create a function whose `this` binding doesn't change, and methods apply() and call() can laso set the `this` value for a particular call

#### Description

- value of `this` depends on how the function is called
- `this` is a binding that the language creates when the function body is evaluated
- the value of `this` is the object that the functiuon is accessed on, the value is not the object that has the function as an own property, but the object that is used to call the function

- if a function is called with `this` set to undefined or null, `this` gets substituted with `globalThis`
- if the function is called without being accessed on anything, `this` will be undefined — but only if the function is in strict mode.

#### Callbacks

- value of `this` depends on how the callback is called, which is determined by the implementator of the API
  - callbacks are typically called with a `this` value of undefined (calling it directly without attaching it to any object)

#### Arrow function context

- differ in their handling of `this`: they inherit `this` from the parent scope at the time they are defined
  - useful for callbacks and preserving context
  - do not have their own `this` binding - their `this` value cannot be set by bind(), apply(), or call() methods
  - does not point to the current object in object methods

##### Description

- `this` retains the value of the enclosing lexical context's `this`
  - evaluating an arrow function's body, the language does not create a new `this` binding
- in global code, `this` is always `globalThis` regardless of strictness, because of the `global context` binding

```js
const globalObject = this;
const foo = () => this;
console.log(foo() === globalObject); // true
```

- same applies to arrow functions created inside other functions: their this remains that of the enclsoing lexical context
- using call(), bind() or apply(), the `thisArg` parameter is ignored

#### Constructors

- bound to the new object being constructed
- value of `this` becomes the value of the `new` exporession unless the constructor returns another non-primitive value

```js
function C2() {
  this.a = 37;
  return { a: 38 };
}

o = new C2();
console.log(o.a); // 38
```

#### super

- when a function is invoked in the super.method() form, the `this` inside the method function is the same value as the `this` value around the super.method() call, and is generally not equal to the object that `super` refers to
  - this is because super.method is not an object member access - it's a special syntax with different binding rules

### Class context

- class can be split into two context: static and instance
- constructors, methods and instance field initializers (public or private) belong to the instance context

  - static methods, static field initializers, and static initialization blocs belong to the static context - `this` value is different in each context

- class contructors are always called with `new`, so their behavior is the same as function constructors: `this` value is the new instance being created

  - `this` value is the object that the method was accessed of the class

- static methods are not properties of `this`, they are properties of the class itself - accessed on the class and `this` is the value of the class or a subclass
  - static initialization blocks are also evaluated with `this` set to the current class

#### Derived class constructors

- unlike base class constructors, derived constructors have no initial `this` binding

  - calling super() creates a `this` binding within the constructor and essentially has the effect of evaluating the following line of code, where `Base` is the base class:

  ```js
  this = new Base();
  ```

- referring to `this` before calling super() will throw an error :warning:

### Global context

- in the global execution context (outside of any functions or classes) `this` value depends on what execution context the script runs it

  - like callbacks, `this` value is determined by the runtime environment - the caller

- at the top level of a script, `this` refers to `globalThis` whether in strict mode or not - global object

  - this === window

  ```js
  // In web browsers, the window object is also the global object:
  console.log(this === window); // true

  this.b = "MDN";
  console.log(window.b); // "MDN"
  console.log(b); // "MDN"
  ```

- if the source is loaded as a `module` `this` is always undefined at the top level

- object literals con't create a `this` scope - only functions (methods) defined within the object do

  - inherits the value from the surrounding scope

  ```js
  const obj = {
    a: this,
  };

  console.log(obj.a === window); // true
  ```
