# Temporal Dead Zone in JavaScript Explained (TDZ)

Temporal dead zone in JavaScript (TDZ) is one of the topics every JavaScript developer should know. This tutorial will teach you all you need to know about it. You will learn what temporal dead zone in JavaScript is and how it works. You will also learn about scope and variable declaration and initialization.<!--more-->
<!--
Table of Contents:
## Three types of variables
## Three types of scopes
### Scope and var
### Scope and let (and const)
## Variable declaration and initialization
### Declaration and initialization differences between var, let and const
### Variable declaration and global object
## Entering the temporal dead zone in JavaScript
### Temporal dead zone and var
## The cause of temporal dead zone
## Conclusion: Temporal dead zone in JavaScript explained
-->

*Note to the reader: if you already understand variables, scope and variable declaration and initialization, you can skip the beginning and scroll to the last section.*

## Three types of variables

In the beginning, there was only one type of variables in JavaScript. When you wanted to declare a new variable you had to use the `var` keyword. This changed when [ECMAScript 6] (ES6) specification was released. One change that was introduced by this specification were two new types of variables.

These new two types of variables were [let] and [const]. There are [differences] between them, the `var`, `let` and `const`. Some of these differences are more important and some less. Among these differences are two that are important to understand how temporal dead zone in JavaScript works and also how it works with each type.

```JavaScript
// Declare variable with var keyword
var myVariableVar = 'Lex'

// Declare variable with let keyword
let myVariableLet = 47

// Declare variable with const keyword
const myVariableConst = ['DC']
```

## Three types of scopes

The first important difference is how these variables work with scope. In JavaScript, there are two, well, three, types of scope, global, local or function and block. Global scope is a scope outside any function or code block. Local or function scope is a scope inside functions. When you create a function you also create a local scope.

Variables declared in a global scope are visible and accessible everywhere. Variables declared in a local are accessible and visible only inside that scope, not outside it. The third scope, block, is created by using a pair of curly brackets. For example, when you use [if...else statement], some [loop] and so on, you are also creating block scope.

```JavaScript
// Variable in a global scope
let myGlobalVariable = 'Global'

// Variable in a local (function) scope
function myFunc() {
  // This is new local scope
  // created for this function
  let myLocalVariable = 'Local'
}

// Variable in a block scope
if (true) {
  // New block scope is created inside the curly brackets
  let myBlockVariable = 'Block'
}
```

### Scope and var

Important thing about `var` variable is that it cares only about the first two: global and local scope. It doesn't care about the third: block scope. Let's say you declared a variable using `var` in the global scope. Then, you created a block scope with `if...else` statement. Inside it you declared another `var` variable.

This new variable has the same name as the global `var`. Since `var` doesn't care about block scope the `var` inside the `if...else` will overwrite the global `var`.

```JavaScript
// Declare variable with var
var myVariableVar = 'Lex'

// Create block scope with if...else statement
if (true) {
  // Declare new variable with var,
  // but use the same name as for the first var
  var myVariableVar = 'Alexander'
}

// Log the value of myVariableVar
console.log(myVariableVar)
// Output:
// 'Alexander'
```

### Scope and let (and const)

The above will not happen if you declare those variables with `let`. The `let` variable knows and respects block scope. By using the `if...else` statement you create new block scope. This scope limits the visibility and accessibility of the new `let` variable. JavaScript basically "sees" these two `let` as two different variables.

```JavaScript
// Declare variable with let
let myVariableLet = 'Lex'

// Create block scope with if...else statement
if (true) {
  // Declare new variable with let,
  // but use the same name as for the first let
  let myVariableLet = 'Alexander'
}

// Log the value of myVariableLet
console.log(myVariableLet)
// Output:
// 'Lex'
```

The `const` variable works in the same way as let. It also respects block scope. So, block-scoped `const` will not collide with global `const`, or the other way around.

```JavaScript
// Declare variable with const
const myVariableConst = 'Lex'

// Create block scope with if...else statement
if (true) {
  // Declare new variable with const,
  // but use the same name as for the first const
  const myVariableConst = 'Alexander'
}

// Log the value of myVariableConst
console.log(myVariableConst)
// Output:
// 'Lex'
```

## Variable declaration and initialization

When you create a new variable, there are two steps that happen. The first step is about declaring the variable. This means that JavaScript creates an identifier for the name of the variable you just created and reserves memory for it. The second step is about initializing the variable.

Variable initialization means assigning a value to the variable. This might happen right away during declaration if you create a variable and assign it a value. Or, it will happen later, when you assign that variable some value. It might also never happen of you don't assign that variable any value.

```JavaScript
// Declare variable
var myVariableVar
let myVariableLet

// Initialize variable
myVariableVar = 'Dex'
myVariableLet = 33

// Declare and initialize variable
let myVariableLetTwo = 'Let\'s do it all at once.'
```

### Declaration and initialization differences between var, let and const

What you need to know is that for this process is a bit different for some types of variables. The first step is the same. What differs is the second step. When you declare a variable with `var` without initializing it will be initialized anyway. Variables you declare with `var` will have the default value of `undefined`.

The `undefined` is also what you get if you try to access the value of declared, but not initialized `var` variable. Variables you declare with `let` and `const` work differently. They don't have any default value and you can't access them before you initialize them, before you assign them some value.

Well, this is more true for `let` rather than `const`. The `const` has to be declared and initialized. Some value is [required]. One interesting thing about `var` is that you can re-declare it as many times as you want. If you re-declare it in the same scope, the newer will overwrite the older.

This doesn't work with `let` and it also doesn't work with `const`. When you try to re-declare `let` or `const`, in the same scope, JavaScript will throw `SyntaxError` saying that some identifier has already been declared.

```JavaScript
// Declare variable with var
// This will work flawlessly
var myVariableVar = 'first'
var myVariableVar = 'second'

console.log(myVariableVar)
// Output:
// 'second'


// Declare variable with let
let myVariableLet = 'first'
let myVariableLet = 'second'
// SyntaxError: Identifier 'myVariableLet' has already been declared


// Declare variable with const
const myVariableConst = 'first'
const myVariableConst = 'second'
// SyntaxError: Identifier 'myVariableConst' has already been declared
```

### Variable declaration and global object

There is one more difference in the terms of variable declaration between `var` and `let` and `const`. When you declare variable with `var` it will get automatically bind to the Global object, `Window` in case of browser. This automatic binding doesn't happen if you declare variables with `let` and `const`.

```JavaScript
// Declare variable with const
var myVariableVar = 'Global citizen'
let myVariableLet = 'mathematics'
const myVariableConst = 'change'

console.log(myVariableVar)
// Output:
// 'Global citizen'

console.log(myVariableLet)
// Output:
// 'mathematics'

console.log(myVariableConst)
// Output:
// 'change'


console.log(window.myVariableVar)
// 'Global citizen'

console.log(window.myVariableLet)
// Output:
// undefined

console.log(window.myVariableConst)
// Output:
// undefined
```

## Entering the temporal dead zone in JavaScript

You understand variables, scope and variable declaration and initialization. Now, let's finally talk about what the temporal dead zone in JavaScript is. In short, temporal dead zone describes a zone where variables are un-reachable. There are variables in the current scope. However, these variables were not declared yet.

If you try to access those variables inside the temporal dead zone JavaScript will throw a `ReferenceError` saying that some variable is not defined. One thing to remember. Temporal dead zone exists only for `let` and `const` variables. These two variables exist in the temporal dead zone from the start until you initialize them.

This is also where the temporal dead zone is. Its beginning is at the beginning of the current scope at which the variable(s) is declared. The end of it is where the variable is actually declared, where you assign that variable some value. The space between these two points is the temporal dead zone.

```JavaScript
// Beginning of the global scope
// and also the beginning
// of the temporal dead zone for global variables
// The temporal dead zone for "myVariableLet" and "myVariableConst"
// The temporal dead zone for "myVariableLet" and "myVariableConst"
// The end of temporal dead zone for "myVariableLet" and "myVariableConst"
let myVariableLet = 33
const myVariableConst = true


// Example of accessing variable in the temporal dead zone
// Beginning of the temporal dead zone for "status" variable
// This is the temporal dead zone for "status" variable
// This is the temporal dead zone for "status" variable

// Try to access the "status" variable
// INSIDE the temporal dead zone
console.log(status)
// Output:
// Uncaught ReferenceError: status is not defined

// This is the temporal dead zone for "status" variable
// The end of temporal dead zone for "status" variable
let status = 'Jack'

// Try to access the "status" variable
// OUTSIDE the temporal dead zone
console.log(status)
// Output:
// 'Jack'
```

### Temporal dead zone and var

As usually, there is always some exception. This applies to temporal dead zone as well. The exception is the `var`. For `var`, there is no such a thing as a temporal dead zone. As you know, `var` has a default value of `undefined`. If you don't initialize it when you declare it, it will be initialized for you, with the default value.

```JavaScript
// Try to access the "myVar" variable
// This will actually work
console.log(myVar)
// Output:
// undefined

// There is no the temporal dead zone for var

var myVar = 'Bug'

// Try to access the "myVar" variable again
console.log(myVar)
// Output:
// 'Bug'
```

## The cause of temporal dead zone

You know what the temporal dead zone in JavaScript is. Let's also quickly talk about why it exists. Whenever you run your JavaScript code it goes through two phases. The first phase is called compilation, or creation. During this phase, your code is being compiled into byte code.

The second phase is called execution. During this phase, your code is being executed. It is also during this second phase, the execution, when your variables are assigned their values. Back to the phase one, compilation. During this first phase another interesting thing happens.

During this phase, JavaScript engine goes through your code, "collects" variables and allocates memory for them, also for function declarations. It is at this moment, variables you declared with `var` are assigned the default value of `undefined`. Memory will also be allocated for `let` and `const` variables, but no values will be assigned.

This process of collecting declarations is called [hoisting]. This is also why the temporal dead zone exists, at least for `let` and `const`. In case of `let` and `const`, there is a moment when these variables are declared, but not initialized. Remember, declaration happens in the first phase, while initialization in the second.

This means that, during the first phase, `let` and `const` exist in the temporal dead zone. This is because they are not initialized with any value. On the other hand, the `var` is always initialized with the value of `undefined` by default. That's why it is never in the temporal dead zone.

When JavaScript engine enters the second phase, compilation or creation, it also initializes `let` and `const` variables. This is the moment when these variables can leave the temporal dead zone. Note that when exactly this happens depends on when you initialize those variables in you code.

So, remember, all variables get hoisted. However, when `var` variables are hoisted they are also initialized with the value of `undefined`. When the `let` and `const` are hoisted they are not initialized with any value. That is the reason the temporal dead zone exists and why it exists only for `let` and `const` and not `var`.

## Conclusion: Temporal dead zone in JavaScript explained

Temporal dead zone in JavaScript (TDZ) may sound complicated. It is not. It can be relatively easy, especially if you understand how variables, scope and variable declaration and initialization work. I hope that this tutorial explained all these topics and helped you understand what temporal dead zone in JavaScript is and how it works.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[ECMAScript 6]: https://www.ecma-international.org/ecma-262/6.0/
[let]: https://blog.alexdevero.com/javascript-variables-introduction/#let
[const]: https://blog.alexdevero.com/javascript-variables-introduction/#const
[differences]: https://blog.alexdevero.com/javascript-variables-introduction/
[loop]: https://blog.alexdevero.com/javascript-loops/#for-loop
[required]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const#Description
[hoisting]:

<!--
### Meta:
-
-->

<!--
### Keywords:
- Temporal Dead Zone in JavaScript
- Temporal Dead Zone
-->

<!--
### Resources:
-
-->
