## 1. How is error handling performed in JavaScript Promises?

- JavaScript Promises handle errors using the `.catch()` method or by providing a second argument to `.then()`.
- If an error is thrown or a Promise is rejected, it **bubbles down the chain** until it is caught by a `.catch()` or an error handler.
- Errors can come from:
  - A rejected Promise
  - A thrown exception inside a `.then()` handler
  - An error inside the executor function

## 2. What is the role of the `.catch()` method in a Promise chain?

- `.catch()` is used to handle **any error or rejection** that occurs in the Promise chain.
- It acts as a **centralized error handler**, similar to a `catch` block in synchronous `try...catch` statements.
- It catches:
  - Rejections from a Promise
  - Exceptions thrown in `.then()` or earlier `.catch()` handlers

**Example:**
```javascript
doSomethingAsync()
  .then(result => {
    return process(result);
  })
  .catch(error => {
    console.error('An error occurred:', error);
  });
```
## 3. Can `.then()` handle errors? How is it different from `.catch()`?

- `.then()` can handle errors by providing a **second argument** as an error handler:

  ```javascript
  somePromise.then(
    result => console.log(result),   // success handler
    error => console.error(error)    // error handler
  );
  ```
- However, this approach:

    - Only catches errors from the current `.then()` call and not from the whole chain

    - Can make the code less readable and harder to maintain

- `.catch()` is generally preferred because:

    - It captures all rejections or exceptions from the preceding chain

    - It allows for cleaner separation of success and error logic
## 4. What happens when an error is not handled in a Promise?

- If a Promise is **rejected** or an error is thrown inside it and **no `.catch()` handler or error handler is attached**, the error becomes an **unhandled Promise rejection**.
- Unhandled Promise rejections can lead to:
  - **Warning messages** in the console (in most environments).
  - In Node.js, unhandled rejections may cause the process to **emit a warning** or even **terminate** (depending on the Node.js version and settings).
  - In browsers, unhandled rejections trigger the **`unhandledrejection` event**, which can be caught globally.
- Unhandled errors can cause bugs that are **hard to debug** and may lead to **unstable application behavior**.
- It is considered a best practice to **always handle Promise rejections** to avoid these issues.

**Example of unhandled rejection:**
```javascript
new Promise((resolve, reject) => {
  reject(new Error("Oops!")); // No .catch() attached
});
```

## Normal Errors
## 1. What is a “normal error” in the context of Promises?

- A **normal error** refers to a **synchronous JavaScript error** (an exception) that is thrown inside a Promise executor or within a `.then()` handler.
- Examples include using `throw new Error("message")` or any runtime error like `ReferenceError`, `TypeError`, etc.
- These errors cause the Promise to **immediately reject** with the thrown error as the rejection reason.

## 2. What happens when you throw a regular error in a `.then()` block?

- Throwing an error inside a `.then()` handler causes the **Promise returned by that `.then()` to reject** with the thrown error.
- This rejection can then be caught by the next `.catch()` or error handler in the chain.
- This mechanism allows for **propagating synchronous errors as Promise rejections**.

**Example:**
```javascript
Promise.resolve(10)
  .then(value => {
    if (value > 5) {
      throw new Error("Value is too high!");
    }
    return value;
  })
  .catch(error => {
    console.error("Caught error:", error.message);
  });
```
- Output: `Caught error: Value is too high!`
## 3. How does JavaScript treat a `throw` statement inside a Promise executor function?

- If you `throw` an error inside the Promise executor function (the function passed to the `Promise` constructor), JavaScript **automatically rejects the Promise** with that error.
- This means you do **not need to manually call `reject()`** when throwing inside the executor.
- The thrown error becomes the rejection reason for the Promise.

## 4. Provide an example of a Promise that throws a synchronous error

```javascript
const promise = new Promise((resolve, reject) => {
  // Synchronous error thrown inside executor
  throw new Error("Something went wrong!");
});

promise
  .then(() => {
    console.log("This will not run");
  })
  .catch(error => {
    console.error("Caught error:", error.message);
  });

// Output:
// Caught error: Something went wrong!
```