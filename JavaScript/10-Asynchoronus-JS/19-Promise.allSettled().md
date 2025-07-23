## 1. What is the `Promise.allSettled()` method in JavaScript?

- `Promise.allSettled()` is a method that takes an iterable of Promises and returns a new Promise.
- This new Promise resolves **after all of the input Promises have settled** (either fulfilled or rejected).
- It is useful when you want to know the outcome of all Promises without failing fast on any rejection.

## 2. What type of argument does `Promise.allSettled()` accept?

- It accepts an **iterable** (e.g., an array) of Promises or values.
- Non-Promise values are treated as immediately fulfilled Promises.

---

## 3. What does `Promise.allSettled()` return?

- It returns a Promise that resolves with an **array of objects**, each representing the outcome of the corresponding Promise.
- Each object has:
  - A `status` property: `"fulfilled"` or `"rejected"`.
  - If fulfilled, a `value` property containing the resolved value.
  - If rejected, a `reason` property containing the rejection reason.

### Example returned array:
```json
[
  { "status": "fulfilled", "value": 42 },
  { "status": "rejected", "reason": "Network error" }
]
```
## 4. How is the result of `Promise.allSettled()` structured?

- The result is an **array of objects**, where each object corresponds to an input Promise.
- Each object contains:
  - A `status` property indicating the outcome (`"fulfilled"` or `"rejected"`).
  - If the Promise fulfilled, a `value` property with the resolved value.
  - If the Promise rejected, a `reason` property with the rejection reason.

## 5. What are the possible status values in the results of `Promise.allSettled()`?

- `"fulfilled"` — The Promise was resolved successfully.
- `"rejected"` — The Promise was rejected.

## 6. Provide an example where `Promise.allSettled()` is used with both resolved and rejected Promises.

```javascript
const promise1 = Promise.resolve(42);
const promise2 = Promise.reject("Error occurred");
const promise3 = Promise.resolve("Success");

Promise.allSettled([promise1, promise2, promise3])
  .then(results => {
    results.forEach((result, index) => {
      if (result.status === "fulfilled") {
        console.log(`Promise ${index + 1} fulfilled with value:`, result.value);
      } else {
        console.log(`Promise ${index + 1} rejected with reason:`, result.reason);
      }
    });
  });
```
#### Output:

```javascript
Promise 1 fulfilled with value: 42
Promise 2 rejected with reason: Error occurred
Promise 3 fulfilled with value: Success
```

## Behavior and Characteristics
## 1. How does `Promise.allSettled()` differ from `Promise.all()` in handling rejections?

- **`Promise.all()`**:
  - Returns a Promise that **rejects immediately** as soon as **any** of the input Promises reject.
  - Does **not wait** for the other Promises to settle.
- **`Promise.allSettled()`**:
  - Returns a Promise that **resolves only after all** input Promises have settled, regardless of whether they fulfilled or rejected.
  - Provides the full outcome of each Promise without short-circuiting on rejection.

## 2. What happens if all Promises are fulfilled in `Promise.allSettled()`?

- The returned Promise resolves with an array where **all results have a `status` of `"fulfilled"`**.
- Each object contains the resolved `value` of the corresponding Promise.

## 3. What happens if all Promises are rejected in `Promise.allSettled()`?

- The returned Promise still **resolves** (does not reject).
- The result array contains objects where each has a `status` of `"rejected"` and a `reason` property with the rejection reason.
- This allows handling or inspecting all errors without failing fast.
## 4. Does the order of results in `Promise.allSettled()` match the order of input Promises?

- Yes, the results array returned by `Promise.allSettled()` **maintains the order** of the input Promises.
- Each result corresponds to the Promise at the same index in the input iterable, regardless of the order in which the Promises settle.

## 5. Can `Promise.allSettled()` be used with non-Promise values?

- Yes, `Promise.allSettled()` accepts an iterable of Promises **or non-Promise values**.
- Non-Promise values are treated as **already fulfilled Promises** with their value.

## 6. How long does `Promise.allSettled()` wait before settling?

- `Promise.allSettled()` waits until **all input Promises have settled** (either fulfilled or rejected).
- It settles only after every Promise in the iterable has either resolved or rejected.
## 7. What are the properties of a fulfilled result object in `Promise.allSettled()`?

- `status`: A string with the value `"fulfilled"`.
- `value`: The resolved value of the Promise.

**Example:**
```json
{
  "status": "fulfilled",
  "value": 42
}
```
## 8. What are the properties of a rejected result object in `Promise.allSettled()`?

- `status`: A string with the value `"rejected"`.
- `reason`: The reason or error for which the Promise was rejected.

**Example:**
```json
{
  "status": "rejected",
  "reason": "Network error"
}
```

## Use Cases and Best Practices
## 1. When should you prefer `Promise.allSettled()` over `Promise.all()`?

- When you want to **wait for all Promises to settle**, regardless of whether they fulfill or reject.
- When you need to **handle both success and failure results** of multiple Promises without failing fast.
- Useful when you want a **complete overview of all outcomes**, not just the first failure.

## 2. How can `Promise.allSettled()` be used to implement robust error reporting?

- By collecting the results of all Promises, including rejections, you can **log or report all errors at once**.
- This enables better debugging and recovery strategies, since no failure is silently ignored or causes early exit.
- You can iterate through the results to distinguish between successes and failures, then handle or report accordingly.

## 3. What are some real-world scenarios where `Promise.allSettled()` is useful?

- Fetching data from **multiple APIs or servers**, where some may fail but you still want all available data.
- Running multiple independent background tasks where **all results need to be recorded**, regardless of success.
- Performing bulk operations (e.g., file uploads) where **you want a report of which succeeded or failed**.
- UI rendering scenarios where partial data should be displayed even if some requests fail.

## 4. How do you filter successful results from `Promise.allSettled()`?

You can filter the results array to extract only the fulfilled Promises like this:

```javascript
Promise.allSettled(promises).then(results => {
  const successfulResults = results
    .filter(result => result.status === "fulfilled")
    .map(result => result.value);

  console.log('Successful values:', successfulResults);
});
```
## 5. How do you filter failed results from `Promise.allSettled()`?

You can filter the results array to extract only the rejected Promises like this:

```javascript
Promise.allSettled(promises).then(results => {
  const failedResults = results
    .filter(result => result.status === "rejected")
    .map(result => result.reason);

  console.log('Failed reasons:', failedResults);
});
```
## 6. Can `Promise.allSettled()` be used with async/await? Provide an example.

Yes, `Promise.allSettled()` works smoothly with async/await syntax.

```javascript
async function fetchAll() {
  const promises = [
    Promise.resolve('Success 1'),
    Promise.reject('Error 1'),
    Promise.resolve('Success 2'),
  ];

  const results = await Promise.allSettled(promises);

  results.forEach((result, index) => {
    if (result.status === 'fulfilled') {
      console.log(`Promise ${index} fulfilled with:`, result.value);
    } else {
      console.log(`Promise ${index} rejected with:`, result.reason);
    }
  });
}

fetchAll();
```
## 7. What are the limitations of `Promise.allSettled()`?

- It **always resolves**, so it does not fail fast on the first rejection like `Promise.all()`.
- The caller must manually inspect each result to handle successes and failures.
- Not suitable when you want to stop execution immediately on any error.
- Can produce verbose results if many Promises reject, requiring extra handling logic.

## 8. How does `Promise.allSettled()` help avoid unhandled promise rejections?

- By waiting for **all Promises to settle** (either fulfilled or rejected), it ensures that every rejection is accounted for.
- Prevents unhandled rejection warnings by capturing errors as part of the results.
- Encourages explicit handling of both successful and failed Promises in batch asynchronous operations.
