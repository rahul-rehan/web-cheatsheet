## 1. What happens when all Promises passed to `Promise.any()` are rejected?

- If **all Promises are rejected**, `Promise.any()` will:
  - **Reject with an `AggregateError`**.
  - This error contains a list of **all rejection reasons** from the input Promises.

## 2. What is an `AggregateError` in the context of `Promise.any()`?

- `AggregateError` is a special error object introduced in ES2021.
- It represents **multiple errors** at once — in this case, all the rejection reasons from the input Promises.
- It has a `message` and an `errors` array:
  - `message`: General error message.
  - `errors`: An array of individual rejection reasons.

## 3. How can you handle an `AggregateError` returned by `Promise.any()`?

You can catch the error using `.catch()` or a `try...catch` block in an `async` function. Inside the catch, you can access the `.errors` property of the `AggregateError` to examine each reason.

### Example:

```javascript
const p1 = Promise.reject("Error from p1");
const p2 = Promise.reject("Error from p2");

Promise.any([p1, p2])
  .then(result => {
    console.log("Resolved with:", result);
  })
  .catch(error => {
    if (error instanceof AggregateError) {
      console.error("All promises rejected:");
      error.errors.forEach((e, i) => {
        console.error(`Error ${i + 1}:`, e);
      });
    } else {
      console.error("Unexpected error:", error);
    }
  });
```
## 4. Provide an example where all Promises are rejected and `Promise.any()` fails

```javascript
const a = Promise.reject("Network error");
const b = Promise.reject("Timeout error");
const c = Promise.reject("Auth error");

Promise.any([a, b, c])
  .then(result => {
    console.log("This will not run.");
  })
  .catch(error => {
    console.error("Promise.any failed with AggregateError:");
    console.error("Number of errors:", error.errors.length);
    console.log(error.errors); // ["Network error", "Timeout error", "Auth error"]
  });
```
- In this case, all Promises reject.

- `Promise.any()` rejects with an `AggregateError` that includes all three rejection reasons.