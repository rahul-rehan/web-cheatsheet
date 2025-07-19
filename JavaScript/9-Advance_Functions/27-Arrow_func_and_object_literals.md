## 1. What happens when you try to return an object literal directly from an arrow function?

- If you try to return an object literal **directly without parentheses** in an arrow function with an implicit return, JavaScript interprets the curly braces `{}` as the start of a function body block instead of an object.
- This leads to **unexpected behavior** or syntax errors because the function body expects statements, not an object literal.

## 2. Why must object literals be wrapped in parentheses when returned directly?

- Wrapping the object literal in **parentheses `()`** tells JavaScript to treat the curly braces as an **object literal** instead of a function block.
- This enables implicit return of the object in concise arrow functions.

## 3. Provide an example of an arrow function that returns an object literal.

```javascript
const createUser = (name, age) => ({ 
  name: name, 
  age: age 
});

console.log(createUser("Alice", 30)); 
// Output: { name: "Alice", age: 30 }
```
- Here, the parentheses around the object literal allow the arrow function to return the object directly.
## 4. What syntax error might you encounter if you forget parentheses around the object?

- If you forget to wrap an object literal in parentheses when returning it directly from an arrow function with implicit return, JavaScript treats the `{}` as a **function body block**, not an object.
- This can cause a **SyntaxError** or unexpected behavior, such as:

```plaintext
SyntaxError: Unexpected token ':'
```
- Because JavaScript expects statements inside the function body but encounters object property syntax instead.

#### Example of erroneous code:
```javascript
const getUser = () => { name: "Bob" }; // Incorrect — treated as block, not object
```
- This will not return the object and may throw an error.