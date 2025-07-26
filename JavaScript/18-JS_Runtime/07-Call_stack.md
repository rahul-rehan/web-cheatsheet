## 1. What is the call stack in JavaScript?

- The **call stack** is a **data structure** (stack) used by JavaScript to keep track of **execution contexts** created when functions are called.
- It follows a **Last-In, First-Out (LIFO)** order, meaning the most recently added execution context is the first to be executed and removed.
- It helps manage the order of function calls and returns during program execution.

## 2. How does the call stack help JavaScript manage function execution?

- When a function is called, JavaScript **creates a new execution context** for that function and **pushes it onto the call stack**.
- The function at the **top of the stack** is the one currently being executed.
- When a function finishes executing, its execution context is **popped off** the stack, and control returns to the previous execution context below it.
- This mechanism ensures that JavaScript executes functions in the correct order and properly handles nested and recursive function calls.

## 3. Is the call stack part of the JavaScript engine or the browser?

- The **call stack is part of the JavaScript engine**, which is the component responsible for interpreting and executing JavaScript code.
- It is **not part of the browser itself**, but the browser provides the environment (like the DOM and Web APIs) where the JavaScript engine runs.
- Different JavaScript engines (like V8 in Chrome, SpiderMonkey in Firefox) implement their own call stacks internally.

---

**Summary:**

| Question                       | Answer                                             |
|-------------------------------|----------------------------------------------------|
| What is the call stack?        | Data structure managing execution contexts (LIFO). |
| How does it manage execution?  | Pushes contexts on function call, pops on return, manages order of execution. |
| Part of JavaScript engine or browser? | Part of JavaScript engine, not the browser itself. |

## 4. What data structure is used to implement the call stack?

- The call stack is implemented using a **stack data structure**.
- A stack operates on a **Last-In, First-Out (LIFO)** principle:
  - The most recently added item (execution context) is the first to be removed.
  - New execution contexts are **pushed** onto the top of the stack when functions are called.
  - Execution contexts are **popped** off the stack when functions return.

## 5. What is the role of the call stack in single-threaded execution?

- JavaScript is **single-threaded**, meaning it can execute only one piece of code at a time.
- The call stack **manages the order** of execution contexts, ensuring that only one function executes at any moment.
- It keeps track of which function is currently running and where to return after the function finishes.
- By handling execution contexts in a LIFO manner, the call stack enables **nested function calls, recursion, and proper function returns** in a single-threaded environment.
- It prevents simultaneous execution of multiple functions, thus avoiding race conditions in single-threaded JavaScript.

---

**Summary:**

| Question                           | Answer                                         |
|----------------------------------|------------------------------------------------|
| Data structure used for call stack | Stack (LIFO)                                   |
| Role in single-threaded execution  | Manages execution order, ensures one function runs at a time, supports nested calls and returns |
