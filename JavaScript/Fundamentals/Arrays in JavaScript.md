# Arrays in JavaScript

## Arrays are objetcs
- contains properties
- access properties with bracket notation
- array functions come from their prototype
- can create arrays in many of the same ways as objects

## Ways arrays are unlike objects
- properties are zero-based numbers
- cannot use dot notation
- new Array.prototype functions

## Creating arrays
- `new` syntax
  - data passed into the Array constructor function affects the array that is created
  ```js
  const myArray = new Array(1,2,3); // [1,2,3]
  const myArray2 = new Array(5);    // creates blank array with size of 5
  ```

- `Array literal` syntax
  - square brackets
  ```js
  const myArray = [5];    // array with one item, value 5  
  ```

- `Object.create`
  - Object.create(Array.prototype)

- `Array.of`
  - same as `new` syntax, but adding one numeric number means one item, not array length
    ```js
    const myArray = Array.of(1,2,3); // [1,2,3]
    const myArray2 = Array.of(5);    // array with one item, value 5  
     ```

- `Array.from`
  - works with <b>Array-like objects</b>
    - an object which is iterable, but does not link to Array.prototype
    ```js
    const myString = "JavaScript;
    const stringArray = Array.from(myString)
    ```
  - <b>NodeLists and HTMLCollections</b>
    ```js
    const divs = document.querySelectorAll("div");  // not 100% array
    const forms = document.forms;                   // not 100% array

    const divArray = Array.from(divs)               // now is 100% array
    const formArray = Array.from(forms)             // now is 100% array
    ```

## Identifying arrays
- `instanceof` operator
  ```js
  myArray.content = [];
  myArray.content instanceof Arrays;    // true
  myArray.content instanceof Object     // true
  ```

- `isPrototypeOf` function
  - called on a prototype, passing in the object to check
  - Array.prototype.isPrototypeOf(array)
    - returns true for Array and for Array in Prototype chain

- `Array.isArray` function
  - only returns true if the object's direct prototype is Array.prototype

## Adding and accessing array elements
- arrays as `stacks`
  - index 0 at the bottom, LIFO -> last in first out
  - array.push(): pushes item into the next empty slot of the array
  - array.pop(): takes the last item out of an array and returns it
- arrays as `queue`
  - FIFO -> first in first out
  - functions shift and unshift are slower because it affects all items in the array (items changes index)
  - array.shift(): pulls the first (at index 0) element in the array out of the array and returns it
  - array.unshift(): pushes item in the start of array, at index 0

## Cutting up arrays
- using `delete`
  - not recommended, deletes the element at this index
    - array length not changed but at that index there is no value
- `slice()`
  - to cut, seperate
  - array.slice(startIndex, endIndex)
    ```js
    const sliced = array.slice(1);      // from 1 to rest of the array
    const sliced2 = array.slice(1, -1)  // item at index 2 and item at index 1
    ```
  - non-desctructive
- `splice()`
  - to unite by inerweaving the strands, to unite link, or to insert as if by splicing
  - array.splice(startIndex, cutAmount, itemsToAdd)
    - removes a number of elements from an array, beginning at the start index
    ```js
    const removed = array.splice(2, 1)
    removed[0]  // only contains one element
    ```
  - destructive
    - non-destructive is `toSpliced()`

## Putting together arrays
- `concat` function
  - called on the array wants to be added to, passing in the array we want to add
  - can take in multiple arrays, combining them all
  - array1.concat(array, array2);
- `spread` operator
  - unpacks an interable object, like array in place
  - array = [ ...array1, ...array2]
    ```js
      array = [array1, array2]          // creates two-dimensional array
      array = [ ...array1, ...array2]   // unpacks elements and we get array with all elements of previous arrays
    ```

## Cloning arrays
- `spread` operator
  ```js
  const array = [ ... array1 ];
  ```

## Sorting arrays
- `reverse()`
  - reverses the order of an arary
- `toReversed()`
  - creates new reversed array
- `sort()`
  - using to sort function with a comparison function allows to sort by any criteria
  - two arguments, a & b 
  - return 1, -1 or 0
    - +1: a is higher -> a should be sorted higher
    - -1 b is higher -> b should be sorted higher
    - 0 a & b are equal
  ```js
  const comparisonFunction = ((a, b) => {
    if(a.title < b.title) return 1  // a should be sorted first
    if(b.title < a.title) return -1
    return 0;
  });

  // shorten function of above code
  const comparisonShorten = ((a,b) => {
    return a.title - b.title; // when be is larger than a, negative number is returned
  })
  ```
- `toSorted()`
  - same as `sort()` but does not change array

## Sparse arrays
- array with empty indexes
  - deleting an array element
    ```js
    delet array[3];
    ```
  - initializing an array with a length but not filling it
    ```js
    let array = new Array(3);
    array[1] = "banana";
    ```
  - adding to an array at an idenx greater than its length
    ```js
    let fruits = ["apple", "banana"];
    fruits[5] = "cherry";
    ```

- avoid adding elements to array by index using function `push()` :exclamation:
- avoid initializing arrays with a capacity, JavaScript arrays are dynamic :exclamation:

## Maps, Sets and Typed arrays
- Arrays
  - <b>comparised of:</b> key-values
  - <B>are ordered:</b> in any way
  - <b>keys are:</b> zero-indexed numbers
  - <b>values are:</b> anything

- Maps
  - <b>comparised of:</b> key-values
  - <B>are ordered:</b> insertion order
  - <b>keys are:</b> anything
  - <b>values are:</b> anything
  - allows keys of any type and also keep track of their element's insertion order

- Sets
  - <b>comparised of:</b> unique values
  - <B>are ordered:</b> in any way
  - <b>keys are:</b> n/a
  - <b>values are:</b> anything
  - enforce unique values when adding elements

- Typed arrays
  - <b>comparised of:</b> key-values
  - <B>are ordered:</b> in any way
  - <b>keys are:</b> zero-indexed numbers
  - <b>values are:</b> only specified type
  - performance important 
  - Int8Array
  - Float64Array
  - ... 

<hr>

## Array iteration 

### Loops
- for loop
  - <b>iterate through</b>: an index
  - <b>sparse array handling</b>: no handling
  - <b>continue and break</b>: yes

- for...in
  - <b>iterate through</b>: enumerable properties
  - <b>sparse array handling</b>: no handling
  - <b>continue and break</b>: yes
  - for objects, because of iteration of enumerable properties

- for...of
  - <b>iterate through</b>: iterable objects
  - <b>sparse array handling</b>: no handling
  - <b>continue and break</b>: yes
  - for arrays because of iteration of iterable objects (not enumerable properties)

- forEach
  - <b>iterate through</b>: an array elements
  - <b>sparse array handling</b>: ignores undefined
  - <b>continue and break</b>: no

### Sumarizing arrays
- `join()`
  - returns a single string from an array by calling toString on each element
  - can receive seperator string as argument
 `some()`
  - returns boolean if the array matches certain criteria
    -  returns true if some of the elements in the array match the given criteria
 `every()`
  - returns boolean if the array matches certain criteria
    -  returns true if all the elements in the array match the given criteria
    ```js
    let array = [2, 4, 6];
    array.every(element => {
      return element > 4
    });
    // false
    ```
- `reduce()` 
  - executes a user-supplied "reducer" callback function on each element of the array
  - function body should return how the active element should affect the accumulator
    ```js
    let total = cart.products.reduce(
      (acumulator, product)=> {
        return accumulator + product.price;
      });
    ```
  - a reference to the current element's index can be used by passing a third argument
  - the initial value of the accumulator can be passed in as second argument to reduce
    ```js
        let total = cart.products.reduce(
      (acumulator, product)=> {
        return accumulator - product.price;
      }, 25); // initial value, accumulator starts as 25
    ```
- `reduceRight()`
  - same as `reduce()` function but starts at the end of array, from the last index of array (from right to left)

### Searching through arrays
- `includes()`
  - returns true if the array includes the element passed into the function
  - because objects are reference types, searching for a new object always return false. Returns true if the same reference is included in the array
  - second parameter defines the infrx from which to start searching
- `find()`
  - returns the first element in an array which matches the criteria
- `findIndex()`
  - returns the index of the first instance of the element in an array
- `findLastIndex()`
  - returns the index of the last instance of the element in an array
- `filter()`
  - returns a shallow-copy array of all elements matching the criteria
    ```js
    let bookmarkedBlocks = course.filter(block => {
      return block.bookmarked == true;
    });
    ```

### Map
- chaining array functions 
- `map()`
  - applies a function to every element in an array, and then returns that array
  - called on: array
  - argument: function
  - returns: array