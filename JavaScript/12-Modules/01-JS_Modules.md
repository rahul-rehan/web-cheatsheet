## 1. What are JavaScript modules and why are they used?

JavaScript modules are reusable pieces of code that are encapsulated in separate files or blocks. They allow developers to organize code into smaller, manageable, and maintainable units. Modules can export variables, functions, or classes, which can then be imported and used in other modules or scripts.

Modules are used to:
- Promote code reuse and separation of concerns.
- Avoid polluting the global namespace.
- Manage dependencies between different parts of an application.
- Improve maintainability and scalability of codebases.

## 2. What are the advantages of using modules in JavaScript?

- **Encapsulation:** Keeps variables and functions scoped within the module, preventing global scope pollution.
- **Reusability:** Enables sharing code across different parts of an application or even across projects.
- **Maintainability:** Easier to read, debug, and maintain smaller, focused code files.
- **Dependency Management:** Clear declaration of dependencies via `import` and `export`.
- **Better Tooling Support:** Modern bundlers and IDEs offer enhanced support for modules (tree shaking, code splitting).
- **Standardization:** ES modules are part of the official ECMAScript standard, ensuring consistent behavior across environments.

## 3. What is the difference between a script and a module in JavaScript?

| Feature               | Script                                  | Module                                |
|-----------------------|-----------------------------------------|-------------------------------------|
| Scope                 | Variables declared globally (window)    | Variables scoped to the module only  |
| Default mode           | Non-strict mode by default               | Always in strict mode                 |
| Import/Export support  | No built-in import/export                | Supports `import` and `export`       |
| Loading behavior       | Loaded and executed immediately         | Loaded asynchronously and deferred   |
| `this` context        | Refers to global object (`window`)       | Undefined in the top-level context   |
| `<script>` tag usage  | `<script>` with no `type` or `type="text/javascript"` | `<script type="module">` required |
## 4. How do you define a module in a JavaScript file?

A JavaScript file becomes a module when it uses the `export` or `import` statements. You define a module by exporting variables, functions, or classes from one file, and importing them into another.

**Example:**

```js
// mathUtils.js - exporting from a module
export function add(a, b) {
  return a + b;
}

export const PI = 3.14159;
```
```js
// app.js - importing into another module
import { add, PI } from './mathUtils.js';

console.log(add(2, 3));  // 5
console.log(PI);         // 3.14159
```
In HTML, modules are loaded using the `<script>` tag with `type="module"`:

```html
<script type="module" src="app.js"></script>
```
## 5. How do modules help in organizing and reusing code?

- **Encapsulation:** Modules keep code scoped, avoiding pollution of the global namespace and making large codebases easier to manage.
- **Separation of Concerns:** Functionality can be divided into separate modules, improving code clarity and maintainability.
- **Reusability:** Modules allow you to export and import code across different parts of an application or even different projects.
- **Dependency Management:** Explicit imports clarify dependencies, making debugging and optimization easier.
- **Collaboration:** Modular code enables multiple developers to work on different parts of a project simultaneously without conflicts.
