# Web APIs

- `Application Programming Interfaces` are constructs that allows developers to create complex functionality more easily

## APIs in client-side JavaScript

- built on top of the core JavaScript language

  - `browser APIs`

    - built into web browser
    - expose data from the browser
    - <b>APIs for manipulating documents loaded into the browser</b>

      - `DOM (Document Object Model) API`
        - allows creating, removing and changing HTML, dynamically apllying new styles to pages...

    - <b>APIs that fetch data from the server</b>

      - `Fetch API`
      - `XMLHttpRequest`

    - <b>APIs for drawing and manipulating graphics</b>

      - `Canvas`
        - allows to programmatically update the pixel data contained in an HTML &lt;`canvas`&gt; element to create 2D and 3D scenes.

    - <b>audio and video APIs</b>

    - <b>device APIs</b>

      - enable interaction with device hardware
      - `Geolocation API`

    - <b>client-side storage APIs</b>
      - enables to store data on the client-side
      - `Web Storage API`
      - `IndexedDB API`

  - `third-party APIs`
    - not built into the browser
    - have to retrieve code and information from somewhere on the web
    - `Google Maps API`

### Relationship between JavaScript, JavaScript tools and APIs

- `JavaScript libraries`
  - one or more JavaScript files containing custom functions that can be attached into code
  - calling library method: developer is in control
- `JavaScript frameworks`
  - tend to be packages of HTML, CSS, JavaScript and other technologies that need to be installed and then use to work entire web app from start
  - framework calls the developer's code.

### How do APIs work

#### Based on objects

- JavaScript objects serve as containers for the data the API uses and the functionality the API makes available (contained in object proeprties and methods). So we can access that objects with our code

#### APIs have recongnizable entry points

- `DOM API` entry points are hanging off in `Document` object
  ```js
  const em = document.createElement("em"); // create a new em element
  const para = document.querySelector("p"); // reference an existing p element
  ```
- `Canvas API` relies on getting a context object to use to manipulate things, graphical context
  - context object is created by getting a reference to the &lt;`canvas`&gt; element and then calling its `HTMLCanvasElement.getContext()` method
    ```js
    const canvas = document.querySelector("canvas");
    const ctx = canvas.getContext("2d");
    ```
  - then we can call properties and methods of the context object, `CanvasRenderingContext2D`
    ```js
    Ball.prototype.draw = function () {
      ctx.beginPath();
      ctx.fillStyle = this.color;
      ctx.arc(this.x, this.y, this.size, 0, 2 * Math.PI);
      ctx.fill();
    };
    ```

#### APIs use events to handle changes in state

#### APIs have security mechanisms where appropriate

- for example: only working on pages server over HTTPS due to transmitting potentially snsitive data
- some requests permission to be enabled from the user
  - `Notifications API` asks for pop-up dialog box permission
- `HTMLMediaElement APIs` has security mechanism called `autoplay policy` that disables automatically play audio when page loads
