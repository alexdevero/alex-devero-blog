# Variable scope and Lexical Environment in JavaScript
<!--more-->
<!--
Table of Contents:
-->

## Variable scope

Every time you declare a variable or a function its visibility and accessibility is limited. There is one thing that determines this. It called a "scope", or "variable scope". This scope says where you can access specific variable and function and where you can't. In JavaScript, there are two types of scope, global and local scope.

### Global scope

When you declare variable outside any function or code block (`{ ... }`) it will be automatically in a global scope. For every JavaScript document, there is only one global scope. If you declare multiple variables or functions in a global scope, they will all end up at the same place.

Variable and functions declared in a global scope are usually called "global variables" and "global functions". When a variable or function is global it automatically becomes visible and accessible from anywhere. You can access it, reference it and modify.

```JavaScript
// Global variable:
var name = 'Jack'
let age = 37
const species = 'human'

// Global function:
function readName() {
  return name;
}

// Call the readName() function:
readName()
// Output:
// 'Jack'

// Global arrow function:
const readAge = () => age

// Call the readName() function:
readAge()
// Output:
// 37
```


## Conclusion: [...] ...

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[]:

<!--
### Meta:
-
-->

<!--
### Keywords:
- Variable scope
-->

<!--
### Resources:
-
-->
