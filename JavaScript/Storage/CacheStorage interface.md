# CacheStorage interface

- represents the storage for `Cache` objects
- provides a master directory of all the named caches that can be accessed by a `ServiceWorker` or other type of worker or `window` scope
- maintains a mapping of string names to corresponding `Cache` objects
- access `CacheStorage` through the global `caches` property
  - `CacheStorage.open()` to obtain `Cache` instance
  - `CacheStorage.match()` to check if the given Request is a key in any of Cache objects that the CacheStorage object tracks
