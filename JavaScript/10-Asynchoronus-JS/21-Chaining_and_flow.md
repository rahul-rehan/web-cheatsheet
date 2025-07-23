## 1. How does `finally()` behave when chained after a `.catch()`?

- When `finally()` is chained after a `.catch()`, it still runs **regardless of whether the `.catch()` handled the error or not**.
- It does not interfere with the value or error being passed unless it throws or returns a rejected Promise.
- The chain continues with the original rejection (if unhandled) or the handled result.

## 2. What happens if `finally()` returns a new Promise?

- The chain will **wait for the Promise returned by `finally()` to settle** before proceeding.
- If that Promise:
  - **Resolves**, the original value (from `.then()` or `.catch()`) continues down the chain.
  - **Rejects**, the chain is **rejected with this new error**, overriding the previous result.

## 3. Can `finally()` affect the outcome of the chain if it throws an error?

- Yes, if `finally()` throws an error or returns a rejected Promise:
  - The entire chain becomes **rejected** with that new error.
  - This **replaces** any previous resolved or rejected value.

**Example:**
```javascript
Promise.resolve('done')
  .finally(() => {
    throw new Error('Something went wrong in finally');
  })
  .then(result => {
    console.log(result); // This won't run
  })
  .catch(err => {
    console.error('Caught:', err.message); // Output: Caught: Something went wrong in finally
  });
```
## 4. What is the difference between placing logic in `then()` vs `finally()` for side effects?

- **`then()`**:
  - Executes **only when the Promise is fulfilled**.
  - Use it for side effects or logic that depends on the **resolved value**.
  - You can access the resolved value directly as an argument.

- **`finally()`**:
  - Executes **regardless of the Promise outcome** (fulfilled or rejected).
  - Ideal for **side effects that must always run**, such as cleanup tasks, UI resets, or logging.
  - **Does not receive the result or error** of the Promise.

### Summary:

| Aspect              | `then()`                        | `finally()`                              |
|---------------------|----------------------------------|-------------------------------------------|
| Runs on             | Fulfillment only                | Always (fulfilled or rejected)            |
| Receives value/error| Yes (value)                     | No                                        |
| Use case            | Dependent logic on result       | Cleanup, resetting state, hiding spinners |

**Example:**
```javascript
fetchData()
  .then(data => {
    console.log('Data:', data);  // Runs only on success
  })
  .catch(error => {
    console.error('Error:', error);  // Runs on failure
  })
  .finally(() => {
    hideLoading();  // Runs regardless
  });
```

## Error Handling and Best Practices
## 1. Should you use `finally()` for logic that depends on resolved or rejected values? Why or why not?

- **No**, you should **not** use `finally()` for logic that depends on resolved or rejected values.
- `finally()` **does not receive any arguments**, so it **cannot access** the result or error of the Promise.
- Use `.then()` for handling resolved values and `.catch()` for handling errors instead.

## 2. What are common mistakes developers make when using `finally()`?

- **Expecting access to resolved or rejected values** inside `finally()`, which is incorrect.
- **Throwing errors or returning rejected Promises** inside `finally()` unintentionally, which can **override the original result**.
- **Performing essential logic** (e.g., returning values or handling data) in `finally()`, which should be placed in `.then()` or `.catch()`.

## 3. What are best practices for using `finally()` in large Promise chains?

- Use `finally()` only for **side effects** that must run regardless of outcome, like:
  - Hiding loading indicators
  - Closing connections
  - Cleaning up resources
- Avoid placing **core business logic** in `finally()`.
- Keep the `finally()` block **short and safe**—do not throw errors or include logic that can fail.
- If cleanup logic is asynchronous, ensure it **returns a resolved Promise** to avoid disrupting the chain.
## 4. How can `finally()` help make asynchronous code more reliable and maintainable?

- `finally()` ensures that certain logic **always runs**, whether a Promise is **fulfilled or rejected**.
- It helps **centralize cleanup tasks** (e.g., hiding loaders, closing connections), reducing duplication in `.then()` and `.catch()` blocks.
- By separating cleanup from main logic, it improves the **readability, structure, and maintainability** of asynchronous code.
- It prevents bugs caused by **forgotten cleanup** in one branch of the logic (e.g., only in success or failure).

## 5. Can `finally()` be used inside an `async/await` function? Provide an example.

Yes, `finally()` can be used in `async/await` code to run logic after a `try...catch` block, similar to synchronous `finally`.

**Example:**
```javascript
async function loadData() {
  showLoadingSpinner();
  try {
    const response = await fetch('https://api.example.com/data');
    const data = await response.json();
    console.log('Data:', data);
  } catch (error) {
    console.error('Error fetching data:', error);
  } finally {
    hideLoadingSpinner(); // Always runs, even if fetch fails
  }
}

loadData();
```
- In this example, `hideLoadingSpinner()` is guaranteed to run, making the code more robust and predictable.