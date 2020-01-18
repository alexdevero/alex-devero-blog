# ES6, ES7, ES8 & Writing Modern JavaScript Pt1 - Scope, let, const, var

Have you ever wondered what is the difference between `var`, `let` and `const`? Do you know when to use them? And what about scope and hoisting, and why so many JavaScript developers hate `var`? Learn about all these topics in this article. Master the nuts and bolts of ES6, ES7, ES8. Learn how to write modern JavaScript!

<!--
Table of Contents:
## Let & const
### The problem with var no.1: Scope
### The problem with var no.2: Hoisting
### Let and const come to rescue
### Let, const and the difference between them
### When to use what
## Epilogue: ES6, ES7, ES8 and Beyond - Writing Modern JavaScript Pt1
-->

## Let & const

Until the introduction of ES6 you could define variables only with `var` keyword. ES6 introduced two new ways to declare variables, or two new keywords. These keywords are `let` and `const`. But first, what's wrong with `var`. Two things. The first one is scope. When you declare new variable with `var` it is declared in its execution scope.

In JavaScript, before ES6, there were two types of scope, global and local. Global variables are accessible everywhere. You can access them, and change their value, from any part of your code. Local variables are accessible only the scope they are declared in. This also means that you can access them, and change their value, only inside that scope.

The scope changes with the most immediately enclosing function. If you declare variable outside any function, is accessible globally. If you declare it inside a function, it is accessible only in that function. This is the local scope. The problem is that this rule applies only to functions. It doesn't apply to loops or statements.

### The problem with var no.1: Scope

Let's say you have a function with a loop or statement. Inside this loop or statement is a variable declared with `var` keyword. Due to how `var` works, this variable is accessible also in the enclosing function, not just in that loop or statement. In other words, the local scope is the function, not the loop or statement. Let's take a look at few examples.

```
///
// Example no.1: function with if statement and local variable
function testOne() {
  if (true) {
    // Local variable declared inside the statement
    // but accessible in the scope of "test" function.
    var z = 19
  }

  // Print the value of variable 'z'
  console.log(z)
}

testOne()
// Prints: '19'

///
// Example no.2: global variable and function with if statement with local variable
// Variable declared in global scope
var z = 'Superman'

function testTwo() {
  if (true) {
    // Variable declared inside the statement, in the local scope
    // but accessible in the scope of "test" function.
    var z = 'Batman'
  }

  // Print the value of variable 'z'
  console.log(z)
}

testTwo()
// Prints: 'Batman'
//value of local variable "z" declared inside the if statement, not the value of global variable "z"

///
// Example no.3: global variable and function with local variable and if statement with another local variable
// Variable declared in global scope
var z = 'Superman'

function testThree() {
  // First local variable
  // What you want to print
  var z = 'Iron man'

  if (true) {
    // Second local variable
    // Collides with 'Iron Man' variable 'z' declared in the same scope
    var z = 'Batman'
  }

  // Print the value of variable 'z'
  console.log(z)
}

testThree()
// Still prints: 'Batman'

///
// Example no.4: function with for loop and local variable
function testFour() {
  for (var i = 0; i < 3; i++) {
    console.log('Looped!')
  }

  // Try to print the value of variable "i" (hint: it will work).
  // Notice that there is no explicitly declared local or global
  // variable "i",other than the one in the for loop
  console.log(i)
}

testFour()
// Prints:
// 'Looped!'
// 'Looped!'
// 'Looped!'
// 3 (WTF??)
```

As you can see on the example above, the function prints 'Batman', the value of the local variable "z" declared inside the inner `if` statement. It doesn't matter that the `console.log` is declared outside the `if` statement. The same is true about the second example as well. Here, `console.log` again prints the value of the local variable "z" declared inside the `if` statement.

The third example is the best demonstration of the problem with `var` and scope. Here, `console.log` again prints 'Batman', value of local variable "z" even though there is another local variable declared right inside the function. As you can see it doesn't matter. The local variable "z" with value "Iron man" is ignored and Batman wins again.

The most interesting is the fourth example. Here, you can print the value of variable "i" even though you never explicitly declared it inside the function, or outside. That doesn't matter. Since `var` is bound to the most immediately enclosing function, the variable "i" "escapes" from the `for` loop and becomes accessible in the scope of the "testFour" function.

### The problem with var no.2: Hoisting

The second problem with `var` is hoisting. Hoisting is a mechanism built in JavaScript that automatically moves variables and function declarations to the top of their scope. This happens right before the code is executed. What this means is that you can reference a variable before you actually declare it.

Even though this variable doesn't exist, your code will work. Meaning, JavaScript will return `undefined`. This is not what should happen. What should happen is that you should get a reference error saying that the variable you are referencing is not defined.

```
///
// Example no.1: Hoisting in global scope
// Print the value of variable x
console.log(x) // Prints: undefined (??)

// Create variable 'x'
var x = 'The variable has been hoisted.'

///
// Example no.2: Hoisting and function
function testOne() {
  // Create variable 'a'
  var a = 'Hello'

  // Print the value of variable 'a' and 'b'
  console.log(a + ' ' + b)

  // Create variable 'b'
  var b = 'World'
}

testOne()
// Prints: 'Hello undefined'
```

### Let and const come to rescue

Now, let's talk about ES6. With the introduction of ES6, there are now two other ways, or keywords, JavaScript developers can use to declare variables. These are `let` and `const`. What's more, these two new types of variables also solve those two major issues with `var`, the issue with scope as well as the issue with hoisting.

Let's talk about the scope first. When you use declare variables with `let` or `const` these variables re accessible only in that scope. This still sounds like `var`, right? Well, not exactly. There is one difference. Both `let` and `const` are block scope local variables. This is another thing ES6 introduced. What is a block-scoped variable?

A block-scoped variable is a variable that is accessible only in the block, statement, or function expression in which you declared it. In other words, when you declare a block-scoped variable, using `let` or `const`, inside a loop or a statement it is not accessible outside it, as the `var` variable would.

Let's get back to the previous examples. But now, let's declare all variables using `let` instead of `var` so you can see the difference.

```
///
// Example no.1: local variable inside an if statement
function testOne() {
  if (true) {
    // Variable declared inside the statement
    // but accessible in the scope of "test" function.
    let x = 19
  }

  // Try to print the value of variable 'x'
  console.log(x)
}

testOne()
// Correctly prints: ReferenceError: x is not defined

///
// Example no.2: global variable and function with an if statement with local variable
// Variable declared in global scope
let z = 'Superman'

function testTwo() {
  if (true) {
    // Variable declared inside the statement
    // but accessible in the scope of "test" function.
    let z = 'Batman'
  }

  // Print the value of variable 'z'
  console.log(z)
}

testTwo()
// Correctly prints: 'Superman'
// Value of global variable "z", not the local "z" inside the if statement.

///
// Example no.3: global variable and function with local variable and if statement with another local variable
// Variable declared in global scope
let z = 'Superman'

function testThree() {
  // What you want to print
  let z = 'Iron man'

  if (true) {
    // Collides with 'Iron Man' variable 'z' declared in the same scope
    let z = 'Batman'
  }

  // Print the value of variable 'z'
  console.log(z)
}

testThree()
// Correctly prints: 'Iron man'

///
// Example no.4: function with for loop and local variable
function testFour() {
  for (let i = 0; i < 3; i++) {
    console.log('Looped!')
  }

  // Try to print the value of "i" (hint: it will work)
  // Notice that there is no explicitly declared "i"
  // other than the one in the for loop
  console.log(i)
}

testFour()
// Correctly prints:
// 'Looped!'
// 'Looped!'
// 'Looped!'
// 'error'
// 'ReferenceError: i is not defined'
```

Let's do one more quick test so you can see how `let` variables handle hoisting.

```
///
// Example no.1: Hoisting in global scope
// Print the value of variable x
console.log(x) // Correctly prints: ReferenceError: x is not defined

// Create variable 'x'
let x = 'The variable has NOT been hoisted!'

///
// Example no.2: Hoisting and function
function testOne() {
  // Create variable 'a'
  let a = 'Hello'

  // Print the value of variable 'a' and 'b'
  console.log(a + ' ' + b)

  // Create variable 'b'
  let b = 'World'
}

testOne()
// Correctly prints:
// 'error'
// 'ReferenceError: b is not defined'
```

As you can see, the difference between `var` and `let` is significant. All variables are now accessible only in the scopes they are declared in, including loops and statements. There is also no longer any problem with hoisting. When you try to reference any variable before you declare it you will get a reference error, not `undefined`.

This is exactly what we want. Anything to say? Thank you ES6. That was `let`, but what about `const`. Since `const` is block-scoped just as `let`, you will get the same result if your replace `let` with `const`. Well, almost. There is one exception.

### Let, const and the difference between them

The `let` and `const` are similar in how they work. Yet, there are two important differences. First, `const` is read-only, `let` is not. When you declare a variable using `const`, you can't change its value. If you try it, you will get a type error: `Assignment to constant variable.`. With `let`, you can change the value any time and as many times as you want.

Second, when you use `const` you have to declare the variable with value. With `let`, you can declare variable without a value, or as undefined. And assign a value to it later. If you try to declare `const` without a value you will get a syntax error: `Missing initializer in const declaration`.

This makes sense because, as you've just learned, `const` are read-only. You can't change their value after you declare them. Think about it. If you can't change the value of `const`, you can't declare `const` without a value and assign it value later. That would basically mean changing the original, although undefined, value. For this reason, JavaScript does not allow to declare `const` without a value.

What about the one exception I mentioned above? The exception is the example number four with `for` loop. Here, you have to use `let` for the `initialization` variable, or the "i" variable. Again, this makes sense. The `for` loop updates the value of `initialization` variable with every iteration, either decreases or increases it developing on the final expression.

Since `const` is read-only `for` loop can't update it. What if you try to use `const` to declare the `initialization` variable? The loop will go only through the first iteration because JavaScript allows to assign a value to `const` only once. Then, you will get a type error: `Assignment to constant variable`. So, no `const` here, only `let`.

```
///
// Example: for loop and using const to declare initialization variable
// Syntax of for loop: for (initialization; condition; final-expression)
for (const i = 0; i < 10; i++) {
  console.log('Looping!')
}

// Correctly prints:
// "Looping!"
// "error"
// "TypeError: Assignment to constant variable.
```

Well, the read-only thing is not exactly true. Read-only is not the same as immutable. In other words, there is a way to change the value of a variable you declared using `const`. You can change the value if it is an array or object, or something similar. Meaning, you can change the values inside the array or the properties of the object, even add new.

```
///
// Example no.1: const, array and changing values of array items
// Declare new variable x using const
const x = [1, 2, 3]

// Print the value of x
console.log(x)
// Prints: [1, 2, 3]

// Change the items of array stored inside x
x[0] = 'Dog'
x[1] = 'Cat'
x[2] = 'Armadillo'

// Add new items to the array stored inside x
x[3] = 'Snake'
x[4] = 'Harry Potter'

// Print the value of x
console.log(x)
// Prints: ["Dog", "Cat", "Armadillo", "Snake", "Harry Potter"]

///
// Example no.2: const, object and changing values
const y = {
  name: 'Joe Doe',
  age: 33,
  living: true
}

console.log(x)
// Prints:
// [object Object] {
//   age: 33,
//   living: true,
//   name: "Joe Doe"
// }

// Change values
y.name = 'Scarlett Seer'
y.age = 21

// Add new keys to the object stored inside y
y.height = 1.72
y.weight = 63

console.log(x)
// Prints:
// [object Object] {
//   age: 21,
//   height: 1.72,
//   living: true,
//   name: "Scarlett Seer"
// }
```

### When to use what

One way that will help you decide when to use `let` or `const` is to think about how they work. Both `let` and `const` are block-scoped variables. The `let` allows you to declare variable as undefined, without a value. The `let` allows you to change the value any time you want. The `let` works like `var`, except the scope ... And hoisting.

The `const` doesn't allow any of this. When you use `const` you have to declare it with a value. This value can't be changed later, unless it is an array or object, or something similar. Then, you can change the content of the array or object as you want. Conclusion?

Use `let` every time when you know, or think, you will need to reassign the variable, or change its value, some times later in the future. Also, use `let` when you want to declare the `initialization` variable when you work with loops. For anything else, just stick with `const`. In other words, make `const` your default choice.

Making `const` your default choice will help you make your JavaScript code cleaner. The `const` is a clear signal that the variable is not going to be reassigned in the future. What about `var`? You don't need it anymore with the introduction of ES6. You can cover the majority of possible scenarios, if not all of them, with `let` and `const`.

## Epilogue: ES6, ES7, ES8 and Beyond - Writing Modern JavaScript Pt1

Congratulations! You've just finished the first part of ES6, ES7, ES8 and Beyond series! By now, you know what the difference between `var`, `let` and `const` is and when to use them. You also know what scope and hoisting is about and why it created so much hate among many JavaScript developers in relation to `var`. What's coming next?

In the next part you will learn about topics such as template and object literals, destructuring, spread and rest operator, new loops and much much more! Until then, practice what you've learned today so you can truly master those topics. Remember, the best way to master JavaScript is by writing JavaScript. So, go and write some code!

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[]:

<!--
#### Meta:
-
-->

<!--
#### Inspiration:
- https://medium.com/podiihq/javascript-variables-should-you-use-let-var-or-const-394f7645c88f
- https://medium.com/javascript-scene/javascript-es6-var-let-or-const-ba58b8dcde75
- https://scotch.io/tutorials/understanding-scope-in-javascript#toc-execution-context
- https://scotch.io/tutorials/understanding-hoisting-in-javascript
- https://www.sitepoint.com/back-to-basics-javascript-hoisting/
-->
