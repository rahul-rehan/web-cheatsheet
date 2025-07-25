## 1. Can `const` be used with objects and arrays? Can their contents be modified?

- Yes, `const` can be used to declare **objects** and **arrays**.
- The variable binding itself cannot be reassigned to a different object or array.
- However, **the contents of the object or array can be modified** (e.g., properties or elements can be changed, added, or removed).

## 2. What happens if you try to reassign a new object to a `const` variable?

- Attempting to reassign a new value (object, array, or any other type) to a `const` variable results in a **TypeError**.
- This is because `const` variables are read-only references after initialization.

```js
const arr = [1, 2, 3];
arr.push(4); // Allowed: modifying contents
console.log(arr); // [1, 2, 3, 4]

arr = [5, 6]; // TypeError: Assignment to constant variable
```
## 3. When should you prefer `const` over `let` or `var`?

- Prefer `const` by default to declare variables whose **bindings should not change**.
- Use `const` to make your code **more predictable and safer** by preventing accidental reassignment.
- Use `let` only when you expect the variable to be **reassigned later**.
- Avoid `var` in modern JavaScript due to its function scope and hoisting issues; prefer `let` and `const` instead.

## 4. Can you use `Object.freeze()` with `const` objects? What does it do?

- Yes, you can use `Object.freeze()` on objects declared with `const` (or `let`).
- `Object.freeze()` **prevents modification** of the object's properties: you cannot add, delete, or change existing properties.
- It **makes the object immutable**, but only shallowly (nested objects are not frozen).
- `const` prevents reassignment of the variable binding, while `Object.freeze()` prevents modification of the object itself.

```js
const obj = { name: "Alice" };
Object.freeze(obj);

obj.name = "Bob"; // Fails silently in non-strict mode or throws error in strict mode
console.log(obj.name); // "Alice"
```

## Best Practices and Comparison
## 1. Why is `var` generally discouraged in modern JavaScript?

- `var` is function-scoped, not block-scoped, which can lead to unexpected behaviors.
- Variables declared with `var` are hoisted and initialized with `undefined`, which can cause confusing bugs.
- Lack of block scope means `var` can leak outside loops or conditionals unintentionally.
- Modern JavaScript prefers `let` and `const` for clearer, more predictable scoping rules.

## 2. When is it appropriate to use `let` instead of `const`?

- Use `let` when you expect the variable's value to be **reassigned or updated** later.
- Examples: counters in loops, variables whose values depend on conditional logic or need to change over time.
- If the value will never change after assignment, prefer `const` for safety.

## 3. What are some common bugs caused by improper use of `var`?

- **Variable hoisting issues:** accessing a `var` variable before declaration yields `undefined` instead of an error.
- **Scope leakage:** variables declared inside blocks (like loops or `if` statements) leak to the outer function or global scope.
- **Accidental overwrites:** re-declaring the same `var` variable multiple times silently overwrites previous values.
- **Loop closures:** using `var` in loops can cause closures to capture the same variable instance, leading to unexpected behavior in callbacks.

```js
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100); // Logs 3, 3, 3 instead of 0,1,2
}
```
## 4. What is the preferred variable declaration keyword in modern JavaScript, and why?

- The preferred keywords are **`const`** and **`let`**.
- **`const`** is preferred by default because it signals that the variable should not be reassigned, helping prevent bugs.
- **`let`** is used when reassignment is necessary.
- Both `let` and `const` are block-scoped, reducing the risk of accidental variable leakage and making code behavior more predictable.
- `var` is generally avoided due to its function-scoping and hoisting behavior which can lead to confusing bugs.

## 5. Provide an example where using `var` leads to unexpected behavior compared to `let` or `const`.

```js
function example() {
  for (var i = 0; i < 3; i++) {
    setTimeout(() => console.log(i), 100);
  }
}

example(); 
// Output after 100ms:
// 3
// 3
// 3

// Explanation: `var` is function-scoped, so the same `i` is shared in all closures.
// By the time the timeouts run, the loop has completed and `i` is 3.

function exampleLet() {
  for (let i = 0; i < 3; i++) {
    setTimeout(() => console.log(i), 100);
  }
}

exampleLet();
// Output after 100ms:
// 0
// 1
// 2

// Explanation: `let` is block-scoped, so each iteration gets its own `i` binding.
```

## Advanced Scenarios
##  1. Can `let` and `const` declarations exist in the global scope?

- Yes, `let` and `const` can be declared in the global scope.
- However, unlike `var`, they **do not** create properties on the global object (`window` in browsers).
- They are scoped to the global lexical environment but are **not accessible** as `window` properties.

## 2. Are `var`, `let`, and `const` added as properties on the `window` or global object?

- **`var`** declarations in the global scope **are added** as properties on the global object (`window` in browsers).
- **`let`** and **`const`** declarations in the global scope **are NOT added** as properties on the global object.
  
Example:

```js
var a = 1;
let b = 2;
const c = 3;

console.log(window.a); // 1
console.log(window.b); // undefined
console.log(window.c); // undefined
```
## 3. What is block scope shadowing with `let` or `const`? Provide an example.

- Block scope shadowing happens when a variable declared inside a block (using `let` or `const`) has the same name as a variable declared outside that block.
- The inner variable **shadows** or hides the outer variable **only within the block** where it is declared.
- This means inside the block, references to that variable name use the inner variable, while outside the block the outer variable remains accessible.

**Example:**

```js
let x = 10;

{
  let x = 20;  // This 'x' shadows the outer 'x' inside this block
  console.log(x); // Output: 20
}

console.log(x); // Output: 10 (outer 'x' is unaffected)
```
- The inner `x` is a different variable limited to the block scope, so it does not affect the outer `x`.