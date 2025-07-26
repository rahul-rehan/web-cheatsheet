## 1. What is an execution context in JavaScript?

An **execution context** is an abstract concept representing the environment in which JavaScript code is evaluated and executed. It contains information about the variables, functions, and the scope chain that are accessible during the execution of a piece of code.

## 2. What are the types of execution contexts in JavaScript?

There are three main types of execution contexts:

1. **Global Execution Context (GEC)**  
   The default or base context where the entire JavaScript code runs initially.

2. **Function Execution Context**  
   Created whenever a function is invoked, containing its own scope, variables, and arguments.

3. **Eval Execution Context**  
   Created by the `eval()` function when executing code strings, but its use is generally discouraged.

## 3. What is the role of the global execution context?

- The **global execution context** is the base context created when the JavaScript engine starts executing the script.  
- It creates the global object (`window` in browsers, `global` in Node.js) and sets up the `this` keyword to reference the global object.  
- Variables and functions declared globally become properties and methods of the global object.  
- Only one global execution context exists per JavaScript program.

## 4. When is a function execution context created?

A **function execution context** is created **every time a function is invoked/called**. When a function runs, JavaScript creates a new execution context specifically for that function, which contains all the information necessary to execute the function (like arguments, local variables, the scope chain, and the value of `this`).

## 5. What is the difference between global and function execution contexts?

| Aspect                        | Global Execution Context                       | Function Execution Context                          |
|-------------------------------|-----------------------------------------------|---------------------------------------------------|
| **Creation**                  | Created once when the JavaScript program starts | Created each time a function is called            |
| **Scope**                    | Represents the global scope (e.g., `window` in browsers) | Represents the local scope of the function         |
| **Lifetime**                 | Lives throughout the lifetime of the program  | Exists only during the function's execution        |
| **Variables**                | Contains global variables and functions        | Contains function arguments, local variables       |
| **`this` value**             | Refers to the global object (`window` in browsers) | Depends on how the function is called               |
| **Stack**                   | Bottom of the call stack                        | Pushed on top of the call stack when function runs |

---

In summary, the **global execution context** is the default environment where the entire code runs, while **function execution contexts** are temporary environments created for running individual functions.
