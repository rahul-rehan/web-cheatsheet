## 1. What is the purpose of the unary + operator in JavaScript?

The unary `+` operator converts its operand to a number. It is often used to convert strings or other types into numeric values.

**Example:**
```javascript
console.log(+"42");    // 42 (number)
console.log(+true);    // 1
console.log(+"abc");   // NaN (cannot convert to number)
```
## 2. How does the unary - operator work on non-numeric values?

The unary `-` operator first converts the operand to a number (similar to unary `+`), then negates it.

**Examples:**

```javascript
console.log(-"5");      // -5 (string converted to number, then negated)
console.log(-true);     // -1 (true converted to 1, then negated)
console.log(-null);     // -0 (null converts to 0, negated is -0)
console.log(-"abc");    // NaN (cannot convert to number)
```
## 3. What is the output of `typeof "hello"` and why?

```javascript
typeof "hello";  // "string"
```
**Explanation:**

The `typeof` operator returns the data type of its operand as a string. Since `"hello"` is a string literal, `typeof` returns `"string"`.
## 4. What does the delete operator do? Can it delete variables declared with let or const?

- The `delete` operator removes a property from an object.
- It **cannot delete variables** declared with `let`, `const`, or `var`.
- It only works on object properties, not on standalone variables.
  
Example:

```javascript
const obj = { a: 1, b: 2 };
delete obj.a;       // true, property 'a' removed
console.log(obj);   // { b: 2 }

let x = 10;
delete x;           // false, cannot delete variable
console.log(x);     // 10
```
## 5. How does the typeof operator behave for null, NaN, undefined, and arrays?

| Value       | `typeof` Result | Explanation                                                                 |
|-------------|-----------------|-----------------------------------------------------------------------------|
| `null`      | `"object"`      | A historical JavaScript bug; `null` is a primitive but `typeof` returns `"object"`. |
| `NaN`       | `"number"`      | `NaN` is a special numeric value representing Not-a-Number.                 |
| `undefined` | `"undefined"`   | Represents an uninitialized or missing value.                               |
| `[]` (array)| `"object"`      | Arrays are objects in JavaScript; `typeof` does not distinguish arrays.     |

To accurately check for arrays, use:

```javascript
Array.isArray([]);
```
which returns `true`.