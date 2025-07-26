## 1. What is the event loop in JavaScript?

- The **event loop** is a core part of the JavaScript runtime that manages **asynchronous operations** in a **single-threaded environment**.
- It coordinates the execution of code, handling of events, and execution of queued callback functions (like those from `setTimeout`, promises, or user input).
- The event loop continuously monitors the **call stack** and the **task queues**, and moves tasks from the queue to the stack when appropriate.

## 2. Why is the event loop essential in JavaScript’s concurrency model?

- JavaScript is **single-threaded**, which means only one operation can run at a time.
- The event loop is essential because it allows JavaScript to perform **asynchronous operations** (e.g., I/O, timers, HTTP requests) **without blocking** the main thread.
- It enables **concurrent-like behavior** by scheduling tasks to be executed **after the current call stack is cleared**, thus keeping the UI responsive.

## 3. How does the event loop enable non-blocking behavior in JavaScript?

- When an asynchronous function (like `fetch()` or `setTimeout()`) is called, it registers the task with the **Web APIs** (in browsers) or the Node.js APIs.
- The main thread continues executing other code **without waiting** for the async task to finish.
- Once the async operation completes, its callback is placed in the **task queue**.
- The **event loop checks** if the call stack is empty, and if so, **pushes the callback onto the stack** for execution.
- This mechanism ensures that long-running operations **don’t block** the main thread and UI remains smooth.

---

**Summary:**

| Question                                 | Answer                                                                                  |
|------------------------------------------|-----------------------------------------------------------------------------------------|
| What is the event loop?                  | A mechanism that manages execution of async tasks and callbacks in JavaScript.          |
| Why is it essential?                     | It enables asynchronous, non-blocking operations in a single-threaded environment.      |
| How does it enable non-blocking behavior?| By deferring async callbacks to a queue and running them only when the call stack is clear. |

## 4. What are the core components involved in the event loop mechanism?

The core components of the **event loop mechanism** in JavaScript are:

1. **Call Stack**  
   - The data structure that keeps track of the currently executing functions.
   - Functions are pushed onto the stack when called and popped off when completed.

2. **Web APIs (Browser APIs)**  
   - Provided by the browser or environment (e.g., Node.js).
   - Handles asynchronous tasks like `setTimeout`, `fetch`, DOM events, etc.
   - These APIs run independently of the call stack.

3. **Task Queue (Callback Queue or Macro Task Queue)**  
   - Stores callbacks from Web APIs (e.g., `setTimeout` or `click` handlers).
   - The event loop moves tasks from this queue to the call stack when it is empty.

4. **Microtask Queue**  
   - A special queue for tasks like resolved Promises and `queueMicrotask`.
   - Always given priority over the task queue.

5. **Event Loop**  
   - Continuously checks if the call stack is empty.
   - If it is, it pushes the next task (microtask first, then task queue) to the call stack for execution.

---

## 5. Is JavaScript single-threaded or multi-threaded?  
**Explain in the context of the event loop.**

- JavaScript is **single-threaded** by design — only **one operation can run at a time** on the main thread.
- The **event loop** allows JavaScript to handle **concurrent operations** (e.g., network requests, timers) in a **non-blocking way**.
- While JavaScript itself runs on a single thread, the **runtime environment (e.g., browser or Node.js)** uses **multi-threaded capabilities** to handle background tasks via Web APIs.
- These tasks run independently and use the event loop to **communicate results back to the main thread**.

---

### Example:

```js
console.log("Start");

setTimeout(() => {
  console.log("Timeout callback");
}, 0);

Promise.resolve().then(() => {
  console.log("Promise callback");
});

console.log("End");
```
### Step-by-step Breakdown:

1. `"Start"` is logged from the call stack.

2. `setTimeout` registers its callback with the **Web APIs**.

3. `Promise.resolve().then(...)` is added to the **microtask queue**.

4. `"End"` is logged from the call stack.

5. The call stack is now empty, so the **event loop runs microtasks first**:
   - Logs `"Promise callback"`.

6. Then the event loop processes the **task queue**:
   - Logs `"Timeout callback"`.

---

### Output:

```sql
Start
End
Promise callback
Timeout callback
```