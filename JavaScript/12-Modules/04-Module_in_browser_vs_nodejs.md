## 1. How do you enable ES modules in the browser?

To enable ES modules in the browser, you use the `<script>` tag with the `type="module"` attribute. This tells the browser to treat the script as a module, allowing the use of `import` and `export` statements.

## 2. What type of script tag do you use for modules in HTML?

You use the following script tag to load JavaScript modules in HTML:

```html
<script type="module" src="path/to/module.js"></script>
```
## 3. How do you enable modules in Node.js?

In Node.js, modules can be enabled by either:

- Using the `.mjs` file extension for your JavaScript files, which signals that the file is an ES module, **or**

- Adding `"type": "module"` in your `package.json` file, which instructs Node.js to treat all `.js` files in the project as ES modules.

Example `package.json`:

```json
{
  "type": "module"
}
```
## 4. What is the difference between CommonJS (`require`) and ES Modules (`import`) in Node.js?

- **Syntax:**
  - CommonJS uses `require()` to import modules and `module.exports` or `exports` to export.
  - ES Modules use `import` and `export` statements.

- **Loading behavior:**
  - CommonJS modules are loaded synchronously.
  - ES Modules are loaded asynchronously and support static analysis (tree shaking).

- **File extension and configuration:**
  - CommonJS modules typically have `.js` extension and are the default in Node.js.
  - ES Modules use `.mjs` extension or `.js` with `"type": "module"` in `package.json`.

- **Scope:**
  - CommonJS modules have their own module scope.
  - ES Modules also have strict mode enabled by default.

- **Interop:**
  - ES Modules support `import` of CommonJS modules but require `default` import syntax or named imports via compatibility layers.
  - CommonJS cannot directly `require` ES Modules without dynamic import or additional tooling.

## 5. Can you mix CommonJS and ES Modules in the same file?

No, you cannot mix `require()` and `import` statements **in the same file** directly because:

- ES Modules use static `import` syntax which must be at the top level and cannot coexist with CommonJS `require` calls in the same file.

However, you can:

- Use dynamic `import()` inside CommonJS modules.
- Use `require()` inside ES Modules via dynamic import or special interop mechanisms.

For full compatibility, separate files/modules should use one system or the other.
