## 1. What is promise chaining in JavaScript?

Promise chaining is the process of linking multiple `.then()` calls in a sequence, where each `.then()` runs after the previous Promise is resolved. This allows you to perform a series of asynchronous operations in order, passing results from one step to the next.

## 2. How does returning a value from a `.then()` affect the next `.then()` in the chain?

When you return a **value** from a `.then()` callback:

- That value is automatically wrapped in a resolved Promise.
- The next `.then()` in the chain receives this returned value as its input.

If you return a **Promise**, the next `.then()` waits for that Promise to resolve and then receives its resolved value.

## 3. How can you perform a sequence of asynchronous operations using promise chaining?

You perform a sequence by returning a Promise or a value from each `.then()` callback, which feeds into the next `.then()`. This way, each asynchronous operation waits for the previous one to complete before starting.

### Example:

```javascript
doFirstTask()
  .then(result1 => {
    console.log("First task result:", result1);
    return doSecondTask(result1);
  })
  .then(result2 => {
    console.log("Second task result:", result2);
    return doThirdTask(result2);
  })
  .then(result3 => {
    console.log("Third task result:", result3);
  })
  .catch(error => {
    console.error("Error in chain:", error);
  });
```
## 4. Provide an example of chaining multiple `.then()` methods together

You can chain multiple `.then()` methods to perform a sequence of asynchronous operations, where the output of one step is passed to the next.

### Example:

```javascript
Promise.resolve(5)
  .then(value => {
    console.log("Step 1:", value);
    return value * 2;
  })
  .then(value => {
    console.log("Step 2:", value);
    return value + 3;
  })
  .then(value => {
    console.log("Step 3:", value);
  });
```
## 5. What happens if one of the `.then()` handlers in a chain throws an error?

If a `.then()` handler throws an error (or returns a rejected Promise), the Promise chain is **short-circuited**, and control is passed to the nearest `.catch()` handler. Subsequent `.then()` handlers are skipped until the error is handled.

## 6. How does `.catch()` work in a promise chain?

- `.catch()` registers a callback to handle any **rejection** or **error** that occurs in the Promise chain before it.
- It **catches errors thrown in any preceding `.then()`** or the initial Promise rejection.
- After `.catch()` handles an error, the chain can continue if `.catch()` returns a value or Promise.

### Example:

```javascript
Promise.resolve(10)
  .then(value => {
    throw new Error("Something went wrong!");
  })
  .then(() => {
    // This will be skipped due to the error above
    console.log("This will not run");
  })
  .catch(error => {
    console.error("Caught error:", error.message);
  });
```

## 7. How can you rethrow an error inside a `.catch()` and handle it later in the chain?

You can **rethrow an error inside a `.catch()`** by using the `throw` statement or returning a rejected Promise. This passes the error down the chain to be handled by a later `.catch()`.

### Example:

```javascript
Promise.reject("Initial error")
  .catch(error => {
    console.log("Caught first error:", error);
    throw new Error("Rethrown error");
  })
  .catch(error => {
    console.log("Caught rethrown error:", error.message);
  });
```
## 8. Can a `.then()` block return a new Promise?

Yes, a `.then()` callback can return a **new Promise**. The next `.then()` in the chain will wait for this Promise to resolve or reject before continuing.

## 9. What is the difference between returning a plain value vs. returning a Promise in a `.then()`?

- **Returning a plain value:**  
  The value is automatically wrapped in a resolved Promise, and passed to the next `.then()` immediately.

- **Returning a Promise:**  
  The next `.then()` waits for this Promise to settle (resolve or reject), and receives its resolved value or rejection reason.

### Example:

```javascript
Promise.resolve(10)
  .then(value => {
    return value * 2; // Plain value returned
  })
  .then(value => {
    console.log(value); // Output: 20
    return new Promise(resolve => {
      setTimeout(() => resolve(value + 5), 1000);
    });
  })
  .then(value => {
    console.log(value); // Output after 1 second: 25
  });
```