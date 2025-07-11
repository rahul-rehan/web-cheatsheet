## 1. What are the advantages and disadvantages of recursion compared to iteration?

#### Advantages of Recursion:
- **Simpler and clearer code** for problems that have a natural recursive structure (e.g., tree traversals, divide-and-conquer algorithms).
- **Easier to implement** complex problems like backtracking, graph traversals, and combinatorial problems.
- **Less code** is often needed, making the logic easier to understand at a high level.

#### Disadvantages of Recursion:
- **Higher memory usage** due to function call stack overhead.
- Risk of **stack overflow** if recursion depth is too large.
- Sometimes **slower performance** compared to iterative solutions.
- Can be harder to debug because of many nested calls.


## 2. Which problems are best suited for recursive solutions?

- Problems with **divide-and-conquer** approach (e.g., merge sort, quicksort).
- **Tree and graph traversals** (e.g., depth-first search).
- Problems involving **backtracking** (e.g., puzzles like Sudoku, N-Queens).
- Calculations based on **mathematical recurrence relations** (e.g., Fibonacci sequence).
- Any problem where the solution naturally breaks down into **smaller subproblems of the same type**.


## 3. Convert a recursive factorial function to an iterative one.

#### Recursive factorial:

```javascript
function factorialRecursive(n) {
  if (n === 0) return 1;
  return n * factorialRecursive(n - 1);
}
```
#### Iterative factorial:
```javascript
function factorialIterative(n) {
  let result = 1;
  for (let i = 1; i <= n; i++) {
    result *= i;
  }
  return result;
}
```
## 4. Compare performance of a recursive vs iterative Fibonacci function.

- **Recursive Fibonacci (naive):**

```javascript
function fibonacciRecursive(n) {
  if (n === 0) return 0;
  if (n === 1) return 1;
  return fibonacciRecursive(n - 1) + fibonacciRecursive(n - 2);
}
```
- **Performance:**

    - Has exponential time complexity: 𝑂(2𝑛).

    - Makes many redundant calculations (overlapping subproblems).

    - Causes a large number of recursive calls and high call stack usage.

    - Inefficient for large `n` and can lead to stack overflow.
- **Iterative Fibonacci:**

```javascript
function fibonacciIterative(n) {
  if (n === 0) return 0;
  let a = 0, b = 1;
  for (let i = 2; i <= n; i++) {
    const temp = a + b;
    a = b;
    b = temp;
  }
  return b;
}
```
- **Performance:**

    - Has linear time complexity:O(n).

    - Uses a simple loop without recursive overhead.

    - Much more efficient and avoids stack overflow.

    - Preferred for large n in practical applications.

## 5. When should you avoid recursion in JavaScript?

- When the recursion depth can become very **large**, risking a **stack overflow** error.
- If there is a more **efficient iterative solution** available.
- When **performance and memory usage** are critical concerns.
- If the JavaScript engine does **not support tail call optimization**, making deep recursion unsafe.
- When the recursive logic makes the code **hard to understand or maintain**.
- When debugging recursive functions becomes too complex due to many nested calls.

> In these cases, consider using iteration, memoization, or explicit data structures (like stacks) to avoid the pitfalls of recursion.
