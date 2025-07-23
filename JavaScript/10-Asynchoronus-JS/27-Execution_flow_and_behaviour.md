## 1. How does async/await improve readability compared to Promise chaining?

- `async/await` allows writing asynchronous code that looks and behaves like synchronous code, making it easier to read and understand.  
- It avoids deeply nested `.then()` chains and callback hell, reducing indentation and complexity.  
- Error handling is simpler with `try/catch` instead of separate `.catch()` handlers.  
- Overall, `async/await` leads to cleaner and more maintainable code.

## 2. What happens to code execution after an await statement?

- When the JavaScript engine reaches an `await` statement, it pauses the execution of the current async function until the awaited Promise settles.  
- While waiting, the event loop can continue executing other tasks (non-blocking behavior).  
- After the Promise resolves or rejects, execution resumes from the point after the `await`, using the resolved value or handling the rejection.

## 3. Is await blocking or non-blocking? Explain with an example.

- `await` is **non-blocking** for the overall JavaScript runtime because it only pauses the execution of the current async function, allowing other code to run.  
- However, within the async function itself, it **blocks** further lines until the awaited Promise settles.

### Example:
```js
console.log('Start');

async function asyncTask() {
  console.log('Before await');
  await new Promise(resolve => setTimeout(resolve, 1000)); // Waits 1 second
  console.log('After await');
}

asyncTask();

console.log('End');
```
#### Output:

```pgsql
Start
Before await
End
After await
```
- Here, the function pauses at `await` but the rest of the script (`console.log('End')`) runs immediately without waiting.
## 4. How can you run multiple await operations in parallel instead of sequentially?

- To run multiple async operations **in parallel**, start all the Promises **without awaiting** them immediately.  
- Collect the Promises in variables or an array, then use `Promise.all()` with `await` to wait for all to resolve together.  
- This avoids waiting for each operation to complete before starting the next, improving efficiency.

### Example:
```js
async function fetchMultiple() {
  const promise1 = fetch('/api/data1');
  const promise2 = fetch('/api/data2');
  const promise3 = fetch('/api/data3');

  // Wait for all promises to resolve in parallel
  const [res1, res2, res3] = await Promise.all([promise1, promise2, promise3]);

  console.log(res1, res2, res3);
}
```
## 5. Can an async function be used as a callback? What are the considerations?

- Yes, an async function can be used as a callback since it returns a Promise.  
- However, if the caller **does not handle the returned Promise**, any errors inside the async callback may go unhandled, causing potential issues.  
- Some functions or methods (like `Array.prototype.forEach`) **do not support async callbacks properly** because they don't wait for or handle Promises returned by the callback.  
- When using async callbacks, ensure the caller either supports Promises or explicitly handles them.

### Considerations:
- Avoid using async callbacks with functions that do not handle Promises.  
- Prefer using `for...of` loops with `await` for asynchronous iteration instead of async callbacks in array methods.  
- When using async callbacks with event handlers or APIs, verify that those APIs support Promise-based callbacks.

### Example:
```js
async function asyncCallback(item) {
  await someAsyncOperation(item);
  console.log('Processed:', item);
}

// Using async callback with forEach (not recommended)
items.forEach(async (item) => {
  await asyncCallback(item); // Errors here may be unhandled
});
```
