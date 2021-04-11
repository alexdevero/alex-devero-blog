# Variable Scope, Lexical Scope and Code Blocks in JavaScript

Variable scope, lexical scope and code blocks are things every JavaScript developer works with every day. In this tutorial, you will learn about them all. You will learn about variable scope and how it works with different types of variables. After that, you will learn about lexical scope and code blocks.<!--more-->
<!--
Table of Contents:
## Variable scope
### Global scope
### Local and function scope
### Nested local scopes
## Lexical scope
## Code block and block scope
## Some advantages of using global scope
## Some disadvantages of using global scope
## Some advantages of using local and block scope
## Some disadvantages of using local and block scope
## Conclusion: Variable scope, lexical scope and code blocks in JavaScript
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

Previously you've learned that you can create "nested" local scopes with functions. You've also learned that these inner functions have access to the variables you declared outside them, in the outer scopes. This type of scope, the ability to access outer resources, is called a "lexical" scope or "static" scope.

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

If you declare `let` or `const` variable inside a code block, it will behave as if it is in a local scope. It will be visible and accessible only inside that code block. This is why these two variables are called "block-scoped" variables. Remember that this doesn't apply to `var` variables.

This type of variable works only with global and scope. It doesn't work with block scope. If you declare `var` variable inside a code block it will be visible and accessible from the outside. If there is another variable with the same name in the outside scope, the newer variable will overwrite the older.

This will not happen if you use either `let` or `const` variable. This can be a good reason to stop using `var`.

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

## Some advantages of using global scope

Accessibility is one reason to using global scope for variables and functions. This can be useful for creating global constants, variables you want to keep unchanged and use on multiple places. The same applies not only to constants but also to variables that store data you want to access from multiple places.

It can be useful to have this kind of data declared as global. On the same note, global scope can be also useful for "general" and "utility" functions. These are the functions you want to use often and from multiple places. Making them accessible everywhere by default can be useful.

## Some disadvantages of using global scope

The main disadvantages of using global scope is security. When something is accessible everywhere anyone can see it. Also, unless you restrict, anyone can also modify it. This might okay for some public data, but not for data that should stay private. Even in case of public data can this be debatable.

Think about it. If some part of your code doesn't use specific piece of data, does it really need to know about it? Does it really need to this data even exists? Using global scope for variables also creates opportunities for collisions. You forget you used some variable name earlier and use it again.

As a result, you accidentally overwrite the old variable or function with the new one. Another type of issues that can happen is when one part of program changes global variable used in another part of program that doesn't expect this change to happen. This can lead to unpredictable results, especially in complex programs.

Excessive use of global scope can negatively impact performance of your code. Variables you declare as global will likely remain in the memory as long as the program execution is running. Lastly, global variables can make code refactoring a living hell. If you change variable used on many places, your code can break on many places.

## Some advantages of using local and block scope

Local variables are more secure. Local scope automatically restricts the accessibility and visibility of each variable, or function. Code in the outer scope can't see it, access it or modify it. This also creates fewer opportunities for name collisions. This is especially true for `let` and `const` variables.

You can safely have as many variables with the same name as you want. None of them will be overwritten as long as each is in a different scope. There is also a smaller chance of variable unexpectedly changing by other part of code. Local scope ensures that only local code can interact with local variables.

Another advantage of local variables is in terms of memory management and performance. Local variables exist only as long as the scope in which they are defined exits. Once the scope is gone, some function execution is terminated, data inside it is deleted and memory space it occupied is released.

The last advantage of keeping things local is when comes time for refactoring. Refactoring will be much easier to do when your code is focused in a smaller scope and/or on fewer places.

## Some disadvantages of using local and block scope

There is only one disadvantage of local data I can think of right now. It can make sharing data more difficult. This at least used to be an issue in the past. Now? It is no longer such an problem when you can use `import` and `export` statement. However, sharing global variables is still a bit easier.

That said, one can resolve this by making some data, such as "general" constants, global. If some data are ought to be shared often, with many places, should these data be kept as local at the first place? That is, I guess, up to every developer to decide.

## Conclusion: Variable scope, lexical scope and code blocks in JavaScript

The idea of variable scope, lexical scope and code blocks can seem tricky, especially at the beginning. However, these concepts are really not that difficult to understand. I hope that this tutorial helped you understand each of these concepts, what are they about, how they work and what to watch for.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[scope]: https://developer.mozilla.org/en-US/docs/Glossary/Scope
[if...else]: https://blog.alexdevero.com/javascript-if-else-statement/
[switch]: https://blog.alexdevero.com/javascript-switch-statement/
[loops]: https://blog.alexdevero.com/javascript-loops/

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
