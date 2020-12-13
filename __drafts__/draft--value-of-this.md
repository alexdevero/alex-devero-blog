# Quick Guide To this Keyword In JavaScript: What this Is And When

Many JavaScript developers try their best to avoid using `this` keyword. One reason is because what `this` refers to changes. This quick guide will help you with it. You will learn what `this` keyword refers to in specific contexts and situations. This will help you predict what you can expect when you use it.<!--more-->
<!--
Table of Contents:
-->

## Quick introduction

The `this` is a special keyword in JavaScript. There is one problem JavaScript developers struggle with when they learn about `this`. It can have different values. It can refer to different things. What determines what `this` refers to is context, the context at which you use it. Let's take a look at these contexts and what to expect from `this` keyword in each of them.

## Strict and sloppy mode

In JavaScript, there are two modes or variants of JavaScript you can work with. The first one is [strict mode]. The second one is [sloppy mode]. By default, you write your JavaScript code in a sloppy mode. This mode is more ... sloppy. It allows you to do things that would be [forbidden] in a strict mode. These things would not work.

JavaScript offers you an option to switch from sloppy mode to strict mode. You can do this by using `'use strict'` statement at the beginning of your code. Any code that follows after this statement will automatically follow the rules and restrictions of strict mode. This also includes the `this` keyword.

## Global scope and this

When you are in a global scope, the `this` keyword will refer to the global object `window`. This is the case at least if you are in the browser. If you are in a Node.js environment, the `this` will refer to global object called `global`. In a global scope, it doesn't matter if you are in a sloppy mode or a strict mode.

```JavaScript
// Global context example no.1: sloppy mode
console.log(this)
// Output:
// Window {0: Window, 1: Window, window: Window, self: Window, document: document, name: "", location: Location, …}

// In Node.js:
console.log(this)
// Output:
// <ref *1> Object [global] {
//   global: [Circular *1],
//   clearInterval: [Function: clearInterval],
//   clearTimeout: [Function: clearTimeout],
//   setInterval: [Function: setInterval],
//   setTimeout: [Function: setTimeout] {
//     [Symbol(nodejs.util.promisify.custom)]: [Getter]
//   },
//   queueMicrotask: [Function: queueMicrotask],
//   clearImmediate: [Function: clearImmediate],
//   setImmediate: [Function: setImmediate] {
//     [Symbol(nodejs.util.promisify.custom)]: [Getter]
//   }
// }


// Global context example no.2: strict mode
// Switch to strict mode.
'use strict'

console.log(this)
// Output:
// Window {0: Window, 1: Window, window: Window, self: Window, document: document, name: "", location: Location, …}

// In Node.js:
console.log(this)
// Output:
// <ref *1> Object [global] {
//   global: [Circular *1],
//   clearInterval: [Function: clearInterval],
//   clearTimeout: [Function: clearTimeout],
//   setInterval: [Function: setInterval],
//   setTimeout: [Function: setTimeout] {
//     [Symbol(nodejs.util.promisify.custom)]: [Getter]
//   },
//   queueMicrotask: [Function: queueMicrotask],
//   clearImmediate: [Function: clearImmediate],
//   setImmediate: [Function: setImmediate] {
//     [Symbol(nodejs.util.promisify.custom)]: [Getter]
//   }
// }
```

## Functions and this

When it comes to [functions], the mode at which you are makes a difference for the `this` keyword. When you are in sloppy mode, this will refer to the global object `window`. Global object `global` in Node.js. This is true even for functions declared inside another functions, in a local scope.

```JavaScript
// Function example no.1: function in a global scope
// Declare a function.
function foo() {
  // Log the value of this
  console.log(this)
  console.log(this === window)
}

// Invoke foo() function.
foo()
// Output:
// Window {0: Window, 1: Window, window: Window, self: Window, document: document, name: "", location: Location, …}
// true


// Function example no.2: function in a local scope
// Declare a function.
function foo() {
  return function bar() {
    // Log the value of this
    console.log(this)
    console.log(this === window)
  }
}

// Invoke foo() and bar() functions.
foo()()
// Output:
// Window {0: Window, 1: Window, window: Window, self: Window, document: document, name: "", location: Location, …}
// true
```

### Strict mode

This will change if you switch your JavaScript code to strict mode. In a strict mode, the default value of `this` in a function is set to `undefined`.

```JavaScript
// Strict mode example no.1: function in a global scope
// Switch to strict mode.
'use strict'

// Declare a function.
function foo() {
  // Log the value of this
  console.log(this)
  console.log(this === window)
}

// Invoke foo() function.
foo()
// Output:
// undefined
// false


// Strict mode example no.2: function in a local scope
// Switch to strict mode.
'use strict'

// Declare a function.
function foo() {
  return function bar() {
    // Log the value of this
    console.log(this)
    console.log(this === window)
  }
}


## Arrow functions

With [arrow functions], `this` keyword works differently than with regular functions. Arrow functions don't have their own `this`. When you use `this` in an arrow function it will inherit its value from its context. Context here is the context at which you defined that arrow function.

// Invoke foo() and bar() functions
foo()()
// Output:
// undefined
// false
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
-
-->

<!--
### Resources:
-
-->
