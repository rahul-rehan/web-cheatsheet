## 1. What is `Promise.all()` in JavaScript?

`Promise.all()` is a method that takes multiple Promises and returns a single Promise that:

- Resolves when **all** of the input Promises have resolved.
- Rejects as soon as **any one** of the input Promises rejects.

It is used to run multiple asynchronous operations in parallel and wait for all of them to complete.

## 2. What kind of argument does `Promise.all()` accept?

`Promise.all()` accepts an **iterable** (usually an array) of Promises or values. Non-Promise values in the iterable are treated as resolved Promises.

Example argument:

```javascript
Promise.all([promise1, promise2, value3]);
```
## 3. What does `Promise.all()` return?

`Promise.all()` returns a new Promise that:

- Resolves with an **array of resolved values** from all the input Promises, in the same order as the input iterable.
- Rejects immediately with the **reason of the first rejected Promise** among the inputs.

### Example:

```javascript
Promise.all([
  Promise.resolve(1),
  Promise.resolve(2),
  3 // Non-Promise value treated as resolved
])
.then(results => {
  console.log(results); // Output: [1, 2, 3]
})
.catch(error => {
  console.error("One of the promises rejected:", error);
});
```
## 4. What happens when all Promises passed to `Promise.all()` are fulfilled?

When **all Promises** passed to `Promise.all()` are fulfilled:

- The returned Promise **resolves**.
- It resolves with an **array of all the resolved values** from the input Promises.
- The resolution happens only after **every Promise** in the iterable has resolved.

## 5. In what order are values returned by `Promise.all()`?

The array of values returned by the resolved Promise from `Promise.all()`:

- Maintains the **same order as the input iterable**, regardless of the order in which the individual Promises resolve.
- This ensures predictable mapping between input Promises and their results.

## 6. Provide an example using `Promise.all()` with three asynchronous tasks.

```javascript
function asyncTask(id, delay) {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve(`Task ${id} completed`);
    }, delay);
  });
}

Promise.all([
  asyncTask(1, 300),
  asyncTask(2, 100),
  asyncTask(3, 200)
])
.then(results => {
  console.log(results);
  // Output after ~300ms:
  // ["Task 1 completed", "Task 2 completed", "Task 3 completed"]
})
.catch(error => {
  console.error("One of the tasks failed:", error);
});
```
#### In this example:

- Even though Task 2 finishes before Task 1 and Task 3, the results array preserves the input order.