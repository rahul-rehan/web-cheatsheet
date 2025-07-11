## 1. What are default parameters in JavaScript?

**Default parameters** allow you to assign default values to function parameters. If no argument is provided for a parameter when the function is called, the default value is used instead of `undefined`.

## 2. How do you set a default value for a parameter in a function declaration?

You can set a default value by using the assignment operator (`=`) in the function declaration:

```javascript
function greet(name = "Guest") {
  console.log("Hello, " + name);
}
```
If no argument is passed for `name`, it defaults to `"Guest"`.
## 3. Provide an example of a function using default parameters

```javascript
function calculateArea(width = 1, height = 1) {
  return width * height;
}

console.log(calculateArea(5, 10)); // Output: 50
console.log(calculateArea(7));     // Output: 7 (height defaults to 1)
console.log(calculateArea());      // Output: 1 (both default values used)
```
This example demonstrates how default parameter values ensure the function still works even if some or all arguments are missing.
## 4. What is the behavior if `undefined` is explicitly passed to a parameter with a default value?

- If `undefined` is passed as an argument, the parameter will use its **default value**.
- This behavior is intentional and allows selective use of default values.

#### Example:

```javascript
function greet(name = "Guest") {
  console.log("Hello, " + name);
}

greet(undefined); // Output: Hello, Guest
```
## 5. What happens if a `null` value is passed to a parameter with a default?

- If `null` is explicitly passed to a parameter with a default value, the default **is not used**.
- `null` is treated as a **deliberate value**, not a missing one.
- Therefore, the function will use `null` as the parameter’s value.

#### Example:

```javascript
function greet(name = "Guest") {
  console.log("Hello, " + name);
}

greet(null); // Output: Hello, null
```
Unlike `undefined`, `null` does not trigger the default value.
## 6. Can you use an expression or another function call as a default value?

- **Yes**, JavaScript allows you to use any valid expression as a default value for a parameter.
- This includes calling another function or using calculations.

#### Example:

```javascript
function getDefaultName() {
  return "Anonymous";
}

function greet(name = getDefaultName()) {
  console.log("Hello, " + name);
}

greet(); // Output: Hello, Anonymous
```
This makes default parameters flexible and dynamic, allowing complex logic or computed values to be used as defaults.
## 7. Are default parameters evaluated at function definition or invocation time?

- **Default parameters are evaluated at the time the function is invoked**, not when the function is defined.
- This means the default value expression is **re-evaluated every time** the function is called, allowing it to reflect dynamic values.

#### Example:

```javascript
let counter = 0;

function increment(value = ++counter) {
  console.log(value);
}

increment(); // Output: 1
increment(); // Output: 2
increment(); // Output: 3
```
The default value of `value` is evaluated at each invocation, so it changes based on `counter`.
## 8. Can default parameters depend on earlier parameters? Provide an example.

- **Yes**, default parameters in JavaScript can depend on parameters that come before them in the function declaration.
- This allows for dynamic default values based on previously passed arguments.

#### Example:

```javascript
function multiply(a, b = a * 2) {
  return a * b;
}

console.log(multiply(3));    // Output: 18 (b = 3 * 2)
console.log(multiply(3, 4)); // Output: 12 (b = 4)
```
In this example, `b` is given a default value based on `a`. If `b` is not provided, it defaults to `a * 2`.
## 9. What is the difference between setting default values manually using `if` and using ES6 default parameters?

#### Using `if` statement (pre-ES6):
- Default values are set **inside** the function body.
- You typically check if the argument is `undefined` and assign a default value manually.

```javascript
function greet(name) {
  if (name === undefined) {
    name = "Guest";
  }
  console.log("Hello, " + name);
}
```
#### Using ES6 default parameters:
- Default values are assigned in the function signature.

- More concise and readable.

- Automatically applies when the argument is undefined.

```javascript
function greet(name = "Guest") {
  console.log("Hello, " + name);
}
```
ES6 default parameters are cleaner, safer, and work better with functions expecting complex default behavior (like expressions or functions).
## 10. How do default parameters affect the `length` property of a function?

- The `length` property of a function returns the number of parameters **before the first parameter that has a default value**.

#### Examples:

```javascript
function fn1(a, b, c) {}               // fn1.length === 3
function fn2(a, b = 2, c) {}           // fn2.length === 1
function fn3(a = 1, b = 2, c = 3) {}   // fn3.length === 0
```
- In `fn2`, since `b` has a default value, parameters after `b` are not counted in the length.

- In `fn3`, all parameters have default values, so length is `0`.

This behavior helps identify how many arguments a function expects before defaults kick in.