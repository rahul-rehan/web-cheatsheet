## 1. Write a recursive function to calculate the factorial of a number.

```javascript
function factorial(n) {
  if (n === 0) return 1;           // Base case
  return n * factorial(n - 1);     // Recursive case
}
```
## 2. Write a recursive function to compute the nth Fibonacci number.

```javascript
function fibonacci(n) {
  if (n === 0) return 0;            // Base case 1
  if (n === 1) return 1;            // Base case 2
  return fibonacci(n - 1) + fibonacci(n - 2);  // Recursive case
}
```
This function calculates the Fibonacci number at position `n` by summing the two previous Fibonacci numbers recursively, with base cases defined for `n = 0 and n = 1`.
## 3. How do you recursively reverse a string or an array?

#### Recursive reversal of a string:

```javascript
function reverseString(str) {
  if (str === "") return "";        // Base case: empty string
  return reverseString(str.slice(1)) + str[0];  // Recursive case
}
```
#### Recursive reversal of an array:
```javascript
function reverseArray(arr) {
  if (arr.length === 0) return [];  // Base case: empty array
  return reverseArray(arr.slice(1)).concat(arr[0]);  // Recursive case
}
```
**Explanation:**

- Both functions work by removing the first element and recursively reversing the rest.

- The base case returns an empty string or array.

- Then the removed element is added back at the end, effectively reversing the order.
## 4. Write a recursive function to sum the elements of an array.

```javascript
function sumArray(arr) {
  if (arr.length === 0) return 0;          // Base case: empty array
  return arr[0] + sumArray(arr.slice(1));  // Recursive case: first element + sum of rest
}
```
## 5. Write a recursive function to calculate the power of a number (e.g., `pow(x, n)`).

```javascript
function pow(x, n) {
  if (n === 0) return 1;                   // Base case: any number to the power 0 is 1
  return x * pow(x, n - 1);                // Recursive case: x multiplied by x^(n-1)
}
```
This function calculates `x` raised to the power `n` by recursively multiplying `x` with the result of `pow(x, n-1)` until `n` reaches 0.