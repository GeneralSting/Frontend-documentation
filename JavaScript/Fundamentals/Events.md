# JavaScript events

- the system produces/fires a signal of some kind when an event occurs
- to react to an event, attach an `event handler`
- `focus`, `blur`, `dblclick`

## Multiple listeners for a single event

```js
myElement.addEventListener("click", functionA);
myElement.addEventListener("click", functionB);
```

## Event handler properties

- objects such as buttons have properties whose name is `on` followed by the name of the event

  - `onclick`

  ```js
  btn.onclick = () => {
    const rndCol = `rgb(${random(255)}, ${random(255)}, ${random(255)})`;
    document.body.style.backgroundColor = rndCol;
  };

  function bgChange() {
    const rndCol = `rgb(${random(255)}, ${random(255)}, ${random(255)})`;
    document.body.style.backgroundColor = rndCol;
  }

  btn2.onclick = bgChange;
  ```

## Event objects

- `event` object (event, evt, e) is automatically passed to event handlers to provide extra features and info.

### Attribute target

- e.target -> element itself
- the `target` property of the event object is always a reference to the element the event occurred upon.

### Extra properties

- some event objects add extra properties that are relevant to that particular type of event
  - `keydown` event fires when the user presses a key.
    - event object is a `KeyboardEvent` which is a specialized `Event` object with a `key` property that tells which key was pressed

### Preventing default behavior

- most used for web forms, prevent submit, first check entered data
  - `preventDefault()`
- some browsers support automatic form data validation features - do not rely on them
- `submit` event is fired on a form when it is submitted

## Event bubbling

- describes how the browser handles events targeted at nested elements

  - event bubbles up from the innermost element that was clicked

  ```js
  <div id="container">
    <button>Click me!</button> // if we click on button we also click on div,
    parent element
  </div>;

  const output = document.querySelector("#output");
  function handleClick(e) {
    console.log(`You clicked on a ${e.currentTarget.tagName} element`);
    // You clicked on a BUTTON element
    // You clicked on a DIV element
    // You clicked on a BODY element
  }

  const container = document.querySelector("#container");
  const button = document.querySelector("button");

  document.body.addEventListener("click", handleClick);
  container.addEventListener("click", handleClick);
  button.addEventListener("click", handleClick);
  ```

### Fixing bubbling problems with stopPropagation()

- `Event` object has a function `stopPropagation()` when called inside an event handler, prevents the event from bubbling up to any other elements.

### Event capture

- when event `capture` is enabled, the event fires first on the least nested elment and then on successively more nested elements, until the target is reached
  - opposite of bubbling event
  ```js
  document.body.addEventListener("click", handleClick, { capture: true });
  ```

### Event delegation

- `event.target` gets the element that was the target of the event (innermost element)
- `event.currentTarget` gets the element that handled the event

  ```js
  <div id="container">
    <div class="tile"></div> 
    <div class="tile"></div>
  </div>

  container.addEventListener("click", (event) => {
    event.target.style.backgroundColor = bgChange();        // gets clicked inner, child element (div class="tile" element)
    event.currentTarget.style.backgroundColor = bgChange(); // gets clicked element that handles event -> container element(object)
  });
  ```
