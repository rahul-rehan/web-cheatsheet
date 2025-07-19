## 1. How Do You Access the Name of a Function?

You can access a function's name using the `.name` property.

#### Example:
```javascript
function greet() {
  return 'Hello';
}
console.log(greet.name); // Output: "greet"
```
## 2. What Does the `length` Property of a Function Represent?

The `.length` property of a function indicates the number of formal parameters the function expects (i.e., the number of named arguments defined in the function signature).

#### Example:
```javascript
function multiply(x, y, z) {
  return x * y * z;
}

console.log(multiply.length); // Output: 3
```
## 3. How Can You Access the Body or Source of a Function?

You can access the source code (body) of a function as a string using the `.toString()` method on the function object.

#### Example:
```javascript
function greet(name) {
  return `Hello, ${name}!`;
}

console.log(greet.toString());
/*
Output:
function greet(name) {
  return `Hello, ${name}!`;
}
*/
```
## 4. Can functions have properties assigned to them like objects? Provide an example.

Yes, in JavaScript, functions are objects and can have properties assigned to them.

**Example:**
```javascript
function sayHello() {
  console.log("Hello!");
}

sayHello.customProperty = "I am a property on a function";
console.log(sayHello.customProperty); // Output: I am a property on a function
```
## 5. What is the difference between a regular function and a constructor function?

- **Regular Function:** Called normally to execute code and optionally return a value.
- **Constructor Function:** Called with the `new` keyword to create and initialize a new object.
  
**Key differences:**

- Constructor functions are invoked with `new`.
- Inside a constructor, `this` refers to the newly created object.
- Constructor functions return the new object by default (unless explicitly returning another object).
- By convention, constructor functions have names starting with an uppercase letter.

## 6. How can you determine if a function is a generator function?

- Generator functions are declared with an asterisk (`function*`).
- You can detect a generator function by checking its constructor name:

```javascript
function* genFunc() {
  yield 1;
}

console.log(genFunc.constructor.name); // "GeneratorFunction"
```
- Or by using `Object.prototype.toString`:

```javascript
console.log(Object.prototype.toString.call(genFunc)); // "[object GeneratorFunction]"
```