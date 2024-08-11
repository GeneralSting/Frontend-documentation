# Intersection Observer

- API provides a way to asynchronously observe changes in the intersection of a target element with an ancestor element or with a top-level document's `viewport`
  - viewport represents a polygonal (normally rectangular) area in computer graphics that is currently being viewed - `layout viewport`
  - refers to the part of the document that is beign viewed which is currently visible in its window of (or screen if the document is being viewed in full screen mode)
  - content outside is not visible onscreen until scrolled into view
  - the portion of the viewport that is currenlty visible is called the `visual viewport`
    - it can be smaller than the layout viewport, such as when the user has pinched-zoomed
    - layout viewport remains the same

## Usage

- lazy-loading of images or other content as a page is scrolled
- implementing "infinite scrolling" websites
- reporting of visibility of adverisements in order to calculate ad revenues
- deciding whether or not to perform tasks or animation processes based on whether or not the user will see the result

- avoids involving the event handlers and loops calling methods like `Element.getBoundingClientRect()` to build up the needed information for every element affected
  - all code runs on the main thread, even one of these can cause performance problems

## Intersection Observer concepts

- the Intersection Observer API allows to configure a callback that is called when either of these circumstances occur:

  - a `target` intersects (is visible on viewport) either the device's viewport or a specified element
    - that specified element is called the **root element** or **root** for the purpose of the Intersection Observer API
  - the first time the observer is initially asked to watch a target element

- the degree of intersection between the target element and its root is the **intersection ratio**

  - represents the percentage of the target element which is visible as a value between 0.0 and 1.0

- when an IntersectionObserver is created, it's configured to watch for given ratios of visibility within the root
  - the configuration cannot be changed once the IntersectionObserver is created, so a given observer object is only useful for watching for specific changes in degree of visibility; however, you can watch multiple target elements with the same observer

### Constructor

- IntersectionObserver()

### Instance properties

- **all are ready only**

#### IntersectionObserver.root

- the Element or Document whose bounds are used the bounding box when testing for intersection
  - if no root value is passed to the constructor - value is null which means the top-level document's viewport is used

#### IntersectionObserver.rootMargin

- an offset rectangle applied to the root's `bounding box` when calculating intersections, effectively shrinking or growing the root for calculation purposes
  - bounding box is the smallest possible rectangle (aligned with the axes of that element's user coordinate system) that entirely encloses it and its descendants
    - it is the invisible rectangular box the browser places the object in when it draws the object on a page
  - each offset can be expressed in pixels or as a percentage - _default is 0px 0px 0px 0px_

#### IntersectionObserver.thresholds

- list of thresholds sorted in increasing numeric order, where each threshold is a ratio of intersection area to bounding box of an observer target
  - notifications for a target are generated when any of the trhesholds are crossed for that target - if no value was passed to the constructor, 0 is as default value

### Instance methods

#### IntersectionObserver.disconnect()

- stops the IntersectionObserver object from observing any target

#### IntersectionObserver.observe()

- tells the IntersectionObserver a target element to observe

#### IntersectionObserver.takeRecords()

- returns an array of IntersectionObserverEntry objects for all observed targets

#### IntersectionObserver.unobserve()

- tells the IntersectionObserver to stop observing a particular target element

## Interfaces

- IntersectionObserver
- InterSectionObserverEntry
  - describes the intersection between the target element and its root container at a specific moment of transition
  - can be only obtained in two ways:
    - as an input to IntersectionObserver callback
    - calling IntersectionObserver.takeRecords()

## Example

```js
let options = {
  root: document.querySelector("#scrollArea"),
  rootMargin: "0px",
  threshold: 1.0,
};

let observer = new IntersectionObserver(callback, options);
```
