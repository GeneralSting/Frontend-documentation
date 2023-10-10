# Working with JSON
- standard text-based format for representing structured data based on JavaScript object sytnax
- <b>JSON</b> exists as a string - converted to a native JavaScript object (deserialization) when needed as data
  - <b>deserialization</b> 
    - string into native object
  - <b>serialization</b>
    - native object into string
  - JavaScript provides a global <b>JSON</b> object that has methods available for converting

- <b>MIME type</b> is <b>application/json</b>
  - <b>MIME type</b> or media type or content type is a string sent along with a file indicating the type of the file
    - describing the content format, audio/ogg, image/png

- <b>JSON</b> text can look like JavaScript object or like array

## Converting between objects and text
- <b>parse()</b>
  - accepts a JSON string as a parameter and returns object
- <b>stringify()</b>
  - accepts an object as parameter and returns JSON string