## 1. What does the resolved value of `Promise.all()` look like?

- The resolved value of `Promise.all()` is an **array** containing the resolved values of all input Promises.
- The order of values in the array corresponds to the **order of the Promises passed** to `Promise.all()`, regardless of when each Promise resolves.

## 2. If one of the Promises resolves immediately and others take time, when does `Promise.all()` resolve?

- `Promise.all()` resolves **only after all** Promises in the iterable have resolved.
- Even if one Promise resolves immediately, the returned Promise waits for the **slowest Promise** to settle before resolving.
- The resolved array will contain all the resolved values once all Promises finish.

## 3. Can `Promise.all()` be used with non-Promise values? What happens in that case?

- Yes, `Promise.all()` can accept **non-Promise values** (e.g., numbers, strings, objects).
- Non-Promise values are treated as if they are **already resolved Promises**.
- They appear in the resolved array as-is, without delay.

### Example:

```javascript
Promise.all([
  Promise.resolve("fast"),
  42,             // Non-Promise value
  new Promise(resolve => setTimeout(() => resolve("slow"), 1000))
])
.then(results => {
  console.log(results); // Output after 1 second: ["fast", 42, "slow"]
});
```
## 4. What is the behavior of `Promise.all([])`?

- When `Promise.all()` is called with an **empty array** (`[]`):
  - It returns a Promise that **resolves immediately**.
  - The resolved value is an **empty array** (`[]`).
- This happens because there are no Promises to wait for, so the operation is considered complete right away.

### Example:

```javascript
Promise.all([])
  .then(results => {
    console.log(results); // Output: []
  });
```
