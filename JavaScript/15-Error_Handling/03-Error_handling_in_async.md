## 1. How do you handle errors in asynchronous code using try...catch with async/await?

- Wrap the `await` calls inside a `try` block.  
- Use the `catch` block to handle any errors thrown by the awaited Promises.  
- This approach allows synchronous-looking error handling for async operations.

```js
async function fetchData() {
  try {
    const data = await fetch('https://api.example.com/data');
    console.log(await data.json());
  } catch (error) {
    console.error('Error fetching data:', error);
  }
}
```
## 2. What happens if you forget to use try...catch with await?

- If the awaited Promise rejects and there is no `try...catch`, the error will be unhandled.  
- This may cause the program to crash or produce unhandled promise rejection warnings.  
- Proper error handling ensures your app can recover gracefully or fail in a controlled manner.

## 3. How do you catch errors in Promise chains using `.catch()`?

- Attach a `.catch()` method at the end of the Promise chain to handle any rejected Promises.  
- The `.catch()` method receives the error object and lets you handle it appropriately.

```js
fetch('https://api.example.com/data')
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error fetching data:', error));
```
## 4. What happens if you forget to use try...catch with await?

- If the awaited Promise rejects and there is no `try...catch`, the error will be unhandled.  
- This may cause the program to crash or produce unhandled promise rejection warnings.  
- Proper error handling ensures your app can recover gracefully or fail in a controlled manner.

## 5. How do you catch errors in Promise chains using `.catch()`?

- Attach a `.catch()` method at the end of the Promise chain to handle any rejected Promises.  
- The `.catch()` method receives the error object and lets you handle it appropriately.

```js
fetch('https://api.example.com/data')
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error fetching data:', error));
```

## Advanced & Practical Scenarios
## 1. How can you wrap third-party code to ensure proper error handling?

- Use `try...catch` blocks around third-party code to catch synchronous errors.  
- For asynchronous third-party code, use Promises with `.catch()` or async/await with `try...catch`.  
- Wrap callbacks with error handlers if the third-party API uses callbacks.  
- This prevents uncaught errors from crashing your application and allows graceful recovery.

## 2. How does the `window.onerror` or `window.addEventListener('error')` work?

- `window.onerror` is a global event handler that catches uncaught JavaScript errors in the browser.  
- It provides information about the error message, source file, line number, and column number.  
- Similarly, `window.addEventListener('error', handler)` listens for error events globally.  
- These mechanisms help in logging and reporting errors that were not caught elsewhere.

## 3. How does Node.js handle errors differently from the browser?

- In Node.js, unhandled errors in asynchronous code (like Promises) cause unhandled promise rejections, which can terminate the process if not handled.  
- Node.js provides `process.on('uncaughtException')` and `process.on('unhandledRejection')` to catch unhandled errors globally.  
- Unlike browsers, Node.js runs on the server where crashing can have more serious consequences, so explicit error handling is critical.  
- Node.js APIs often use error-first callbacks (`(err, result) => {}`) to propagate errors synchronously through callbacks.
## 4. What is a synchronous vs asynchronous error?

- **Synchronous error:** Occurs during the normal, linear execution of code and can be caught immediately by `try...catch`. For example, accessing a property of `undefined` in the same call stack.
- **Asynchronous error:** Occurs outside the current call stack, such as in callbacks, timers, Promises, or async functions. These errors cannot be caught by a surrounding synchronous `try...catch` unless the asynchronous code is awaited or handled properly.

## 5. Can try...catch catch syntax errors? Why or why not?

- No, `try...catch` cannot catch syntax errors because syntax errors occur **before** the code is executed (during parsing).  
- `try...catch` only works for **runtime errors** that occur while the code is executing.

## 6. Can try...catch catch errors inside event handlers or callback functions?

- No, `try...catch` cannot directly catch errors thrown asynchronously inside event handlers or callbacks because these execute outside the scope of the original `try...catch` block.  
- To catch such errors, you need to place a `try...catch` **inside** the event handler or callback function itself.
