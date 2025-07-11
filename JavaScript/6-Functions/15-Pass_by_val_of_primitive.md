## 1. What are primitive data types in JavaScript?

Primitive data types in JavaScript are the most basic types of data. They include:

1. **Number** – e.g., `42`, `3.14`
2. **String** – e.g., `"Hello"`, `'World'`
3. **Boolean** – `true` or `false`
4. **undefined** – a variable that has been declared but not assigned a value
5. **null** – represents an intentional absence of any value
6. **Symbol** – a unique and immutable value used as an object property key
7. **BigInt** – used for large integers beyond the safe limit for numbers

These types are **immutable** and **passed by value** in JavaScript.


## 2. What happens when you pass a number, string, or boolean to a function?

When you pass a **primitive value** (like a number, string, or boolean) to a function:

- The function receives a **copy** of that value.
- Any changes made to the parameter inside the function **do not affect** the original value outside the function.


## 3. Will changes to a primitive parameter inside a function reflect outside the function? Why or why not?

**No**, changes to a primitive parameter **will not reflect** outside the function.

#### Reason:

JavaScript passes primitive values **by value**, meaning the function gets a **copy** of the original variable. Any modification to the parameter inside the function affects only the **local copy**, not the original variable.

#### Example:

```javascript
function changeValue(x) {
  x = x + 10;
  console.log("Inside function:", x);
}

let num = 5;
changeValue(num);
console.log("Outside function:", num); // Output: 5
```
In this example, `num` remains `5` outside the function, because only a copy of it was modified inside the function.
## 4. Provide an example where a primitive value is passed to a function and explain the behavior.

#### Example:

```javascript
function updateValue(x) {
  x = x * 2;
  console.log("Inside function:", x);
}

let num = 10;
updateValue(num);
console.log("Outside function:", num); // Output: 10
```
**Explanation:**
- The variable num holds a primitive number value (10).

- When passed to updateValue(), a copy of the value is given to the parameter x.

- Modifying x inside the function does not affect the original variable num.

- Therefore, num remains unchanged outside the function.

This demonstrates that primitive values are passed by value, not by reference.
## 5. Is `null` or `undefined` treated as a primitive when passed to a function?

Yes, both `null` and `undefined` are **primitive data types** in JavaScript.

When passed to a function:

- They are treated like all other primitives.
- A **copy** of the value is passed to the function.
- Modifying the parameter inside the function **does not** affect the original variable.

---

#### Example:

```javascript
function checkValue(x) {
  x = "changed";
  console.log("Inside function:", x);
}

let val = null;
checkValue(val);
console.log("Outside function:", val); // Output: null
```
**Explanation:**
- The variable `val` is initially `null`.

- A copy of `val` is passed into the `checkValue` function.

- The function modifies `x`, but this does not change the original variable `val` outside the function.

This confirms that both `null` and `undefined` are primitives and are passed by value in JavaScript.