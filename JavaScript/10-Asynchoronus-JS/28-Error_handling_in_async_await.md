## 1. How do you handle errors in async/await code?

- Errors in async/await code are typically handled using `try...catch` blocks.  
- Wrapping the `await` calls inside a `try` block allows you to catch and handle any rejected Promises or thrown errors gracefully.  
- This approach makes asynchronous error handling look and behave like synchronous code, improving readability and maintainability.

## 2. Provide an example using try...catch in an async function

```js
async function fetchData() {
  try {
    const response = await fetch('https://api.example.com/data');
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error('Error fetching data:', error);
  }
}
```
## 3. What happens if you await a rejected Promise without a try...catch?

- Awaiting a rejected Promise without a `try...catch` causes the async function to immediately throw the rejection as an error.
- This unhandled rejection will propagate up the call stack.
- If the rejection is not caught anywhere, it may lead to:
  - Unhandled promise rejection warnings.
  - Application crashes or unexpected behavior.
- Therefore, it is important to handle errors using `try...catch` or by attaching `.catch()` handlers to avoid such issues.
## 4. How do you handle multiple await operations with different failure points?

- Use separate `try...catch` blocks around each `await` if you want to handle errors individually for each operation.
- Alternatively, wrap multiple awaits inside a single `try...catch` if the same error handling logic applies.
- For more complex flows, consider using helper functions with their own error handling or Promise utilities like `Promise.allSettled()` to handle multiple results and errors concurrently without stopping at the first failure.

**Example:**

```js
async function processMultiple() {
  try {
    const result1 = await asyncOperation1();
  } catch (error) {
    console.error('Error in operation 1:', error);
  }

  try {
    const result2 = await asyncOperation2();
  } catch (error) {
    console.error('Error in operation 2:', error);
  }
}
```
## 5. How is error propagation different in async/await compared to .then()/.catch()?

- In `.then()/.catch()`, errors propagate through the Promise chain and must be handled with `.catch()` or subsequent error handlers.
- In `async/await`, errors behave like synchronous exceptions and can be caught using `try...catch` blocks.
- Async/await provides more straightforward, linear error handling that resembles traditional synchronous code.
- If an error is not caught inside an async function, it causes the returned Promise to reject, similar to throwing an error in a Promise chain.
# Summary

| Aspect             | .then()/.catch()                 | async/await                 |
|--------------------|---------------------------------|-----------------------------|
| **Error handling style** | Promise chain with `.catch()`      | `try...catch` blocks         |
| **Propagation**         | Passed through Promise chain     | Thrown as exceptions         |
| **Readability**         | Can be less intuitive with nested chains | More linear and synchronous-like |
