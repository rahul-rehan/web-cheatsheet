## 1. What is the global object in a browser environment?

In a browser environment, the global object is the **`window`** object. It represents the global scope and provides access to browser APIs and global variables.


## 2. What is the global object in Node.js?

In Node.js, the global object is called **`global`**. It serves as the global scope in Node.js and provides access to global variables and functions.


## 3. How does `globalThis` unify access to the global object across environments?

`globalThis` provides a **standard, environment-agnostic way** to access the global object regardless of whether the code is running in a browser, Node.js, Web Workers, or other JavaScript environments. This avoids the need to check or guess which global object name to use (`window`, `global`, `self`, etc.).
## 4. Provide examples showing `window`, `global`, `self`, and `globalThis` in different environments

```js
// In Browser
console.log(window === globalThis); // true
console.log(self === globalThis);   // true

// In Node.js
console.log(global === globalThis); // true
// window and self are undefined in Node.js

// In Web Workers (browser background threads)
console.log(self === globalThis);   // true
// window is undefined in Web Workers
```
## 5. What happens if you access a property on `globalThis` that doesn’t exist?

Accessing a property that does not exist on `globalThis` returns `undefined` without throwing an error.

```js
console.log(globalThis.nonExistentProperty); // undefined
```