## 1. How does the event loop differ in Node.js vs browser environments?

- Both environments follow the **event loop model**, but Node.js has a **more structured loop** with **specific phases**, while browsers use a simpler task/microtask queue approach.
- Node.js:
  - Designed for server-side operations and heavy I/O.
  - Has **multiple event loop phases** (e.g., timers, I/O callbacks, close callbacks).
  - Supports additional APIs like `process.nextTick()` and `setImmediate()` that affect task scheduling.
- Browser:
  - Prioritizes UI rendering and interactivity.
  - Manages the event loop in coordination with rendering and animation frames.
  - Relies on task and microtask queues, without formal loop phases exposed to developers.

## 2. What are phases in Node.js's event loop?

Node.js's event loop has **six main phases**, executed in order each tick:

1. **Timers**  
   - Executes callbacks scheduled by `setTimeout()` and `setInterval()`.

2. **Pending Callbacks**  
   - Executes I/O callbacks deferred to the next loop iteration.

3. **Idle, Prepare** *(internal use)*  
   - Used internally by Node.js.

4. **Poll**  
   - Retrieves new I/O events; executes I/O-related callbacks (e.g., file or socket reads).

5. **Check**  
   - Executes callbacks from `setImmediate()`.

6. **Close Callbacks**  
   - Executes `close` event callbacks, like `socket.on('close', ...)`.

> Between each phase, **microtasks** (from `Promise.then()` and `process.nextTick()`) are processed.

## 3. How does `process.nextTick()` differ from `Promise.then()` in Node.js?

| Feature                | `process.nextTick()`                            | `Promise.then()`                          |
|------------------------|--------------------------------------------------|-------------------------------------------|
| Queue Type             | **Next Tick Queue**                             | **Microtask Queue**                       |
| Priority               | Runs **before** any other microtasks            | Runs **after** `process.nextTick()`       |
| Use Case               | Schedule immediate callbacks after current op   | Handle async resolution of promises       |
| Caution                | Overuse may **starve the event loop**           | More predictable, follows spec-compliant order |

- `process.nextTick()` is **Node-specific**, and always runs **before** `Promise.then()` and other microtasks.
- It is often used for **backward compatibility** or to **defer execution** without yielding to the event loop.

---

**Example Execution Order:**

```js
setTimeout(() => console.log('setTimeout'), 0);
setImmediate(() => console.log('setImmediate'));
process.nextTick(() => console.log('nextTick'));
Promise.resolve().then(() => console.log('Promise.then'));
```

#### Output:

```javascript
nextTick
Promise.then
setTimeout
setImmediate
```
#### Summary:

- Node.js event loop is phase-driven and tailored for server-side use.

- Browsers focus on responsiveness and animation.

- `process.nextTick()` runs earlier than `Promise.then()`, making it powerful but potentially risky if misused.

## 4. What happens when both a `setTimeout()` and a `Promise.then()` are scheduled? Which runs first?

- When both are scheduled:
  - `Promise.then()` is placed in the **microtask queue**.
  - `setTimeout()` is placed in the **macrotask queue**.
- **Microtasks run before macrotasks**, so the `Promise.then()` callback will execute first—even if `setTimeout(..., 0)` is used.

**Example:**

```js
setTimeout(() => console.log("setTimeout"), 0);
Promise.resolve().then(() => console.log("Promise.then"));
```
#### Output:

```javascript
Promise.then
setTimeout
```

## 5. What is starvation in the event loop, and how can it occur?

- **Starvation** in the event loop happens when one queue—typically the **microtask queue**—is constantly being filled with tasks, preventing the event loop from reaching and processing other queues, like the **macrotask queue**.
- This leads to:
  - **Delayed execution** of macrotasks (e.g., `setTimeout`, I/O callbacks).
  - **Unresponsive UI** or server-side delays.
  - **Frame drops** and poor performance in the browser.


### Causes of Starvation:

- Continuously scheduling microtasks, such as:
  - Recursively calling `Promise.then()`
  - Using `queueMicrotask()` inside itself
  - Overusing `process.nextTick()` in Node.js

### Example of Microtask Starvation:

```js
function blockEventLoop() {
  queueMicrotask(blockEventLoop);
}

blockEventLoop(); // This will prevent the event loop from reaching any macrotasks
```
In the example above, the event loop never proceeds to the next phase because the microtask queue is never empty.

## 6. How does `queueMicrotask()` differ from `setTimeout()`?

| Feature              | `queueMicrotask()`                                | `setTimeout()`                              |
|----------------------|---------------------------------------------------|---------------------------------------------|
| Queue Type           | Microtask queue                                   | Macrotask (task) queue                      |
| Execution Timing     | After the current execution context, before any macrotask | After all microtasks and synchronous code   |
| Delay                | No delay — runs as soon as possible               | Minimum delay of ~4ms (in browsers)         |
| Priority             | Higher — runs before any macrotasks               | Lower — runs after microtasks               |
| Use Case             | High-priority short async logic                   | Deferred execution or scheduling            |

### Example:

```js
queueMicrotask(() => console.log("microtask"));
setTimeout(() => console.log("macrotask"), 0);
console.log("sync");
```
#### Output:

```bash
sync
microtask
macrotask
```
#### Summary:
- `queueMicrotask()` is useful for scheduling short, high-priority tasks that need to run immediately after the current synchronous code.

- `setTimeout()` is better suited for deferring execution or creating delays.