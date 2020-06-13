# JavaScript Functions - All You Need to Know Pt.3
In the world of JavaScript functions there are topics that may sound more difficult than they are. This article will help you understand them. Learn about advanced topic such as recursions, immediately-invoked functions, callbacks and also the latest arrival, arrow functions.<!--more-->
<!--
Table of Contents:
## Recursive JavaScript functions, aka recursions
### Recursive JavaScript functions in practice
## Immediately-invoked functions
## Callback functions
## Arrow functions
### Single-line and multi-line arrow functions
### Immediately-invoked arrow functions
### Arrow functions and this
## Closures
## Conclusion: JavaScript Functions
-->

JavaScript Functions - All You Need to Know [Part 1].

JavaScript Functions - All You Need to Know [Part 2].

## Recursive JavaScript functions, aka recursions

When it comes to JavaScript functions there are few topics that frequently confuse beginners. One of these topics are recursions, also called recursive functions. So, what is this "recursive" thing all about? Recursion is a technique for repeating some operation over and over again until it arrives at a result.

The way recursion is done is by creating a function that calls, or returns, itself inside itself. Then, when you invoke the function, it will call, and re-invoke, itself as many times as necessary. Or, infinitely if you forget to add some terminal case. Terminal case is a condition that causes the function to stop when the condition is met.

Interestingly, in some programming languages recursion is the main way, or at least, one of the often used ways, for looping. This is not the case in JavaScript. However, that doesn't mean that you can't use recursions in JavaScript. You can, with JavaScript functions. And, it also doesn't mean that using recursion is bad.

In fact, there are situations where using recursions is favorable. For example, doing some math operations, sorting and traversing nodes of complex or non-linear data structures. In these, and other cases, recursion is one of the most effective approaches. This is also why you may hear about recursions often.

Another upside of recursions is that there are easy to test. They are easy to test because it is easy to write them as [pure functions]. Pure functions are functions that 1) always return the same value for the same argument(s). This makes the function predictable, i.e. you don't have to guess what happens given specific input.

If you use the same input over and over again, like one hundred times, it will always return the same output, i.e. one hundred times. 2) has no side effects. Having no side effects means that function doesn't change local, or global, variables. So, when you invoke that function you don't have to worry about what other parts of code it may change.

In case of recursion, both these conditions are true. They consistently return the same value for the same input. They also don't have any side effects. They don't change any external variables. Depending on what you do, you may never need to use recursions. Maybe just to gain some street cred among your colleagues.

### Recursive JavaScript functions in practice

That said, it is still good to know at least how may recursions look like. This will help you recognize it in the code. It can also help you understand how it works and how to use it. A very good use case for recursion is factorial. Factorial is about multiplying a number again and again by each preceding integer, all the way down to one. Factorial of 5 is 5 x 4 x 3 x 2 x 1.

So, how can you use JavaScript function to handle this, to create function that will use recursion to calculate factorial? First, you will need to create a function. Let's call it `calcFactorial`, using some [good naming practices]. This function will take one parameter, some number for which you want to calculate the factorial.

Inside this function, you will use `if else` statement. This statement will check if the number, passed as argument, is bigger than 0. If the number is bigger that 0 it will multiply it by the value returned by `calcFactorial`, after being subtracted by 1. If it is not bigger than 0, it will return 1, and do nothing more.

This one is optional. If you want to make your `calcFactorial` function foolproof, you can also add one more `if else` statement to check if the number passed as argument is indeed a number. If it is not, it will return some error message and terminate the function. Otherwise, it will proceed.

```js
// Factorial example
// Create function for calculating factorial
function calcFactorial(num) {
  // Optional: check for numbers
  if (typeof(num) !== 'number') return 'The num must be a number.'

  if (num > 0) {
    // If num is bigger that 0
    // multiply the num by returned value
    // of calcFactorial subtracted by 1
    return (num * calcFactorial(num - 1))
  } else {
    // This is the terminal case
    // If value is 0, return 1, and do nothing after it
    return 1
  }
}

// Calculate factorial of 11
calcFactorial(11)
// 39916800

// Try to invoke calcFactorial with string
calcFactorial('152')
// 'The num must be a number.'
```

Another good example of recursion is creating a function that will work as a countdown. Similarly to the recursion function, this one will also take a number as a parameter.

```js
// Create function for countdown
function countdown(num) {
  // Optional: check for numbers
  if (typeof(num) !== 'number') return 'The num must be a number.'

  if (num > 0) {
    // If num is bigger that 0
    // log the current value of num
    console.log(num)

    // Then return the countdown function itself,
    // passing num subtracted by 1 as an argument
    return countdown(num - 1)
  } else {
    // This is the terminal case
    // If value is 0, return current value of num
    // and do nothing after it
    return num
  }
}

// Countdown from 10
countdown(10)
// 10
// 9
// 8
// 7
// 6
// 5
// 4
// 3
// 2
// 1
// 0
```

As you can see on both examples, our functions indeed meet both conditions for being pure. First, they always return the same value for the same argument(s). It never happens the factorial function returned a different output for the same input, or number. The same applies to the countdown function.

What about the second condition? Neither of these functions has side effects. They don't make any changes to outside environment. That's it for recursive JavaScript functions.

## Immediately-invoked functions

Another frequently mentioned thing, in the terms of JavaScript functions, are immediately-invoked functions. These functions are also referred to via its acronym IIFE. Before we get into this, there is one thing you must understand. In the past, there was only one way to declare variables in JavaScript, using [var].

There was no `let` and `const`. The problem with `var` is that it doesn't work with block scope. It works only with global or function scope. JavaScript developers needed some way to make `var` work in a block scope. So, they created it. They used JavaScript functions to create emulated scope that allowed to use `var` in block-like scope.

Nowadays, this is no loner need thanks to ES6 and `let` and `const`. Nonetheless, it can happen that you will encounter immediately-invoked functions from time to time. So, it is good to know how they look and how to use them. Creating immediately-invoked function is simple. You use function expression to create new function, i.e. `function() {}`.

Note that you are not assigning that function to any variable. Next, you wrap this function with parenthesis and add another set of parenthesis to call it, i.e. `(function() {})()`. Why this? When JavaScript encounters "function" keyword in your code, it thinks you want to create a new function using [function declaration].

The problem is that function declaration must have a name. What if there is none? When there is no name, JavaScript will throw an error: `SyntaxError: Unexpected token`. This makes sense because it expects some name. It doesn't expect a parenthesis so soon. What if you try to solve this problem by giving the function a name?

It will not work either. What's the problem here? When you create a function with function declarations JavaScript will not allow you to call that function immediately, i.e. `function myFunc() {}()`. This will lead to another syntax error: `SyntaxError: Unexpected token`. The only way around this problem is wrapping the function with parenthesis, i.e. `(function() {})()`.

Doing this tells JavaScript that the function you are creating is created in the context of another expression. Now, we are no longer talking about function declaration, but about [function expression]. With function expression we no longer need any name for our function and we can also call it immediately.

Wrapping a function with parenthesis is not the only way to create immediately-invoked functions in JavaScript. You can also use either `!` (NOT operator) or `+` (unary plus) and put it right at the start of the function, i.e. `!function() {}()` or `+function() {}()`. Both will work. However, the approach with parenthesis is more common.

One more thing. It is not necessary to put the second pair of parenthesis, those that will invoke the function, after the parenthesis you used to wrap the function. You can also put them inside the wrapping parenthesis, right after the closing curly bracket, i.e. `(function() {}())`.

As I mentioned, `var` variables work only with global and function scope. Creating JavaScript functions this way, as immediately-invoked, creates new function scope, something like an emulation for a block scope. This allows you to have `var` variables restricted, or visible, only where you want them, inside the newly created function scope.

```js
// Creating IIFE example no.1:
// invoking parenthesis outside wrapping parenthesis
(function() {
  // ... some code
})()


// Creating IIFE example no.2:
// invoking parenthesis inside wrapping parenthesis
(function() {
  // ... some code
}())


// Creating IIFE example no.3:
// using ! (NOT operator)
!function() {
  // ... some code
}()


// Creating IIFE example no.4:
// Using + (unary operator)
+function() {
  // ... some code
}()


// This will not work
function() {
  // ... some code
}()
// SyntaxError: Unexpected token

// This will also not work
function myFunc() {
  // ... some code
}()
// SyntaxError: Unexpected token
```

## Callback functions

Another interesting thing in the world of JavaScript functions are callback functions. The idea here is that you pass a function as an argument to another function when you call it. And, you also expect that the function, you passed in as an argument, will be sooner or later called, or "called back", inside the function you called.

This may sound weird, but it is like passing value, reference to a variable or an object. This time, you are passing a function and, instead of processing that function, you call it. Let's take a look at simple example. Imagine you have a function `eatFood()`. This function will take two parameters.

The first parameter will be the food you are about to eat. The second parameter will be a callback function, function you want to "call back" inside that `eatFood()` function. The function we will pass in will be `washTheDishes()` function. The `washTheDishes()` function, will log a message about washing dishes in 1-second intervals, for five seconds.

The `eatFood()` function will log a message about what food we are eating. When we are done with eating, we will call the callback function. In this case, the `washTheDishes()` function.

```js
// Create washTheDishes function
// This function will be used as a callback function
function washTheDishes() {
  // Wash the dishes, 1 plate per second
  let washingInterval = setInterval(() => {
    console.log('Washing the dishes...')
  }, 1000)

  // After 5 seconds
  setTimeout(() => {
    // Stop washing dishes
    clearInterval(washingInterval)

    // Show message
    console.log('Dishes are clean!')
  }, 5000)
}


// Create eatFood function
// This function will take two parameters - food and callback function
function eatFood(food, callbackFunc) {
  // Eat the food
  console.log(`Eating ${food}.`)

  // HERE IS THE CALLBACK FUNCTION:
  // Call the callback function (function passed as an argument)
  callbackFunc()
}

// Call eatFood function
// passing 'steak', and washTheDishes function as arguments
eatFood('steak', washTheDishes)
// 'Eating steak.'
// 'Washing the dishes...'
// 'Washing the dishes...'
// 'Washing the dishes...'
// 'Washing the dishes...'
// 'Washing the dishes...'
// 'Washing the dishes...'
// 'Dishes are clean!'
```

This is how callback functions look like, and work, in a nutshell. One function, passed into another function, that is called later from that another function. Another "mysterious" thing in the world of JavaScript functions that is simpler than it may sound.

## Arrow functions

Arrow functions are the latest addition to the world of JavaScript functions. Arrow functions were added to JavaScript in ES6 specification. Since then, they got a lot of traction. Some JavaScript developers love them, some hate them. This relationship is very similar to [JavaScript classes].

Some developers prefer arrow functions over regular JavaScript function because they use simple and concise syntax. This is also one reason some developers hate arrow functions. One argument against arrow function is that they are hard to read. There is some truth on this. The syntax of arrow functions is really short and simple.

It consists of parenthesis (for parameters), equal and right angle sign (`=>` or arrow), and curly brackets (for block of code), i.e. `() => { someExpression }`. Well, the parenthesis and curly brackets are actually optional. You don't have to use parenthesis if arrow function takes one parameter. And, if arrow function is a one-liner, you don't have to use curly brackets.

If, on the other hand, arrow function takes either no or two or more parameters the parenthesis around parameters are required. Omitting them will cause a syntax error. The same for curly brackets. If arrow function is a multi-line the curly braces are required. So, the only thing that is really required is the `=>`, arrow.

So far, you can create arrow functions only with function expressions, i.e. `let myFunc = () => someExpression`. Function declaration will not work, i.e. something like `myFunc() => { someExpression }` will cause syntax error. Note: we already used arrow functions in the example with `washTheDishes()` function, section "callback functions". Hint: look at the `setInterval` and `setTimeout`.

```js
// Create multi-line arrow function without any parameters
let myArrowFunc = () => {
  // ... some code
}


// Create multi-line arrow function with one parameter
let myArrowFunc = (param) => {
  // ... some code
}

// or
// Parenthesis are optional with one parameter
let myArrowFunc = param => {
  // ... some code
}

// Similar to "standard" function
let myArrowFunc = function() {
  // ... some code
}


// Create multi-line arrow function with multiple parameters
let myArrowFunc = (paramOne, paramTwo, paramThree) => {
  // ... some code
}


// Create one-line arrow function without any parameters
let myArrowFunc = () => // ... some code

// Is the same as:
let myArrowFunc = () => {/* ... some code */}


// Create one-line arrow function with one parameter
let myArrowFunc = param => // ... some code

// Is the same as:
let myArrowFunc = param => {/* ... some code */}


// Create arrow function with multiple parameters
let myArrowFunc = (paramOne, paramTwo, paramThree) => // ... some code

// Is the same as:
let myArrowFunc = (paramOne, paramTwo, paramThree) => {/* ... some code */}
```

### Single-line and multi-line arrow functions

One interesting thing on arrow functions is that you can omit the curly brackets if the function is single-line. If it is single-line, the function will automatically evaluates the expression, the right side. You can imagine a `return` statement right after the arrow symbol, i.e. `let myArrowFunc = () => return ...`, but don't use it literally.

This is important to remember when you use arrow functions. When you accidentally use a one-liner arrow function, and add `return` statement, JavaScript will throw a syntax error: `SyntaxError: Unexpected token`. You can use the `return` statement only if arrow function is a multi-line.

```js
// This - single-line and implicit return
let myArrowFunc = () => /* ... some code */

// Is similar to this - multi-line and explicit return
let myArrowFunc = () => {
  return // ... some code
}


// This works - single-line and no explicit return
let myArrowFunc = () => /* ... some code */

// This also works - multi-line + return
let myArrowFunc = () => {
  return // ... some code
}

// This also works - no return at all
let myArrowFunc = () => {
  // ... some code
}


// This doesn't work - single-line and explicit return
let myArrowFunc = () => return /* ... some code */
```

### Immediately-invoked arrow functions

Similarly to "standard" JavaScript functions, arrow functions can be also created as immediately-invoked. All you need to do is omit the `function` keyword and add the arrow symbol (`=>`), i.e. `(() => {})()`.  When you use immediately-invoked arrow functions you have to put the last pair of parenthesis, for calling the function, outside the wrapping parenthesis.

If you try to put those parenthesis inside it, right after the closing curly bracket, JavaScript will throw a syntax error. So, no `(() => {}())`. The same will happen if you use `!` (NOT operator) or `+` (unary plus). Both will lead to an error. Hence, the only valid way to create a immediately-invoked arrow function is using the wrapping parenthesis, and keeping the invoking parenthesis outside wrapping parenthesis.

```js
// Immediately-invoked arrow function
// This will work
(() => {/* some code */})()


// This will not work - invoking parenthesis inside wrapping parenthesis
(() => {/* some code */}())

// This will also not work - unary plus
+() => {/* some code */}()

// This will also not work - NOT operator
!() => {/* some code */}()
```

### Arrow functions and this

Another significant difference between "standard" JavaScript functions and arrow functions is a lack of `this`. When you use JavaScript functions, the value of `this` will depend on how you called that function. It can be a new object if you called the function as a [Function constructor].

In case you are using strict mode, the value of `this` will be `undefined`. If you called the function inside an object, as an object method, the value of `this` will be the base object. The same happens if you called the function inside a class, as a class method. Then, the value of `this` will be the base class.

This doesn't apply to arrow functions. Arrow functions don't have their own `this`. They have a "lexical scope". When you try to access `this` inside an arrow function, an arrow function will search for the value of `this` in its enclosing scope. Put simply, no matter how you call them, arrow functions always inherit `this` from the outside.

```js
// 'this' in functions example
// Create Function constructor
function MyFunctionConstructor() {
  // Add some property
  this.name = 'My Function Constructor'

  // Log this
  console.log(this)
}

// Create instance of Function constructor
const myFunc = new MyFunctionConstructor()

// Create arrow function
const myArrowFunc = () => {
  // Log this
  console.log(this)
}

// Call myFunc instance
myFunc
// MyFunctionConstructor {name: 'My Function Constructor'}

// Call myArrowFunc
myArrowFunc()
// Window


// 'this' in object example
// Create object with title and names properties and one function
// that will loop over names and return a short message with current name and the title of the object

// ! This will not work: using "standard" function inside forEach()
// This will not work because function in forEach
// has its own 'this' that defaults to 'undefined'
const obj = {
  title: 'My object',
  names: ['Tony', 'Cindy', 'Trevor'],
  logNames() {
    this.names.forEach(function(name) {
      // This WILL NOT work:
      // TypeError: Cannot read property 'title' of undefined
      // 'this' here will be 'undefined'
      // So, 'this.title' will throw an error
      console.log(`The name of object "${this.title}" is ${name}.`)
    })
  }
}

obj.logNames()
// TypeError: Cannot read property 'title' of undefined (in "${this.title}")


// This will work: using arrow function inside forEach()
const obj = {
  title: 'My object',
  names: ['Tony', 'Cindy', 'Trevor'],
  logNames() {
    // This WILL work:
    this.names.forEach((name) => {
      // 'this' here will be the base object - obj variable
      // So, 'this.title' will correctly return 'My object'
      console.log(`The name of object "${this.title}" is ${name}.`)
    })
  }
}

obj.logNames()
// 'The name of object "My object" is Tony.'
// 'The name of object "My object" is Cindy.'
// 'The name of object "My object" is Trevor.'


// One more object example:
// This will also NOT work because arrow function does not have
// its own this - it inherits it from parent (function) context (global object).
const obj = {
  title: 'My object',
  // Use arrow function as object method
  logTitle: () => {
    // Log the title
    console.log(this.title)
  }
}

obj.logTitle()
// TypeError: Cannot read property 'title' of undefined

// This WILL work
// 'this' here, inside standard function in an object,
// will refer to the 'obj' itself, which has 'title' property
const obj = {
  title: 'My object',
  // Use standard function as object method
  logTitle: function() {
    // Log the title
    console.log(this.title)
  }
}

obj.logTitle()
// 'My object'


// 'this' in class example
// Create a class Person with two properties, name and languages
// and one method that will loop over languages and return a short message with person's name and current language

// ! This will not work for the same reason as mentioned in the previous example:
// This will not work because function in forEach
// has its own 'this' that defaults to 'undefined'
class Person {
  constructor(name, languages) {
    this.name = name
    this.languages = languages
  }

  sayHi() {
    this.languages.forEach(function(language) {
      // This WILL NOT work:
      // TypeError: Cannot read property 'name' of undefined
      // 'this' here will be again 'undefined'
      // So, 'this.name' will throw an error
      console.log(`Hi, my name is ${this.name} and I like ${language}.`)
    })
  }
}

// Create instance of Person class
const matthew = new Person('Matthew', ['JavaScript', 'Python', 'C++'])

// Call sayHi() method
matthew.sayHi()
// TypeError: Cannot read property 'name' of undefined


// This will work: using arrow function inside forEach()
// Create Person class
class Person {
  constructor(name, languages) {
    this.name = name
    this.languages = languages
  }

  sayHi() {
    this.languages.forEach((language) => {
      console.log(`Hi, my name is ${this.name} and I like ${language}.`)
    })
  }
}

// Create instance of Person class
const matthew = new Person('Matthew', ['JavaScript', 'Python', 'C++'])

// Call sayHi() method
matthew.sayHi()
// 'Hi, my name is Matthew and I like JavaScript.'
// 'Hi, my name is Matthew and I like Python.'
// 'Hi, my name is Matthew and I like C++.'
```

In the examples above, you can see that the value of `this` in arrow function is always the value of `this` in the outer scope. In the first example, it is a `Window` object, or global `this`. In the second example, the value of `this` is the `obj` object. Lastly, in the third example, the value of `this` is the `Person` class.

The fact that arrow functions don't have their own `this` also means you can't use them as Function constructor, such as the `MyFunctionConstructor()` in the example above.

## Conclusion: JavaScript Functions

Congratulations! You've just finished the third and last part of this mini series focused on JavaScript functions. In this part, you've learned about recursions, immediately-invoked functions, callbacks and arrow functions. I hope you enjoyed this article and learned something new, something that will help you get better in JavaScript.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Part 1]: https://blog.alexdevero.com/javascript-functions-pt1/
[Part 2]: https://blog.alexdevero.com/javascript-functions-pt2/
[pure functions]: https://en.wikipedia.org/wiki/Pure_function
[good naming practices]: https://blog.alexdevero.com/javascript-functions-pt2/#functions-and-naming-conventions
[var]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var
[function declaration]: https://blog.alexdevero.com/javascript-functions-pt1/#function-declaration-and-function-expression
[function expression]: https://blog.alexdevero.com/javascript-functions-pt1/#function-declaration-and-function-expression
[JavaScript classes]: https://blog.alexdevero.com/javascript-classes-pt1/
[Function constructor]: https://blog.alexdevero.com/javascript-functions-pt2/#function-constructor

<!--
### Meta:
-
-->

<!--
#### Resources:
-->
