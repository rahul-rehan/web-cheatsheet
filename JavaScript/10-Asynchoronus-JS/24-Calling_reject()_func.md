## 1. How does calling `reject()` manually affect the Promise state?

- Calling `reject()` **explicitly changes the Promise's state from pending to rejected**.
- It signals that the asynchronous operation has failed and provides a reason (usually an error or message) for the rejection.
- Once rejected, the Promise will skip any `.then()` handlers and invoke the nearest `.catch()` handler.

## 2. Provide an example where a Promise is explicitly rejected using the `reject()` function

```javascript
const promise = new Promise((resolve, reject) => {
  // Simulate an error condition
  const error = new Error("Something went wrong!");
  reject(error);
});

promise
  .then(() => {
    console.log("This will not run");
  })
  .catch(error => {
    console.error("Promise rejected:", error.message);
  });

// Output:
// Promise rejected: Something went wrong!
```
## 3. Can you pass custom error objects to the `reject()` function?

- Yes, you can pass **any value** to `reject()`, including custom error objects, strings, numbers, or plain objects.
- However, it is **best practice** to pass **Error objects** (or instances of custom error classes) because they provide meaningful error information such as stack traces.
  
**Example:**

```javascript
class CustomError extends Error {
  constructor(message) {
    super(message);
    this.name = "CustomError";
  }
}

const promise = new Promise((resolve, reject) => {
  reject(new CustomError("Custom error occurred"));
});

promise.catch(error => {
  console.error(error.name);    // CustomError
  console.error(error.message); // Custom error occurred
});
```
## 4. Is calling `reject()` the same as throwing an error inside the executor?

- **Calling `reject()`** explicitly rejects the Promise with the given reason.
- **Throwing an error** inside the executor function automatically causes the Promise to be rejected with that error.
- Both approaches result in the Promise being rejected, but calling `reject()` is more explicit and controlled.
- Example equivalence:

```javascript
// Using reject()
new Promise((resolve, reject) => {
  reject(new Error("Failed"));
});

// Throwing an error
new Promise((resolve, reject) => {
  throw new Error("Failed");
});
```
Both Promises will be rejected with the error `"Failed"`.
## 5. What happens if both `resolve()` and `reject()` are called? Which one takes effect?

- A Promise’s state can **only be settled once**: either fulfilled or rejected.
- The **first call to `resolve()` or `reject()` takes effect**, and any subsequent calls are ignored.
- If `resolve()` is called first, the Promise becomes fulfilled; calling `reject()` afterwards has no effect.
- If `reject()` is called first, the Promise becomes rejected; calling `resolve()` afterwards is ignored.

**Example:**

```javascript
const promise = new Promise((resolve, reject) => {
  resolve("Success");
  reject(new Error("Failure"));  // Ignored
});

promise.then(value => console.log(value))  // Logs: Success
       .catch(error => console.error(error));
```
