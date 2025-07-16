## 1. What is the value of `this` when a function is called normally (not as a method)?

- When a function is called **normally** (i.e., not as a method on an object), `this` refers to:
  - The **global object** (`window` in browsers) in **non-strict mode**.
  - **`undefined`** in **strict mode**.

## 2. How does strict mode affect `this` in regular function invocations?

- In **strict mode**, `this` inside a regular function call is **`undefined`** instead of defaulting to the global object.
- This helps prevent unintended errors caused by accidental global variable manipulation.

## 3. What happens if a function is assigned to a variable and then called? What is `this`?

- When a function is assigned to a variable and then called, it behaves like a normal function call.
- Thus, `this` will be:
  - The **global object** in **non-strict mode**.
  - **`undefined`** in **strict mode**.
