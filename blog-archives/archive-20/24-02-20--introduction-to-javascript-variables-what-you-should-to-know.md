# Introduction to JavaScript Variables - What You Should to Know
Knowing how to work with JavaScript variables is a must for every web and JavaScript developer. In this tutorial, you will learn the basics, how to declare, initialize and re-assign JavaScript variables and how to use `var`, `let` and `const`. You will also learn about scope.<!--more-->
<!--
Table of Contents:
## Introduction to JavaScript variables
## Variable declaration, initialization and re-assignment
### Variable declaration
### Variable initialization
### Re-assigning JavaScript variables
## Accessing JavaScript variables
## JavaScript variables and scope
### Local and global scope
### "Nested" local scopes
### Block scope, var, let and const
## Var
## Let
## Const
### Partially immutable
## Naming variables
## Conclusion: Introduction to JavaScript Variables
-->

## Introduction to JavaScript variables

Similarly to many other programming languages, JavaScript also has variables. An easy way to think about variables is to think about them as storage containers. Each of these containers has a name, a variable name. You can use these containers to store various types of data, such as numbers, strings, objects, arrays, etc.

The best thing is that you can use the data they are storing later. When you want to use these data later you do it by using the name of some specific container, or variable. This is also called referencing a variable. When you reference a variable, use its name, JavaScript will return the value is assigned to that variable, data stored in that container.

## Variable declaration, initialization and re-assignment

One thing before we take a look at the types of JavaScript variables you can use. We should briefly talk about declaration and initialization. When it comes to JavaScript variables, or variables in general, you will encounter these two terms very often. What these terms, declaration and initialization, actually mean?

### Variable declaration

Variable declaration means you are creating a variable with or without assigning it any value. You can declare variable with `var`, `let` or `const` keywords. We will take a look at each of these later. Now, let's focus on declaration itself. In JavaScript, it is allowed to declare, or create, multiple variables at the same time.

When you want to do this there are two things to remember. First, you must use the same keyword, `var`, `let` or `const`, for all variables. You use the keyword only once, at the beginning of the line. Second, you separate variables with commas. Otherwise, you can declare, or create, all variables individually. This allows you to use different keywords, if you want.

```JavaScript
// Variable declaration example no.1:
/// Declare one variable at the time
var firstVariable
var secondVariable
var thirdVariable

// Or, using let
let firstVariable
let secondVariable
let thirdVariable


// Variable declaration example no.2:
// Declare multiple variable at once
// NOTE: Use 'var' or 'let' keywords only once
// before the first variable, at the beginning of the line.
var firstVariable, secondVariable, thirdVariable

// Or, using let
let firstVariable, secondVariable, thirdVariable
```

### Variable initialization

Variable initialization means you are storing some value in a variable. You can do variable initialization at the time of variable declaration, when you create the variable. Or, you can initialize it later, when you assign the variable a value. There is one exception. You can initialize later only `var` and `let`.

You can't initialize `const` variables later. You can initialize `const`, assign it a value, only at the time you declare it. Otherwise, JavaScript will throw a syntax error. We will talk about this later in this tutorial, in the section dedicated to `const` variables.

```JavaScript
// Variable initialization example no.1:
// Declare variables and initialize them later
var myVariable
let anotherVariable

// initialize the myVariable variable
myVariable = 'Bang'
anotherVariable = 'Boom'


// Variable initialization example no.2:
// Declare and initialize variables at the same time
var myVariable = 'Dang'
let anotherVariable = 'Doom'


// Variable declaration example no.3:
// Declare and initialize multiple variables at once
var myVariable = 'John', anotherVariable = 'Doe'
let myVariable = 'John', anotherVariable = 'Doe'
```

### Re-assigning JavaScript variables

In case of `var` and `let`, you can also re-assign them. You can assign them different values after you initialized them, i.e. assign them some value for the first time. You can't re-assign `const`. Re-assigning JavaScript variables uses the same syntax as initializing them, i.e. assigning them value for the first time.

You specify the variable you want to re-assign. Variable whose value you want to change. Then, you assign it a new value, using equal sign and the value. That's it. When you try to access that variable, you will get that new value.

```JavaScript
// Re-assign variables
// Declare and initialize variables
var myVariable = 'This is var.'
let myAnotherVariable = 'This is let.'

// Re-assign previously initialized variables
myVariable = 'This is new value for var variable.'
myAnotherVariable = 'This is new value for let variable.'
```

## Accessing JavaScript variables

That was about creating and updating JavaScript variables. Another thing you need to know is how to access them. Or, how can you access the value that is stored in a specific variable. You can do this by using the name of the variable that contains the value you want to access. This is also called "referencing a variable".

```JavaScript
// Declare and initialize variable
var myVarVariable = 85
let myLetVariable = 'Enter the void.'
const myConstVariable = 'Change is the only constant.'


// Access the values in myVarVariable and myLetVariable
myVarVariable
// 85
myLetVariable
// 'Enter the void.'
myConstVariable
// 'Change is the only constant.'


// Re-assign myVarVariable and myLetVariable
myVarVariable = 'New York'
myLetVariable = 'Madrid'


// Access the values in myVarVariable and myLetVariable again
myVarVariable
// 'New York'
myLetVariable
// 'Madrid'
```

## JavaScript variables and scope

In JavaScript, there are two types of scope. The first type of scope is `global`. The second one is `local`. Global scope is a scope, or environment, outside any [function]. Any variable declared in global scope is visible and accessible for the rest of your code. Local scope is a scope that exists within a function.

### Local and global scope

Every time you create a function JavaScript also creates a new local scope for that function. This scope, also called `Function scope`, is then applied to all variables you declare inside that function. Any variable declared in local scope is called local variable. Local variables are not visible or accessible outside that scope.

When you try to access some local variable from the global scope, the outside, JavaScript will throw reference error about variable not defined. So, remember that when you declare a local variable, you can use that variable only in that scope, or in that function. Otherwise, your code will not work.

JavaScript variables declared in local scope are not visible, and accessible, outside that scope. However, they will be visible, and accessible, if you create new local scope inside the previous local scope. If you create a function inside a function that second, child, function can work with variables declared inside the outer, parent, function.

```JavaScript
// Variable declared in global scope
var globalVariable = 'I am global'
const globalConstVariable = 'I am also global'

// Try to access the value of globalVariable
globalVariable
// 'I am global'

globalConstVariable
// 'I am also global'


// Variable declared in local scope (function scope) example 1:
function myFunc() {
  var myLocalVariable = 'I am local'
  let myLocalLetVariable = 'I am also local'

  // Try to access the value of myLocalVariable
  // from the inside of the myFunc function
  myLocalVariable
  // 'I am local'

  myLocalLetVariable
  // 'I am also local'
}

// Try to access the value of myLocalVariable
// from the outside of the myFunc function
myLocalVariable
// ReferenceError: myLocalVariable is not defined

myLocalLetVariable
// ReferenceError: myLocalVariable is not defined
```

### "Nested" local scopes

One thing to remember in the terms of these "nested" scopes. Variables you declare inside outer functions are visible, and accessible, in inner functions. Variables you declare inside inner functions are not visible, or accessible, in outer functions. It is like local and global scope.

Anything created in a global scope, or outer functions, is visible, and accessible in local scope, or inner functions. Anything created in a local scope, or inner functions, is not visible, or accessible, in global scope, or outer functions.

So, let's say you have one inner function A inside outer function B, and function A contains some variables. These variables, declared in inner function A, will not be accessible in outer function B.

```JavaScript
// Scope and nested functions example 1:
// Accessing Local variable in outer function from inner function
// Outer function
function myFunc() {
  // Local variable
  var myLocalVariable = 'I am local'
  let myLocalLetVariable = 'I am also local'

  // Inner function
  function myInnerFunc() {
    // Try to access the value of myLocalVariable
    // from function inside the myFunc function
    myLocalVariable
    // 'I am local'

    myLocalLetVariable
    // 'I am also local'
  }
}


// Scope and nested functions
// Accessing Local variable in inner function from outer function
// Outer function
function myFunc() {
  // Inner function
  function myInnerFunc() {
    // Local variable that is visible only in myInnerFunc
    var myLocalVariable = 'I am local'
    var myLocalLetVariable = 'I am also local'
  }

  // Try to access the value of myLocalVariable
  // from the outer myFunc function
  myLocalVariable
  // ReferenceError: myLocalVariable is not defined

  myLocalLetVariable
  // ReferenceError: myLocalLetVariable is not defined
}
```

### Block scope, var, let and const

So far, we focused solely on `global` and `local` scope. From this angle, the `var`, `let` and `const` variables work very much the same. Well, not so fast. Aside to `global` and `local` scope, there is also a `block` scope. This type of scope is limited to block statements and expressions.

In JavaScript, and some other programming languages, a block is defined by a pair of curly brackets. Some examples of a block statement can be [if...else], [for] and [while] statements. All these statements create new block scope. This is important because it is where `var` and `let` and `const` work differently.

The `var`, for example, doesn't care about block scope. When you declare a variable using `var` in a block scope, like in an `if` statement, it is still visible everywhere. What about `let` and `const`? These are different. They respect scope. Variables declared with `let` or `const` will be visible only inside that block scope.

When you try to access any `let` or `const` variable outside the block scope JavaScript will throw a reference error about variable not being defined. When you try to access `var` variable outside the block scope you will get the value.

```JavaScript
// Example of a block scope
// Create an if statement
if (true) {
  // Create new variables using var, let and const
  var myVarVariable = 'I am \'var\' in block scope'
  let myLetVariable = 'I am \'let\' in block scope'
  const myConstVariable = 'I am \'const\' in block scope'
}

// Try to access the value of myVarVariable (created with var)
myVarVariable
// 'I am \'var\' in block scope'

// Try to access the value of myLetVariable (created with let)
myLetVariable
// ReferenceError: myLetVariable is not defined

// Try to access the value of myConstVariable (created with const)
myConstVariable
// ReferenceError: myConstVariable is not defined
```

This is one reason JavaScript developers prefer `let` and `const` over `var`. With `let` and `const`, you have more control over code. The rules of visibility, and accessibility, for JavaScript variables are much more strict. It is less likely to happen that one variable will collide, or overwrite, another. Especially in case of `const`.

## Var

There are three types of JavaScript variables you can use. These are `var`, `let` and `const`. The first type of variable is `var`. This type of variables has been in JavaScript since the beginning. It is also usually the first of JavaScript variables people get familiar with. Well, at least it used to be this way.

Nowadays, thanks to popularity of `let` and `const`, `var` is slowly losing traction. Nonetheless, since `var` is still one of JavaScript variables, it is still good to know about how it, and how it works. Knowing about how `var` variables work is also necessary if you want to really understand why `let` and `const` are usually better choices for JavaScript variables than `var`.

With `var`, you can either declare a variable first and initialize it later or you can declare it and initialize it and the same time. The way to declare variable using `var` is very simple, just like using the rest of JavaScript variables. You use the `var` keyword followed by the variable name.

If you want to only declare a variable without initializing it, here is where you stop. Otherwise, you also initialize it, i.e. assign that variable a value. When you declare a variable using `var`, you can re-assign that variable any time later. There is no restriction that could prevent you from changing your variables declared with `var`.

```JavaScript
// Declare var variable
var myVariable

// Initialize myVariable variable
myVariable = 55


// Declare and initialize myVariable variable
var mySecondVar = 'JavaScript'

// Access the value of mySecondVar variable
mySecondVar
// 'JavaScript'


// Re-assign myVariable variable
// Change the value of myVariable variable
mySecondVar = 'TypeScript'

// Access the value of mySecondVar variable
mySecondVar
// 'TypeScript'
```

When you declare new variable using `var` make sure to not to use the same name for another variable, declared in the same scope. Otherwise, it could happen that you declare new variable that uses the same name as another variable you declared earlier. If both variables are either in a global, or in the same local, scope the newer will overwrite the older.

So, make sure to either use different names or different scopes. Also remember that `var` don't work with block scope. So, creating two variables with the same name, one in a global scope and one in a block scope, will lead to collision. The newer variable will again overwrite the older.

```JavaScript
// Accidentally overwriting variables
// Declare myVariable
var myVariable = 'I am the first myVariable.'

// Declare another variable
// using the same name you used previously
var myVariable = 'I am the second myVariable.'

// Access the value of myVariable variable
myVariable
// 'I am the second myVariable.'


// Var variables and block scope
// Create global variable myVar
var myVar = 'I am global variable.'

if (true) {
  // Create another variable myVar
  // inside a block scope created by if...else statement
  // This variable will overwrite the first, global, myVar variable
  var myVar = 'I am inside an if...else statement.'
}

// Access the value of myVariable variable
myVar
// 'I am inside an if...else statement.'
```

## Let

The second type of variable is `let`. This type of variable is new. It was added to JavaScript with ES6 specification. The `let` variable works in a similar way to `var`. Similarly to `var`, with `let` you can also either declare a variable first and initialize it later or you can declare it and initialize it and the same time.

Also similarly to `var`, when you declare variable with `let` you can change it, re-assign it, any time you want. There is, again, no restriction that could prevent you from changing your variables declared with `let`.

```JavaScript
// Declare let variable
let myLetVariable

// Initialize myLetVariable variable
myLetVariable = 'JavaScript'


// Declare and initialize mySecondLetVariable variable
let mySecondLetVariable = 'ECMAScript'

// Access the value of mySecondLetVariable variable
mySecondLetVariable
// 'JavaScript'


// Re-assign mySecondLetVariable variable
// Change the value of mySecondLetVariable variable
mySecondLetVariable = 'ES6'

// Access the value of mySecondVar variable
mySecondLetVariable
// 'ES6'
```

About the differences. As we discussed in the section about JavaScript variables and scope, `let` variables are restricted to block scope. `let` variables are not accessible outside the block they were declared in. So, when you use variables with the same name, one in a block scope and the other outside it, you don't have to worry about one overwriting the other.

```JavaScript
// Let variables and block scope
// Create global variable myLetVariable
let myLetVariable = 'I am global let variable!'

if (true) {
  // Create another variable myLetVariable
  // inside a block scope created by if...else statement
  // This variable will NOT overwrite
  // the first, global, myLetVariable variable
  let myLetVariable = 'I am let inside an if...else statement!'
}

// Access the value of myLetVariable variable
// The value will be the same
// because the myLetVariable inside
// if...else statement had no effect
// outside the block scope created
// by the if...else statement
myLetVariable
// 'I am global let variable!'
```

## Const

Similarly to `let`, `const` is also new addition to JavaScript, added in ES6 specification. Another thing `const` variables share with `let` is that they are also restricted to block scope. So, when you declare a variable using `const` inside a block, it will be visible, and also accessible, only inside that block.

However, this is where the similarity with `let` ends. The first difference is that, with `const`, you can only declare a variable and initialize it the same time. You can't declare a variable and initialize it later. JavaScript variables declared with `const` are constants. They can't be changed, or re-assigned, later.

For this reason, it is also not possible to declare `const` variables and initialize them, assign them a value, later. If that, JavaScript will throw a syntax error about missing initializer in const declaration. If you try to change `const` variable, JavaScript will throw type error about assignment to constant variable.

So, remember, when you use `const` variables, you have to initialize them right when you declare them. And, you can't re-assign these variable later.

```JavaScript
// Declare const variable
const myConstVariable = 'I am a constant.'

// Access the value of mySecondLetVariable variable
myConstVariable
// 'I am a constant.'


// Try to re-assign myConstVariable variable
myConstVariable = 'I am ... an updated constant.'
// TypeError: Assignment to constant variable.

// Access the value of myConstVariable variable
myConstVariable
// 'I am a constant.'


// Const variables and block scope
// Create global variable myConstVariable
const myConstVariable = 'I am global const variable!'

if (true) {
  // Create another variable myConstVariable
  // inside a block scope created by if...else statement
  // Similarly to let, this variable will also NOT overwrite
  // the first, global, myConstVariable variable
  const myConstVariable = 'I am const inside an if...else statement!'
}

// Access the value of myConstVariable variable
// The value will be the same
// because the myConstVariable inside
// if...else statement had no effect
// outside the block scope created
// by the if...else statement
myConstVariable
// 'I am global const variable!'
```

### Partially immutable

I mentioned that it is not possible to re-assign `const` variables. That's true. Some developers also think that `const` variables, or their values, are immutable. This is not true. While you can't re-assign `const` you can change its value. Well, partially. You can't change the value of `const` if the value is a [primitive data type].

For example, if the value of `const` is a `number` or `string`, you can't change it. You can't change that number, or string, into a different number, or string. However, if the value of `const` is an [object] you can change properties of that object. Or, if it is a collection such as [array] you can change the content of that `array`.

That said, that doesn't mean you can change the object, or array, itself by re-assigning it. You can't. You can change only the content of that object or array stored inside a `const`.

```JavaScript
// Const variables and primitive data types
// Create const variable holding a string
const myConstVariable = 'I am a const variable.'

// Try to change the value of myConstVariable, re-assign it
myConstVariable = 'I am updated const.'
// TypeError: Assignment to constant variable.


// Const variables and arrays
// Create const variable holding an array
const myArray = [0, 1, 2, 3]

// Try to change the value of myArray, re-assign it
myArray = [4, 5, 6, 7]
// TypeError: Assignment to constant variable.


// Try to change the items inside myArray array
myArray[0] = 'one'
myArray[1] = 'two'
myArray[2] = 'three'
myArray[3] = 'four'

// Access the value of myArray variable
// Hint: Value of myArray, the items
// inside the array will be different!
myArray
// [ 'one', 'two', 'three', 'four' ]


// Const variables and objects
// Create const variable holding an object
const myObj = {
  name: 'Tony',
  age: 32
}

// Try to change the value of myObj, re-assign it
myObj = {
  name: 'Francis',
  age: 25
}
// TypeError: Assignment to constant variable.

// Try to change the properties and values myObj object
myObj.name = 'Andrew'
delete myObj.age
myObj.isHappy = true

// Access the value of myObj variable
// Hint: Properties and values of myObj
// inside the object will be different!
myObj
// {
//   name: 'Andrew',
//   isHappy: true
// }
```

## Naming variables

You know how to declare, initialize and re-assign JavaScript variables. You also know what types of variables can you use. The last thing you need to know is how to create a valid variable name. Fortunately, variable names are very flexible and here are only three rules you have to follow.

First, a variable name can start with a letter (lowercase and uppercase), underscore `_`, or dollar sign `$`. Second, variable name can't start with a number. However, it is allowed to use numbers in variable names after the first letter, as well as letters (lowercase and uppercase), underscores, or dollar signs.

Third, don't use any of JavaScript's reserved keywords. If you break any of those rules, JavaScript will throw a syntax error and your code will fail to run.

```JavaScript
// Example of valid variables names
let camelCased = 'first word is lowercase any additional word starts with uppercase letter'
let go2go = 'letters with numbers, but not starting with numbers'
let JAVASCRIPT_IS_AWESOME = 'uppercase letters with underscores'
let _Language_ = 'starting and ending with underscore, containing letters'
let $_$ = 'dollar signs and underscores'
let $_foo3 = 'mix of dollar sign, underscores, letters and numbers'
let _12foo = 'starts with underscores, contains numbers and letters'
let _ = 'contains only underscore'
let $ = 'contains only dollar sign'


// Example of invalid variables names
let some% = 'Don\'t use percentage symbol'
let 11years = 'Don\'t start with number(s)'
let function = 'Don\'t use reserved keywords'
let some-var = 'Don\'t use dashes'
let one variable = 'Don\'t use spaces'
```

## Conclusion: Introduction to JavaScript Variables

Congratulations! You've just finished this tutorial on JavaScript variables. By now, you know what are variables and how to declare, initialize, re-assignment and access them. You also know how to use `var`, `let` and `const` and how each of these types works with scope.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[function]: https://blog.alexdevero.com/javascript-functions-pt1/
[if...else]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/if...else
[for]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for
[while]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/while
[primitive data type]: https://blog.alexdevero.com/javascript-basics-data-types-pt1/
[object]: https://blog.alexdevero.com/javascript-objects-pt1/
[array]: https://developer.mozilla.org/en-US/docs/Glossary/array

<!--
### Meta:
-
-->

<!--
#### Resources:
-
-->
