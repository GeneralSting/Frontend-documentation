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
