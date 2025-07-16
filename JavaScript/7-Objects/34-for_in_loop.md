## 1. What is the purpose of the `for...in` loop in JavaScript?

The `for...in` loop is used to **iterate over the enumerable properties (keys)** of an object. It allows you to access each key in the object one at a time.

## 2. What does the `for...in` loop iterate over?

The `for...in` loop iterates over **enumerable property names (keys)** of an object. This includes both inherited and own properties, unless filtered using methods like `hasOwnProperty()`.

**Example:**
```javascript
const user = { name: "Alice", age: 25 };
for (let key in user) {
  console.log(key);        // "name", "age"
  console.log(user[key]);  // "Alice", 25
}
```
## 3. How is `for...in` different from `for`, `for...of`, and `forEach()`?

| Loop Type     | Iterates Over                | Use Case                                           |
|---------------|------------------------------|----------------------------------------------------|
| `for...in`    | Keys of an object (enumerable)| Iterating over object properties                   |
| `for...of`    | Values of iterable objects    | Iterating over arrays, strings, maps, sets, etc.   |
| `for`         | Numeric index or counter      | Custom iteration logic with index control          |
| `forEach()`   | Values of an array            | Array iteration using a callback function          |

#### Key Differences:
- `for...in` is used to **iterate over object keys**.
- `for...of` is used to **iterate over iterable values** like arrays, strings, and maps.
- `forEach()` is an **array method** that applies a callback to each element.
- `for` is a **traditional loop** best suited when index-based control or conditional iteration is required.
## 4. Provide an example of iterating over the properties of an object using `for...in`

```javascript
const user = {
  name: "John",
  age: 30,
  role: "Admin"
};

for (let key in user) {
  console.log(`${key}: ${user[key]}`);
}
```
### Output:

```makefile
name: John
age: 30
role: Admin
```
## 5. What is the output order of properties in a `for...in` loop? Is it guaranteed?

The **output order of properties** in a `for...in` loop is **not guaranteed** according to the ECMAScript specification.

However, most JavaScript engines follow these general rules:

1. **Integer-like keys** (e.g., `"0"`, `"1"`, `"2"`) are iterated in **ascending numeric order**.
2. **String keys** (non-integer) are iterated in the **order in which they were added** to the object.

> ⚠️ Since this behavior is not formally guaranteed, it is **not safe to rely on the property order** in a `for...in` loop for consistent behavior across different browsers or JavaScript engines.

If consistent ordering is required, use:
```javascript
Object.keys(obj).forEach(key => {
  console.log(`${key}: ${obj[key]}`);
});
```