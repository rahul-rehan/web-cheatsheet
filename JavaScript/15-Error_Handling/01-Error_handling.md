## 1. What is an error in JavaScript?

An **error in JavaScript** is an object that represents a problem that occurs during the execution of code. Errors can be:
- **Syntax errors**: Detected during parsing.
- **Runtime errors**: Occur while the code is running (e.g., accessing an undefined variable).
JavaScript provides built-in mechanisms to throw, catch, and handle these errors using `try...catch`.

## 2. What are the different types of built-in error objects in JavaScript?

JavaScript provides several built-in error types, each representing a different kind of error:

- **Error**: The generic error object.
- **SyntaxError**: Invalid syntax (e.g., `eval('foo bar')`).
- **ReferenceError**: Reference to an undefined variable (e.g., `console.log(x)` when `x` is not declared).
- **TypeError**: A value is not of the expected type (e.g., calling a non-function).
- **RangeError**: A value is out of range (e.g., `new Array(-1)`).
- **URIError**: Malformed URI passed to functions like `decodeURI()`.
- **EvalError**: Issues with the `eval()` function (rarely used today).
- **AggregateError**: Used with `Promise.any()` to represent multiple errors.

## 3. How do you throw an error manually in JavaScript?

You can throw an error using the `throw` statement. This can be a string, number, object, or an instance of an `Error`.

```js
// Throwing a custom error
throw new Error("Something went wrong");

// Throwing a specific error type
throw new TypeError("Invalid type provided");

// Throwing a string (not recommended)
throw "Manual error";
```
Manually thrown errors can be caught and handled using `try...catch` blocks.
## 4. What is the syntax for a try...catch block?

The `try...catch` block is used to handle exceptions in JavaScript. It allows you to write error-handling code separately from the normal logic.

```js
try {
  // Code that might throw an error
} catch (error) {
  // Code to handle the error
}
```
You can also optionally include a finally block:

```js
try {
  // risky operation
} catch (error) {
  // handle error
} finally {
  // cleanup code (executes regardless of error)
}
```
## 5. What happens if an error occurs inside the try block?

- JavaScript immediately stops executing the `try` block.
- Control is passed to the `catch` block.
- The error is handled or logged in the `catch` block.
- If a `finally` block is present, it runs regardless of whether an error occurred or not.
- If no error occurs, the `catch` block is skipped.

## 6. Can the catch block access the error object? What properties does it usually have?

Yes, the `catch` block receives an **error object** which typically has the following properties:

- `name`: The type of the error (e.g., `"TypeError"`).
- `message`: A descriptive error message.
- `stack`: A stack trace showing where the error occurred (may be environment-dependent).

Example:

```js
try {
  throw new TypeError("Invalid input");
} catch (error) {
  console.log(error.name);    // "TypeError"
  console.log(error.message); // "Invalid input"
  console.log(error.stack);   // Stack trace (if available)
}
```
## 7. What is the purpose of the finally block in try...catch...finally?

- The `finally` block contains code that **always executes** after the `try` and `catch` blocks.
- It is used to perform **cleanup actions**, such as closing files, releasing resources, or resetting states.
- Ensures certain code runs **regardless of whether an error occurred or not**.

## 8. Will the finally block execute even if there is a return or throw?

- Yes, the `finally` block **executes even if**:
  - The `try` or `catch` block contains a `return` statement.
  - An error is thrown and not caught.
- However, if the `finally` block itself contains a `return` or throws an error, it can override the original return or error.

Example:

```js
function example() {
  try {
    return "from try";
  } finally {
    console.log("finally runs");
  }
}

console.log(example()); 
// Output:
// finally runs
// "from try"
```