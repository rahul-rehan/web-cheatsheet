# Primitive Data Types

## 1. What are primitive data types in JavaScript?

Primitive data types are the most basic data types in JavaScript. They represent **single values** and are **immutable**, meaning their value cannot be changed once created. Operations on primitive types produce new values rather than modifying the original value.

---

## 2. List all the primitive data types available in JavaScript.

JavaScript has **7 primitive data types**:

- `string` — represents textual data
- `number` — represents both integer and floating-point numbers
- `bigint` — represents integers with arbitrary precision
- `boolean` — represents logical true or false
- `undefined` — a variable that has been declared but not assigned a value
- `null` — represents the intentional absence of any object value
- `symbol` — represents a unique and immutable identifier

---

## 3. How is a string defined in JavaScript? Give examples.

- A **string** in JavaScript is a sequence of characters used to represent text.
- Strings can be defined using **single quotes (' ')**, **double quotes (" ")**, or **backticks (` `)**.

**Examples:**
```javascript
let singleQuote = 'Hello';
let doubleQuote = "World";
let backticks = `Hello World`;
```

## 4. What are template literals and how are they different from regular strings?

- **Template literals** are string literals enclosed in backticks (`` ` ``) that allow for **embedded expressions**, **multi-line strings**, and **string interpolation**.
- Unlike regular strings (single or double quotes), template literals support **variable interpolation** using `${expression}` syntax.

**Example:**
```javascript
let name = 'Alice';
let greeting = `Hello, ${name}!`;  // Template literal with interpolation

console.log(greeting); // Outputs: Hello, Alice!

// Multi-line string example
let multiLine = `This is line 1
This is line 2`;
console.log(multiLine);
```
Difference:
Regular strings require concatenation for variables and do not support multi-line strings without escape characters, whereas template literals make it easier and more readable.

## 5. How is a number represented in JavaScript? What are some common numeric operations?

- In JavaScript, **numbers** are represented using the **64-bit floating point format (IEEE 754)**, which means all numbers (both integers and decimals) are stored as floating-point values.
- Numeric operations include:
  - Arithmetic: `+`, `-`, `*`, `/`, `%` (modulus)
  - Increment/decrement: `++`, `--`
  - Exponentiation: `**`
  - Comparison: `<`, `>`, `<=`, `>=`, `===`, `!==`

**Example:**
```javascript
let x = 10;
let y = 3;

console.log(x + y);  // 13
console.log(x - y);  // 7
console.log(x * y);  // 30
console.log(x / y);  // 3.3333333333333335
console.log(x % y);  // 1
console.log(x ** y); // 1000
```
## 6. What is the difference between number and bigint in JavaScript?

- **`number`** type can safely represent integers between **-(2^53 - 1)** and **2^53 - 1** due to floating point precision limits.
- **`bigint`** is a newer primitive type that can represent **integers of arbitrary size** beyond the safe integer limits of `number`.
- `number` can represent decimals and floating point values, whereas `bigint` only represents whole integers.

---

## 7. When should you use bigint instead of number?

- Use `bigint` when you need to work with **very large integers** that exceed the safe integer range of `number` (`Number.MAX_SAFE_INTEGER`).
- Useful in applications like cryptography, large financial calculations, or working with precise integer arithmetic beyond `number` limits.

---

## 8. How do you create a bigint in JavaScript? Give an example.

- You can create a bigint by appending an **`n`** to the end of an integer literal or by using the `BigInt()` constructor.

**Examples:**
```javascript
const bigIntLiteral = 123456789012345678901234567890n;
const bigIntConstructor = BigInt("123456789012345678901234567890");

console.log(bigIntLiteral);      // 123456789012345678901234567890n
console.log(bigIntConstructor);  // 123456789012345678901234567890n
```

## 9. What is boolean data type? What are the possible values it can hold?

- The **boolean** data type in JavaScript represents a logical entity and can hold **only two possible values**:
  - `true`
  - `false`
- Booleans are commonly used in conditional statements and logical operations.

---

## 10. How do non-boolean values behave in boolean contexts (truthy/falsy)?

- In JavaScript, values that are **not explicitly boolean** are often evaluated in boolean contexts (e.g., conditions in `if` statements).
- These values are classified as either **truthy** or **falsy**:
  - **Truthy:** Values that evaluate to `true` in boolean contexts (e.g., non-empty strings, non-zero numbers, objects, arrays).
  - **Falsy:** Values that evaluate to `false` in boolean contexts. The falsy values are:
    - `false`
    - `0`
    - `-0`
    - `0n` (BigInt zero)
    - `""` (empty string)
    - `null`
    - `undefined`
    - `NaN`

---

## 11. What is undefined in JavaScript? How is it typically encountered?

- `undefined` is a primitive value that indicates a variable has been declared but **has not been assigned a value**.
- It is also the default return value of functions that do not explicitly return anything.
- It can appear when accessing properties or array elements that do not exist.

**Example:**
```javascript
let a;
console.log(a);        // undefined

function foo() {}
console.log(foo());    // undefined

let obj = {};
console.log(obj.prop); // undefined
```
## 12. What is the difference between undefined and null?

| Aspect         | `undefined`                                   | `null`                                     |
| -------------- | --------------------------------------------- | ------------------------------------------ |
| Meaning        | Variable declared but not assigned a value    | Represents intentional absence of a value  |
| Type           | Type is `"undefined"`                          | Type is `"object"` (historical quirk)      |
| Usage          | Usually set by JavaScript automatically       | Usually set by programmer to indicate "no value" |
| Equality       | `undefined == null` is `true`, but `undefined === null` is `false` |

**Summary:**  
`undefined` means a variable is uninitialized, while `null` is used to explicitly indicate "no value."

## 13. What is the type of null according to typeof operator? Why is it considered a historical bug?

- According to the `typeof` operator, the type of `null` is `"object"`.
- This is considered a **historical bug** in JavaScript that dates back to its first implementation.
- Originally, values were stored as a type tag and a value; the tag for objects was `0`.
- Since `null` was represented as the null pointer (`0x00`), `typeof null` incorrectly returned `"object"`.
- Despite being recognized as a bug, it was never fixed to maintain backward compatibility.

---

## 14. What is symbol in JavaScript? Why was it introduced?

- A **Symbol** is a primitive data type introduced in ES6.
- It represents a **unique and immutable identifier**.
- Symbols were introduced to allow the creation of unique property keys that avoid name collisions, especially useful for adding properties to objects without affecting or being affected by other code.

---

## 15. How do you create and use symbol values in JavaScript?

- You create a symbol using the `Symbol()` function.
- Symbols can optionally have a description (a string) for debugging purposes.
- Symbols are often used as **property keys** in objects.

**Example:**
```javascript
const sym1 = Symbol('id');
const sym2 = Symbol('id');

const obj = {};
obj[sym1] = 'value1';
obj[sym2] = 'value2';

console.log(obj[sym1]); // 'value1'
console.log(obj[sym2]); // 'value2'
```

## 16. Can two symbols with the same description be equal? Why or why not?

- **No**, two symbols created with the same description are **not equal**.
- Each call to `Symbol()` creates a **unique and distinct symbol**, regardless of the description.
- The description is only for debugging and does not affect symbol identity.

**Example:**
```javascript
const symA = Symbol('desc');
const symB = Symbol('desc');

console.log(symA === symB); // false
```
## 17. How do you use symbol to create private properties in objects?

- Symbols can be used as **keys for object properties** to create properties that are not easily accessible or enumerable.
- Since each symbol is unique, it helps create **private-like properties** that won’t conflict with other property names or show up in normal enumeration (e.g., `for...in` loops or `Object.keys()`).

**Example:**
```javascript
const _privateProp = Symbol('private');

const obj = {
  [_privateProp]: 'secret',
  publicProp: 'visible'
};

console.log(obj.publicProp);        // 'visible'
console.log(obj[_privateProp]);     // 'secret'

// The symbol-keyed property does not show up in normal enumeration
for (let key in obj) {
  console.log(key);  // only logs 'publicProp'
}

console.log(Object.keys(obj));       // ['publicProp']
console.log(Object.getOwnPropertySymbols(obj)); // [Symbol(private)]
```

## 18. What is the output of `typeof undefined`, `typeof null`, and `typeof Symbol()`?

| Expression           | Output                      |
|----------------------|-----------------------------|
| `typeof undefined`    | `"undefined"`               |
| `typeof null`         | `"object"` (historical bug)|
| `typeof Symbol()`     | `"symbol"`                  |

---

## 19. How are JavaScript primitive types different from reference types (objects)?

- **Primitive types** (string, number, bigint, boolean, undefined, null, symbol) store **actual values** directly.
- **Reference types** (objects, arrays, functions) store **references (pointers)** to the location in memory where the data is held.
- Primitives are immutable, whereas objects are mutable.
- When assigning or passing primitives, a **copy of the value** is used.
- When assigning or passing objects, a **reference to the object** is used.

---

## 20. Are primitive values mutable or immutable in JavaScript?

- Primitive values are **immutable**, meaning once a primitive value is created, it **cannot be changed**.
- Operations on primitives produce new values rather than modifying the original.

**Example:**
```javascript
let str = "hello";
str.toUpperCase();
console.log(str);  // "hello" — original string remains unchanged
```
