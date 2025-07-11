## 1. What is recursion in JavaScript?

Recursion in JavaScript is a programming technique where a function **calls itself** either directly or indirectly in order to solve a problem. Recursive functions typically break a complex problem into smaller, more manageable sub-problems of the same type.


## 2. What are the two main components of a recursive function?

1. **Base Case**  
   The condition that stops the recursion by not making any further recursive calls. It prevents infinite recursion and eventually terminates the function.

2. **Recursive Case**  
   The part of the function where it calls itself with a modified argument, moving towards the base case.


## 3. How does a recursive function differ from an iterative one?

- **Recursive function** solves a problem by repeatedly calling itself, breaking the problem into smaller sub-problems, often relying on the function call stack to keep track of progress.

- **Iterative function** uses loops (like `for`, `while`) to repeat operations until a condition is met, managing state explicitly via variables.

**Differences:**

| Aspect            | Recursive Function                     | Iterative Function                |
|-------------------|--------------------------------------|---------------------------------|
| Uses              | Function calls itself                 | Loops (`for`, `while`, etc.)    |
| State management  | Implicit via call stack               | Explicit via variables          |
| Readability       | Can be more intuitive for divide-and-conquer problems | Sometimes more straightforward |
| Performance       | May cause stack overflow if too deep | Generally more memory efficient  |

---

#### Example of a recursive function (factorial):

```javascript
function factorial(n) {
  if (n === 0) return 1;       // Base case
  return n * factorial(n - 1); // Recursive case
}
```
## 4. What is a base case in recursion and why is it necessary?

A **base case** is a condition within a recursive function that stops the recursion by **not making any further recursive calls**. It defines the simplest, smallest instance of the problem that can be solved directly without further recursion.

**Why is it necessary?**

- It **prevents infinite recursion** and eventual stack overflow.
- It provides a **termination point** for the recursive calls.
- Ensures that the function can return a result instead of calling itself endlessly.


## 5. What happens if a recursive function does not have a base case?

If a recursive function does **not** have a base case:

- The recursion will continue **indefinitely** (or until the call stack limit is reached).
- This leads to a **stack overflow error**, crashing the program.
- The function will never return a result because there is no stopping condition.


## 6. Can all problems solved with recursion be solved using loops? Explain.

**Yes**, in theory, any problem that can be solved with recursion can also be solved using loops (iteration).

**Explanation:**

- Recursion and iteration are both techniques for repeating operations.
- Recursive calls can be simulated using loops and explicit data structures like **stacks** to keep track of state.
- Some problems (like tree traversals or backtracking) are naturally easier or more intuitive to implement recursively.
- Iterative solutions may be more efficient in terms of memory because they avoid the overhead of function calls and the call stack.

> However, recursion can sometimes lead to clearer and simpler code for problems that are naturally recursive.

---

#### Example:

- **Factorial** can be implemented recursively or iteratively.

Recursive:

```javascript
function factorial(n) {
  if (n === 0) return 1;
  return n * factorial(n - 1);
}
```
**Iterative:**

```javascript
function factorial(n) {
  let result = 1;
  for (let i = 1; i <= n; i++) {
    result *= i;
  }
  return result;
}
```