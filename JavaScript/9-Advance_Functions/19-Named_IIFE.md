## 1. What is a named IIFE?

- A **named IIFE** is an Immediately Invoked Function Expression that has a **name (identifier)** assigned to the function.
- The name can be used inside the function body for recursion or debugging purposes.
- The function is still executed immediately after it is defined.

## 2. How is a named IIFE different from an anonymous IIFE?

| Aspect                | Named IIFE                           | Anonymous IIFE                   |
|-----------------------|------------------------------------|---------------------------------|
| Function has a name    | Yes (e.g., `function foo() {...}`) | No (e.g., `function() {...}`)    |
| Recursion possible     | Yes, can call itself by name       | No, cannot refer to itself by name |
| Debugging              | Easier to identify in stack traces | Less descriptive in debugging    |

## 3. Can you recursively call a named IIFE? Provide an example.

- Yes, a named IIFE can recursively call itself using its function name.

#### Example:

```javascript
(function factorial(n) {
  if (n <= 1) {
    console.log(1);
    return 1;
  }
  console.log(n);
  return n * factorial(n - 1);
})(5);
```
#### Output:
```
5
4
3
2
1
```
## 4. Does the function name inside a named IIFE leak into the outer scope?

- **No**, the function name inside a named IIFE is **local to the function itself**.
- It **does not pollute or leak into the outer/global scope**.
- The name is only accessible **inside the IIFE**, which allows for recursion or referencing itself.

## 5. In which scenarios is using a named IIFE preferable?

- When you need to **perform recursion** within the IIFE.
- For better **debugging**, since named functions show up with their name in stack traces.
- When you want clearer **code readability**, making it easier to understand the function's purpose.
- To **avoid anonymous functions**, which can be harder to identify in debugging tools.

## 6. Provide an example of a named IIFE used for recursion.

```javascript
(function countdown(n) {
  if (n <= 0) {
    console.log("Done!");
    return;
  }
  console.log(n);
  countdown(n - 1); // Recursive call using the function name
})(3);

/* Output:
3
2
1
Done!
*/
```
