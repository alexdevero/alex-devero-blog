# JavaScript Functions - All You Need to Know Pt.1
Functions are fundamental part of JavaScript programming language. Every JavaScript developer should know how to work with them. This tutorial will teach you the basics of JavaScript functions. You will learn how to create functions and how to use parameters and arguments.<!--more-->
<!--
Table of Contents:
## The Basic
## Function declaration and function expression
## Calling or invoking functions
## Function parameters
## Functions and default parameters
## Functions, parameters and arguments
## The arguments object
## Functions are... objects
## Return
## Conclusion: JavaScript Functions

JavaScript Functions - All You Need to Know [Part 2].
-->

## The Basic

What are functions? One way to think about functions is as building blocks of programs. You can also think about them as a subprograms that are created with the purpose to do specific tasks. The main reason developers use functions is because they allow you to re-use chunks of code, without the need to write the code over and over again.

Let's say you've just created a function with some code inside it. Now, when you want to execute the code inside that function all you need to do is to call that function. "Calling a function" is also called "invoking a function". Another great thing on functions is that you can also pass values into them.

This means that even though the code inside the function remains the same what happens after calling the function can differ. What's more, you call also pass another function as a value and then call that function you passed inside the function.

## Function declaration and function expression

In JavaScript, there are two ways to create functions. One is by using function declaration. The second is by using function expression. When you want to create a function using function declaration you start with `function` keyword, followed by the name of the function, followed by parenthesis with parameters and curly brackets with code to be executed.

When you define function using function declaration it will be [hoisted]. Put simply, you can call that function before you define it in your code. JavaScript will move the function declaration to the top of the scope during the runtime. When you run the code, the function is actually available before you call it.

```js
// Function declaration example
function myFunction() {
  // some code
}


// Function declaration and hoisting
// Call myFunction before you define it
myFunction()
// 'I run!'

// Create myFunction
function myFunction() {
  console.log('I run!')
}
```

In case of function expressions, you define either named or anonymous function. Using function expressions allows you to assign the function to a variable. When some function is anonymous it means that that function has no name. Unlike function declaration, function expressions are not hoisted.

A function expression is created only when the execution reaches its location in your code. It is this moment from which it is usable, not sooner. Keep this in mind when you use function expression. You can't use functions created with function expression before you define them. About the syntax.

When you want to use function expression you start with `let`, `const` or `var` keyword to declare a variable. Then, you add equal sign followed by `function` keyword, followed by parenthesis with parameters and curly brackets with code to be executed.

```js
// Function expression example
const myFunction = function() {
  // some code
}


// Function expression and hoisting
// Call myFunction before you define it
myFunction()
// ReferenceError: myFunction is not defined

// Create myFunction
const myFunction = function() {
  console.log('Let\'s try this.')
}
```

## Calling or invoking functions

Function is not executed until you call it, or invoke it. In order to call, or invoke, a function you must reference it using the function name, followed by an open and closed parenthesis (`()`). If a function has some parameters (more about this in the next section) you pass them inside those parenthesis.

```js
// Example no.1: Calling, or invoking, function with no parameters.
// Define a function printMessage using function declaration
function printMessage() {
  return 'Hello from printMessage function!'
}

// Call or invoke printMessage function
printMessage()
// 'Hello from printMessage function!'


// Or, using function expression
const printMessage = function() {
  return 'Hello from printMessage function!'
}

// Call or invoke printMessage function
printMessage()
// 'Hello from printMessage function!'


// Example no.2: Calling, or invoking, function with parameters.
function returnDouble(num) {
  return num * 2
}

// Call or invoke returnDouble function
returnDouble(98)
// 196


// Or, using function expression
const returnDouble = function(num) {
  return num * 2
}

// Call or invoke returnDouble function
returnDouble(656)
// 1312
```

## Function parameters

Functions allow you to pass data into them using parameters. These parameters are also called function arguments. When you define a function that accepts a parameter, you can call it without passing them. The function will still execute. The problem is that missing parameter can cause some things, that depend on that parameter, to break.

So, when you specify parameters for functions make sure to also pass the necessary data when you call those functions. When it comes to parameters, there is ([theoretically]) no limit to how many of them you can use. The only thing to remember, if you want to use multiple parameters, is to separate them with comas.

```js
// Create function that accepts one parameter - name
function greeting(name) {
  return `Hello ${name}! Nice to meet you.`
}

// Call getting function, passing some name
greeting('Tommy')
// "Hello Tommy! Nice to meet you."


// Call getting function without passing anything
greeting()
// "Hello undefined! Nice to meet you."


// Create function that accepts four parameters - name, age, sex, nationality
function createUser(name, age, sex, nationality) {
  // do something
}

createUser('Nikolaj Chernov', 38, 'male', 'Russian')
```

## Functions and default parameters

When you specify parameter for function its default value will be `undefined`. This value will change when you call that function and pass some data to it. This is why, in the example above, calling `greeting()` function without passing any name led to `undefined` in the returned message.

Fortunately, there is now a way to prevent this from happening. Since the release of ES6 specification you can use something called default parameters. Put simply, you can specify function parameter and set it to some default value. Then, when you call that function without passing anything that parameter will no longer be `undefined`.

Instead, that parameter will contain the default value you specified earlier. If you do, pass something, JavaScript will use the data you passed and ignore the default. Using default parameters are very useful. They can help you avoid issues caused by forgetting to pass some data to the function.

The syntax for default parameters is very easy. When you specify the parameter, inside parenthesis, you follow it with equal sign and something. This "something" will be the default value for that parameter, i.e. `function myFunction(myParam = 'Default value') {}`.

```js
// Create greeting function with name parameter
// that has default value of 'Anonymous'
function greeting(name = 'Anonymous') {
  console.log(`Hello ${name}!`)
}

// Call greeting() without passing any name
greeting()
// 'Hello Anonymous!'

// Call greeting() with some name
greeting('Toby')
// 'Hello Toby!'


// Using default parameters with parameters no.1
// Set 55 to be a default value for parameter b
function doTheMath(a, b = 55) {
  return a * b
}

doTheMath(5)
// 275


// Using default parameters with parameters no.2
// Set default values for all parameters
function introduction(name = 'Joe', sex = 'male', age = 28) {
  return `Hi, my name is ${name}, I am ${sex} and I am ${age} years old.`
}

introduction('Sandra', 'female')
// 'Hi, my name is Sandra, I am female and I am 28 years old.'
```

## Functions, parameters and arguments

When it comes to functions, there is one thing that often confuses developers. This thing are function parameters and arguments. The problem is that both names actually talk about the same thing. They both talk about function parameters. It is no wonder many developers use these terms interchangeably.

However, there is a difference. The difference, and way to distinguish between parameters and arguments, is when you use these terms. When you are defining functions, you talk about function parameters. Here, parameters are the names created in the function definition. So, it is correct to say that some function accepts, one or more "parameters".

Something else is when you talk about calling, or invoking, a function. Here, arguments are the values the function you invoke, or call, receives. So, the correct term to use is "argument", i.e. passing something to function as an argument, or calling a function with argument.

```js
// Function parameters
// Use when defining a function
// Function with parameter 'param'
function funcOne(param) {}

// Or
const funcTwo = function(param) {}


// Function arguments
// Use when calling or invoking a function
// Call funcOne with 'This is an argument.' passed as an argument
funcOne('This is an argument.')

// Or
// Call funcTwo with 'This is also an argument.' passed as an argument
funcTwo('This is also an argument.')
```

## The arguments object

Since we are talking about parameters and arguments, there is one interesting you should know. Every function contains something called arguments object. This is an object that contains values of all arguments passed to the function. What's more, you can access this object in your code.

The whole object is accessible via `arguments`. When you want to access only some arguments you can use index. This index is based on the position of the argument in argument list (the order in which you passed all arguments to the function). Remember that index in arrays and objects starts with 0.

```js
function createUser(name, age, sex, nationality) {
  console.log(arguments)
  // [object Arguments] {
  //   0: "Thomas More",
  //   1: 43,
  //   2: "male",
  //   3: "American"
  // }

  // Access the first argument
  console.log(arguments[0])
  // "Thomas More"

  // Access the second argument
  console.log(arguments[1])
  // 43

  // Access the third argument
  console.log(arguments[2])
  // "male"

  // Access the fourth argument
  console.log(arguments[3])
  // "American"

  // Check the number of arguments
  console.log(arguments.length)
  // 4
}

createUser('Thomas More', 43, 'male', 'American')
```

## Functions are... objects

This may sound weird, but functions are actually objects. Or, function objects to be more specific. This may sound weird. However, in JavaScript there are only two types of "things". The first one are [primitive types]. The second? Object. In JavaScript, if something is not a primitive type it is an object.

This is why functions are technically objects. Otherwise, they would have to be primitive types, which they are not. Since there is no third type, they are objects. This is a good thing because in JavaScript objects allow you to do a lot of things. Since functions are objects you can do many things with them as well.

For example, you can pass one function into another. Or, you can also return a function from another function. A bit of lingo. When function accepts another function as a parameter, or it returns a function, it is called a [high-order function]. One example of high-order function is JavaScript [map()] method.

```js
// Simple high-order function no.1: function accepting function as a parameter
// Create first function
function doSomething(func) {}

// Create second function
function doSomethingElse() {}

// Call the first function and pass the second
doSomething(doSomethingElse)


// Simple high-order function no.2: function returning function
// Create first function
function doSomething() {
  return 'Do something.'
}

// Create second function
function doSomethingElse() {
  // Call the first function
  return doSomething()
}

// Call the second function
doSomethingElse()
// 'Do something.'
```

## Return

This is another interested thing. In JavaScript, functions always return something, some value. This is true even if you don't explicitly specify any returning value. In that case, if there is no explicitly specified return, the function will return `undefined` (more about [undefined]). Otherwise, it will return the value you specified.

You can specify what should a function return using `return` keyword. When you work with functions and `return` keyword, there is one important thing to remember. Function will stop executing under the conditions. First, there is no more code to execute, including loops. Second, there is a `return` keyword.

This, second condition, is especially important to remember because it means that any code you write after the `return` keyword will never execute. When function encounters `return` keyword it will do two things. First, it will return the thing you want it to return. Second, it will stop execution.

This scenario, when there is a code after `return` keyword, is also called "unreachable code" because it is literally beyond the reach. So, pay attention to when you use the `return` keyword in a function. If you want all the code to be executed, put it at the end of the code block inside the function.

This natural behavior of functions is not bad. It can be actually quite useful. It can help you terminate execution of your code when it is not necessary. For example, by using `if` statement at the top of the function. Based on the condition you can either return, anything or nothing, or let the function to execute the rest of the code.

```js
// Example of function with explicit return
// note: using 'return' keyword
function sayHi() {
  return 'Hello, nice to meet you'
}

sayHi()
// 'Hello, nice to meet you'


// Example of function without explicit return
// note: not using 'return' keyword
function returnNothing() {
  // nada
}

returnNothing()
// undefined


// Example: return or execute function based on condition
function iMightNotReturn() {
  // Random number is 6 stop execution - return nothing
  if (Math.floor(Math.random() * 10) === 6) return

  // Else continue executing the code
}
```

There is another good thing about functions always returning something. You can use function, and function expression, to return a value and save it to a variable.

```js
// Use function expression to create a function
// that takes one parameter, a number,
// and returns that number divided by 2
let divideByTwo = function(number) {
  // return the number divided by 2
  return number / 2
}

// Declare new variable that invokes the divideByTwo function
// and save the value returned by the divideByTwo function
// inside the variable
let age = divideByTwo(39)

console.log(age)
// 19.5
```

## Conclusion: JavaScript Functions

Congratulations! You've just finished the first part of this tutorial focused on JavaScript Functions. Let's do a quick recap. First, you've learned about the basic of JavaScript functions. You've learned about function declaration and function expression and how to use these two to define functions. Next, you've learned how to call, or invoke, functions.

After this, you've learned about function parameters, default parameters, the difference between parameters and arguments and the arguments object and how to use it. Lastly, you've learned about two perks. First, that functions are actually objects, function objects to be more specify. Second, that functions always return something.

Next steps? Revisit what you've learned today and go through code examples we worked with. Make sure you understand everything. If there is something you are not sure about, read it and practice few more times. Otherwise, get ready for the [Part 2].

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
<!-- [Part 2]:  -->
[undefined]: https://blog.alexdevero.com/javascript-basics-data-types-pt2/#undefined
[primitive types]: https://blog.alexdevero.com/javascript-basics-data-types-pt1/
[high-order function]: https://blog.bitsrc.io/understanding-higher-order-functions-in-javascript-75461803bad
[map()]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map
[hoisted]: https://developer.mozilla.org/en-US/docs/Glossary/Hoisting
[theoretically]: https://stackoverflow.com/questions/22747068/is-there-a-max-number-of-arguments-javascript-functions-can-accept

<!--
### Meta:
-
-->

<!--
#### Resources:
- https://www.geeksforgeeks.org/functions-in-javascript/
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions
- https://javascript.info/advanced-functions
-->
