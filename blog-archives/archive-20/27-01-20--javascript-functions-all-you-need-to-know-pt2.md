# JavaScript Functions - All You Need to Know Pt.2
Functions are important part of JavaScript. This tutorial will help you understand them. Learn about how variables, scope and `this` work in the context of JavaScript functions and get a brief introduction to `call()`, `apply()` and `bind()` methods, and how to use them to change value of `this`.
<!--more-->
<!--
Table of Contents:
## Functions, variables and scope
## Functions and this
## Call(), apply() and bind()
## Function constructor
## Rest parameters
## Functions and naming conventions
## Conclusion: JavaScript Functions
-->

JavaScript Functions - All You Need to Know [Part 1].

## Functions, variables and scope

When you work with JavaScript function you have to remember one thing. All variables you declare inside a function will be declared as local variables. This means these variables will be visible only inside that function. If you try to access them outside the function you will get an error about undefined variable. This rule applies to all types of variables, `var`, `let` and `const`.

```js
///
// Local variable example
// Declare logVars function
function logVars() {
  var ex1 = 'I\'m var inside logger function'
  let ex2 = 'I\'m let inside logger function'
  const ex3 = 'I\'m const inside logger function'

  console.log(ex1)
  console.log(ex2)
  console.log(ex3)
}

// Try to access the ex variable
console.log(ex1)
// ReferenceError: ex1 is not defined

console.log(ex2)
// ReferenceError: ex2 is not defined

console.log(ex3)
// ReferenceError: ex3 is not defined

// Invoke logVars function to log ex variable
logVars()
// 'I\'m var inside logger function'
// 'I\'m let inside logger function'
// 'I\'m const inside logger function'
```

On the other hand, functions can access variables declared in the outer scope. These variables are also called global variables. So, if you declare some variable somewhere in your code before function you can access that variable inside that function. What's more. You can also modify global variables, variables that exist in the outer scope, inside functions.

```js
// Define variables in global scope
var name = 'John Doe'
let age = 27
const language = 'English'

// Declare changeVars function
function changeVars() {
  // Access variables in global scope
  console.log(name)
  // 'John Doe'

  console.log(age)
  // 27

  console.log(language)
  // 'English'

  // Change the value of name and age variables in global scope
  name = 'Jack Sawyer'
  age = 31
}

// Invoke changeVars function to log and change some global variables
changeVars()

// Log global scope variables
console.log(name)
// 'Jack Sawyer'

console.log(age)
// 31

console.log(language)
// 'English'
```

When you work with functions and variables there is one thing you must pay attention to. If you declare a variable, and it has the same name as a global variable, the function will ignore the outer, global, variable and work with the local. There are things to do. First, double-check you chose a different name.

Second, make sure if you really want to declare a variable or if you want to access, or modify, existing variable instead. When it comes to variables and global scope, it is a good practice to minimize the use of global variables. It is better to declare your variables inside function where you want to use them, if it is possible.

```js
// Declare global variable someVar
let someVar = 'There will be dragons.'

// Declare readVars function
function readVars() {
  // Declare local variable someVar
  let someVar = 'No dragons in plain sight.'

  // Log the value of local variable someVar
  console.log(someVar)
}

// Invoke readVars function
readVars()
// 'No dragons in plain sight.'

// Log the value of global variable someVar
console.log(someVar)
// 'There will be dragons.'
```

## Functions and this

If there is one thing that cause JavaScript developers a lot of troubles and headaches it is `this`. In case of JavaScript functions, the `this` can cause some headaches as well. When you work with functions and `this` there are two things that can happen. When you use [strict-mode] `this` will reference the global object, or `window`.

On the other hand, when you are in strict mode, the value of `this`, when you access it from the inside of a function, will be [undefined].

```js
// This example 1: This in a non-strict mode
// Declare thisExample function
function logThis() {
  console.log(this)
  // [object Window]

  console.log(this === window)
  // true

  console.log(this === undefined)
  // false
}

// Invoke logThis
logThis()


// This example 2: This and strict mode
// Set strict mode
'use strict'

// Declare thisExample function
function logThisTwo() {
  console.log(this)
  // undefined

  console.log(this === window)
  // false

  console.log(this === undefined)
  // true
}

// Invoke logThisTwo
logThisTwo()
```

## Call(), apply() and bind()

As you know, the value of `this` inside a function, at least in `strict mode`, will be `undefined`. However, this doesn't mean you can't change it. You can. You can change the value of `this` with the help of `call()`, `apply()` and `bind()` methods. The first two, the `call()` and `apply()` are very similar.

The main difference between these two is that `call()` method accepts an argument list. The `apply()` method accepts an array of arguments. The last one, `bind()`, creates a new function that will have the value of `this` set to the first parameter you passed to the `bind()` function.

One important thing about `bind()`. I works only once. `bind()` will not work if you use try to use it again on a function you already "bound". It will always return the first value you passed to the `bind()` function.

```js
// call() example
// Declare function that logs this
function bar() {
  console.log(this)
}

// Invoke bar
bar()
// undefined

// Invoke bar and use call to change the value of this
bar.call(7)
// 7
bar.call('call')
// 'call'


// apply() example
function bar() {
  console.log(this);
}

// Invoke bar
bar()
// undefined

bar.apply(7)
// 7
bar.apply('apply')
// 'apply'


// bind() example
function bar() {
  console.log(this);
}

// Invoke bar
bar()
// undefined

// Create new function using bind and bind this to 7
const bazz = bar.bind(7)

// Invoke new function bazz
bazz()
// 7


// This will not work
// Try to re-bind bazz to 'What?!'
const bazzy = bazz.bind('What?!')

// Invoke bazzy
bazzy()
// 7
// returns the same value you bound to bazz earlier
```

The `call()`, `apply()` and `bind()` methods are advanced and very powerful features of JavaScript. Explaining thoroughly how these methods work, and how you can use them, is beyond the scope of this tutorial. If you want to learn more about these methods I recommend you take a look at Mozilla Developer Network. There is a detailed documentation for [call()], [apply()] as well as [bind()].

## Function constructor

There is another interesting thing you can do with JavaScript functions, that is related to `this`. In the [previous part], you've learned that functions are actually objects, or function objects. You can use functions, or rather [Function constructors] to create new function, or instances of that Function constructor.

The best way to think about Function constructor is to think about it as a blueprint. This is useful when you want to create multiple similar objects with the same properties and methods. Instead of repeating yourself again and again you create just one object, one Function constructor.

Then when you want to create multiple copies, also called instances, of that object you don't have to write all the code again. Instead, you take that Function constructor you created earlier and use it to create its instances. All these instances will automatically inherit all methods and properties the Function constructor contains.

The way you create properties and methods inside the Function constructor is by using `this`. When you want to create new property, you use `this` followed by the property/method name and assign it some value, i.e. `this.propName = 'something'`. In case of methods, the process is similar.

The only difference is that now, you assign a function, instead of a primitive, i.e. `this.methodName = function() {}`. When you want to access some property, or method, that belongs to the Function constructor you use the `this` followed by the property/method name again, i.e. `this.propName`.

One important thing. When you want to create an instance of a Function constructor you have to use `new` keyword, i.e. `let newInstance = new SomeConstructor()`. This is really important to remember. If you forget to use the `new` keyword, you will be changing the global object, instead of changing the instance you've just created.

```js
// Declare Function constructor Book
// That accepts three parameters - title, author, type
function Book(title, author, type) {
  // Create properties from passed parameters
  this.title = title
  this.type = type
  this.author = author

  // Create method that returns info
  // about book created with Book Function constructor
  this.getBookDetails = function () {
    return `${this.title} written by ${this.author}.`
  }
}

// Create instance of Book function
// REMEMBER!: Always use 'new' when calling constructor
const petSematary = new Book('Pet Sematary', 'Steven King', 'Fiction')

// Log details of petSematary
console.log(petSematary.getBookDetails())
// 'Pet Sematary written by Steven King.'


// Create another instance of Book function
// REMEMBER!: Always use 'new' when calling constructor
const warAndPeace = new Book('War and Peace', 'Leo Tolstoy', 'Fiction')

// Log details of warAndPeace
console.log(warAndPeace.getBookDetails())
// 'War and Peace written by Leo Tolstoy.'
```

_A quick side note: It is a good practice to always start the name of the Function constructor with upper-case letter. This will not change how JavaScript compiles your code. However, it will help make your code clearer and readable._

## Rest parameters

Sometimes, you may not know exactly how many parameters someone may pass into a function. Or, it might just be handy to not to limit the number of parameters a function can operate with. Whatever the case is, rest parameters is what you are looking for. Rest parameters allow the function to use all parameters passed into it.

The syntax of rest parameters is very simple. You use three dots followed by the name of the array that will contain all parameters, i.e. `...params`. The name can be anything you want. As I mentioned, you will get all parameters in the form of an array. So, when you want to access those parameters you can uses indices, `map()`, `forEach()`, etc.

```js
// Declare function with rest parameters
// 'allParams' will be the name of the array that contains all parameters
function useRestParams(...allParams) {
  // Get all parameters
  console.log(allParams)
  // [ 5, 8, 9, 6, 7, true, 'Bingo' ]

  // Get first parameter
  console.log(allParams[0])
  // 5

  // Get second parameter
  console.log(allParams[1])
  // 8

  // Get last parameter
  console.log(allParams[allParams.length - 1])
  // 'Bingo'

  // Get number of parameters passed into the function
  console.log(allParams.length)
  // 7
}

// Invoke useRestParams function
useRestParams(5, 8, 9, 6, 7, true, 'Bingo')
```

JavaScript also allows you to combine "standard" parameters with rest parameters. If you decide to use this combination of "standard" and rest parameter there is one thing you must pay attention to, the order of parameters. The rest parameters must be always at the end. This makes sense because rest parameters gather all remaining arguments.

```js
// Create function that combines "standard" parameters and rest parameters
function buyCar(model, manufacturer, color, ...restOfParams) {
  console.log(model)
  // 'RX-8'

  console.log(manufacturer)
  // 'Mazda'

  console.log(color)
  // 'red'

  console.log(restOfParams)
  // [ 'no transmission', 'electric', 'remote control', 'with GPS' ]
}

buyCar('RX-8', 'Mazda', 'red', 'no transmission', 'electric', 'remote control', 'with GPS')


// This will not work
function buyCar(model, ...restOfParams, manufacturer, color) {}

buyCar('RX-8', 'Mazda', 'red', 'no transmission', 'electric', 'remote control', 'with GPS')
// SyntaxError: Rest parameter must be last formal parameter
```

## Functions and naming conventions

We discussed a lot of things and went through many examples. One thing that remains untouched are naming practices and conventions. Let's take a break from code and take a look at how to name functions properly. First, allowed characters. Naming conventions for functions are the same as conventions for naming variables.

This means that function name can start with, and contain, any letter, underscore (_) or dollar sign ($). It is not allowed to start the name with a number. However, you can include numbers in the name, just make sure the name doesn't begin with any of them. That is about allowed characters. Now, let's talk about some good practices.

Functions are usually used to execute some actions, with the exception of Function constructors. For this reason, it is a good practice to use, or include, verbs in the name. For example, "get...", "delete...", "create...", "log...", "show...", "open...", "check...", etc. Another good practice is to keep the name brief and accurate.

There is no need to use names that look more like a sentence from Shakespeare. That said, the opposite is also not a good thing to do, i.e. using names with ultra short cryptic acronyms nobody can explain what they mean. So, not too short and not too long. The name should also be descriptive.

It should describe what the function does. So, when someone read your code he will have at least some clue about what the function does. Another commonly used practice, also related to verbs, is to start a function name with a verbal prefix that describes what the function does, i.e. the examples with verbs we discussed earlier.

## Conclusion: JavaScript Functions

Functions are a fundamental part of JavaScript. I hope this tutorial helped learn about how they work and how to use them. Let's do a quick recap. In this article, you've learned about variables and scope and how `this` works in functions. Next, you've learned how to change value of `this` using `call()`, `apply()` and `bind()` methods.

As next, you've also learned about Function constructor and how to use rest parameters. Finally, you've learned about conventions and good practices for naming functions. Next steps? Revisit anything you are not sure you understand, and spend some time practicing what you've learned. This will help you remember it.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Part 1]: https://blog.alexdevero.com/javascript-functions-pt1/
[strict mode]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode
[undefined]: https://blog.alexdevero.com/javascript-basics-data-types-pt2/#undefined
[previous part]: https://blog.alexdevero.com/javascript-functions-pt1/#functions-are8230-objects
[Function constructor]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function
[call()]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call
[apply()]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply
[bind()]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind

<!--
### Meta:
-
-->

<!--
#### Resources:
-->
