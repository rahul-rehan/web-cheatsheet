# JavaScript Functions in Variables

## 1. How can you store a function in a variable in JavaScript?

In JavaScript, functions are first-class objects, which means you can assign them to variables just like any other value. Here's how you can store a function in a variable:

```javascript
const greet = function() {
    console.log("Hello, world!");
};
```
You can then call the function using the variable name:

```javascript
greet(); // Output: Hello, world!
```
## 2. What is the difference between a named function and a function expression stored in a variable?

There are two main ways to define functions in JavaScript: **function declarations** (named functions) and **function expressions** (often stored in variables).

### Named Function (Function Declaration):

```javascript
function sayHello() {
    console.log("Hello!");
}
```
- Hoisted to the top of the scope — can be called before its definition.

- Has a fixed name (`sayHello` in this case).
### Function Expression:
```javascript
const sayHi = function() {
    console.log("Hi!");
};
```
- Not hoisted — cannot be used before the declaration.

- Typically anonymous, though you can name them internally.

- Assigned to a variable and called using the variable name.
## 3. Can you overwrite a function stored in a variable?

Yes, in JavaScript, you can overwrite (or reassign) a function that is stored in a variable. This is possible because functions are treated as values, and variables that hold functions can be reassigned just like any other variable (as long as they're declared with `let` or `var`).

#### Example:

```javascript
let greet = function() {
    console.log("Hello!");
};

greet(); // Output: Hello!

// Overwriting the function with a new one
greet = function() {
    console.log("Hi there!");
};

greet(); // Output: Hi there!
```
⚠️ Note: If the function is stored in a variable declared with `const`, you cannot overwrite it.

```javascript
const greet = function() {
    console.log("Hello!");
};

greet = function() { // ❌ This will throw an error
    console.log("Hi!");
};
```
In summary, you can overwrite a function stored in a variable, as long as that variable is not declared with const.

## 4. What happens if you assign a function to another variable? Will both variables refer to the same function?

Yes, when you assign a function to another variable, both variables will **refer to the same function** in memory. Functions in JavaScript are objects, so assigning them simply copies the reference — not the function itself.

#### Example:

```javascript
function original() {
    console.log("This is the original function.");
}

const alias = original;

original(); // Output: This is the original function.
alias();    // Output: This is the original function.
```
In this example, both `original` and `alias` point to the same function, so invoking either one produces the same result.
## 5. Provide an example where a function is assigned to a variable and then invoked.

In JavaScript, you can assign a function to a variable and then use that variable to invoke the function. This is a common pattern in functional programming.

#### Example:

```javascript
const greet = function(name) {
    console.log(`Hello, ${name}!`);
};

const sayHello = greet;

sayHello("Alice"); // Output: Hello, Alice!
greet("Bob");      // Output: Hello, Bob!
```
In this case, `sayHello` is assigned the same function as `greet`, and both can be used to invoke it.
## 6. How does storing functions in variables help in creating callbacks or dynamic behavior?

Storing functions in variables allows you to treat them like any other data — you can **pass them as arguments**, **store them in data structures**, or **reassign them** at runtime. This flexibility is key to enabling **callbacks**, **event-driven programming**, and **dynamic behavior** in JavaScript.

#### Benefits:

- ✅ **Callbacks**: You can pass functions to other functions to be executed later.
- 🔁 **Dynamic behavior**: You can change the logic of your program at runtime by swapping functions.
- 🔧 **Higher-order functions**: Functions that return or accept other functions as arguments promote clean, modular code.

#### Example: Using a function as a callback

```javascript
function processUserInput(callback) {
    const name = "Charlie";
    callback(name);
}

const sayHi = function(name) {
    console.log(`Hi, ${name}!`);
};

processUserInput(sayHi); // Output: Hi, Charlie!
```
Here, `sayHi` is passed as a callback to `processUserInput`, demonstrating how function variables enable flexible and dynamic code.