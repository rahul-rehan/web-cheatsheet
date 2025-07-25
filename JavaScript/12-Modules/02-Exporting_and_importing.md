## 1. What is the syntax to export a single value from a module?

```js
// Export a single value as default
export default function greet() {
  console.log("Hello!");
}
```

## 2. How do you export multiple values from a module?
```js
// Named exports for multiple values
export const name = "Alice";
export function greet() {
  console.log("Hello!");
}
```
or

```js
const name = "Alice";
function greet() {
  console.log("Hello!");
}

export { name, greet };
```
## 3. What is the difference between named exports and default exports?

- **Named Exports:**
  - Allow exporting multiple values from a module.
  - Imported using the exact exported names enclosed in curly braces.
  - Example:
    ```js
    // Exporting
    export const foo = 1;
    export function bar() {}
    
    // Importing
    import { foo, bar } from './module.js';
    ```

- **Default Exports:**
  - Export a single value as the default from a module.
  - Imported without curly braces and can be given any name by the importer.
  - Example:
    ```js
    // Exporting
    export default function() {}
    
    // Importing
    import myFunction from './module.js';
    ```

- **Key Differences:**
  - Named exports support multiple exports per module; default exports allow only one default export.
  - Import syntax differs: named exports require curly braces; default exports do not.
  - Default export can be renamed on import; named exports must use the exact exported name (unless aliased).
## 4. Example of Default Export and Named Export in the Same File

```js
// mathUtils.js

// Named export
export function add(a, b) {
  return a + b;
}

// Default export
export default function multiply(a, b) {
  return a * b;
}
```
```js
// Usage in another file

import multiply, { add } from './mathUtils.js';

console.log(add(2, 3));       // Output: 5
console.log(multiply(2, 3));  // Output: 6
```
## 5. What is the syntax for importing a default export?

```js
import defaultExport from './module.js';
```
## 6. What is the syntax for importing named exports?

```js
import { namedExport1, namedExport2 } from './module.js';
```
## 7. Can you rename imports while importing? How?
Yes, you can rename imports using the as keyword:

```js
Copy
Edit
import { namedExport as aliasName } from './module.js';
```
#### Example:

```js
import { add as sum } from './mathUtils.js';

console.log(sum(2, 3)); // Uses the renamed import 'sum'
```
## 8. Can you import everything from a module as a namespace? How?

Yes, you can import all exports from a module as a namespace object using the `* as` syntax:

```js
import * as myModule from './module.js';

// Usage:
myModule.namedExport1();
myModule.namedExport2();
```
## 9. What happens if you try to import a module twice?

When you import the same module multiple times in different places, the module is **only evaluated once**. The result of the first import is **cached**, and all subsequent imports reference this cached module. This means:

- The module code runs a single time.
- All imports share the same module instance.
- Changes to exported values (if mutable) are reflected across all imports.

This caching behavior improves performance and ensures consistency across your application.
