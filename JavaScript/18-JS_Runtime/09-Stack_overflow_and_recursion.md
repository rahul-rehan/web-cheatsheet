## 1. What is a stack overflow error in JavaScript?

- A **stack overflow error** occurs when the **call stack exceeds its maximum size limit**.
- This happens when too many execution contexts are pushed onto the call stack without being popped off.
- The JavaScript engine throws a **`RangeError: Maximum call stack size exceeded`** when this limit is breached.
- It typically indicates runaway recursion or excessively deep nested function calls.

## 2. How can infinite recursion lead to a stack overflow?

- **Infinite recursion** occurs when a function keeps calling itself **without a proper base case or termination condition**.
- Each recursive call creates a new execution context that is pushed onto the call stack.
- Since the function never stops calling itself, the call stack keeps growing until it hits the maximum size.
- At that point, a **stack overflow error is thrown**, crashing the program or halting execution.

## 3. How can you prevent stack overflow in recursive functions?

- **Ensure a proper base case:** Always define a clear and reachable base case to stop recursion.
- **Limit recursion depth:** Avoid excessively deep recursive calls by restructuring the problem or limiting input size.
- **Use iterative approaches:** Convert recursion to iteration using loops when possible.
- **Optimize recursion:** Apply techniques like **memoization** to reduce unnecessary recursive calls.
- **Use tail recursion:** Write recursive functions in a way that the recursive call is the last operation (enables tail call optimization).

## 4. What is tail call optimization and how does it relate to the call stack?

- **Tail Call Optimization (TCO)** is a feature where the JavaScript engine **reuses the current function’s stack frame** for a function call if it is the last operation in the function (a **tail call**).
- This means the call stack does **not grow** with each recursive call in tail-recursive functions.
- TCO helps **prevent stack overflow** by keeping the call stack size constant during deep or infinite tail recursion.
- Note: Not all JavaScript engines currently support TCO, so its availability may vary.

---

**Summary:**

| Question                         | Answer                                                                                  |
|---------------------------------|-----------------------------------------------------------------------------------------|
| How to prevent stack overflow?  | Use base cases, limit recursion depth, convert to iteration, memoize, and write tail-recursive functions. |
| What is tail call optimization? | Reuse current stack frame for last call in function to avoid growing call stack, preventing overflow. |
