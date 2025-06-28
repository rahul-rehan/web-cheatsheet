## 1. What does the remainder (%) operator do in JavaScript?

The `%` operator returns the remainder left over when one number is divided by another. It is not the modulo operator and follows the sign of the dividend (the left-hand operand).

---

## 2. What is the output of `10 % 3` and why?

```javascript
console.log(10 % 3);  // 1
```
**Explanation:**

`3` goes into `10` three times (3 × 3 = 9), leaving a remainder of `1`.
## 3. What is the result of a negative dividend in remainder operation, e.g., `-13 % 5`?

```javascript
console.log(-13 % 5);  // -3
```
**Explanation:**  
The remainder keeps the **sign of the dividend** (`-13`), so the result is `-3`.
## 4. What happens when we use the remainder operator with floating-point numbers?

It still returns the remainder after division, but with potential precision issues due to floating-point arithmetic.

```javascript
console.log(5.5 % 2);  // 1.5
```
## 5. How can the remainder operator be used to check if a number is even?

Use `% 2` and check if the result is `0`:

```javascript
function isEven(n) {
  return n % 2 === 0;
}

console.log(isEven(4));  // true
console.log(isEven(7));  // false
