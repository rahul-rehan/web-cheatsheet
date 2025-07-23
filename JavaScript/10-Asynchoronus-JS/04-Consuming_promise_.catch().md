## 1. What is the purpose of `.catch()` in a Promise chain?

The `.catch()` method is used to handle **errors or rejections** in a Promise chain. It catches:

- Errors explicitly passed via `reject()`
- Any exceptions (`throw`) that occur in the executor or inside any `.then()` callbacks

It improves readability and centralizes error handling in asynchronous workflows.

## 2. How is `.catch()` different from passing an error handler to `.then()`?

While `.then()` can take two arguments (`onFulfilled`, `onRejected`), `.catch()` is specifically designed for error handling.

### Differences:

- `.then(onFulfilled, onRejected)` mixes success and error logic, making code harder to read and maintain.
- `.catch(onRejected)` is **dedicated to error handling** and is usually placed at the end of the chain, making the code cleaner and more modular.

**Example:**

```javascript
// Less preferred: error handler inside .then()
promise.then(result => {
  // success
}, error => {
  // error
});

// Preferred: separate .catch() block
promise
  .then(result => {
    // success
  })
  .catch(error => {
    // error
  });
```
## 3. Where should you place `.catch()` in a chain to handle all potential errors?

You should place `.catch()` at the **end of the Promise chain** to catch:

- Any rejections from the Promise itself
- Any errors thrown in any preceding `.then()` callbacks

This ensures **centralized error handling** for the entire chain.

## 4. Provide an example of error handling using `.catch()`

```javascript
const getUserData = (userId) => {
  return new Promise((resolve, reject) => {
    if (!userId) {
      reject("Invalid user ID");
    } else {
      resolve({ id: userId, name: "Alice" });
    }
  });
};

getUserData(null)
  .then(data => {
    console.log("User:", data);
  })
  .catch(error => {
    console.error("Error occurred:", error);
  });
```
#### Output:
```javascript
Error occurred: Invalid user ID
```
This example demonstrates using `.catch()` to gracefully handle an error when the Promise is rejected.
## 5. Can `.catch()` itself return a resolved Promise?

Yes, `.catch()` **can return a resolved Promise**.

When you return a value (or a resolved Promise) inside a `.catch()` handler, the Promise chain continues with a **fulfilled state** using that value. This effectively recovers from the error and allows subsequent `.then()` calls to execute as if no error occurred.

### Example:

```javascript
Promise.reject("Something went wrong")
  .catch(error => {
    console.error("Caught error:", error);
    return "Recovered value"; // Returning a resolved value
  })
  .then(result => {
    console.log("Result after recovery:", result);
  });
```
#### Output:
```yaml
Caught error: Something went wrong
Result after recovery: Recovered value
```
This feature is useful to handle errors gracefully and provide fallback values.