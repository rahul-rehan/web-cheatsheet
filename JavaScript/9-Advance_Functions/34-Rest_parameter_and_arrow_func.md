## 1. Can arrow functions use rest parameters? Provide a basic example.

Yes, **arrow functions can use rest parameters** just like regular functions. This is the preferred way to handle multiple arguments in arrow functions because the `arguments` object is not available in them.

#### Example:
```javascript
const logAll = (...args) => {
  console.log(args);
};

logAll(1, 2, 3); // Output: [1, 2, 3]
```
## 2. Why is using rest parameters often preferred in arrow functions over `arguments`?

- Arrow functions **do not have their own `arguments` object**, so trying to use `arguments` inside an arrow function can lead to unexpected behavior.
- Rest parameters provide a **clear, explicit, and modern** way to handle variable numbers of arguments.
- Rest parameters return a **true array**, allowing the use of array methods like `.map()`, `.filter()`, and `.reduce()` without conversion.
- They are more **readable and maintainable**, especially in functional programming styles.

## 3. Provide an example of an arrow function that calculates the sum of all its arguments using rest parameters

```javascript
const sum = (...numbers) => numbers.reduce((total, num) => total + num, 0);

console.log(sum(1, 2, 3, 4)); // Output: 10
console.log(sum());           // Output: 0
```
In this example:

- `...numbers` gathers all the passed arguments into an array.

- `reduce()` is used to sum all the elements.
## 4. Can you use destructuring in combination with rest parameters in arrow functions?

Yes, you can combine **destructuring** and **rest parameters** in arrow functions. This allows for flexible and readable parameter handling, especially when working with objects or arrays.

#### Example with object destructuring:
```javascript
const displayUser = ({ name, age, ...rest }) => {
  console.log(name);  // e.g., "Alice"
  console.log(age);   // e.g., 30
  console.log(rest);  // other properties
};

displayUser({ name: "Alice", age: 30, role: "admin", active: true });
````
#### Example with array destructuring:
```javascript
const logFirstAndRest = ([first, ...rest]) => {
  console.log(first); // e.g., 1
  console.log(rest);  // e.g., [2, 3, 4]
};

logFirstAndRest([1, 2, 3, 4]);
```
## 5. What happens if you try to use both named parameters and rest parameters in an arrow function?

You **can** use both named parameters and rest parameters in an arrow function, but the **rest parameter must always be the last parameter**.

#### ✅ Correct usage:
```javascript
const greetUsers = (greeting, ...names) => {
  console.log(greeting);
  console.log(names);
};

greetUsers("Hello", "Alice", "Bob");
// Output:
// Hello
// ["Alice", "Bob"]
```
#### ❌ Incorrect usage (SyntaxError):
```javascript
const invalid = (...args, extra) => {
  // SyntaxError: Rest parameter must be last formal parameter
};
```
If you try to place a rest parameter anywhere other than the end of the parameter list, JavaScript will throw a SyntaxError.