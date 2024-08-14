# Inheritance and Object prototypes

## Object prototypes

- `prototype` are the mechanism by which JavaScript objects inheirt features from one another

### Prototype chain

- every object in JS has a built-in property, which is called its **prototype**
  - prototype itself is an object, so the prototype will have its own prototype. so the prototype will have its own prototype, making `prototype chain`
    - the chain ends when we react a prototype that has `null` for its own prototype
    - the property of an object that points to its prototype is not called prototype - it is not standard name, all browsers use` __proto__`
    - standard way to access an object's prototype is the `Object.getPrototypeOf()` method

## Inheritance

- refers to passing down characteristics from a prent to a child so that a new piece of code can reuse and build upon the features of an existing one
- JS implements inheritance by using **objects**

  - each object has an internal link to another object called its prototype. That prototype object has a prototype of its own, and so on until an object is reached with `null` as its prototpye
    - `null` has no prototype and acts as the final link in this **prototype chain**

- classes are not widely adopter and have become a new paradigm in JS, classes do not bring a new iheritance pattern - classes abstract most of the prototypal mechanism away
