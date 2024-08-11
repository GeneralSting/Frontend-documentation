# AbortController

- `AbortController` interface represents a controller object that allows to abort one or more `Web requests` as and when desired

  - create a new AbortController object using the `AbortController()` constructor
  - communicating with an async operation is done using an `AbortSignal` object

- this feature is available in `Web Workers` :heavy_check_mark:

## Constructor

- AbortController()

## Instance properties

- `AbortController.signal`
  - read only property
  - returns an AbortSignal object instance, which can be used to communicate with, or to abort, an async operation

## Instance methods

- `AbortController.abort()`
  - aborts an async operation before it has completed - able to abort `fetch requests`, consumption of any response bodies, and streams

## AbortSignal

- `AbortSignal` interface represents a signal object that allows to communicate with an async operation such as fetch request and abort it if required via an AbortController object

  - AbortSignal -> EventTarget, inherits events from its parent interface, `EventTarget`
    - `abort` is event of the AbortSignal, fired when the associated request is aborted - using AbortController.abort()

- this feature is available in `Web Workers` :heavy_check_mark:

### Instance properties

- inherits properties from its parent interface, EventTarget

- `AbortSignal.aborted`

  - read only property
  - Boolean that indicates wheter the request(s) the signal is communicating with is/are aborted

- `AbortSignal.reason`

## Example

- when we might use a signal to abort downloading a video using the `FETCH API`
- when `abort()` is called, the fetch() promise rejects with a `DOMException` name `AbortError`

  ```js
  let controller;
  const url = "video.mp4";

  const downloadBtn = document.querySelector(".download");
  const abortBtn = document.querySelector(".abort");

  downloadBtn.addEventListener("click", fetchVideo);

  abortBtn.addEventListener("click", () => {
    if (controller) {
      controller.abort();
      console.log("Download aborted");
    }
  });

  async function fetchVideo() {
    controller = new AbortController();
    const signal = controller.signal;

    try {
      const response = await fetch(url, { signal });
      console.log("Download complete", response);
      // process response further
    } catch (err) {
      console.error(`Download error: ${err.message}`);
    }
  }
  ```
