# HTML vector graphics
- small file sizes and highly scalable

## Vector graphics
- `raster images`
  - defined using a grid of pixels
  - showing where each pixel is to be placed
  - Bitmap (.bmp), PNG, JPEG, GIF

- `vector images`
  - defined using algorithms - contains shape and path definitions
  - `SVG`
    - Scalable Vector Graphics, 2D vector image based on an XML syntax
    - XML-based language, it's bassically markup, like HTML
    - defines elements for creating basic shapes
      - &lt;circle&gt;
      - &lt;rect&gt;
    - elements for complex shapes
      - &lt;path&gt;
        - generic element to define a shape
        - attributes:
          - <span style="color: #ffc75f">d</span>
            - defines the shape of the path
            - value type is string, default value is empty string
          - <span style="color: #ffc75f">pathLength</span>
            - total length for the path in user units
            - value type is number, default value is none
          - core attributes
            - <span style="color: #ffc75f">id</span>
            - <span style="color: #ffc75f">tabindex</span>
              - allows control wather an element is focusable and to define the relative order or the element for the purpose of sequential focus navigation
              - default value: none
      - &lt;polygon&gt;
        - defines a closed shape consisting of a set of connected straight line segments
        - last point is connected to the first point
    - featrues
      - &lt;feColorMatrix&gt; - transform colors using a transformation matrix
      - &lt;animate&gt; - animate parts of vector graphic
      - &lt;mask&gt; - apply a mask over the top of image
  
    - text in vector images remains accessible
    - can be styled via CSS or scripted via JavaScript

### Adding SVG to page

#### img element
- to embed an SVG via an &lt;`img`&gt; element, reference is needed inside <span style="color: #ffc75f">src</span> attribute
  - add <span style="color: #ffc75f">height</span> & <span style="color: #ffc75f">width</span> attributes

  ```js
  <img
    src="example.svg"
    alt="svg example purpose, description"
    height="87"
    width="100" />
  ```

- SVG file can be cached by the browser, resulting in faster loading times for any page that uses the image loaded in the future  :white_check_mark:
- cannot manipulate image with JavaScript :x:
- to control the SVG content with CSS - external stylesheets takes no effect, inline CSS style must be included inside of SVG code  :x:
- cannot restyle the image with CSS pseudoclasses (:focus)  :x:

#### svg element
- &lt;`svg`&gt;
```js
<svg width="300" height="200">
  <rect width="100%" height="100%" fill="green" />
</svg>
```
- assign `classes` and `ids` to SVG elements to style them with CSS :white_check_mark:
- if using SVG in multiple places - duplcation makes for resource-intensive maintenance :x:
- browser cannot cache inline SVG :x:
