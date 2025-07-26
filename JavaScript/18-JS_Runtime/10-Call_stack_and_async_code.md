## 1. Does asynchronous code like `setTimeout()` use the call stack directly?

- **No**, asynchronous functions like `setTimeout()` do **not use the call stack directly** when they are initially called.
- Instead, when `setTimeout()` is invoked, its callback function is registered with the **Web APIs** environment (provided by the browser or Node.js), which handles the timer separately.
- The callback itself is not executed immediately but scheduled to run later.

## 2. Where do asynchronous callbacks go while the call stack is busy?

- Asynchronous callbacks wait in the **task queue** (also called the **callback queue** or **event queue**).
- The **event loop** continuously monitors the call stack.
- When the call stack becomes empty (i.e., all synchronous code has finished executing), the event loop moves the next callback from the task queue onto the call stack.
- Only then is the asynchronous callback executed, creating a new execution context pushed onto the call stack.

---

**Summary:**

| Question                                | Answer                                                          |
|----------------------------------------|-----------------------------------------------------------------|
| Does `setTimeout()` use the call stack directly? | No, it registers the callback in Web APIs; callback runs later. |
| Where do async callbacks wait while call stack is busy? | They wait in the task queue until the call stack is empty.      |

## 3. What is the event loop and how does it interact with the call stack?

- The **event loop** is a mechanism that allows JavaScript to perform **non-blocking asynchronous operations** despite being single-threaded.
- It continuously monitors two main things:
  - The **call stack** (where functions are executed).
  - The **task queue** (where asynchronous callbacks wait).
- When the call stack is **empty**, the event loop takes the first callback from the task queue and **pushes it onto the call stack** for execution.
- This process enables JavaScript to handle async operations like timers, I/O, and promises without blocking the main thread.

## 4. Example: How the call stack handles async code with `setTimeout`

```js
console.log("Start");

setTimeout(() => {
  console.log("Inside setTimeout");
}, 0);

console.log("End");
```
### Step-by-step explanation:

1. The global execution context is created and pushed onto the call stack.

2. `console.log("Start")` runs:  
   - Logs `"Start"` to the console.

3. `setTimeout` is called:  
   - Registers the callback function with the Web APIs environment.  
   - The callback is scheduled to run after 0 milliseconds but is **not executed immediately**.

4. `console.log("End")` runs:  
   - Logs `"End"` to the console.

5. The global execution context finishes, and the call stack becomes empty.

6. The event loop detects the empty call stack and moves the `setTimeout` callback from the task queue to the call stack.

7. The callback executes, logging `"Inside setTimeout"` to the console.

8. The callback’s execution context is popped off the call stack.
