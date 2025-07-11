## 1. How can a function be passed as an argument to another function in JavaScript?

In JavaScript, functions are **first-class citizens**, which means they can be passed as arguments to other functions just like any other value.

#### Syntax:

```javascript
function greet(name) {
    console.log(`Hello, ${name}!`);
}

function processUserInput(callback) {
    const userName = "Alice";
    callback(userName);
}

processUserInput(greet); // Output: Hello, Alice!
```
Explanation:
- `greet` is passed without parentheses, which means its reference (not the result of calling it) is passed to `processUserInput`.

- Inside `processUserInput`, the `callback` is executed with a value.
## 2. What is a callback function? Give a simple example.

A **callback function** is a function that is **passed as an argument** to another function and is **invoked inside** that outer function to complete some kind of action or routine.

#### Example:

```javascript
function displayMessage(message) {
    console.log(message);
}

function getMessage(callback) {
    const message = "This is a callback example.";
    callback(message);
}

getMessage(displayMessage); // Output: This is a callback example.
```
Explanation:
- `displayMessage` is the callback function.

- It is passed to `getMessage` as an argument.

- Inside `getMessage`, the `callback` is executed with a `message` value.

Callback functions are commonly used in asynchronous operations, event handlers, and array methods like `map`, `filter`, and `forEach`.
## 3. What is the difference between passing a function reference vs. calling it inside the argument?

There is an important distinction between **passing a function reference** and **calling a function immediately** when used as an argument in JavaScript.

| Concept               | Function Reference                  | Function Call                     |
|-----------------------|--------------------------------------|------------------------------------|
| **Syntax**            | `doSomething(callback)`              | `doSomething(callback())`          |
| **What is passed**    | The function itself (reference)      | The return value of the function   |
| **When it's called**  | Later, inside the outer function     | Immediately, before the outer function executes |
| **Use case**          | Useful for callbacks and deferred execution | Useful when you need the result right away |

#### Example:

```javascript
function sayHello() {
    return "Hello!";
}

function greet(message) {
    console.log(message);
}

// Passing function reference
greet(sayHello);     // Output: function sayHello() { return "Hello!"; }

// Calling the function inside the argument
greet(sayHello());   // Output: Hello!
```
Explanation:
- `greet(sayHello)` passes the function itself. It doesn’t execute `sayHello`; it just passes the reference.

- `greet(sayHello())` calls `sayHello` immediately, and the return value` ("Hello!")` is passed to `greet`.

✅ Use function reference when you want the function to be called later (e.g., in callbacks).

⚠️ Use function call only when you want the function to execute immediately and pass its result.

## 4. How are anonymous functions commonly used in function parameters (e.g., in `setTimeout`, `map`, etc.)?

Anonymous functions are **functions without a name**, and they are often used **inline** when passing as arguments to other functions — especially for short, one-time-use logic.

### Examples:

- **Using in `setTimeout`:**

    ```javascript
    setTimeout(function() {
        console.log("This runs after 1 second");
    }, 1000);
    ```
- **Using in map:**

    ```javascript
    const numbers = [1, 2, 3];
    const squares = numbers.map(function(num) {
        return num * num;
    });

    console.log(squares); // Output: [1, 4, 9]
    ```
Why use anonymous functions?

- Reduces the need to declare separate named functions.

- Keeps code compact and localized.

- Great for single-use logic or callbacks.
## 5. Why is passing a function useful in asynchronous operations or event handling?

Passing a function allows for **deferred execution**, which is essential in asynchronous and event-driven programming.

#### Use Cases:

- **Asynchronous operations:** You can pass a function to be executed later, for example, after a delay or when data is ready (like after fetching from an API).
- **Event handling:** You can define behavior that runs when a user interacts with the interface, such as clicking a button.

### Examples:

- **Asynchronous (setTimeout):**

    ```javascript
    setTimeout(() => {
        console.log("Executed after delay");
    }, 2000);
    ```
- Event handling:

    ```javascript
    document.getElementById("myButton").addEventListener("click", function() {
        alert("Button clicked!");
    });
    ```
Benefits:
- Organizes code flow to be responsive and non-blocking.

- Avoids freezing the main thread during long-running or delayed tasks.

- Allows behavior to be defined dynamically and executed when needed.
## 6. What is the purpose of higher-order functions?

A **higher-order function** is a function that **accepts other functions as arguments**, **returns a function**, or **both**.

#### Purpose:

- Enables **functional programming** techniques.
- Promotes **code reusability** and **abstraction**.
- Helps in building **flexible and composable** logic.

#### Example:

```javascript
function repeatAction(action, times) {
    for (let i = 0; i < times; i++) {
        action();
    }
}

repeatAction(() => console.log("Repeat this!"), 3);
// Output:
// Repeat this!
// Repeat this!
// Repeat this!
```
Common higher-order functions:
- `map`, `filter`, `reduce`, `forEach`

- Custom utilities that accept or return functions

Higher-order functions are fundamental to JavaScript’s functional style and are widely used in libraries like Lodash, React, and many asynchronous workflows.