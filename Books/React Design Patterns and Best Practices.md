# React Design Patterns and Best Practices

## Michele Bertoli

## Build easy to scale modular applications using the most powerful components and design patterns

### Declarative programming

- the fact that React offers a declarative approach makes it easy to use, and consequently, the
  resulting code is simple, which often leads to fewer bugs and more maintainability.

### React elements

- to control the UI flow, React uses a particular type of object, `element`
  - `immutable objects`, once element is created it can't change its children or attributes
  - only way to update the UI is to create a new element and pass it to `ReactDOM.render()`
- whenever you call `createClass`, extend `Component` or simply declare a stateless function, you are creating a component

  - React manages all the instances of your components at runtime, and there can be more than one instance of the same component in the memory at a given point in time

- elements have a type, which is the most important attribute and some properties
  - special property called `children` which is optional and represents the direct descendant of the element
  - type tells React how to deal with the element itself
    - type string represents a `DOM node`
    - type function is the `component` element

#### React Element Tree

- simplified form of the DOM. It's like a snapshot. React has the current snapshot and when the state of na application changes, it creates a new state that reflects how the DOM should look like. React compares those two snapshots and makes required changes to the DOM so that it mirrors the new snapshot. After that the old, outdated snapshot is trashed and the new one becomes the current snapshot of the DOM

### React and react-dom

- React is split into these two scripts/packages
  - `react` implements the core features of the library
  - `react-dom` contains all the browser-related features

### Babel

- transpilation is process that compiles the source into a new source rather than into an executable
- HTML button is transipled into the following: `React.createElement('button')`
- created _Button_ component is transpiled into the following: `React.createElement(Button)`

### Basics of functional programming

- functional programming is a declarative paradigm
- first-class objects
  - functions/components are objects
  - `Higher-order Components (HoC)`
- purity
  - no sideeffects, function does not change anything that is not local to the functions itself
- immutablity
  - pure functions do not mutate the state
  - instead of changing the value of a variable, function creates a new avriable with a new value and returns it
- currying
  - process of converting a function that takes multiple arguments into a function that takes one argument at a time, returning another function
- composition
  - functions and components can be combined to produce new functions with more advanced features and properties

### Autobinding

- E2015 arrow function automatically binds the current this to the body of the function

```js
() => this.setState();
```

gets transpiled into the following code with Babel:

```js
var _this = this;

(function () {
  return _this.setState();
});
```

- binding a function inside the render method has in fact an unexpected sife-effect because the arrow function gets fired every time the component is rendered
  - if we are passing the function down to a child component, it receives a new prop on each update which leads to inefficient rendering
  - best way to solve it is to bind the function isnde the construction in a way that it does not ever change even if the component renders multiple times:

```js
class Button extends React.Component {
  constructor(props) {
    super(props);
    this.handleClick = this.handleClick.bind(this);
  }
  handleClick() {
    console.log(this);
  }
  render() {
    return <button onClick={this.handleClick} />;
  }
}
```

### Stateless functions

#### State

- the name stateless tells us clearly that the stateless functional components do not have any internal state, and the fact that this does not exist enforces it. That makes them extremely powerful and easy to use at the same time
- the stateless functional components only receive props and context and they return the elements

#### The this keyword

- one thing that makes the stateless functional components different from their stateful counterparts is the fact that `this` does not represent the component during their execution

### The render method

#### Cheat sheet from Dan Abramov

```js
function shouldIKeepSomethingInReactState() {
  if (canICalculateItFromProps) {
    // do not duplicate data from props in state.
    // calculate what you can in render() method
    return false;
  }
  if (!amIUsingItInRenderMethod()) {
    /*
    do not keep something in the state 
    if you do not use it for rendering
    for example, API subscriptons are 
    better of as custom private fields 
    or variables in external modules
    */
    return false;
  }
  // you can use React state for this!
  return true;
}
```

### Children prop

- special prop that can be passed from the owners to the components defined inside their render method
- described as **opaque** because it is a property that does not tell anything about the value it contains

### Container and Presentational pattern

- react components typically contain a mix of `logic` and `presentation`
- `Container` knows everything about the logic of the component and it's where the APIs are called
  - deals with data manipulation and event handling
  - more concerned about the behavior
  - render their presentational components
  - make API calls and manipulate data
  - define event handlers
- `Presentational` component is where the UI is defined and it receives data in the form of props from the container
  - logic-less
  - functional stateless component
  - more concerned with the visual representation
  - render the HTML markup
  - receive data from the parents in the form of props
