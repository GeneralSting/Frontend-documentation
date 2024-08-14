# Object prototypes

- mechanism by which JavaScript objects inherit features from one another

## The prototype chain

- every object in JavaScript has a built-in property which is called its <b>`prototype`</b>
- <b>`prototype`</b> itself is an object
  - prototype will have its own prototype - <b>`prototype chain`</b>
  - <b>`prototype chain`</b> ends when <b>`prototype`</b> that has <b>`null`</b> for its own <b>`prototype`</b> is reached
  - if the object's <b>`prototype`</b> cannot be found search continues through <b>`prototype chain`</b>, if the end of the chain is reached, returned value is <b>`undefined`</b>
    - myObject.toString()
      1. looks for toString in myObject - cannot find
      2. look in the <b>`prototype`</b> object of myObject for toString - property founded
      3. call founded <b>`prototype`</b> property

<hr>

- <b>`Object.getPrototypeOf()`</b>
- :exclamation: <b>`Object.prototype`</b> is the most basic <b>`prototype`</b>, all objects have by default :exclamation:
  - <b>`prototype`</b> of <b>`Object.prototype`</b> is <b>`null`</b> - end of the prototype chain

## Shadowing properties

- overriding object's properties by giving to the new property same name as existed property

  ```js
  const myDate = new Date(1995, 11, 17);

  console.log(myDate.getYear()); // 95

  myDate.getYear = function () {
    console.log("something else!");
  };

  myDate.getYear(); // 'something else!'
  ```

  - it is possible because property is given to the object so when looking for that property it will first be searched inside object, then it will be continue search through <b>`prototype chain`</b>

## Setting a prototype

- <b>`Object.create()`</b>
  - creates a new object and allows to specify an object that will be use as the new object's <b>`prototype`</b>
- constructors
  - in JavaScript all functions have a property named <b>`prototype`</b>
  - when function is called as a constructor, <b>`prototype`</b> property is set as the prototype of the newly constructed object (\_\_proto\_\_)
    ```js
    Object.assign(Person.prototype, personPrototype);
    // or
    // Person.prototype.greet = personPrototype.greet;
    ```

### Own properties
- properties that are defined directly in the object are called <b>`own properties`</b>
  - <b>`Object.hasOwn()`</b> method checks weather a property is an own property