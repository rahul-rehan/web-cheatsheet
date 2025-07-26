## 1. What is the callback queue (also called task queue or message queue)?

- The **callback queue** (also known as the **task queue** or **message queue**) is a data structure that stores **asynchronous callback functions** waiting to be executed.
- These callbacks come from asynchronous operations like:
  - `setTimeout()`
  - DOM events (e.g., `click`, `keydown`)
  - `setInterval()`
  - Web API responses
- Each callback in the queue waits its turn to be **moved to the call stack** by the event loop.

## 2. When are callbacks from the queue moved to the call stack?

- The **event loop** continuously checks if the **call stack is empty**.
- If the call stack is empty:
  - The event loop moves the **first callback** from the callback queue to the call stack.
  - The callback is then **executed**.
- **Microtasks** (like resolved promises and `queueMicrotask()`) are given **priority** over tasks in the callback queue.
  - The event loop **processes all microtasks first** before handling the next callback from the task queue.

---

**Summary:**

| Concept                 | Description                                                                 |
|--------------------------|-----------------------------------------------------------------------------|
| Callback Queue           | Queue where async callbacks wait before being executed                     |
| When Callbacks Run       | Moved to the call stack only when it is empty and all microtasks are processed |

## 3. What happens if the call stack is not empty when a task is ready in the queue?

- If the **call stack is not empty**, the **event loop cannot push any new tasks** (including asynchronous callbacks) from the **callback queue** to the stack.
- The ready task will remain **in the queue, waiting** until the stack is completely cleared.
- This means:
  - Asynchronous callbacks like those from `setTimeout`, DOM events, or network requests will be **delayed**.
  - The program continues executing **synchronous code** before handling the queued tasks.
- **Long-running synchronous code** can block the event loop, causing the UI to freeze and making apps unresponsive.

## 4. What is the order of execution between synchronous and asynchronous code?

1. **Synchronous code** is executed **immediately** on the **call stack**, in the order it appears.
2. Once all synchronous code is complete and the call stack is empty:
   - The **event loop** checks the **microtask queue** (e.g., resolved Promises, `queueMicrotask()`).
   - **All microtasks are executed before any task from the callback queue.**
3. After the microtask queue is cleared, the event loop moves the next task from the **callback queue** to the call stack and executes it.

### Example:

```js
console.log("A");

setTimeout(() => {
  console.log("B");
}, 0);

Promise.resolve().then(() => {
  console.log("C");
});

console.log("D");
```
#### Output:

```css
A
D
C
B
```
### Explanation:

- `"A"` and `"D"` are **synchronous** → executed **immediately**.
- The promise callback `"C"` is a **microtask** → runs **next**, after synchronous code.
- The `setTimeout` callback `"B"` is a **task** → runs **last**, after all microtasks are completed.
