## 1. What happens to the call stack when a function is invoked?

- When a function is invoked:
  - A new **execution context** is created for that function.
  - This execution context is then **pushed onto the top** of the **call stack**.
  - The JavaScript engine begins executing the function’s code within this context.
- If the function calls another function, a new execution context is created and pushed onto the stack.
- Once a function finishes executing, its execution context is **popped off** the call stack, and control returns to the previous context.

## 2. What happens if the call stack is blocked for too long?

- If the call stack is blocked for too long (e.g., due to heavy computation or an infinite loop), the following issues occur:
  - **The browser becomes unresponsive**, and the UI may freeze.
  - **Asynchronous callbacks** (from `setTimeout`, events, or promises) in the task/microtask queues cannot be executed.
  - The **event loop is stalled**, preventing further execution of queued operations.
  - The user may see a “Page Unresponsive” warning or a performance slowdown.
- To avoid this, long-running tasks should be:
  - Broken into smaller chunks using `setTimeout`, `requestAnimationFrame`, or `Web Workers`.
  - Offloaded to background threads where possible (e.g., using `Web Workers` in the browser).

---

**Summary:**

| Question                             | Answer                                                                                   |
|--------------------------------------|------------------------------------------------------------------------------------------|
| What happens on function invocation? | A new execution context is created and pushed onto the call stack.                      |
| What if call stack is blocked too long? | UI freezes, event loop stalls, async callbacks are delayed, and browser may become unresponsive. |

## 3. How does the event loop handle asynchronous operations like `setTimeout()`?

- When `setTimeout()` is called:
  1. The callback function and the delay are passed to the **Web APIs** (provided by the browser or runtime).
  2. The JavaScript engine **continues executing** other code without waiting for the timer.
  3. After the delay, the callback is **moved to the task queue**.
  4. The **event loop** waits for the **call stack to be empty**, and then pushes the callback onto the call stack.
  5. The callback is finally **executed**.

> Note: Even with a delay of `0ms`, the callback is not executed until all synchronous code completes.

## 4. What is the difference between synchronous and asynchronous execution in the event loop?

| Aspect                   | Synchronous Execution                             | Asynchronous Execution                                      |
|--------------------------|---------------------------------------------------|-------------------------------------------------------------|
| Timing                   | Runs **immediately** in sequence                  | Scheduled to run **later**, outside current execution flow  |
| Call Stack               | Executed **directly** on the call stack           | Executed **after** being queued by the event loop           |
| Blocking Behavior        | **Blocks** further code execution                 | **Does not block** the main thread                          |
| Example                  | `console.log("Hello")`                            | `setTimeout(() => console.log("Hi"), 1000)`                |

- **Synchronous code** is executed line-by-line, blocking the main thread until each line is completed.
- **Asynchronous code** is deferred via the event loop, allowing the main thread to remain responsive and continue processing other tasks.

---

**Summary:**

- The **event loop** enables non-blocking execution by deferring asynchronous callbacks until the call stack is clear.
- Understanding the difference between synchronous and asynchronous execution helps prevent UI freezing and ensures responsive application design.
