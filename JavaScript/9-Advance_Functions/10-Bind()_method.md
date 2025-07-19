## 1. What is the purpose of the `bind()` method in JavaScript?

- The `bind()` method creates a **new function** that, when called, has its `this` keyword set to the provided value.
- It allows you to **permanently bind** a function’s `this` context and optionally preset some arguments.
- Unlike `call()` and `apply()`, it does **not invoke the function immediately**; instead, it returns a new function for later use.

## 2. What is the syntax of `bind()`?

```javascript
const boundFunction = originalFunction.bind(thisArg[, arg1[, arg2[, ...]]]);
```
- **`thisArg`**: The value to be used as `this` inside the new function.

- **`arg1, arg2, ...`** (optional): Arguments to prepend to the arguments passed to the bound function when it is called.
## 3. How does `bind()` differ from `call()` and `apply()`?

| Feature           | `bind()`                                  | `call()`                               | `apply()`                              |
|-------------------|-------------------------------------------|--------------------------------------|---------------------------------------|
| Invocation        | Returns a **new function** without invoking it immediately | **Immediately** invokes the function | **Immediately** invokes the function  |
| `this` Binding    | Permanently sets `this` for the new function | Sets `this` for one immediate call   | Sets `this` for one immediate call    |
| Arguments         | Can preset arguments for future calls     | Arguments passed individually         | Arguments passed as an array           |
| Use Case          | Useful for creating functions with bound `this` and partial arguments | Useful for immediate function calls with a specific `this` | Useful for immediate calls when arguments are in an array |

**Summary:**  
- `bind()` creates a new function with a fixed `this` and optional preset arguments.  
- `call()` and `apply()` invoke the function immediately with a specified `this` context, differing mainly in how arguments are passed.
## 4. What does `bind()` return when used on a function?

- The `bind()` method returns a **new function** with the specified `this` value and optional preset arguments.
- This new function can be called later, maintaining the bound context and arguments.

## 5. Does `bind()` execute the function immediately? Why or why not?

- No, `bind()` does **not** execute the function immediately.
- Instead, it creates and returns a new **bound function** that can be invoked later.
- This allows you to set the `this` context and partially apply arguments without running the function right away.
## 6. What happens to the `this` value inside a function after using `bind()`?

- After using `bind()`, the `this` value inside the bound function is **permanently set** to the provided context (`thisArg`).
- Regardless of how or where the bound function is called later, `this` will always refer to the bound context.

## 7. Can you partially apply arguments using `bind()`? Provide an example.

- Yes, `bind()` allows **partial application** by presetting some arguments when creating the bound function.
- These preset arguments are prepended to any arguments provided when the bound function is called.

#### Example:

```javascript
function multiply(a, b) {
  return a * b;
}

// Partially apply the first argument as 2
const double = multiply.bind(null, 2);

console.log(double(5)); // Output: 10 (2 * 5)
console.log(double(10)); // Output: 20 (2 * 10)
```
- In this example, `double` is a new function that always multiplies its argument by 2.

- The first argument `2` is preset via `bind()`, demonstrating partial application.