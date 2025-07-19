## 1. What is the purpose of rest parameters in JavaScript?

Rest parameters allow a function to accept an **indefinite number of arguments** as an array. This is useful when you don’t know in advance how many arguments will be passed to the function. Rest parameters provide a clean and modern alternative to using the `arguments` object.

## 2. What is the syntax for using rest parameters in a function definition?

You use the `...` (three dots) syntax before the parameter name:

```javascript
function sum(...numbers) {
  return numbers.reduce((total, n) => total + n, 0);
}
```
In this example, `numbers` is an array that holds all arguments passed to the `sum` function.
## 3. How do rest parameters differ from the `arguments` object?

| Feature                 | Rest Parameters                             | `arguments` Object                          |
|-------------------------|---------------------------------------------|---------------------------------------------|
| **Type**                | Real array                                  | Array-like object (not a real array)        |
| **Declaration**         | Explicit (defined using `...`)              | Implicit (available in non-arrow functions) |
| **Availability in arrow functions** | ✅ Available                     | ❌ Not available                            |
| **Supports array methods** | ✅ Yes (e.g., `.map()`, `.filter()`)     | ❌ No (must be converted to an array first) |
| **Use case flexibility** | More modern and flexible                   | More limited and legacy-oriented            |

**Summary:**  
Rest parameters are explicitly declared, behave like real arrays, and are compatible with arrow functions and array methods. In contrast, the `arguments` object is implicit, not available in arrow functions, and lacks array method support.
## 4. Can a function have multiple rest parameters? Why or why not?

No, a function **cannot have more than one rest parameter**.  
This is because the rest parameter collects all **remaining arguments** into a single array, and allowing multiple rest parameters would create ambiguity about how to distribute the arguments.

Additionally, the rest parameter must always be the **last parameter** in the function definition.

## 5. What data type is the value collected by rest parameters?

Rest parameters collect arguments into a **real array**.  
This means the collected value is of type `Array`, and you can use all standard array methods on it (like `.map()`, `.filter()`, `.reduce()`, etc.).

## 6. Provide an example of a function that uses rest parameters to accept any number of arguments

```javascript
function multiplyAll(...numbers) {
  return numbers.reduce((product, num) => product * num, 1);
}

console.log(multiplyAll(2, 3));        // Output: 6
console.log(multiplyAll(1, 2, 3, 4));  // Output: 24
console.log(multiplyAll());            // Output: 1 (neutral value for multiplication)
```
n this example, `...numbers` gathers all passed arguments into an array, allowing the function to multiply any number of values.
## 7. In what position must the rest parameter appear in the parameter list?

The **rest parameter must appear at the end** of the function’s parameter list.

This is because it gathers all remaining arguments into a single array. Placing it anywhere else would create ambiguity in how arguments are assigned to parameters.

#### ✅ Correct usage:
```javascript
function example(a, b, ...rest) {
  console.log(a, b, rest);
}
```
#### ❌ Incorrect usage (SyntaxError):
```javascript
function example(...rest, a, b) {
  // SyntaxError: Rest parameter must be last formal parameter
}
```