## 1. What is the purpose of the `finally()` method in a Promise chain?

- The `finally()` method is used to define a callback that runs **after a Promise is settled**, regardless of whether it was **fulfilled or rejected**.
- It is typically used for **cleanup operations** like closing connections, hiding loading indicators, or resetting state.

## 2. What does the `finally()` method return?

- The `finally()` method returns a **Promise**.
- It passes through the original resolved value or rejection reason **unchanged** to the next handler in the chain.
- If `finally()` throws an error or returns a rejected Promise, the chain will be **rejected with that new error** instead.

## 3. When is the `finally()` method executed in a Promise lifecycle?

- `finally()` is executed **after the Promise is settled**, meaning:
  - After `.then()` if the Promise is fulfilled.
  - After `.catch()` if the Promise is rejected.
- It always runs, making it ideal for code that should execute no matter the outcome.
## 4. Does `finally()` receive any arguments? Why or why not?

- No, the `finally()` callback **does not receive any arguments**.
- It is designed for **side effects or cleanup tasks** that do **not depend on the outcome** of the Promise.
- If you need to access the resolved value or rejection reason, use `.then()` or `.catch()` instead.

## 5. How is `finally()` different from `.then()` and `.catch()` in behavior?

- `.then()` is called when a Promise is **fulfilled** and receives the resolved value.
- `.catch()` is called when a Promise is **rejected** and receives the error or reason.
- `finally()` is called **after the Promise is settled**, **regardless of the result**, and receives **no arguments**.
- It does **not modify** the resolved/rejected value unless it throws or returns a rejected Promise.

## 6. Provide a basic example demonstrating the use of `finally()`.

```javascript
fetch('https://api.example.com/data')
  .then(response => response.json())
  .then(data => {
    console.log('Data received:', data);
  })
  .catch(error => {
    console.error('Fetch failed:', error);
  })
  .finally(() => {
    console.log('Fetch attempt completed.');
  });
```
#### Output (success case):

```css
Data received: { ... }
Fetch attempt completed.
```
#### Output (failure case):

```pgsql
Fetch failed: TypeError: Failed to fetch
Fetch attempt completed.
```

## Usage Scenarios
## 1. What are typical use cases for the `finally()` method?

- **Cleanup operations** that should run regardless of Promise success or failure.
- **Resetting UI state**, such as hiding loaders or enabling buttons.
- **Releasing resources**, like closing database connections or network sockets.
- **Logging** that needs to run whether the operation succeeded or failed.

## 2. How can you use `finally()` to perform cleanup tasks?

- Place any cleanup logic inside the `finally()` block so it runs after the Promise settles.
- This ensures that your cleanup code is **not duplicated** in both `.then()` and `.catch()` blocks.

**Example:**
```javascript
doAsyncTask()
  .then(result => {
    console.log('Task succeeded:', result);
  })
  .catch(error => {
    console.error('Task failed:', error);
  })
  .finally(() => {
    cleanupResources(); // Always runs
  });
```
## 3. Can `finally()` be used to show or hide a loading spinner? How?

- Yes, `finally()` is ideal for showing or hiding a loading spinner.
- You can display the spinner **before** the async operation begins and hide it in the `finally()` block, ensuring it gets hidden regardless of whether the Promise was fulfilled or rejected.

**Example:**
```javascript
showLoadingSpinner();

fetch('https://api.example.com/data')
  .then(response => response.json())
  .then(data => {
    displayData(data);
  })
  .catch(error => {
    showError(error);
  })
  .finally(() => {
    hideLoadingSpinner(); // Always runs
  });
```
## 4. What happens if you return a value from the `finally()` block?

- The value returned from `finally()` is **ignored**.
- It does **not affect** the next `.then()` or `.catch()` in the Promise chain.
- The original resolved or rejected value is passed through unchanged.

## 5. What happens if you throw an error inside a `finally()` block?

- If an error is thrown in the `finally()` block (or it returns a rejected Promise), the entire chain will **reject with that new error**.
- The original Promise result is overridden by the new error from `finally()`.

## 6. Does the original resolved/rejected value get changed by `finally()`?

- **No**, unless:
  - The `finally()` block throws an error, or
  - It returns a rejected Promise.
- In those cases, the original result is **replaced** by the new rejection.
- Otherwise, the original fulfillment or rejection is **preserved**.
