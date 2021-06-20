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
export default sumTwoNumbers = (numA, numB) => numA + numB

// File file2.js
// Import exported function sumTwoNumbers with default "import" statement:
import sumTwoNumbers from './file1'
```

Just two statements with very simple and easy to remember syntax and you can use your code anywhere you want. Unfortunately, nothing is usually perfect and even modules have some downsides.

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
