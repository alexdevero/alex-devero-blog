# Variable Scope, Lexical Scope and Environment in JavaScript

Variable scope and lexical environment are two things every JavaScript developer works with every day. In this tutorial, you will learn about both. First, you will learn about variable scope and how it works with different types of variables. After that, you will learn about lexical environment, what it is and how it works.

<!--more-->
<!--
Table of Contents:
-->

## Variable scope

Every time you declare a variable or a function its visibility and accessibility is limited. There is one thing that determines this. It called a [scope], or "variable scope". This scope says where you can access specific variable and function and where you can't. In JavaScript, there are two types of scope, global and local scope.

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

### Local and function scope

Every function you declare creates its own local scope called a function scope. Variables you declare here are local variables. These variables are visible and accessible only inside the scope, the function, at which you declared them. Trying to access them from the outside of the function, the local scope, will return an error.

Local variables exist only in their local scopes. They don't exist outside it. For this reason you can't access, reference or modify any local variable from the global scope. You can do so only inside the scope at which you declared them.

```JavaScript
// Declare a function to create a local scope:
function sayName() {
  // Local scope for this function.

  // Create local variable:
  const name = 'Dory'

  return name
}

// Call sayName() function:
sayName()
// Output:
// 'Dory'

// Try to access local "name" variable
// from a global scope.
console.log(name)
// Output:
// undefined
```

This also means that you can define multiple variables with the same name. These variables will not overwrite each other as long as each is defined in a different local scope. Or, if one is declared in a global scope and the other in a local scope.

```JavaScript
// Create global variable:
let car = 'Tesla'

function createCar() {
  // Create local variable with the same name:
  let car = 'BMW'

  // Log the value of "car" variable:
  console.log(car)
}

// Call the createCar() function:
// This will read the "car" variable
// defined in a local scope (inside the function).
createCar()
// Output:
// 'BMW'

// Log the value of "car" variable:
// This will read the "car" variable
// defined in a global scope (outside the function).
console.log(car)
// Output:
// 'Tesla'
```

### Nested local scopes

You can also create nested local scopes, local scope inside another local scope. You can do this by declaring a function inside another function. Each of these nested functions will create its own local scope. In this case, remember that variables declared in the outer scope will be visible in the inner scope, not the other way around.

This is the same as with global variables being visible in local scopes, but local variable not being visible in the global scope. If you try to access inner local variable from the outer local scope you will get `undefined`.

```JavaScript
// Create a function:
function myFuncOne() {
  // New local scope.
  let author = 'Terry Pratchett'

  // Create local function:
  function myFuncTwo() {
    // New local scope.
    let book = 'Guards! Guards!'
  }
}
```

## Lexical scope

Previously you've learned that you can create "nested" local scopes with functions. You've also learned that these inner functions have access to the variables you declared outside them, in the outer scopes. This type of scope, the ability to access outer resources, is called a "lexical scope" or "static scope".

One thing about lexical scope to remember is what we've already discussed. It works only in top to bottom direction. It doesn't work the other way around.

```JavaScript
// Declare global variable:
let bookSeries = 'Discworld'

// "author", "book" and "character" are not visible here.

function myFuncOne() {
  // New local scope.
  // "bookSeries" is visible here
  // because it is in the outer scope.
  // "book" and "character" are not visible here.
  let author = 'Terry Pratchett'

  function myFuncTwo() {
    // New local scope.
    // "bookSeries" and "author" are visible here
    // because they are in the outer scope.
    // "character" is not visible here.
    let book = 'Guards! Guards!'

    function myFuncThree() {
      // New local scope.
      // "bookSeries", "author" and "book" are visible here
      // because they are in the outer scope.
      let character = 'Captain Sam Vimes'
    }
  }
}
```

## Code block and block scope

Aside to global and local scope there is also something one could call a "block" scope. This is not an "official" type of scope, but it does exist. Block scope was introduced to JavaScript as a part of the ES6 specification. It was introduced along with two new types of variables `let` and `const`.

These two variables, `let` and `const`, work with this scope. The `var` variable doesn't. The result of this difference can be quite significant. Just as local scope is defined by functions, block scope is defined by a block of code (`{}`). This includes [if...else], [switch] statement, [loops] and code blocks in general.

If you declare `let` or `const` variable inside a code block, it will behave as if it is in a local scope. It will be visible and accessible only inside that code block. Remember that this doesn't apply to `var` variables. This type of variable works only with global and scope. It doesn't work with block scope.

If you declare `var` variable inside a code block it will be visible and accessible from the outside. If there is another variable with the same name in the outside scope, the newer variable will overwrite the older. This will not happen if you use `let` or `const` instead. This can be a good reason to stop using `var`.

```JavaScript
// Global variables:
let numOfPages = 336
const read = true
var rating = 4

// Create block scope
if (true) {
  let numOfPages = 253
  const read = false
  var rating = 2

  // Log the value of "numOfPages" variable:
  console.log(numOfPages)
  // Output:
  // 253

  // Log the value of "read" variable:
  console.log(read)
  // Output:
  // false

  // Log the value of "rating" variable:
  console.log(rating)
  // Output:
  // 2
}

// Log the value of "numOfPages" variable:
console.log(numOfPages)
// Output:
// 336

// Log the value of "read" variable:
console.log(read)
// Output:
// true

// Log the value of "rating" variable:
console.log(rating)
// Output:
// 2

// NOTE: global "rating" was overwritten
// by "rating" declared inside the if...else statement.
// Other variables remained unchanged because
// they were restricted to the block scope
// of the if...else statement.
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
