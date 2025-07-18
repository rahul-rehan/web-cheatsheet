## 1. What is `new.target` in JavaScript?

`new.target` is a special meta-property available inside constructors and functions that lets you determine whether the function was called using the `new` operator.

## 2. When is `new.target` defined and when is it undefined?

- `new.target` is **defined** when a function or constructor is called with the `new` keyword.
- It is **undefined** when the function is called without `new` (i.e., as a regular function call).

## 3. What value does `new.target` return when a constructor is called using `new`?

When called with `new`, `new.target` returns a reference to the constructor or function that was directly invoked with `new`. This allows the constructor to detect if it was called with `new` and even which subclass was instantiated.
## 4. How does `new.target` help in identifying constructor calls?

`new.target` allows a function or constructor to detect if it was called with the `new` operator. If `new.target` is defined (not `undefined`), it confirms that the function was invoked as a constructor. This helps enforce correct usage by throwing errors or altering behavior when called without `new`.

## 5. In which versions of JavaScript is `new.target` available?

`new.target` was introduced in **ES6 (ECMAScript 2015)** and is available in all modern JavaScript environments that support ES6 or later.
