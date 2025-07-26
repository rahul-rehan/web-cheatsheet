## 1. What is the call stack in JavaScript?

The **call stack** is a data structure (a stack) used by JavaScript to keep track of function execution contexts. It manages the order in which functions are called and executed, ensuring that JavaScript executes code in a **last-in, first-out (LIFO)** manner.

## 2. How does JavaScript use the call stack to manage execution contexts?

- When JavaScript starts running, it creates the **global execution context** and pushes it onto the call stack.
- Whenever a function is invoked, a new **function execution context** is created and **pushed on top** of the call stack.
- JavaScript always executes the context on the **top of the stack**.
- When a function finishes executing, its execution context is **popped off** the stack, and control returns to the context below it.
- This mechanism ensures functions are executed in the correct order and helps manage nested function calls.

## 3. What happens when a function is invoked in terms of execution context and call stack?

1. A new **execution context** is created for the invoked function.
2. This new execution context is **pushed onto the top** of the call stack.
3. JavaScript enters the **creation phase** and then the **execution phase** of this function context.
4. The function's code runs while its context is on top of the stack.
5. Once the function finishes, its execution context is **popped off** the call stack.
6. Control returns to the previous execution context below it on the stack.

---

**Summary:**  
The call stack manages execution contexts in a LIFO manner, ensuring JavaScript runs functions and their nested calls in the correct order by pushing and popping contexts as functions are invoked and completed.

## 4. What happens when a function returns or throws an error in terms of execution context?

- When a function **returns** a value or **throws an error**, its **execution context is popped off** the call stack.  
- This means the function’s execution environment is destroyed, and control passes back to the execution context immediately below it on the stack (usually the caller function or the global context).
- If an error is thrown and not caught within the function, it propagates up the call stack, popping execution contexts until a suitable error handler (`try...catch`) is found or the program terminates.

## 5. What is a stack overflow and how does it relate to execution contexts?

- A **stack overflow** occurs when the call stack exceeds its maximum size limit, usually due to **excessive or infinite recursion**.
- Since each function call creates a new execution context pushed onto the call stack, if functions keep calling each other (or themselves) without returning, the stack keeps growing.
- Eventually, the stack runs out of memory space to hold new execution contexts, causing a **stack overflow error** and crashing the program.

---

**Summary:**

| Event                      | Effect on Execution Context and Call Stack                     |
|----------------------------|----------------------------------------------------------------|
| Function returns            | Execution context is popped off the call stack                 |
| Function throws an error    | Execution context is popped off; error propagates up the stack |
| Stack overflow             | Call stack exceeds size limit due to too many execution contexts (e.g., infinite recursion) |
