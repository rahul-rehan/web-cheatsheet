## 1. What is a Promise in JavaScript?

A **Promise** in JavaScript is an object representing the eventual completion (or failure) of an asynchronous operation and its resulting value. It allows asynchronous code to be written in a more manageable and readable way, avoiding deeply nested callbacks (also known as "callback hell").

## 2. What problem do Promises solve in asynchronous programming?

Promises solve the **problem of callback hell** by:

- Allowing **chaining** of asynchronous operations using `.then()`.
- Providing a cleaner, more **structured approach** to handling success and error scenarios.
- Making it easier to **handle multiple asynchronous tasks** in parallel or sequence using methods like `Promise.all()` or `Promise.race()`.
- Improving **error handling** through `.catch()` instead of nesting multiple callbacks.

## 3. What are the three states of a Promise?

A Promise in JavaScript has three possible states:

1. **Pending** – The initial state. The operation has not yet completed.
2. **Fulfilled** – The operation completed successfully.
3. **Rejected** – The operation failed with an error.

## 4. What is the difference between a pending, fulfilled, and rejected Promise?

- **Pending**:  
  The Promise is neither fulfilled nor rejected. It is still waiting for the asynchronous operation to complete.

- **Fulfilled**:  
  The asynchronous operation completed successfully, and the Promise has a resulting value. The `.then()` handler will be called with this value.

- **Rejected**:  
  The asynchronous operation failed, and the Promise has a reason (usually an error). The `.catch()` handler will be called with this reason.
