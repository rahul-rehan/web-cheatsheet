## 1. What is the difference between function parameters and arguments?

- **Parameters** are the variable names listed in a function’s definition. They act as placeholders for the values the function will receive.

- **Arguments** are the actual values passed to the function when it is called.

#### Example:

```javascript
function greet(name) {  // 'name' is the parameter
  console.log(`Hello, ${name}!`);
}

greet("Alice");         // "Alice" is the argument
```
## 2. How are default parameters defined in a function?

Default parameters are defined by assigning a default value to parameters in the function declaration. If no argument is provided for that parameter, the default value is used.

#### Example:

```javascript
function greet(name = "Guest") {
  console.log(`Hello, ${name}!`);
}

greet();         // Output: Hello, Guest!
greet("Alice");  // Output: Hello, Alice!
```
## 3. What happens if an argument is not passed to a required parameter?

If an argument is not passed to a parameter without a default value, the parameter’s value becomes `undefined`. This may cause unexpected behavior if the function relies on that parameter.

#### Example:

```javascript
function greet(name) {
  console.log(`Hello, ${name}!`);
}

greet();  // Output: Hello, undefined!
```
## 4. How do rest parameters work? Provide an example.

Rest parameters allow a function to accept **an indefinite number of arguments** as an array. They are defined by prefixing the last parameter with three dots `...`.

#### Example:

```javascript
function sum(...numbers) {
  return numbers.reduce((total, num) => total + num, 0);
}

console.log(sum(1, 2, 3, 4));  // Output: 10
```
Here, `numbers` is an array containing all the arguments passed to the function.
## 5. Can you use destructuring in function parameters?

Yes, you can use **destructuring** directly in function parameters to unpack values from arrays or properties from objects.

#### Example with object destructuring:

```javascript
function greet({ name, age }) {
  console.log(`Hello, ${name}. You are ${age} years old.`);
}

greet({ name: "Alice", age: 25 });  // Output: Hello, Alice. You are 25 years old.
```
Example with array destructuring:
```javascript
function printCoordinates([x, y]) {
  console.log(`X: ${x}, Y: ${y}`);
}

printCoordinates([10, 20]);  // Output: X: 10, Y: 20
```