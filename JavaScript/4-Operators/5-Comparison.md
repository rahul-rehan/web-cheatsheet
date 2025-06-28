## 1. What is the difference between `==` and `===` in JavaScript?

- `==` is the **loose equality operator** that compares two values for equality after performing type coercion if needed.
- `===` is the **strict equality operator** that compares both value and type without performing any type conversion.

**Example:**

```javascript
0 == "0";   // true (because "0" is coerced to number 0)
0 === "0";  // false (different types: number vs string)
```
## 2. What will be the result of 0 == false and why?

```javascript
0 == false;  // true
```
**Explanation:**

The `==` operator converts `false` to `0` (number) before comparison.

So it becomes `0 == 0`, which is `true`.
## 3. Explain the result of `"5" > 2` in JavaScript.

```javascript
"5" > 2;  // true
```
**Explanation:**

When comparing a string and a number with relational operators (`>`, `<`, etc.), JavaScript converts the string to a number.

`"5"` is converted to `5`, so the comparison is `5 > 2`, which is `true`.
## 4. Why does `null == undefined` return true but `null === undefined` return false?

- `==` is the loose equality operator that performs type coercion.
- According to JavaScript rules, `null` and `undefined` are considered equal with `==`.
- `===` is the strict equality operator that checks both value and type without coercion.
- Since `null` and `undefined` are different types, `null === undefined` returns `false`.

---

## 5. What is the result of `NaN == NaN` and why?

- `NaN == NaN` returns `false`.
- In JavaScript, `NaN` is not equal to anything, including itself.
- This behavior follows the IEEE floating-point standard for "Not-a-Number".

---

## 6. How does JavaScript compare strings using `<` or `>` operators?

- JavaScript compares strings lexicographically, based on Unicode code points.
- Comparison is done character by character from left to right.
- For example, `"apple" < "banana"` is `true` because `"a"` (code 97) is less than `"b"` (code 98).
- Uppercase letters have different Unicode values than lowercase, so `"Z" < "a"` is `true`.
