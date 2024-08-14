# Proxy Objects and Reflect in JavaScript

## Proxy

- `Proxy` object enables us to create a proxy for another object, which can intercept and redefine fundamental operations for that object
- The Proxy object allows you to create an object that can be used in place of the original object, but which may redefine fundamental Object operations like getting, setting, and defining properties. Proxy objects are commonly used to log property accesses, validate, format, or sanitize inputs, and so on.
- two parameters

  - `target`: the original object which you want to proxy
  - `handler`: an object that defines which operations will be intercepted and how to redefined intercepted operations

  <br>
  
  ```js
  const target = {
    message1: "hello",
    message2: "everyone",
  };

  const hanlder = {
    get(target, prop, receiver) {
      // handler function
      return "world";
    },
  };

  const proxy = new Proxy(target, hanlder);
  console.log(proxy.message1); // world
  ```

- `Handler` functions are sometimes called `traps`, presumably because they trap calls to the target object.

## Reflect

- the `Reflect` object is often used with Proxies
- provides some methods with the same names as Proxy `traps`.
- provides the reflective semantics for invoking the corresponding `object internal methods`
  - e.g. `Reflect.get` does not redefine the object's behaviour
- it doesn't "de-proxify"

## Terminology

- `handler`: The object passed as the second argument to the Proxy constructor. It contains the `traps` which define the behavior of the proxy.
- `traps`: The function that define the behavior for the corresponding `object internal method`.
- `target`: Object which the proxy virtualizes. It is often used as storage backend for the proxy.
- `invariants`: Semantics that remain unchanged when implementing custom operations. If your trap implementation violates the invariants of a handler, a `TypeError` will be thrown.

## Proxy example
  ```js
  const legacyFontSizes = {
    extraLarge: {
      replacementName: "gigantic",
      replacementValue: "gigantic"
    },
    extraSamll: {
      replacementName: "tiny",
      replacementValue: "tiny",
    },
  }

  const fontSizes = {
    gigantic: "gigantic",
    large: "large",
    medium: "medium",
    small: "small",
    tiny: "tiny",
  }

  const proxyOptions = {
    get: (target, propName, receiver) => {
      if(propName in legacyFontSizes) {
        const legacyProp = legacyFontSizes[propName]
        console.warn(`${propName} is deprecated.`,
        `Use ${legacyProp.replacementName} instead.` )

        return legacyProp.replacementValue
      }
      return Reflect.get(target, propName, receiver)
    }
  }

  const proxiedFontSizes = new Proxy(fontSizes, proxyOptions);

  // export default proxiedFontSizes;

  console.log(proxiedFontSizes)   // Proxy(Object) {gigantic: 'gigantic', large: 'large', medium: 'medium', small: 'small', tiny: 'tiny'}
  console.log(proxiedFontSizes.extraLarge)  // extraLarge is deprecated. Use gigantic instead. 
                                            // gigantic
  ```

## Object internal methods

- `Objects` are collections of properties, however, the language doesn't provide any machinery to directly manipulate data stored in the object - rather, the object defines some internal methods specifying how it can be interacted with. E.g. when you read `obj.x` you may expect the following to happen:
  - the `x` property is searched up the `property chain` until it is found
  - if `x` is a data property, the property descriptor's `value` attribute is returned.
  - if `x` is an accessor property, the getter is invoked, and the return value of the getter is returned.
- there isn't anything special about this process in the language - it's just because ordinary objects, by default, have a `[[Get]]` method on the object, and the object uses its own internal method implementation to determine what to return
- `arrays` differ from normal objects, because they have `length` property that, when modified, automatically allocates empty slots or removes elements from the array. Similarly, adding array elements automatically changes the `length` property. This is because arrays have a `[[DefineOwnProperty]]` internal method that knows to update `length` when an integer index is written to, or update the array contents when `length` is written to. Such objects whose internal methods have different implementations from ordinary objects are called exotic objects. `Proxy` enable developers to define their own exotic objects with full capacity.
- all objects have the following internal methods:
  | Internal methods | Corresponding traps |
  | ----------- | ----------- |
  | [[GetPrototypeOf]] | getPrototypeOf() |
  | [[SetPrototypeOf]] | setPrototypeOf() |
  | [[IsExtensible]] | isExtensible() |
  | [[PreventExtensions]] | preventExtensions() |
  | [[GetOwnProperty]] | getOwnPropertyDescriptor() |
  | [[DefineOwnProperty]] | defineProperty() |
  | [[HasProperty]] | has() |
  | [[Get]] | get() |
  | [[Set]] | set() |
  | [[Delete]] | setdeleteProperty() |
  | [[OwnPropertyKey]] | ownKeys() |

- function objects also have the following internal methods
  | Internal methods | Corresponding traps |
  | ----------- | ----------- |
  | [[call]] | apply() |
  | [[Construct]] | construct() |

- all internal methods are called by the language itself, and are not directly accessible in JavaScript code 
- the `Reflect` namespace offers methods that do little more than call the internal methods, besides some input normalization/validation
-  `class fields` use the `[[DefineOwnProperty]]` semantic, which is why setters defined in the superclass are not invoked when a field is declared on the derived class.