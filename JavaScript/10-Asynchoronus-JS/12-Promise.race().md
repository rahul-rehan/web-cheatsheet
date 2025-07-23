## 1. What is the `Promise.race()` method in JavaScript?

- `Promise.race()` is a method that takes an iterable of Promises and returns a new Promise.
- This returned Promise **settles as soon as the first Promise in the iterable settles** (either fulfills or rejects).
- It "races" the Promises against each other, resolving or rejecting with the value or reason of the first settled Promise.

## 2. What type of argument does `Promise.race()` accept?

- `Promise.race()` accepts an **iterable** (usually an array) of Promises or values.
- Non-Promise values in the iterable are treated as resolved Promises immediately.

## 3. What does `Promise.race()` return?

- It returns a new Promise that settles with the **value or reason of the first Promise that settles** in the iterable.
- This means the returned Promise resolves or rejects as soon as any input Promise resolves or rejects.
## 4. How does `Promise.race()` determine which promise "wins"?

- `Promise.race()` settles as soon as **the first Promise in the iterable settles** (either fulfills or rejects).
- The "winning" Promise is the one that settles first, regardless of whether it fulfills or rejects.
- The returned Promise adopts the **value or reason** of this first settled Promise.

## 5. What happens if the first settled promise is a rejection?

- If the first settled Promise rejects, `Promise.race()` **immediately rejects** with the same rejection reason.
- The returned Promise's rejection is based on this first rejection.

## 6. What happens if the first settled promise is a fulfillment?

- If the first settled Promise fulfills, `Promise.race()` **immediately resolves** with the fulfillment value.
- The returned Promise resolves with this value without waiting for the others.

## 7. Provide a basic example using `Promise.race()` with two Promises.

```javascript
const promise1 = new Promise((resolve) => setTimeout(() => resolve("First!"), 500));
const promise2 = new Promise((resolve, reject) => setTimeout(() => reject("Second failed"), 300));

Promise.race([promise1, promise2])
  .then(result => {
    console.log("Resolved with:", result);
  })
  .catch(error => {
    console.error("Rejected with:", error);
  });

// Output after ~300ms: "Rejected with: Second failed"
```
#### In this example:

- `promise2` rejects first after 300ms, so `Promise.race()` rejects immediately with that error.

- The result of `promise1` is ignored since it settles later.

## Behavior and Use Cases
## 1. Does `Promise.race()` wait for all Promises to settle?

- No, `Promise.race()` **does not wait** for all Promises to settle.
- It settles (resolves or rejects) **as soon as the first Promise settles**.
- The remaining Promises continue running in the background but their results are ignored by the `Promise.race()` result.

## 2. Can `Promise.race()` be used to implement timeouts? How?

- Yes, `Promise.race()` is commonly used to implement **timeouts** for asynchronous operations.
- You race the original Promise against a timeout Promise that rejects or resolves after a specified delay.
- If the timeout Promise settles first, you can handle the timeout case accordingly.

### Example of timeout implementation:

```javascript
function fetchWithTimeout(url, timeout = 5000) {
  const fetchPromise = fetch(url);

  const timeoutPromise = new Promise((_, reject) => 
    setTimeout(() => reject(new Error("Request timed out")), timeout)
  );

  return Promise.race([fetchPromise, timeoutPromise]);
}

fetchWithTimeout("https://api.example.com/data")
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error("Error:", error.message));
```
## 3. How can you use `Promise.race()` to abort a long-running asynchronous task?

- You can race the long-running Promise against another Promise that **signals an abort**, such as a user action or a timeout.
- When the abort Promise settles first (usually rejects), you handle the cancellation logic.
- This pattern allows you to stop waiting for the long task and respond immediately.

### Example using `Promise.race()` to abort:

```javascript
const longRunningTask = new Promise(resolve => {
  setTimeout(() => resolve("Task completed"), 10000); // Long task takes 10 seconds
});

const abortSignal = new Promise((_, reject) => {
  // Simulate abort signal after 3 seconds
  setTimeout(() => reject(new Error("Task aborted by user")), 3000);
});

Promise.race([longRunningTask, abortSignal])
  .then(result => {
    console.log(result);
  })
  .catch(error => {
    console.error(error.message); // Output: Task aborted by user
  });
```
## 4. In what order are the promises evaluated in `Promise.race()`?

- The Promises are **started immediately and concurrently** as they are passed to `Promise.race()`.
- However, `Promise.race()` does **not depend on the order** in which Promises settle, only on which settles first.
- The order of settlement determines the result, not the order of Promises in the iterable.

## 5. Is the order of promises in the array passed to `Promise.race()` significant?

- The order in the array **is not significant** for determining which Promise settles first.
- The result depends solely on **which Promise settles first** (fulfills or rejects), regardless of its position in the array.

## 6. What happens if one of the Promises never settles?

- If one or more Promises never settle (neither fulfill nor reject), `Promise.race()` will wait indefinitely **unless another Promise settles first**.
- The returned Promise settles as soon as **any Promise settles**, so unresolved Promises only cause delay if they are the only ones.

## 7. What is the return value of `Promise.race()` when it resolves or rejects?

- `Promise.race()` returns a new Promise that settles **with the value or reason of the first settled Promise**.
- If the first settled Promise resolves, `Promise.race()` resolves with its value.
- If the first settled Promise rejects, `Promise.race()` rejects with its rejection reason.
