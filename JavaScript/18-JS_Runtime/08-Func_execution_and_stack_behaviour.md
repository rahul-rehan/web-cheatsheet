## 1. What happens when a function is called in terms of the call stack?

- When a function is called, JavaScript creates a new **execution context** (also called a **stack frame**) for that function.
- This execution context contains information like the function's parameters, local variables, and the current value of `this`.
- The new execution context is then **pushed onto the top** of the call stack.
- The JavaScript engine begins executing the function within this new context.

## 2. What happens when a function returns in terms of the call stack?

- When a function completes execution (returns), its **execution context is popped off** the top of the call stack.
- Control returns to the execution context below it on the stack (usually the caller function or global context).
- The call stack then continues executing the remaining code in the previous context.

## 3. What is a stack frame (or execution context) in the call stack?

- A **stack frame** (or **execution context**) is an object that contains all the information required to run a function, including:
  - The function’s arguments and parameters.
  - Local variables and function declarations.
  - The value of `this`.
  - The scope chain (lexical environment references).
- Each function call creates a new stack frame pushed onto the call stack.
- Stack frames ensure each function has its own independent environment for execution.

---

**Summary:**

| Question                        | Answer                                                        |
|--------------------------------|---------------------------------------------------------------|
| What happens when function is called? | New execution context (stack frame) is created and pushed onto the call stack. |
| What happens when function returns?   | Execution context is popped off the call stack; control returns to previous context. |
| What is a stack frame/execution context? | Data structure containing function’s execution info pushed onto the call stack. |

## 4. Provide a step-by-step example of how the call stack changes during nested function calls

Consider the following code:

```js
function first() {
  second();
}

function second() {
  third();
}

function third() {
  console.log("Inside third");
}

first();
```
### Step-by-step call stack changes:

1. **Global execution context** is created and pushed onto the call stack.

2. `first()` is called:
   - Create a new execution context for `first`.
   - Push `first`’s execution context on top of the call stack.

3. Inside `first()`, `second()` is called:
   - Create a new execution context for `second`.
   - Push `second`’s execution context on top of the call stack.

4. Inside `second()`, `third()` is called:
   - Create a new execution context for `third`.
   - Push `third`’s execution context on top of the call stack.

5. `third()` executes `console.log`, then completes:
   - Pop `third`’s execution context off the call stack.

6. `second()` completes:
   - Pop `second`’s execution context off the call stack.

7. `first()` completes:
   - Pop `first`’s execution context off the call stack.

8. Finally, the program returns to the **global execution context**.
## 5. What happens to the call stack when a function throws an error?

- When a function throws an error, its current execution context is **immediately popped off** the call stack.
- The error then **propagates up the call stack**, causing subsequent execution contexts to be popped one by one.
- This continues until a matching `try...catch` block handles the error.
- If no handler is found, the program terminates with an uncaught error.
- During this process, the call stack **unwinds**, removing stack frames as the error bubbles up.
