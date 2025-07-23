## 1. Can multiple `.then()` handlers be attached to the same Promise?

Yes, you can attach multiple `.then()` handlers to the **same Promise**. Each `.then()` will be called when the Promise settles (resolves or rejects).

## 2. Will all `.then()` handlers run if the Promise is resolved?

Yes, **all `.then()` handlers attached to the same Promise will run** once the Promise is resolved. Each handler receives the resolved value independently.

## 3. In what order are `.then()` handlers executed when attached to the same Promise?

- `.then()` handlers are executed **in the order they were attached**.
- All handlers are called asynchronously, after the current call stack is cleared.

### Example:

```javascript
const promise = Promise.resolve("Done");

promise.then(value => console.log("First handler:", value));
promise.then(value => console.log("Second handler:", value));
promise.then(value => console.log("Third handler:", value));

// Output:
// First handler: Done
// Second handler: Done
// Third handler: Done
```
## 4. What happens if the Promise is rejected and there is no `.catch()` handler?

If a Promise is **rejected** and there is **no `.catch()` handler** (or other rejection handler), the rejection results in an **unhandled promise rejection**. This can:

- Trigger warnings or errors in the runtime environment (e.g., Node.js or browsers).
- Potentially cause the program to crash or behave unpredictably.
- Make debugging difficult, as errors are not properly handled.

## 5. Can `.catch()` handlers be attached multiple times to the same Promise?

Yes, you can attach **multiple `.catch()` handlers** to the same Promise. Each `.catch()` handler will be called independently if the Promise is rejected.

## 6. What should you be cautious about when using multiple handlers on a single Promise?

- **Multiple handlers do not short-circuit each other:** All attached handlers will run independently, so be careful not to duplicate side effects (e.g., multiple error logs or retries).
- **State sharing:** Since a Promise settles only once, all handlers receive the same resolved/rejected value; avoid mutating shared data unexpectedly.
- **Error handling:** If an error is caught and rethrown in one handler, subsequent handlers may also be triggered—plan your error flow carefully.

### Example:

```javascript
const p = Promise.reject("Error occurred");

p.catch(err => {
  console.error("First catch:", err);
  // Rethrow to pass error down the chain
  throw err;
});

p.catch(err => {
  console.error("Second catch:", err);
});
```
