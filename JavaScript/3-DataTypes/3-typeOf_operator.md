# typeof Operator in JavaScript

## 1. What is the purpose of the typeof operator in JavaScript?
The `typeof` operator is used to determine the data type of a given operand (variable or value). It returns a string indicating the type of the operand.

---

## 2. What are the possible return values of the typeof operator?

The `typeof` operator can return the following string values:

| Return Value   | Description                   |
|----------------|-------------------------------|
| `"undefined"`  | The variable is undefined      |
| `"boolean"`    | The value is a boolean         |
| `"number"`     | The value is a number          |
| `"bigint"`     | The value is a BigInt          |
| `"string"`     | The value is a string          |
| `"symbol"`     | The value is a Symbol          |
| `"function"`   | The value is a function        |
| `"object"`     | The value is an object or null |

---

## 3. What is the result of `typeof null` and why is it considered a bug?

- `typeof null` returns `"object"`.

- This is considered a **historical bug** in JavaScript because `null` is a primitive value representing "no value" or "empty," but `typeof` treats it as an object due to legacy reasons in the language's implementation.

- Despite being recognized as a bug, this behavior is maintained for backward compatibility.

## 4. What is the output of `typeof NaN`?

- The output is `"number"`.
- Although `NaN` means "Not-a-Number," it is still classified as a number type in JavaScript.

---

## 5. What is the output of `typeof undefined`?

- The output is `"undefined"`.
- This indicates that the variable or value is undefined.

---

## 6. What is the result of `typeof function() {}` and why?

- The output is `"function"`.
- Functions in JavaScript are a special kind of object, and `typeof` treats them distinctly by returning `"function"`.

---

## 7. How does `typeof` behave with primitive vs reference types?

- For **primitive types** (`string`, `number`, `boolean`, `bigint`, `symbol`, `undefined`), `typeof` returns their respective type names as strings.

- For **reference types** (objects, arrays, functions):
  - Returns `"object"` for most objects and arrays.
  - Returns `"function"` specifically for functions.

- Note: Arrays are technically objects, so `typeof []` returns `"object"`.

## 8. What is the difference between `typeof []` and `typeof {}`?

- Both `typeof []` and `typeof {}` return `"object"`.
- This is because in JavaScript, arrays are a specialized type of object.
- So `typeof` does **not** distinguish between plain objects and arrays.

---

## 9. Can `typeof` be used to accurately detect arrays? Why or why not?

- No, `typeof` **cannot** accurately detect arrays.
- Since `typeof` returns `"object"` for both arrays and regular objects, it can't differentiate between them.

---

## 10. What are the limitations of the `typeof` operator?

- It cannot distinguish between:
  - Arrays and objects (both return `"object"`)
  - `null` and objects (`typeof null` returns `"object"`, which is a known bug)
- It cannot detect more specific object types or complex data structures.
- It does not tell you if a value is `NaN` (which is a number).

---

## 11. How would you check if a variable is an array if `typeof` returns `"object"`?

- Use `Array.isArray()` method which returns `true` if the value is an array, else `false`.

```javascript
const arr = [1, 2, 3];
console.log(Array.isArray(arr));  // true

const obj = { a: 1 };
console.log(Array.isArray(obj));  // false
```