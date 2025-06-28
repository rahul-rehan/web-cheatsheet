## 1. What are compound assignment operators in JavaScript? Provide examples.

Compound assignment operators combine a basic operation with assignment. Instead of writing `x = x + y`, you can use `x += y`.

**Examples:**

```javascript
let x = 5;

x += 3;  // same as x = x + 3;  // x becomes 8
x -= 2;  // same as x = x - 2;  // x becomes 6
x *= 4;  // same as x = x * 4;  // x becomes 24
x /= 6;  // same as x = x / 6;  // x becomes 4
x %= 3;  // same as x = x % 3;  // x becomes 1
```
## 2. What is the difference between `x = x + y` and `x += y`?

Both expressions achieve the same result, but `x += y` is more concise and preferred in idiomatic JavaScript code.

- `x = x + y`: Explicitly adds `y` to `x` and reassigns it.
- `x += y`: Does the same, but is syntactic sugar that improves readability and reduces redundancy.

## 3. How does the bitwise assignment operator `&=` work?

The `&=` operator performs a bitwise AND operation between the left and right operands and assigns the result to the left operand.

**Example:**

```javascript
let a = 6;    // binary: 110
let b = 3;    // binary: 011

a &= b;       // a = a & b → 110 & 011 = 010 → 2

console.log(a);  // Output: 2
```

## 4. Can assignment operators be chained in JavaScript? Example?

Yes, assignment operators can be chained because assignment expressions return the assigned value.

**Example:**

```javascript
let a, b, c;
a = b = c = 5;
console.log(a, b, c);  // Output: 5 5 5
```

In this example, `c` is assigned 5, then `b` gets the value of `c` (which is 5), and finally `a` gets the value of `b` (5).
## 5. What will be the result of: `let a = 1; a += (a *= 2);`?

Let's break down the expression step-by-step:

```javascript
let a = 1;
a += (a *= 2);
````
- `a *= 2` means `a = a * 2`, so `a` becomes `2`.
- The expression becomes: `a += 2` (because `a *= 2` evaluated to `2`).
- Now, `a += 2` means `a = a + 2`, so `a = 2 + 2 = 4`.

Final value of `a` is `4`.

```javascript
console.log(a);  // Output: 4
```