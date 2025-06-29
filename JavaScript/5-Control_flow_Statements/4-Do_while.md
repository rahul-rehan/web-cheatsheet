## 1. What is the difference between `while` and `do-while` loops?

- **`while` loop**:  
  The condition is checked **before** executing the loop body. If the condition is `false` initially, the loop body **does not execute** at all.

- **`do-while` loop**:  
  The loop body is executed **at least once** before the condition is checked. After the first execution, the loop continues running as long as the condition is `true`.

---

## 2. How many times will a `do-while` loop run if the condition is initially false?

A `do-while` loop will run **exactly once** if the condition is initially `false`, because the condition is checked **after** the first execution of the loop body.

---

## 3. What is an infinite loop? How can you accidentally create one using `while`?

- **Infinite loop**:  
  A loop that **never terminates** because its condition always evaluates to `true`.

- **Accidentally creating an infinite loop with `while`:**  
  If the condition in a `while` loop never becomes `false` (often due to missing or incorrect updates inside the loop), the loop will run forever.

#### Example of accidental infinite loop:
```javascript
let i = 0;
while (i < 5) {
  console.log(i);
  // Missing increment: i++ leads to infinite loop
}
```
In this example, since `i` is never incremented, the condition `i < 5` always remains `true`, causing an infinite loop.
## 4. How can you break out of a `while` loop based on user input or a condition?

You can use the `break` statement inside a `while` loop to exit the loop prematurely when a certain condition is met, such as specific user input or any other logical condition.

#### Example:
```javascript
let input;

while (true) {
  input = prompt("Enter 'exit' to quit:");
  if (input === "exit") {
    break;  // Exit the loop if user types 'exit'
  }
  console.log(`You entered: ${input}`);
}
console.log("Loop ended.");
```
## 5. Example of using a `do-while` loop to validate user input

A `do-while` loop ensures the user is prompted at least once and continues to prompt until valid input is received.

```javascript
let age;

do {
  age = prompt("Enter your age (must be a number greater than 0):");
  age = Number(age);
} while (isNaN(age) || age <= 0);

console.log(`Your age is ${age}`);
````
In this example, the loop will keep asking for the user's age until a valid positive number is entered.