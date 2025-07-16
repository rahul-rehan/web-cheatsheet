## 1. What is the `globalThis` object in JavaScript?

`globalThis` is a standardized global object that provides a universal way to access the global scope across different JavaScript environments (like browsers, Node.js, Web Workers, etc.).


## 2. Why was `globalThis` introduced in JavaScript?

Before `globalThis`, different environments had different names for the global object (`window` in browsers, `global` in Node.js, `self` in Web Workers), which made writing portable code difficult. `globalThis` was introduced to provide a **single, consistent reference** to the global object regardless of the environment.


## 3. How is `globalThis` different from `window`, `global`, or `self`?

- `window`: Only available in browsers as the global object.
- `global`: Only available in Node.js as the global object.
- `self`: Refers to the global scope in Web Workers and browsers (worker context).
- `globalThis`: Works in **all** environments, providing a **universal reference** to the global object.

Using `globalThis` ensures code compatibility across different JavaScript environments without needing environment-specific checks.
## 4. Is `globalThis` available in all JavaScript environments?

`globalThis` is widely supported in most modern JavaScript environments, including recent versions of browsers and Node.js. However, it may **not be available in very old environments** or outdated browsers without polyfills.


## 5. When was `globalThis` introduced (ES version)?

`globalThis` was introduced in **ECMAScript 2020 (ES11)**.
