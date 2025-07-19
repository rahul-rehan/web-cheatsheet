## 1. What is the `typeof` a function in JavaScript?

In JavaScript, when you use the `typeof` operator on a function, it returns `"function"`.

```javascript
function greet() {}
console.log(typeof greet); // "function"
```
This is a special case in the `typeof` operator, which normally returns `"object"` for most complex types.

## 2. How is a function represented internally in JavaScript?

In JavaScript, functions are **first-class objects**. This means:

- They are instances of the built-in `Function` constructor.
- They can be assigned to variables, passed as arguments, and returned from other functions.
- Internally, they behave like regular objects but with callable behavior.

Example:

```javascript
function sayHello() {
  console.log("Hello");
}

console.log(typeof sayHello);           // "function"
console.log(sayHello instanceof Object); // true
console.log(sayHello instanceof Function); // true
```
So even though `typeof` returns `"function"`, it is still an object under the hood.
## 3. What is the Difference Between a Function Declaration and a Function Expression?

#### 1. **Function Declaration**
A function declaration defines a named function using the `function` keyword.

```javascript
function sayHello() {
  console.log("Hello!");
}
```
- **Hoisting:** Function declarations are hoisted entirely. You can call the function before its definition.

- **Name:** Always has a name (identifier).
#### 2. **Function Expression**
A function expression assigns a function (named or anonymous) to a variable.

```javascript
const sayHi = function() {
  console.log("Hi!");
};
```
- **Hoisting:** Function expressions are not hoisted like declarations. You cannot call the function before the definition.

- **Name:** Can be anonymous or named.

- **Common Use:** Often used in callbacks or assigned to variables/objects.
#### Example Comparison
```javascript
// Function Declaration
greet(); // ✅ Works
function greet() {
  console.log("Hello from declaration!");
}

// Function Expression
greetAgain(); // ❌ Error: Cannot access 'greetAgain' before initialization
const greetAgain = function() {
  console.log("Hello from expression!");
};
```

## 4. What is the return type of `typeof functionName` in JavaScript?

The `typeof` operator returns a string indicating the type of the unevaluated operand.

When used on a function:

```javascript
function greet() {
  console.log("Hello");
}

console.log(typeof greet); // "function"
```
- The return value of `typeof functionName` is `"function" `if the identifier refers to a function.

- Despite functions being objects internally, JavaScript defines a distinct `"function"` type for clarity and convenience.
## 5. Are All Callable Entities in JavaScript of Type `"function"`?

Yes, in JavaScript, all callable entities (i.e., entities you can invoke using `()`) have a `typeof` equal to `"function"`.

```javascript
function example() {}
console.log(typeof example); // "function"
```
Even classes, which are syntactic sugar over constructor functions, return `"function"` with `typeof`:

```javascript
class MyClass {}
console.log(typeof MyClass); // "function"
```
## 6. How Does JavaScript Treat Functions as First-Class Objects?

JavaScript treats functions as **first-class citizens**, which means:

- **They can be assigned to variables**:
  ```javascript
  const greet = function(name) {
    return `Hello, ${name}`;
  };
  ```
- **They can be passed as arguments to other functions:**

    ```javascript
    function execute(callback) {
    callback();
    }

    execute(() => console.log("Executed!"));
    ```
- **They can be returned from other functions:**

    ```javascript
    function createMultiplier(x) {
    return function(y) {
        return x * y;
    };
    }

    const double = createMultiplier(2);
    console.log(double(5)); // 10
    ```
- **They can have properties and methods like regular objects:**

    ```javascript
    function sayHi() {}
    sayHi.language = "English";

    console.log(sayHi.language); // "English"
    ```
## 7. Is a JavaScript Function Also an Object? How Can You Prove It?
Yes, every function in JavaScript is also an object. This can be proven by the fact that:

- Functions can have properties.

- You can use Object.keys() or Object.getOwnPropertyNames() on them.

- typeof a function returns "function", but it behaves like an object.

```javascript
function hello() {}
hello.customProperty = "I am a function";

console.log(hello.customProperty); // "I am a function"
console.log(typeof hello);         // "function"
console.log(hello instanceof Object); // true
```
Functions in JavaScript are callable objects with additional internal methods like `[[Call]]` and optionally `[[Construct]]`.
## 8. What Properties Can Be Found on a Function Object in JavaScript?

JavaScript functions are objects, and as such, they have various built-in properties:

- **`name`**: The name of the function.
  ```javascript
  function greet() {}
  console.log(greet.name); // "greet"
  ```
- **`length`**: The number of expected arguments.

    ```javascript
    function sum(a, b) {}
    console.log(sum.length); // 2
    ```
- **`prototype`**: Used when the function is intended to be used as a constructor.

    ```javascript
    function Person() {}
    console.log(typeof Person.prototype); // "object"
    ```
- **`caller`** (non-standard / deprecated): Refers to the function that invoked the current one.

- **`arguments`** (deprecated): The arguments passed to the function. Use rest parameters instead.

- **`toString()`**: Returns the source code of the function as a string.

    ```javascript
    function sayHi() { return "hi"; }
    console.log(sayHi.toString());
    ```
## 9. What Is the Significance of the Function Constructor in JavaScript?
The Function constructor allows you to create new functions dynamically at runtime from strings:

```javascript
const sum = new Function('a', 'b', 'return a + b');
console.log(sum(2, 3)); // 5
```
#### Significance:
- Dynamic Code Execution: Functions can be created on-the-fly.

- Less Common in Practice: It's similar to `eval()` and can lead to security and performance issues.

- Use with Caution: It's generally discouraged in favor of declared functions or arrow functions due to readability, maintainability, and security concerns.
## 10. Can You Create a Function Using the `Function` Constructor? Show an Example.

Yes, JavaScript provides a global `Function` constructor that allows you to create a function dynamically from a string of code.

#### Example:
```javascript
const add = new Function('a', 'b', 'return a + b');
console.log(add(2, 3)); // Output: 5
```
- The `Function` constructor takes parameter names as individual string arguments, followed by the function body as the last argument.

- This is similar to using `eval()` and should be used cautiously, as it can introduce security risks and performance issues.
## 11. What Does function instanceof Function Return? Why?
It returns true.

Example:
```javascript
Copy
Edit
function greet() {
  return 'Hello';
}

console.log(greet instanceof Function); // true
```
#### Why?
- In JavaScript, every function is an instance of the built-in `Function` object.

- Functions are treated as first-class objects and are created using the `Function` constructor internally.

- Therefore, any function (including arrow functions, function declarations, and function expressions) satisfies `instanceof Function`.