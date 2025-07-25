## 1. What are "well-known symbols" in JavaScript?

Well-known symbols are built-in Symbol values that JavaScript uses internally to represent specific behaviors or protocols. They allow developers to customize or define how certain language features work on objects.

## 2. Name some examples of well-known symbols and their use cases

- `Symbol.iterator`: Defines the default iterator for an object, enabling it to be iterable with `for...of`.
- `Symbol.toStringTag`: Customizes the default string description of an object used by `Object.prototype.toString()`.
- `Symbol.toPrimitive`: Specifies how an object is converted to a primitive value.
- `Symbol.hasInstance`: Customizes the behavior of the `instanceof` operator.
- `Symbol.asyncIterator`: Defines the default async iterator for asynchronous iteration.

## 3. What is Symbol.iterator and how is it used?

`Symbol.iterator` is a well-known symbol that specifies the method that returns an iterator object for an iterable. It enables objects like arrays, strings, and custom objects to be iterated using `for...of` loops or spread syntax.

**Example:**

```js
const myIterable = {
  data: [1, 2, 3],
  [Symbol.iterator]() {
    let index = 0;
    const data = this.data;
    return {
      next() {
        if (index < data.length) {
          return { value: data[index++], done: false };
        } else {
          return { done: true };
        }
      }
    };
  }
};

for (const value of myIterable) {
  console.log(value); // Logs 1, then 2, then 3
}
```
## 4. What does Symbol.toPrimitive do?

`Symbol.toPrimitive` is a well-known symbol that defines a method to customize how an object is converted to a primitive value (like a string, number, or default). When JavaScript attempts to convert an object to a primitive (e.g., during concatenation or numeric operations), it calls the method defined by `Symbol.toPrimitive` if available.

## 5. How does Symbol.toStringTag affect Object.prototype.toString()?

`Symbol.toStringTag` is a well-known symbol that specifies a string tag used by `Object.prototype.toString()` to create the default string description of an object. By defining `Symbol.toStringTag`, you can customize the output of `Object.prototype.toString.call(obj)`.

**Example:**

```js
const obj = {
  [Symbol.toStringTag]: "CustomObject"
};

console.log(Object.prototype.toString.call(obj)); 
// Output: "[object CustomObject]"
```
