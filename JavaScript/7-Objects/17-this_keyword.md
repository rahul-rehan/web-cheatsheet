## 1. What does the `this` keyword refer to in JavaScript?

- The `this` keyword refers to the **context object** from which a function is called.
- It points to the object that is **currently executing the function** or the object that "owns" the method.

## 2. Is the value of `this` determined at compile time or runtime?

- The value of `this` is determined at **runtime**, based on how a function is called.
- It is **dynamic** and can vary depending on the invocation context.

## 3. How is the value of `this` different in strict mode vs non-strict mode?

| Mode         | `this` Value in a Regular Function Call               |
|--------------|-------------------------------------------------------|
| Non-strict   | Defaults to the **global object** (e.g., `window` in browsers). |
| Strict mode  | `this` is **`undefined`** if not explicitly set by the call. |


## 4. Can `this` ever refer to `undefined` or `null`? Under what conditions?

- Yes, in **strict mode**, if a function is called without an explicit context (e.g., a plain function call), `this` is `undefined`.
- If a function is called with `call()` or `apply()` passing `null` or `undefined` as the context, `this` will be set to the **global object** in non-strict mode, but to `null` or `undefined` in strict mode.
