# Fullscreen API

- adds methods to present a spcific `Element` and its descendants in fullscreen mode, and to exit
- removing all browser user interface elements and other apps from the screen until fullscreen mode is shut off

## Interfaces

- does not have interfaces of its own - augments several other interfaces to add the methods, properties and event handlers

### Instance methods

- add methods to the `Document` nad `Element` interfaces
- `Document.exitFullscreen()`
- `Element.requestFullscreen()`

### Instance properties

- determines if fullscreen mode is supported and available
- `Document.fullscreenElement`
  - returns Element that is fullscreen dispalyed
    - null means none is in fullscreen
  - `ShadowRoot.fullscreenElement`
    - for shadow DOM
- `Document.fullscreenEnabled`

### Events

- `fullscreenchange`
  - sent to an Element
- `fullscreenerror`
  - sent to an Element if error occurs while attempting to switch it into or out of fullscreen mode
