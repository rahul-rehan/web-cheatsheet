## 1. What is the difference between Error, TypeError, ReferenceError, and SyntaxError?

- **Error**  
  The generic error type from which other error types inherit. Used for general exceptions.

- **TypeError**  
  Thrown when a value is not of the expected type, e.g., calling a non-function or accessing a property on `undefined`.

- **ReferenceError**  
  Occurs when trying to access a variable that is not declared or is out of scope.

- **SyntaxError**  
  Raised when the code contains invalid syntax and cannot be parsed.

## 2. What are the standard properties of the Error object?

- **name**: The name of the error type (e.g., `"TypeError"`).
- **message**: A human-readable description of the error.
- **stack**: A string providing the stack trace where the error occurred (useful for debugging).

## 3. How do you create a custom error in JavaScript?

```js
class CustomError extends Error {
  constructor(message) {
    super(message);          // Call the parent constructor with the message
    this.name = "CustomError"; // Set a custom error name
  }
}

// Usage
throw new CustomError("Something went wrong!");
```
## 4. How can you check the type of error in the catch block?

You can check the type of error by using the `instanceof` operator inside the `catch` block:

```js
try {
  // code that may throw an error
} catch (error) {
  if (error instanceof ReferenceError) {
    console.log("Caught a ReferenceError");
  } else if (error instanceof TypeError) {
    console.log("Caught a TypeError");
  } else {
    console.log("Caught some other error");
  }
}
```
## 5. Provide an example of a ReferenceError and explain why it occurs.

```js
try {
  console.log(nonExistentVariable); // ReferenceError: nonExistentVariable is not defined
} catch (error) {
  console.log(error.name);    // "ReferenceError"
  console.log(error.message); // "nonExistentVariable is not defined"
}
```
#### Explanation:
A `ReferenceError` occurs because `nonExistentVariable` is not declared or defined in the current scope. Accessing an undeclared variable causes this error to be thrown.
## 6. Example of a TypeError and Explanation

```js
try {
  let num = 42;
  num.toUpperCase(); // TypeError: num.toUpperCase is not a function
} catch (error) {
  console.log(error.name);    // "TypeError"
  console.log(error.message); // "num.toUpperCase is not a function"
}
```
#### Explanation:
A `TypeError` occurs here because `toUpperCase()` is a method that exists on strings, but `num` is a number. Trying to call a string method on a number results in a `TypeError`.

## Best Practices
## 1. Should you catch all errors in production applications? Why or why not?

- **Not always recommended to catch all errors blindly.**  
- Some errors should propagate so that the application can fail fast and alert developers.  
- Catching errors selectively allows graceful recovery where possible, improving user experience.  
- Over-catching can mask critical bugs, making them harder to detect and fix.

## 2. How can you log errors effectively for debugging?

- Log error **name**, **message**, and **stack trace** for full context.  
- Use centralized logging services or error tracking tools (e.g., Sentry, LogRocket).  
- Include relevant metadata (user ID, environment, timestamp) to reproduce issues.  
- Avoid logging sensitive information to protect user privacy.

## 3. What are the risks of swallowing errors without handling them?

- Errors become **silent failures**, making bugs difficult to detect.  
- Can cause inconsistent application state or unpredictable behavior.  
- Users may face broken features without feedback or recovery options.  
- Increases technical debt and maintenance complexity.
## 4. Why is it bad practice to use empty catch blocks?

- **Silences errors without any handling or logging.**  
- Makes debugging difficult because errors are hidden.  
- Can cause unexpected behavior since failures are ignored.  
- Leads to fragile code and harder maintenance.

## 5. When is it appropriate to re-throw an error in a catch block?

- When you want to perform some action (e.g., logging) but still let the error propagate.  
- To allow higher-level code to handle the error appropriately.  
- When partial handling is done but the error should not be considered resolved.  
- Helps maintain proper error flow and visibility.
