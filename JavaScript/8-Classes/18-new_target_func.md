## 1. Can `new.target` be used inside a regular function?

Yes, `new.target` can be accessed inside any function, including regular (non-class) functions, to detect if the function was called as a constructor with `new`.


## 2. What happens if you access `new.target` in a function that’s not called with `new`?

If a function is called without `new`, `new.target` is `undefined`. This allows the function to differentiate between constructor and normal function calls.

## 3. Example of how `new.target` behaves differently based on how a function is called

```js
function Example() {
  if (new.target) {
    console.log("Called with new");
  } else {
    console.log("Called without new");
  }
}

Example();      // Output: "Called without new"
new Example();  // Output: "Called with new"
```
## 4. How can `new.target` be used to make a function behave only when called as a constructor?

You can use `new.target` inside a function to check if it was called with `new`. If it wasn’t, you can throw an error or redirect the call to ensure the function only behaves as a constructor.

```js
function Person(name) {
  if (!new.target) {
    throw new Error("Person() must be called with new");
  }
  this.name = name;
}

new Person("Alice"); // Works fine
Person("Bob");       // Throws Error: Person() must be called with new
```
## 5. What is the value of `new.target` inside a function that is not a constructor?

When a function is called without the `new` keyword (i.e., not as a constructor), the value of `new.target` inside that function is `undefined`.
