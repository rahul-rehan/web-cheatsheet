## 1. What happens if one Promise is rejected but others fulfill in `Promise.any()`?

- If **at least one Promise fulfills**, `Promise.any()` will:
  - **Resolve** with the first fulfillment value.
  - **Ignore any rejections**, including those that happen before or after the fulfillment.

## 2. Will `Promise.any()` reject if the first Promise is rejected but another one fulfills later?

- **No**, `Promise.any()` does **not reject** if a rejection happens first.
- It only rejects if **all** Promises in the iterable are rejected.
- If **any one Promise eventually fulfills**, the returned Promise will resolve with that value, even if some others reject before it.

## 3. Provide an example where one Promise is rejected and one is fulfilled in `Promise.any()`.

```javascript
const rejectPromise = new Promise((_, reject) => setTimeout(() => reject("Error occurred"), 100));
const resolvePromise = new Promise((resolve) => setTimeout(() => resolve("Success!"), 200));

Promise.any([rejectPromise, resolvePromise])
  .then(result => {
    console.log("Resolved with:", result); // Output: "Resolved with: Success!"
  })
  .catch(error => {
    console.error("All promises rejected:", error);
  });
```
#### In this example:

- The first Promise is rejected after 100ms.

- The second Promise is fulfilled after 200ms.

- `Promise.any()` waits for a fulfillment and eventually resolves with `"Success!"`.