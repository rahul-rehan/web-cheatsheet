## 1. How do you create a Promise using the Promise constructor?

You can create a Promise in JavaScript using the `Promise` constructor by passing it a function (known as the *executor function*) that takes two arguments: `resolve` and `reject`. This function contains the logic for the asynchronous operation and should call `resolve(value)` when the operation is successful, or `reject(error)` if it fails.

## 2. What arguments does the Promise constructor take?

The `Promise` constructor takes **one argument**:

- A function called the **executor function** with two parameters:
  - `resolve`: A function to call when the operation completes successfully.
  - `reject`: A function to call when the operation fails or encounters an error.

```js
new Promise((resolve, reject) => {
  // async logic goes here
});
```
## 3. Provide an example of a manually created Promise.

Here's a simple example of a manually created Promise that resolves after 2 seconds:

```javascript
const myPromise = new Promise((resolve, reject) => {
  setTimeout(() => {
    const success = true;

    if (success) {
      resolve("Operation was successful!");
    } else {
      reject("Something went wrong.");
    }
  }, 2000);
});

// Consuming the Promise
myPromise
  .then(result => {
    console.log(result); // Output: "Operation was successful!"
  })
  .catch(error => {
    console.error(error); // If rejected, logs: "Something went wrong."
  });
```
#### Explanation
- A new `Promise` is created using the `Promise` constructor.

- The executor function includes a `setTimeout` to simulate an asynchronous operation.

- If `success` is `true`, the Promise is resolved with a success message.

- If `success` is `false`, the Promise is rejected with an error message.

- The Promise is then consumed using `.then()` and `.catch()` to handle the result.
## 4. What is the purpose of the `resolve()` and `reject()` functions?

The `resolve()` and `reject()` functions are used inside the executor function of a Promise to indicate the outcome of an asynchronous operation:

- `resolve(value)`:  
  Marks the Promise as **fulfilled** and sets the result to `value`. This will trigger any `.then()` handlers attached to the Promise.

- `reject(reason)`:  
  Marks the Promise as **rejected** and sets the failure `reason` (typically an error). This will trigger any `.catch()` handlers attached to the Promise.

These functions are essential to control the flow of asynchronous logic and communicate success or failure.

## 5. Can a Promise be resolved or rejected more than once?

No, a Promise can **only be resolved or rejected once**.

- After the Promise is settled (either fulfilled or rejected), any subsequent calls to `resolve()` or `reject()` are ignored.
- The state of a Promise is immutable once it has been settled.

Example:

```javascript
const promise = new Promise((resolve, reject) => {
  resolve("First call");
  resolve("Second call"); // Ignored
  reject("This won't work either"); // Ignored
});

promise.then(console.log).catch(console.error);
// Output: "First call"
```
## 6. What happens if you throw an error inside a Promise executor function?

If you throw an error inside the executor function of a Promise, the Promise is **automatically rejected** with the thrown error as the rejection reason.

### Example:

```javascript
const promise = new Promise((resolve, reject) => {
  throw new Error("Something went wrong!");
});

promise.catch(error => {
  console.error(error.message); // Output: "Something went wrong!"
});
```
#### Explanation:
- The `throw` statement inside the executor function causes an exception.

- JavaScript automatically catches this exception and calls `reject()` with the error.

- As a result, the Promise is rejected, and the `.catch()` handler receives the error.