## 1. What is a dynamic import in JavaScript?

A **dynamic import** allows you to load modules on demand, asynchronously, rather than at the start of the program. It enables conditional or lazy loading of modules, improving performance and reducing initial load times.

## 2. What is the syntax for dynamic imports using `import()`?

```javascript
import('./module.js')
  .then(module => {
    // Use the imported module here
  })
  .catch(error => {
    // Handle errors if the module fails to load
  });
```
Or with async/await:

```javascript
async function loadModule() {
  try {
    const module = await import('./module.js');
    // Use the imported module here
  } catch (error) {
    // Handle errors
  }
}
```
## 3. What does `import()` return?

`import()` returns a **Promise** that resolves to the module object when the module is successfully loaded.  
If the module fails to load, the Promise rejects with an error.
## 4. Provide a use case where dynamic import is useful.

Dynamic imports are useful for **code-splitting** and **lazy-loading** modules only when they are needed. For example, loading a large library or feature module on-demand to improve initial page load time and performance:

```js
button.addEventListener('click', async () => {
  const { heavyFunction } = await import('./heavyModule.js');
  heavyFunction();
});
```
## 5. Can you use `await import()` in a non-module script? Why or why not?
No, you **cannot** use `await import()` in a non-module script because:

- The `await` keyword is only valid inside async functions or ES modules.
- Dynamic imports (`import()`) require the JavaScript context to support ES modules.
- Non-module scripts do not support the module syntax or `await` at the top level by default.

To use `await import()`, your script must be a module (e.g., use `<script type="module">`) or be inside an async function.

## Best Practices and Use Cases
## 1. When should you use default exports vs named exports?

- **Default exports** are best when a module exports a single main value or function, making imports simpler and clearer.
- **Named exports** are preferred when a module exports multiple related values or functions, allowing selective imports and better tree-shaking.

## 2. How do modules improve maintainability in large projects?

- Modules help organize code into logical, reusable pieces.
- They promote separation of concerns and encapsulation.
- Modules reduce global scope pollution and naming conflicts.
- Easier to manage dependencies and update parts of the codebase independently.

## 3. What are some common pitfalls when working with modules?

- Confusing default and named exports leading to import errors.
- Circular dependencies causing runtime errors or unexpected behavior.
- Forgetting to use the correct script type (`type="module"`) in browsers.
- Mixing CommonJS and ES Modules improperly in Node.js.
- Not handling asynchronous loading with dynamic imports correctly.
## 4. How does tree shaking work with JavaScript modules?

- Tree shaking is a process used by bundlers (like Webpack or Rollup) to remove unused code from modules during the build.
- It relies on static analysis of ES6 `import` and `export` statements to determine which parts of the code are actually used.
- Only the imported (used) parts of a module are included in the final bundle, reducing bundle size and improving performance.
- Tree shaking works best with **named exports** because it can identify exactly which exports are used; default exports are less optimized in this regard.

## 5. How can you structure a project using modular JavaScript code?

- **Organize code by feature or functionality**, creating separate modules/files for each logical part (e.g., utils, components, services).
- Use **clear and consistent naming conventions** for files and exports.
- Export only what is necessary using **named exports** to enable effective tree shaking.
- Use **index files** (barrel files) to re-export modules for cleaner import paths.
- Avoid circular dependencies to keep modules independent and maintainable.
- Use dynamic imports for code-splitting and loading modules on demand.
- Group related modules into folders to keep the project scalable and easy to navigate.
