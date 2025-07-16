## 1. What is the purpose of the optional chaining operator in JavaScript?

The optional chaining operator (`?.`) allows safe access to nested object properties, methods, or array elements without causing errors if an intermediate property is `null` or `undefined`.

## 2. How does the optional chaining operator prevent runtime errors?

It short-circuits the evaluation and returns `undefined` immediately when encountering `null` or `undefined` in the property chain, instead of throwing a `TypeError`.

## 3. What is the difference between `obj.prop` and `obj?.prop`?

- `obj.prop` directly accesses the `prop` property and throws a runtime error if `obj` is `null` or `undefined`.
- `obj?.prop` safely accesses `prop` only if `obj` is not `null` or `undefined`; otherwise, it returns `undefined` without throwing an error.
## 4. What happens if a property in the chain does not exist when using `?.`?

If any property in the chain is `null` or `undefined`, the optional chaining operator short-circuits and returns `undefined` immediately without throwing an error.

## 5. Is optional chaining only usable with object properties?

No, optional chaining can be used with:
- Object properties (e.g., `obj?.prop`)
- Method calls (e.g., `obj?.method()`)
- Array elements (e.g., `arr?.[index]`)
- Dynamic property access (e.g., `obj?.[key]`)
