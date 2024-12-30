# State structure

## Principles for structuring state

### Group related state

- always updating two or more state variables at the same time, merge them into a single state variable
  - if some two state variables always change togheter, it might be a good idea to unify them into a single state variable
  - if state variable is an object you can't update only one field in it without explicitly copying the other fields

### Avoid contradictions in state

- when multiple variables never can have same value, e.g. boolean status variable, at the same time, it is better to replace them with one _status_ variable that may tako one of valid states

### Avoid redudant state

- if information can be calculated from the component's props or its existing state variables during rendering, do not put that information into that component's state
- don't mirror props in state

  ```jsx
  function Message({ messageColor }) {
    const [color, setColor] = useState(messageColor);
    // ...
  }
  ```

  - in the example if the parent component passes a different value later, the _color_ state variable would not be updated
  - "mirroring" props into state only makes sense when we want to ignore all updates for a specific prop
  - if we want to avoid "mirroring" next code is one of solutions

  ```jsx
  function Message({ messageColor }) {
    const color = messageColor;
    // ...
  }
  ```

### Avoid duplication in state

- when the same data is duplicated between multiple state variables, or within nested objects, it is difficult to keep them in sync - reduce duplication

### Avoid deeply nested state

- deeply hierarchical state is not very convenient to update - flat state is best possible solution
