## 1. Can a function return another function in JavaScript? Provide an example.

Yes, in JavaScript, functions can return other functions. This is a powerful feature that enables function factories, currying, and more.

#### Example:

```javascript
function greet(message) {
    return function(name) {
        console.log(`${message}, ${name}!`);
    };
}

const sayHello = greet("Hello");
sayHello("Alice"); // Output: Hello, Alice!

const sayHi = greet("Hi");
sayHi("Bob");      // Output: Hi, Bob!
```
## 2. What is a closure, and how is it related to returning functions?

A **closure** is a feature in JavaScript where an inner function **remembers and has access to variables** from its **outer (enclosing) function’s scope**, even after the outer function has finished executing.

When a function returns another function, the returned function **retains access to the variables** of the outer function — this is a closure.

#### Example demonstrating closure:

```javascript
function makeCounter() {
    let count = 0;
    return function() {
        count++;
        console.log(count);
    };
}

const counter = makeCounter();
counter(); // Output: 1
counter(); // Output: 2
```
Even though `makeCounter` has finished execution, the returned function still has access to the count variable due to closure.
## 3. How can you use a function that returns a function to create reusable logic?

Functions that return functions can be used to **generate specialized functions** with customized behavior, allowing you to **reuse generic logic with different parameters**.

#### Example: Creating a multiplier function factory

```javascript
function multiplier(factor) {
    return function(number) {
        return number * factor;
    };
}

const double = multiplier(2);
const triple = multiplier(3);

console.log(double(5)); // Output: 10
console.log(triple(5)); // Output: 15
```
Here, `multiplier` returns a new function that multiplies the input by the given factor. This pattern creates reusable and configurable logic easily.

## 4. Provide an example of a function returning another function that uses the outer function’s parameters.

When a function returns another function, the inner function can **access the outer function’s parameters** thanks to closures.

#### Example:

```javascript
function greeting(message) {
    return function(name) {
        console.log(`${message}, ${name}!`);
    };
}

const sayHello = greeting("Hello");
sayHello("Alice"); // Output: Hello, Alice!

const sayGoodbye = greeting("Goodbye");
sayGoodbye("Bob"); // Output: Goodbye, Bob!
```
In this example, the inner function uses the `message` parameter from the outer function.
## 5. How does returning a function help in function currying or partial application?

**Function currying** is the technique of transforming a function with multiple arguments into a sequence of functions, each taking a single argument. Returning functions allows you to **fix some arguments (partial application)** and return a new function waiting for the remaining arguments.

#### Example of currying:

```javascript
function multiply(a) {
    return function(b) {
        return a * b;
    };
}

const multiplyBy2 = multiply(2);
console.log(multiplyBy2(5)); // Output: 10

const multiplyBy3 = multiply(3);
console.log(multiplyBy3(5)); // Output: 15
```
Benefits:
- Breaks down functions into smaller, reusable pieces.

- Allows presetting some arguments, creating specialized versions of a function.

- Improves code readability and reusability.

Partial application is a practical use of currying where you fix some arguments ahead of time.