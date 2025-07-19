## 1. What is the result of `typeof class MyClass {}`? Why?

- The result is `"function"`.
- In JavaScript, classes are essentially special functions (constructor functions) under the hood.
- Therefore, using `typeof` on a class returns `"function"`.

## 2. Is an arrow function also of type `"function"`? What are its limitations?

- Yes, arrow functions have the type `"function"` when checked with `typeof`.
- **Limitations of arrow functions:**
  - They do **not** have their own `this` context; `this` is lexically inherited from the enclosing scope.
  - They cannot be used as constructors (calling with `new` throws an error).
  - They do not have their own `arguments` object.
  - They cannot use `yield`, so they cannot be generator functions.

## 3. How do you distinguish between different kinds of functions at runtime (regular, async, generator)?

- You can inspect the constructor name or use `Object.prototype.toString.call`:

```javascript
function regular() {}
async function asyncFunc() {}
function* generatorFunc() {}

console.log(regular.constructor.name);          // "Function"
console.log(asyncFunc.constructor.name);        // "AsyncFunction"
console.log(generatorFunc.constructor.name);    // "GeneratorFunction"

// Or using toString:
console.log(Object.prototype.toString.call(regular));        // "[object Function]"
console.log(Object.prototype.toString.call(asyncFunc));      // "[object AsyncFunction]"
console.log(Object.prototype.toString.call(generatorFunc));  // "[object GeneratorFunction]"
```
## 4. What is the output of `typeof async function() {}` and why?

- The output is `"function"`.
- Async functions are a special kind of function introduced in ES2017.
- Despite their asynchronous behavior, they are still functions internally, so `typeof` returns `"function"`.

## 5. How does the internal `[[Call]]` method relate to the function type?

- The `[[Call]]` internal method is a specification detail that defines how a function object is invoked (called).
- Any object with a `[[Call]]` method can be called like a function.
- In JavaScript, functions have this `[[Call]]` internal method, which is why they are callable.
- Objects without `[[Call]]` cannot be invoked as functions.

## 6. What is the significance of callable vs. constructible functions in JavaScript?

- **Callable functions**: Functions that can be invoked using `()`. All functions with a `[[Call]]` method are callable.
- **Constructible functions**: Functions that can be used with the `new` keyword to create new instances (they have a `[[Construct]]` internal method).
- Some functions are callable but not constructible, for example:
  - Arrow functions and methods in object literals are callable but **not** constructible (cannot be used with `new`).
- This distinction is important for understanding how different types of functions behave and how they can be used.
## 7. Can you make an object behave like a function by setting its `[[Call]]` internal method?

- No, the `[[Call]]` internal method is a special internal slot provided only by JavaScript function objects.
- You **cannot** manually set or add a `[[Call]]` method to a regular object to make it callable.
- To have callable behavior, an object must be a function or a proxy that intercepts calls.
- However, you can use a **Proxy** with a `apply` trap to simulate function-like behavior on an object.

## 8. How does `Symbol.toStringTag` affect how a function is represented?

- `Symbol.toStringTag` is a well-known symbol that lets you customize the default tag returned by `Object.prototype.toString.call()`.
- For functions, the default `Symbol.toStringTag` value is `"Function"`.
- If you define or override `Symbol.toStringTag` on a function, you can change how it appears when `toString()` is called.
- Example:

  ```js
  function foo() {}
  console.log(Object.prototype.toString.call(foo)); // "[object Function]"

  foo[Symbol.toStringTag] = "MyCustomFunction";
  console.log(Object.prototype.toString.call(foo)); // "[object MyCustomFunction]"
  ```
- This feature helps in identifying or customizing object type strings, especially useful for debugging or custom objects.