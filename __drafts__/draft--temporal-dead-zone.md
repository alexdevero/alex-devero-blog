# Temporal Dead Zone in JavaScript Explained (TDZ)

Temporal dead zone in JavaScript (TDZ) is one of the topics every JavaScript developer should know. This tutorial will teach you all you need to know about it. You will learn what temporal dead zone in JavaScript is and how it works. You will also learn what to avoid to ensure your code works as you want.<!--more-->
<!--
Table of Contents:
-->

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

Variables declared in a global scope are visible and accessible everywhere. Variables declared in a local are accessible and visible only inside that scope, not outside it. The third scope, block, is create by using a pair of curly brackets. For example, when you use [if...else statement], some [loop] and so on, you are also creating block scope.

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

When you create a new variable, there are two steps that happen. The first step is about declare the variable. This means that JavaScript creates an identifier for the name of the variable you just created and reserves memory for it. The second step is about initializing the variable.

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

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[]:

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
