## 1. What is a microtask in JavaScript?

- A **microtask** is a type of asynchronous task that is scheduled to run **immediately after the current execution context completes** and **before any macrotasks**.
- Microtasks are prioritized and **always executed before macrotasks**, as long as the call stack is clear.
- They are often used for lightweight, high-priority asynchronous operations.

## 2. What is a macrotask in JavaScript?

- A **macrotask** (also known simply as a **task**) is an asynchronous operation that is scheduled to run **after all microtasks have completed**.
- Macrotasks are handled by the **task queue** and are scheduled for execution in the **next cycle of the event loop**.
- They are generally used for more delayed or scheduled operations.

## 3. What are some examples of microtasks?

- `Promise.then()` and `Promise.catch()`
- `queueMicrotask()`
- `MutationObserver` callbacks (in the browser)

---

**Comparison Table:**

| Feature       | Microtask                                 | Macrotask                                |
|---------------|--------------------------------------------|-------------------------------------------|
| Runs after    | Current execution context                  | All microtasks and current context         |
| Queue type    | Microtask queue                            | Task (callback) queue                     |
| Examples      | `Promise.then()`, `queueMicrotask()`       | `setTimeout()`, `setInterval()`, `fetch()` |
| Priority      | Higher                                      | Lower                                     |

## 4. What are some examples of macrotasks?

- `setTimeout()`
- `setInterval()`
- `setImmediate()` (Node.js)
- I/O operations (e.g., reading files, network requests)
- UI rendering events (e.g., user interactions like clicks, scrolls)
- `requestAnimationFrame()` (treated as a macrotask in browsers)

## 5. What is the order of execution between microtasks and macrotasks?

1. **Synchronous code** runs first on the call stack.
2. After the synchronous code completes, **all microtasks** in the microtask queue run **to completion**.
3. Once the microtask queue is empty, the event loop processes **one macrotask** from the macrotask (task) queue.
4. The cycle repeats: after the macrotask completes, microtasks are processed again before the next macrotask.

---

**Summary:**

| Execution Step            | Description                                              |
|--------------------------|----------------------------------------------------------|
| 1. Synchronous code       | Runs immediately                                         |
| 2. Microtasks             | Runs all queued microtasks before next macrotask        |
| 3. Macrotasks             | Runs one macrotask after all microtasks are done        |
| 4. Repeat                 | Event loop continues this cycle                          |
