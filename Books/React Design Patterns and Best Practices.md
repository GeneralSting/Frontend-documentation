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

### Data flow

1. `Undirectional Data Flow` - from the root to the leaves, sigle direction from the top to the bottom of the tree
2. Child-parent communication (callbacks), when data goes from child (inner) component (function), those components/functions all called `callbacks`

### Forms

#### Uncontrolled components

- a component that renders form elements, where the form element's data is handled by the **DOM (default DOM behavior)**. To access the input's DOM node and extract its value you can use a _ref_.

```js
const Uncontrolled = () => (
  <form>
    <input type="text" />
    <button>Submit</button>
  </form>
);
```

#### Controlled components

- a component that renders form elements and controls them by keeping the form data in the **component's state**
  - in a controlled component, the form element's data is handled by the **React component** (not DOM) and kept in the component's state. A controlled component basically overrides the default behavior of the HTML form elements.

```js
// if we run this component isnide the browser, we realize that it shows the default value as expected, but it does not let us change the value or type anything else inside it
// input is read-only
// onChange handler expected for full control
const Controlled = () => (
  <form>
    <input type="text" value="Hello React" />
    <button>Submit</button>
  </form>
);
```

### Events

- events work in a slightly different way across the various browsers
- React tries to abstract the way events work and give developers a consistent interface to deal with
  - `synthetic event` is an object that wraps the original event object provided by the browser and it has the same properties, not matter the browser where it is created
    - synthetic events are reused, and that there is a `single global handler`
    - we cannot sotre a synthetic event and reuse it later because it becomes null right after the action
  - single event listener is attached to the root element, which listens to all the events - `event bubbling`
    - when an event is fired by the browser, React calls the handler on the spcific components on its behalf - `event delegation` (memory and speed optimization)

### Universal applications

- `universal application` - app that can run both on the server and on the client side with the same code
- `isomorphic application` - building application that looks the same on the server and the client

### Server-side rendering

- SSR does not give us the level of interactivity for users, while CSR does not get indexed by search engines
- SEO
  - Search Engine Optimization
- common code base
- better performance
  - CSR needs to wait for the bundle to be loaded and run before users can take any actions

### Reconciliation and keys

- `render method` - when React has to display a component and the render methods of its children recursively

  - render method of a component returns a tree of React elements, which React uses to decide which DOM operations have to be done to update the UI

- `reconciliation` - whenever a component's state changes, React calls the render methods on the nodes again and it compares the result with the previous tree of React elements

  - minimum operations required to apply the expected changes on the screen
  - comapring two trees of elements is not free either and React makes two assumptions to reduce its complexity
    - if two elemnts have a different type, they render a different tree
    - developers can use keys to mark children as stable across different render calls
      - warning in the browser console: "Each child in an array or iterator should have a unique "key" prop. Check the render method of `List`."

- React tries to apply the smalles possible number of operations on the DOM because touching the `Document Object Model` is an expensive operation

### Optimization techniques

- Webpack
  - build the bundle setting the NODE*ENV environment variable to \_production*
  - minify the resulting code to save bytes and make the application load faster

```js
new webpack.DefinePlugin({
  'process.env': {
  NODE_ENV: JSON.stringify('production')
  }
}),
```

```js
new webpack.optimize.UglifyJsPlugin();
```

### Common testing solutions

- testing higher-order components
- the page object pattern

### Anti-Patterns

#### Initializing the state using props

- duplicated source of truth
- if the prop passed to the component changes the state does not get updated

#### Mutating the state

- straightforward API to mutate the internal state of components - `setState` function
- mutate state without using setState
  - the state changes without making the component re-render
  - whenever setState get called in future, the mutated state gets applied

#### Using indexed as a key

- index always starts from 0 even if we push a new item to the top of the list so React thinks that we changed the values of the existing items and that we addded a new element at new index value

#### Spreading props on DOM elements

```js
<Component {...props} />
```

- This works very well and it gets transpiled into the following code by Babel: React.createElement(Component, props);
- risk of adding unknown HTML attributes, it is not related only to the spread operator, passing non-standard properties one by one leads to the same issues and warning
  - spread operators _hides_ the single properties we are spreading
- To see the warning in the console, a basic operation we can do is render the following component:

```js
const Spread = () => <div foo="bar" />; // Unknown prop `foo` on <div> tag. Remove this prop from the element
```
