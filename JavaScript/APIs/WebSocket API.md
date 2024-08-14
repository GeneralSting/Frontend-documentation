# WebSocket API

- makes possible to open a two-way interactive communication session between the user's browser and server
- send messages to server and receive event-driven responses without having to poll the server for a reply

## Interfaces

### WebWSocket

- provides the API for creating and managing a `WebSocket` connection to a server
- <b>WebSocket -> EventTarget</b>

```js
// Create WebSocket connection.
const socket = new WebSocket("ws://localhost:8080");

// Connection opened
socket.addEventListener("open", (event) => {
  socket.send("Hello Server!");
});

// Listen for messages
socket.addEventListener("message", (event) => {
  console.log("Message from server ", event.data);
});
```

### CloseEvent

- sent to clients using `WebSockets` when connection is closed
- object's `onclose` attribute
- <b>CloseEvent -> Event</b>
- all instance properties are read only
  - `CloseEvent.code`
    - unsigned short close code
  - `CloseEvent.reason`
    - string
  - `CloseEvent.wasClean`
    - boolean

### MessageEvent

- represents a message received by a target object
- `onmessage` property of the `WebSocket` interface
- the action triggered by this event is defined in a funciton set as the event handler for the relevant message event
- <b>MessageEvent -> Event </b>
