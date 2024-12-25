# The gist of MobX

- signal based state management library
- distinguishes between the following three concepts:

1. `state`
2. `actions`
3. `derivations`

## Define `state` and make it observable

- `state` is the data of application
  - domain specific `state` - todo items
  - view `state` - element
- any data structure can be stored in `state` - object, arrays, classes...
  - marked as observable

## Update state using actions

- methods that modify state are called `actions` in MobX terminology

## Create derivations that automatically respond to state changes

- anything that can be derived from the state without any further interaction is a derivation
- `derivations` exists in many forms:
  - user interface
  - number of remaining todos
  - backed integrations - sending changes to the server
- two kinds of `derivations`:
  - `computed` values - can be derived from the current observable state using a pure function
  - `reactions` - side effects that need to happen automatically when the state changes (bridge between imperative and reactive programming)

### Model derived values using computed

- marked as `computed`
- using JS getter function `get`
  - binds an object property to a function that will be called when that property is looked up

```js
class TodoList {
  todos = [];
  get unfinishedTodoCount() {
    return this.todos.filter((todo) => !todo.finished).length;
  }
  constructor(todos) {
    makeObservable(this, {
      todos: observable,
      unfinishedTodoCount: computed,
    });
    this.todos = todos;
  }
}
```

### Model side effects using reactions

- produce side effects like making network requests
- UI components as reactions

### Reactive React components

- reactive components by wrapping them with the `observer` function
- `observer` converts react components into derivations of the data they render

### Custom reactions

- created using `autorun`, `reaction`, `when` functions
  - #### MobX reacts to any existing observable property that is read during the execution of a tracked function
  ```js
  autorun(() => {
    console.log("Tasks left: " + todos.unfinishedTodoCount);
  });
  ```

## Principles

- uses a uni-directional data flow where actions change the state which in turn updates all affected views
  - `Action` -> `Observable state` -> `Derived values` -> `Reactions`
  1. all derivations are updated `automatically` and `atomically` when the state changes
  2. all derivations are updated `synchronously` by default
  - safe to inspect a computed value directly after altering the state
  3. computed values are updated `lazily`
  - any computed value that is not actively in use will not be updated until it is needed for a side effect
  - if view is not in use it will be garbage collected automatically
  4. computed values should be `pure`
  - not supposed to change state

## React integration

- `observer HOC` that is wrapped around a react component
- `observer` automatically subsribes React components to any observables that are used during rendering
  - automatically re-render component on changes on read observables (subscribed)
- `observer` should be applied to all components that read observable data
- `observable` data passed to child components have to be wrapped with observer as well

  - same for any callback based component
  - possible to convert the observables to plain JS values or structures before passing them to the child

    ```js
    const TodoView = observer(({ todo }: { todo: Todo }) => {
      // WRONG: GridRow.onRender won't pick up changes in todo.title / todo.done
      //        since it isn't an observer.
      return <GridRow onRender={() => <td>{todo.title}</td>} />;

      // CORRECT: wrap the callback rendering in Observer to be able to detect changes.
      return (
        <GridRow
          onRender={() => <Observer>{() => <td>{todo.title}</td>}</Observer>}
        />
      );
    });
    ```
