## 1. What are the different arithmetic operators available in JavaScript?

JavaScript supports the following arithmetic operators:

- `+` : Addition
- `-` : Subtraction
- `*` : Multiplication
- `/` : Division
- `%` : Modulus (remainder)
- `**` : Exponentiation
- `++` : Increment
- `--` : Decrement

---

## 2. What will be the output of `3 + 2 * 4` in JavaScript and why?

**Output:** `11`

**Explanation:**

JavaScript follows operator precedence. Multiplication (`*`) has a higher precedence than addition (`+`), so:

2 * 4 = 8

3 + 8 = 11


## 3. How does JavaScript handle arithmetic with different data types, e.g., `5 + "3"`?

**Output:** `"53"`

**Explanation:**

When adding a number and a string, JavaScript converts the number to a string and performs **string concatenation**, not arithmetic addition.

---

## 4. What will be the result of `10 / 0` in JavaScript?

**Output:** `Infinity`

**Explanation:**

In JavaScript, dividing a number by zero does **not** throw an error. Instead, it returns the special value `Infinity`.
## 5. Is `++x` different from `x++`? Explain with an example.

Yes, they are different:

- `++x` is the **pre-increment** operator: it increments `x` **before** returning the value.
- `x++` is the **post-increment** operator: it returns the value of `x` **before** incrementing it.

**Example:**

```javascript
let x = 5;
console.log(++x); // 6 (x is incremented first, then logged)
console.log(x);   // 6

x = 5;
console.log(x++); // 5 (x is logged first, then incremented)
console.log(x);   // 6
```
## 6. What will be the output of the expression: `2 + 3 * 4 / 2 - 1`?

**Output:** `7`

**Explanation:**

JavaScript follows the standard operator precedence:

1. Multiplication and division are evaluated first (from left to right),
2. Then addition and subtraction (from left to right).

Step-by-step:

```text
3 * 4 = 12  
12 / 2 = 6  
2 + 6 - 1 = 7
```
## 7. How do arithmetic operators behave with `null` or `undefined` values?

- **`null`** is treated as **`0`** in numeric operations.
- **`undefined`** is treated as **`NaN`** (Not-a-Number).

#### Examples:

```javascript
console.log(5 + null);      // 5       (null is converted to 0)
console.log(5 + undefined); // NaN     (undefined becomes NaN)
console.log(null * 3);      // 0
console.log(undefined - 1); // NaN
```