## 1. How are errors inside the Promise executor function caught?

- Errors thrown **inside the Promise executor function** automatically cause the Promise to be **rejected** with that error.
- These errors can be caught by attaching a `.catch()` handler to the Promise.
- This behavior ensures that any synchronous exceptions inside the executor do not crash the program but are handled as Promise rejections.

## 2. What happens if an error is thrown after a `resolve()` call?

- Once a Promise is **settled** (either resolved or rejected), any subsequent calls to `resolve()`, `reject()`, or thrown errors are **ignored**.
- Throwing an error after `resolve()` has no effect on the Promise’s state or outcome.
- The Promise remains in its settled state with the original resolved value.

**Example:**

```javascript
const promise = new Promise((resolve, reject) => {
  resolve("Success");
  throw new Error("Error after resolve"); // Ignored
});

promise
  .then(value => console.log(value))   // Logs: Success
  .catch(error => console.error(error)); // Not called
```
## 3. How can you handle exceptions that occur while resolving or rejecting a Promise?

- Exceptions thrown **inside the Promise executor** or within `.then()`/`.catch()` handlers automatically cause the Promise to reject with that error.
- To handle such exceptions, attach a `.catch()` method to the Promise chain.
- When working with async functions, use `try/catch` blocks around the `await` calls to catch synchronous and asynchronous errors.
- Wrapping async logic properly ensures all errors are caught and handled gracefully.

## 4. What are best practices for wrapping async logic inside try/catch when using Promises?

- Use `try/catch` **inside async functions** when using `await` to handle errors cleanly:

  ```javascript
  async function fetchData() {
    try {
      const data = await fetch('https://api.example.com/data');
      const json = await data.json();
      return json;
    } catch (error) {
      console.error('Error fetching data:', error);
      throw error; // re-throw or handle accordingly
    }
  }
  ```
- When not using async/await, handle errors with `.catch()` at the end of Promise chains.

- Avoid mixing `try/catch` with `.catch()` unnecessarily to keep error handling clear.

- Always handle rejection cases to avoid unhandled promise rejections.

- Use descriptive error messages and logging inside catch blocks for easier debugging.

```javascript
// Using Promise chaining with catch
fetch('https://api.example.com/data')
  .then(response => response.json())
  .then(json => console.log(json))
  .catch(error => console.error('Fetch error:', error));
```