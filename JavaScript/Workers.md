# Workers

- enables tasks to run in a separate <b>thread</b> of execution

- main code and <b>worker</b> code never get direct access to each other's variables
  - can share data in a specific cases
  - workers cannot access <b>DOM</b> (window, document, page elements)

## Thread
- <b>thread</b> is the execution of running multiple tasks or programs at the same time.
- each unit capable of executing code is called a <b>thread</b>
  - <b>main thread</b>
    - used by the browser to handle user events, render and paint the display and to run the majority of the code.
- threading allows web apps to take advantage of modern multi-core processors
   - enabling even better performance than multi-threaded apps running on a single core

## Web workers API
- <b>web worker</b> is an object created using a constructor <b>Worker()</b> that runs a named JS file which contains the code that will run in the worker thread.
- <b>worker global context and functions & supported web APIs</b>
  - cannot manipulate the DOM from inside a worker, or use default methods and properties of window object
- sharing data between <b>workers</b> and <b>main thread</b>
  - postMessage(), send messages
  - onmessage event handler
    - the message is contained within the <b>message</b> event's data property
    - data is copeid rather than shared

### Worker types
- <b>dedicated workers</b> 
  - utilized by a single script
  - context represented by <b>DedicatedWorkerGlobalScope</b> object
    - <b>workers</b> run in a different global context than the current window
    - window is not directly available to <b>workers</b>
    - many of the same methods are defined in a shared mixin <b>WindowOrWorkerGlobalScope</b> and available through their own derived context: <b>WorkerGlobalScope</b>
      - context: <b>DedicatedWorkerGlobalScope</b>
- <b>shared workers</b>
  - utilized by multiple scripts running in different windows but are in the same domain as the worker
  - scripts must communicate via an active port
  - context: <b>SharedWorkerGlobalScope</b>
- <b>service workers</b>
  - act as proxy servers that sit between web apps, the browserm and the network
  - context: <b>ServiceWorkerGlobalScope</b>