## 1. What is the syntax of a basic `for` loop in JavaScript?

```javascript
for (initialization; condition; increment) {
  // code to be executed repeatedly
}
```
- **initialization**: Sets the starting value, executed once before the loop starts.

- **condition**: Evaluated before each iteration; if `true`, the loop continues; if `false`, the loop stops.

- **increment**: Executes after each iteration, often used to update the loop counter.
## 2. What will happen if the `for` loop condition is omitted or always true?

- **If the condition is omitted**, it is treated as `true` by default, resulting in an **infinite loop** unless interrupted by a `break` or other control statement.

```javascript
for (let i = 0; ; i++) {
  console.log(i);
  if (i >= 5) break;  // prevents infinite loop
}
```
- If the condition is always true, the loop will also run infinitely unless you explicitly break out of it.
## 3. Can you use `break` and `continue` within a `for` loop? What’s the difference?

- **`break`**: Immediately exits the entire loop, skipping all remaining iterations.

- **`continue`**: Skips the current iteration and proceeds to the next iteration of the loop.

#### Example:

```javascript
for (let i = 0; i < 5; i++) {
  if (i === 2) continue;  // Skip when i is 2
  if (i === 4) break;     // Exit loop when i is 4
  console.log(i);
}
// Output: 0, 1, 3
```
## 4. How can you iterate over an array using a `for` loop?

You can use a `for` loop to iterate over an array by initializing the loop counter to 0, continuing while it’s less than the array length, and incrementing it on each iteration.

#### Example:
```javascript
const fruits = ["apple", "banana", "cherry"];

for (let i = 0; i < fruits.length; i++) {
  console.log(fruits[i]);
}
```
## 5. What happens if you modify the loop counter inside the loop body?

Modifying the loop counter inside the loop body can change the flow of the loop unexpectedly. It may cause the loop to:

- Skip elements
- Repeat elements
- Create infinite loops if the counter is changed improperly
## 6. How can you use a `for` loop in reverse (from high to low)?

To iterate in reverse, initialize the loop counter to the last index of the array (or highest number), continue while it is greater than or equal to 0, and decrement the counter each iteration.

#### Example:
```javascript
const fruits = ["apple", "banana", "cherry"];

for (let i = fruits.length - 1; i >= 0; i--) {
  console.log(fruits[i]);
}
```