## 1. What is the value of `this` in the global context (outside any function)?

- In the **global context**, `this` refers to the **global object**.
- In browsers, this is typically the `window` object.
- In Node.js, this is the `global` object.


## 2. What does `this` refer to in the browser vs in Node.js global context?

| Environment | `this` in Global Context               |
|-------------|---------------------------------------|
| Browser     | `window` object                       |
| Node.js     | `global` object (or sometimes `{}` in modules) |

## 3. What happens if a function is called in the global scope in strict mode?

- In **strict mode**, if a function is called in the global scope without any object context, `this` is `undefined` inside that function.
- This differs from non-strict mode, where `this` would default to the global object.
