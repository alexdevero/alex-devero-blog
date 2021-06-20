# Blog post title [...]

Dynamic imports are one of the features introduced in JavaScript ES020 specification. This feature makes modules introduced in ES2015, or ES6, more usable and powerful. This tutorial will help you understand what dynamic imports in JavaScript are, how they work and how to use them.<!--more-->

<!--
Table of Contents:
-->

## ES modules and chunking

Modules were introduced as part of the ES2015 (ES6) specification. This gave JavaScript developers a nice and native way to split their JavaScript code into smaller chunks. Modules also made it easier to manage those chunks, making even large codebase more developer-friendly.

The best part of this is that this chunking process is very simple and easy. When JavaScript developer wants to use modules, there are basically only two things she needs to do. First, she needs to remember to export some chunk of her code she wants to use elsewhere. To do this, she has to use the [export statement].

The second thing to do comes when she wants to use one of the chunks she exported. She needs to use the [import statement] to import specific chunk of code in a file where she wants to use it. This will make that exported chunk of code available in the scope of the file she is currently working with.

```JavaScript
// File file1.js
// Export some function with "export" statement:
export const sumTwoNumbers = (numA, numB) => numA + numB

// File file2.js
// Import exported function sumTwoNumbers with "import" statement:
import { sumTwoNumbers } from './file1'

// Use imported function:
sumTwoNumbers(15, 98)
// Output:
// 113


// NOTE:
// You can also export something with default export
export default (numA, numB) => numA + numB

// File file2.js
// Import exported function sumTwoNumbers with default "import" statement:
import sumTwoNumbers from './file1'
```

Just two statements with very simple and easy to remember syntax and you can use your code anywhere you want. Unfortunately, nothing is usually perfect and even modules have some downsides.

## The problem with static imports

One big downside of ES modules is that they are static. This means that when you import some module it will be always imported, regardless if the code is executed or not. let's go back to the example above with `sumTwoNumbers` function. Imagine that this function is called only under some specific condition.

There is some [if...else statement] and the function is called only inside it. When you run this code, the module with `sumTwoNumbers` function will be imported. JavaScript will not care if the `if...else` statement calls the function or not. It will import the module and if the function is not executed it is not JavaScript's problem.

What this means for you, and anyone else running your code, is simple. You will have to download and run everything that is imported somewhere, regardless if it is actually used or not. This may be okay in most situations. However, sometimes, you may want to save some of the user's bandwidth.

One way to do this is by loading those imported modules conditionally. Instead of loading them always, by default, you will load them only when you know they will be used. In case of the `sumTwoNumbers` function and `if...else` statement you can import the function inside the statement.

At that moment, when execution context enter the statement, you know for sure the function will be called. This is where dynamic imports can be useful.

## Dynamic imports to the rescue

The idea of dynamic imports is to import some chunk of code only when you know you will need it. For example, to load the `sumTwoNumbers` function right inside the `if...else` statement where the function is called. If the code block inside the statement never executes, the module with `sumTwoNumbers` is never imported.

Sounds good? It is even better. There is really no new syntax. Dynamic imports use almost the same syntax as static imports. One difference is that instead of using `import` as a statement you use `import` as a function. This function accepts one parameter, the path to the module, and returns a [promise].

```JavaScript
// Dynamic import syntax:
const module = import('path')

// Examples:
const module1 = import('./myModule')

const modulePath = './myModule'
const module2 = import(modulePath)
```

When the module is loaded successfully, the promise resolves to the module content. When there is some problem, the promise rejects. Since the `import()` function returns a promise, the [async/await] syntax (async function and await operator) can be handy and make your code shorter.

```JavaScript
// await example with global await:
const module1 = await import('./myModule')

const modulePath = './myModule'
const module2 = await import(modulePath)

// Use what imported from module2
module2.someExportedFunction()

// await example with async function:
async function loadImport() {
  const module1 = await import('./myModule')

  // ... use the module
  module1.someExportedFunction()
}
```

## Importing with dynamic imports

Similarly to static imports, dynamic imports also allow you to import default exports, named and mix of these two.

### Default exports

You exported something using default export. When you want import it dynamically, you can simply use the `default` property of the object returned by the import promise. Well, almost. The catch is that `default` is reserved keyword in JavaScript. This also means that you can't use it to declare variables, like for imported module.

What you can do to solve this issue is use [destructuring assignment] and create an alias for that default import. Then, you can use that alias to safely use whatever you imported.

```JavaScript
// File 1:
// Use default export to export a function:
export default (numA, numB) => numA * numB

// File 2:
// Create async function:
async function loadModule() {
  // Use dynamic import to import function from "file1"
  // and use destructuring assignment with alias:
  const { default: defaultExport } = await import('./file1')

  // Use the imported function by using the alias:
  defaultExport(315, 414)
}

// Call the loadModule() function:
loadModule()
// Output:
// 130410
```

Another option is to assign the module to a variable without using the destructuring assignment. This will assign the whole module as an object to the variable. Now, you can use this object's `default` property to access the default export.

```JavaScript
// File 1:
// Use default export to export a function:
export default (numA, numB) => numA * numB


// File 2:
async function loadModule() {
  // Assign the module to a variable:
  const myExport = await import('./file1')

  // Use the imported function by using the alias:
  myExport.default(56, 89)
}

// Call the loadModule() function:
loadModule()
// Output:
// 4984
```

### Named exports

Importing named exports with dynamic imports is even easier. There is no need to use aliases. All you have to do is to assign the module to variable, with or without destructuring assignment. Then, you can use whatever you imported. You can do so by accessing the module object if you didn't use the destructuring assignment.

If you used destructuring assignment, you can simply use the variable name you used during the object destructuring.

```JavaScript
// Example without destructuring:
// File 1:
// Use default export to export a function:
export const divideNumbers = (numA, numB) => numA / numB


// File 2:
// Create async function:
async function loadModule() {
  // Assign the module to a variable:
  const myNExport = await import('./file1')

  // Use the imported function by using the alias:
  myNExport.divideNumbers(996598, 15)
}

// Call the loadModule() function:
loadModule()
// Output:
// 66439.86666666667


// Example with destructuring:
// File 1:
export const divideNumbers = (numA, numB) => numA / numB


// File 2:
async function loadModule() {
  // Use destructuring to assign the divideNumbers() function:
  const { divideNumbers } = await import('./file1')

  // Use the imported function by using the alias:
  divideNumbers(477575, 66)
}

// Call the loadModule() function:
loadModule()
// Output:
// 7235.984848484848
```

## Conclusion: [...] ...

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->

[export statement]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export
[import statement]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import

<!--
### Meta:
-
-->

<!--
### Keywords:
-
-->

<!--
### Resources:
-
-->
