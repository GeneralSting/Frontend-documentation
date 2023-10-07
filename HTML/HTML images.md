# HTML images

## Attribute: width and height
- If you specify the actual size of the image in your HTML, using the `width` and `height` attributes, then the browser knows, before it has downloaded the image, how much space it has to allow for it.

## Attribute: title
- `title` provides further supporting information if needed.
- on mouse hover gives a tooltip

## license types
- all right reserved
- permissive
  - MIT, BSD...
  - free to use but must fulfill conditions
    - link to original source
    - indicate any change made
    - not share, not use for commercial work
    - ...
public domain/CC0
  - no rights reserved - no copyright

## Annotating images
- &lt;`figure`&gt;
  - represents self-contained content, potentially with an optional caption
  - doesn't have to be an image
  - can be several images, code snippet, audio, video, table...
- &lt;`figcaption`&gt;
  - tells brosers and assistive technology that the caption describes the other content of the &lt;`figure`&gt; element`

```js
<figure>
  <img
    src="images/image.jpg"
    alt="purpose of the image, image description"
    width="400"
    height="350" />

  <figcaption>
    image caption
  </figcaption>
</figure>
```

## CSS background images
- `background-image` property
  - control background image placement.
  - easy to position and control
  - purpose is decoration only
  - image is invisible to screen readers  :wheelchair:

## Responsive images

### Attributes: srcset & sizes

- provides several additional source images along with hints to help the browser pick the right one
```js
<img
  srcset="first-image.jpg 480w, second-image.jpg 800w"
  sizes="(max-width: 600px) 480px,
         800px"
  src="elva-fairy-800w.jpg"
  alt="Elva dressed as a fairy" />
```
  - `srcset`
    1. image filename
    2. a space
    3. image's intrinsic with in pixels (480w) 
      - <b>w</b> unit used instead of px
  - `sizes`: defines a set of media conditions and indicates what image size would be best to choose
    1. media condition (max-width: 600px) 
      - when the viewport width is 600 pixels or less
    2. a space
    3. width of the slot the image will fill when the media condition is true (480px)

- browser: 
  1. look at its device width
  2. work out which media condition in the `sizes` list is the first one to be true
  3. look at the slot size given to that media query
  4. load the image referenced in the `srcset` list that has the same size as the slot
