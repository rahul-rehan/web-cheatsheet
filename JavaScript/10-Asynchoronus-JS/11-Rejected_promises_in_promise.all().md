## 1. What happens if any one of the Promises passed to `Promise.all()` is rejected?

- If **any one** of the Promises passed to `Promise.all()` is rejected:
  - The returned Promise from `Promise.all()` **immediately rejects** with that rejection reason.
  - It does **not wait** for the other Promises to resolve or reject.

## 2. Does `Promise.all()` wait for all Promises to settle before rejecting?

- No, `Promise.all()` **does not wait** for all Promises to settle.
- It **rejects as soon as the first Promise rejects**, short-circuiting the rest.
- The other Promises continue running in the background but their results are ignored by `Promise.all()`.

## 3. How can you catch an error from a rejected Promise in `Promise.all()`?

- You can catch errors by attaching a `.catch()` handler to the `Promise.all()` call.
- This `.catch()` will receive the rejection reason of the **first Promise that rejects**.

### Example:

```javascript
const p1 = Promise.resolve("Success");
const p2 = Promise.reject("Error occurred");
const p3 = new Promise(resolve => setTimeout(() => resolve("Late success"), 1000));

Promise.all([p1, p2, p3])
  .then(results => {
    console.log("All succeeded:", results);
  })
  .catch(error => {
    console.error("Promise.all rejected with:", error); // Logs: "Promise.all rejected with: Error occurred"
  });
```
## 4. What does the rejected error contain?

- The rejected error from `Promise.all()` contains the **reason of the first Promise that rejects**.
- This reason can be any value that the rejected Promise passes to its `reject()` function, such as an `Error` object, a string, or any other value.

## 5. Provide an example where `Promise.all()` rejects due to a single failing Promise.

```javascript
const p1 = Promise.resolve("Success 1");
const p2 = Promise.reject(new Error("Failed Promise"));
const p3 = Promise.resolve("Success 3");

Promise.all([p1, p2, p3])
  .then(results => {
    console.log("All succeeded:", results);
  })
  .catch(error => {
    console.error("Promise.all rejected with error:", error.message);
    // Output: Promise.all rejected with error: Failed Promise
  });
```
#### In this example:

- `p2` rejects with an `Error`.

- `Promise.all()` immediately rejects with this error and skips `p3`'s result.
## 6. How can you prevent a single rejected Promise from breaking the entire `Promise.all()`?

- You can **handle errors individually for each Promise** by catching errors inside each Promise.
- This way, all Promises resolve successfully from the perspective of `Promise.all()`, even if some contain error information.
- One common pattern is to catch errors and return them as resolved values (e.g., wrapped in an object), so `Promise.all()` always resolves.

### Example:

```javascript
function safePromise(promise) {
  return promise
    .then(value => ({ status: "fulfilled", value }))
    .catch(error => ({ status: "rejected", reason: error }));
}

const p1 = Promise.resolve("Success 1");
const p2 = Promise.reject(new Error("Failed Promise"));
const p3 = Promise.resolve("Success 3");

Promise.all([safePromise(p1), safePromise(p2), safePromise(p3)])
  .then(results => {
    console.log(results);
    /* Output:
    [
      { status: "fulfilled", value: "Success 1" },
      { status: "rejected", reason: Error: Failed Promise },
      { status: "fulfilled", value: "Success 3" }
    ]
    */
  });
```
#### This approach allows you to:

- Get results of all Promises, including errors.

- Avoid the entire `Promise.all()` rejecting due to a single failure.

## Advanced Usage and Best Practices
## 1. How can you use `Promise.all()` to fetch data in parallel from multiple APIs?

- You can initiate multiple API requests (which return Promises) **simultaneously** and pass them to `Promise.all()`.
- `Promise.all()` waits for **all requests** to complete and provides an array of responses.
- This approach improves efficiency by running requests in parallel instead of sequentially.

### Example:

```javascript
const api1 = fetch("https://api.example.com/data1").then(res => res.json());
const api2 = fetch("https://api.example.com/data2").then(res => res.json());
const api3 = fetch("https://api.example.com/data3").then(res => res.json());

Promise.all([api1, api2, api3])
  .then(([data1, data2, data3]) => {
    console.log("Data from API 1:", data1);
    console.log("Data from API 2:", data2);
    console.log("Data from API 3:", data3);
  })
  .catch(error => {
    console.error("Error fetching data:", error);
  });
```
## 2. What are common use cases for `Promise.all()`?

- Running **multiple asynchronous operations in parallel** and waiting for all to complete.
- Fetching data from **multiple APIs simultaneously**.
- Performing **batch processing** tasks (e.g., uploading files, reading multiple files).
- Waiting for multiple independent tasks before proceeding (e.g., loading multiple resources on a page).
- Combining results from several Promises into a single array or object.

## 3. What are potential pitfalls of using `Promise.all()` in production applications?

- **Fails fast:** If any Promise rejects, `Promise.all()` rejects immediately, potentially causing loss of other results.
- **No partial results:** You don’t get results from fulfilled Promises if one fails, unless you handle errors individually.
- **Resource intensive:** Running many requests in parallel can overwhelm servers or the client (e.g., too many API calls at once).
- **Error handling complexity:** Requires careful handling to avoid uncaught rejections.
- **Order dependency:** The result array order is based on input order, which might not match the order of completion.

To mitigate some pitfalls, consider using `Promise.allSettled()`, batching requests, or adding custom error handling.
## 4. How does `Promise.all()` compare with `Promise.allSettled()` in terms of behavior on rejection?

- **`Promise.all()`**:
  - Rejects **immediately** if any Promise in the iterable rejects.
  - Does **not wait** for the other Promises to settle.
  - Returns the rejection reason of the first rejected Promise.
  
- **`Promise.allSettled()`**:
  - Waits for **all Promises** to settle, regardless of whether they fulfill or reject.
  - Always **resolves** with an array of objects describing the outcome of each Promise (`{ status: "fulfilled", value }` or `{ status: "rejected", reason }`).
  - Useful when you want to know the result of **all** Promises without failing fast.

## 5. When should you avoid using `Promise.all()`?

- When you want to **handle all results individually**, including rejected Promises, without failing the entire batch.
- When you expect some Promises to reject but want the overall operation to continue.
- When running a **large number of Promises** that might overwhelm system resources if executed all at once.
- When you want to perform **progressive error handling** or fallback strategies rather than a fail-fast approach.

## 6. Can `Promise.all()` be used inside an async function with `await`? Provide an example.

Yes, `Promise.all()` works well inside async functions with `await`, allowing you to run multiple asynchronous tasks in parallel and wait for all of them to complete.

### Example:

```javascript
async function fetchMultipleData() {
  const api1 = fetch("https://api.example.com/data1").then(res => res.json());
  const api2 = fetch("https://api.example.com/data2").then(res => res.json());
  const api3 = fetch("https://api.example.com/data3").then(res => res.json());

  try {
    const [data1, data2, data3] = await Promise.all([api1, api2, api3]);
    console.log("Data 1:", data1);
    console.log("Data 2:", data2);
    console.log("Data 3:", data3);
  } catch (error) {
    console.error("One of the fetches failed:", error);
  }
}

fetchMultipleData();
```