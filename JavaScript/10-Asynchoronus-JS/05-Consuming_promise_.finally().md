## 1. What is the purpose of `.finally()` in a Promise chain?

The `.finally()` method is used to specify a callback that will be executed **once the Promise is settled**, regardless of whether it was fulfilled or rejected. It is typically used for **cleanup tasks**, such as closing resources, stopping loaders, or resetting states, that should happen after the asynchronous operation completes.

## 2. When is the `.finally()` block executed?

The `.finally()` block is executed **after the Promise is settled**, meaning it runs after the Promise is either:

- **Fulfilled (resolved successfully)**
- **Rejected (failed)**

It runs regardless of the outcome.

## 3. Can you modify the resolved value in `.finally()`?

No, `.finally()` **cannot modify the resolved value or rejection reason** that will be passed down the chain.

- The value or error from the previous Promise is **passed through unchanged** after `.finally()` executes.
- If `.finally()` returns a Promise, the next handler waits for that Promise to settle, but the original resolved/rejected value is still passed on.

### Example:

```javascript
Promise.resolve("Success")
  .finally(() => {
    console.log("Cleanup tasks");
    // Even if you return a value here, it doesn't affect the resolved value
    return "Ignored value";
  })
  .then(result => {
    console.log(result); // Output: "Success"
  });
```
## 4. Provide an example of using `.finally()` to clean up resources

The `.finally()` method is ideal for performing cleanup actions that should run regardless of whether a Promise is fulfilled or rejected, such as stopping loaders or closing connections.

### Example:

```javascript
function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const success = true; // Change to false to simulate error
      if (success) {
        resolve("Data fetched successfully");
      } else {
        reject("Error fetching data");
      }
    }, 1000);
  });
}

fetchData()
  .then(data => {
    console.log(data);
  })
  .catch(error => {
    console.error(error);
  })
  .finally(() => {
    console.log("Cleanup: Hide loader, close connections, etc.");
  });
```
## 5. Does `.finally()` receive any arguments?

No, the `.finally()` callback **does not receive any arguments**.

- It cannot access the resolved value or rejection reason directly.
- Its purpose is solely to execute code after the Promise settles, regardless of the outcome.

If you need to handle the resolved value or error, use `.then()` or `.catch()` respectively before or after `.finally()`.

## Advanced and Best Practices
## 1. What happens if you return a new Promise inside a `.then()` handler?

When you return a new Promise inside a `.then()` handler:

- The next `.then()` in the chain **waits for that new Promise to settle** (either fulfilled or rejected).
- This allows for **sequencing asynchronous operations**, where each step depends on the previous one.
- The resolved value or rejection reason of the returned Promise is passed to the next handler.

### Example:

```javascript
doSomething()
  .then(() => {
    return new Promise((resolve) => {
      setTimeout(() => resolve("Step 2 complete"), 1000);
    });
  })
  .then(result => {
    console.log(result); // Output after 1 second: "Step 2 complete"
  });
```
## 2. What are some common mistakes when working with Promises?

- **Not returning Promises inside `.then()`**: This breaks the chain and leads to unexpected behavior.
- **Forgetting to handle errors**: Omitting `.catch()` can cause uncaught errors.
- **Mixing callbacks and Promises improperly**: Can cause complexity and bugs.
- **Creating unnecessary nested Promises**: Leads to "Promise hell" instead of flattening chains.
- **Ignoring Promise states**: Assuming immediate synchronous resolution.

## 3. How can you convert a callback-based API to return Promises?

You can wrap callback-based functions inside a Promise constructor, a process often called **promisification**.

### Example:

```javascript
function readFilePromise(filePath) {
  return new Promise((resolve, reject) => {
    fs.readFile(filePath, (err, data) => {
      if (err) reject(err);
      else resolve(data);
    });
  });
}
```
Alternatively, libraries like Node.js's `util.promisify` automate this.
## 4. How do Promises differ from async/await in terms of syntax and readability?

- **Promises** use `.then()` and `.catch()` chaining, which can become verbose and nested for complex flows.
- **async/await** syntax allows writing asynchronous code that looks synchronous, improving **readability** and **error handling** with `try/catch`.
- Under the hood, `async/await` is built on Promises.

### Example comparison:

```javascript
// Using Promises
fetchData()
  .then(data => processData(data))
  .then(result => console.log(result))
  .catch(error => console.error(error));

// Using async/await
async function fetchAndProcess() {
  try {
    const data = await fetchData();
    const result = await processData(data);
    console.log(result);
  } catch (error) {
    console.error(error);
  }
}
```
## 5. What are best practices for error handling in Promises?

- Always attach a `.catch()` to handle errors.
- Prefer a single `.catch()` at the end of the chain for centralized error handling.
- Use `try/catch` blocks with async/await for clearer error management.
- Avoid swallowing errors silently.
- Log or propagate errors appropriately.
- Consider using `.finally()` for cleanup tasks regardless of success or failure.
