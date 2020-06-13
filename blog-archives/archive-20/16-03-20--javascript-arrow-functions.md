# JavaScript Arrow Functions - A Friendly Introduction
In this article, you will learn about arrow functions, the syntax, parameters, parentheses and curly brackets, and when you can omit them. You will also learn about implicit and explicit return, immediately invoked arrow functions and the main differences between arrow functions and functions.<!--more-->
<!--
Table of Contents:
## Introduction
## Syntax of arrow functions
## Parameters and (optional) parentheses
## Optional curly brackets
## Implicit and explicit return
## Immediately invoked arrow functions
## Differences between arrow functions and functions
### No arguments object
### No binding of this
## Conclusion: JavaScript Arrow Functions
-->

## Introduction

Arrow functions were one of the most noticeable features to JavaScript that were added with ES6 specification. They were also one of the most discussed features in ES6, along with [classes]. So, let's take a look at what arrow functions are, how they work and how to use them.

## Syntax of arrow functions

The most notable characteristic of arrow function is "fat arrow" (`=>`). It is also due to this "fat arrow" arrow functions got their name, and also nickname "fat arrows". This "fat arrow" stands between parentheses for parameters, which start the arrow function, and function body with some code to execute, which ends the arrow function.

```JavaScript
// Arrow function syntax
let myArrowFunc = () => // concise function body with some code

// Or
let myArrowFunc = () => {/* block function body with some code */}

// Call myArrowFunc
myArrowFunc()
```

If you compare the syntax of arrow functions with functions, you will see that the syntax of these two is very similar. It is for this reason arrow functions are considered an alternative to function expression.

```JavaScript
// Arrow function
const myArrowFunc = () => {/* function body with some code */}

// Function expression
const myArrowFunc = function() {}
```

That said, don't let this similarity fool you. Even though arrow functions may look similar to functions there are some significant, and very important differences. We will talk about all these differences soon.

## Parameters and (optional) parentheses

Arrow functions usually start with parentheses. However, this is not entirely necessary. These parentheses are optional and you can omit them, under one specific condition. The only thing that matters is if specific arrow function accepts any parameter. If it doesn't accept any you have to use empty parentheses (`()`).

The same applies to arrow functions that accept two or more parameters. In this case, you have to wrap these parameters with parentheses (`()`). And, also make sure to separate each parameter with a coma. Now, this leaves us with one possible scenario where parentheses are optional.

When arrow function accepts only one parameter. Then, you can either use or omit parentheses. Remember that if you like to use parentheses there is nothing preventing you from doing so. You can use parentheses all the time, no matter how many parameters there are, and arrow functions will work. Otherwise, remember the rule of one.

```JavaScript
// Arrow function with 0 parameters
// Parentheses are required here
const myArrowFunc = () => // some code


// Arrow function with 1 parameter
// Parentheses are optional here
const myArrowFunc = paramOne => // some code

// This will also work
const myArrowFunc = (paramOne) => // some code

const myArrowFunc = (paramOne) => console.log(paramOne)

// Call myArrowFunc
myArrowFunc('Something')


// Arrow function with 2+ parameters
// Parentheses are required here
const myArrowFunc = (paramOne, paramTwo) => // some code

const myArrowFunc = (paramOne, paramTwo) => paramOne + paramTwo

// Call myArrowFunc
myArrowFunc(13, 46)
// 59
```

## Optional curly brackets

Another thing that is optional in case of arrow functions are curly brackets. Here, the condition is even easier than it was in case of parentheses. That one thing that matters is if arrow function is a one-liner or not. If arrow function is a one-liner you can omit the curly brackets and that function will still work as expected.

Otherwise, if the function body contains code that spans over more than one line, curly brackets are required and you have to use them. Arrow function without curly brackets is called arrow function with a "concise body". Arrow function with curly brackets is called arrow function with a "block body".

Like with parentheses, if you like to use curly brackets you can use them all the time and it will work. If you like to omit them, remember that it is safe to do that only in case of one-line arrow functions.

```JavaScript
// One-line arrow function
// Arrow function with concise body
// Curly brackets are optional here
const myArrowFunc = () => // some code
const myArrowFunc = () => console.log('Hello!')

// This will also work
() => {/* some code */}

const myArrowFunc = () => {/* some code */}
const myArrowFunc = () => { console.log('Hello!') }

// Call myArrowFunc
myArrowFunc()
// Hello!


// Multi-line arrow function
// Arrow function with block body
// Curly brackets are required here
const myArrowFunc = () => {
  // some code
}

const myArrowFunc = () => {
  console.log('This is a multi-line arrow function.')
}

// Call myArrowFunc
myArrowFunc()
// 'This is a multi-line arrow function.'
```

When you think about it, it makes sense. In case of one-liner, it is easy for JavaScript to guess where bodies of arrow functions start and where they end. This is not the case with function body that spans over multiple lines. In this case, JavaScript has no idea where the boundaries of function body are.

Remember that JavaScript doesn't care about white space and indentation. In Python, for example, you can specify where function body starts and ends by indenting that block of code. This will not work in JavaScript. In JavaScript, you can indent your code as you want and JavaScript will just smile and ignore it anyway.

```JavaScript
// This will not work - omitting curly brackets
// Arrow function with concise body
// in multi-line arrow functions
() =>
  // some code

const myArrowFunc = () =>
  // some code
```

## Implicit and explicit return

One interesting thing on arrow functions is that they have an implicit return. Meaning, arrow functions return values automatically. You don't have to use the `return` keyword. That said, this works in two specific situations. The first one is when arrow function is a one-liner.

When it is a one-liner arrow function will automatically return any code in function body. If arrow function is not a one-liner, you have to use `return` statement.

```JavaScript
// One-line arrow function
// Explicit return statement is not needed
() => // some code
const myArrowFunc = () => // some code

// Call myArrowFunc
myArrowFunc()


// Multi-line arrow function
// Explicit return statement is necessary
() => {
  return /* some code */
}
const myArrowFunc = () => {
  return /* some code */
}

// Call myArrowFunc
myArrowFunc()
```

The second situation where you have to use `return` statement is when arrow function uses block body, i.e. function body with curly brackets. This is another thing you have to consider when deciding what syntax do you want to use. Whether you want to use "block body" and curly bracket or "concise body" without curly bracket.

If it is the later, concise body, you don't have to use explicit `return` statement. If the former, block body, make sure to use `return` statement.

```JavaScript
// Arrow function with concise body
// Explicit return statement is not needed
() => // some code (this is concise body)
const myArrowFunc = () => // some code (this is concise body)

// Call myArrowFunc
myArrowFunc()


// Arrow function with block body
// Explicit return statement is necessary
() => {/* some code (this is block body) */}
const myArrowFunc = () => {/* some code (this is block body) */}

// Call myArrowFunc
myArrowFunc()
```

## Immediately invoked arrow functions

One thing JavaScript allows you is to declare and invoke functions at the same time. These functions are called [immediately invoked functions]. One way to create this type of a function is by wrapping the function with parentheses and adding additional pair of parentheses after the wrapping parentheses.

Second way is also about wrapping the function with parentheses and adding additional pair of parentheses after the curly brackets, still inside the wrapping parentheses. Third way is about omitting the wrapping parentheses and putting NOT operator (`!`) at the beginning of the line, in front of the `function` keyword.

Fourth way is similar to the previous, except that you replace the NOT operator with unary operator `+`.

```JavaScript
// Immediately invoked function no.1:
// invoking parentheses outside wrapping parentheses
(function() {
  // some code
})()


// Immediately invoked function no.2:
// invoking parentheses inside wrapping parentheses
(function() {
  // some code
}())


// Immediately invoked function no.3:
// using ! (NOT operator)
!function() {
  // some code
}()


// Immediately invoked function no.4:
// Using + (unary operator)
+function() {
  // some code
}()
```

You can do the same thing also with arrow functions, create immediately invoked arrow functions. The important thing is that, in case of arrow functions, you can use only the first way. Other three will fail. So, wrap the arrow function with parentheses and add additional pair of parentheses after the wrapping parentheses.

```JavaScript
// Immediately invoked one-line arrow function
// This will work
// Wrap arrow function with parentheses
// add additional set of parentheses
// outside the wrapping parentheses
(() => /* some code */)()


// Immediately invoked multi-line arrow function
// This will work
(() => {
  /* some code */
})()


// This will not work
(() => {
  // some code
}())

// This will also not work
!() => {
  // some code
}()

// This will also not work
+() => {
  // some code
  return 'foo'
}()
```

Remember that all the rules about optional parentheses and curly brackets still apply. Meaning, if the arrow function has no or two or parameters, you have to include parentheses. If it is multi-line, you have to use curly brackets and `return` statement. If it is one-line, but uses block body, you also have to use `return` statement.

```JavaScript
// Concise body with implicit return
(() => /* some code */)()

// Block body with explicit return
(() => { return /* some code */ })()

// Or
(() => {
  return /* some code */
})()
```

## Differences between arrow functions and functions

Arrow functions and functions are similar. However, there are at least two important differences. Let's take a look at each of these differences. This will help you decide when it is better to use arrow functions and when functions.

### No arguments object

When you work with functions, you can always access [arguments] object. This object contains all values that were passed to the function when it was invoked. In case of arrow functions, there is no such an object. Even if you do pass some arguments to arrow functions the JavaScript will still throw a [reference error] when you try to access the `arguments` object.

```JavaScript
// Function
const myFunction = function(param) {
  return arguments
}

myFunction('Something')
// { '0': 'Something' }


// Arrow function
const myArrowFunction = (param) => arguments

myArrowFunction('Something')
// ReferenceError: arguments is not defined
```

So, remember, if you plan to use the `arguments` object regular function is a better choice than arrow function.

### No binding of this

Another thing that is missing in arrow functions is `this`. When you work with functions, every time you define a function it also creates its own `this`. If you don't use [strict-mode] `this` will refer to the global `window` object. If you use strict mode, the value of `this` will be undefined.

When you use function to create a [function constructor] `this` will be a new object. If you use function as an object, or a class, method `this` will refer to parent object, or class, of that function.

```JavaScript
// This in non-strict mode
function myFunction() {
  console.log(this, this === window)
}

myFunction()
// [object Window], true


///
// This in strict mode
'use strict'

function myFunction() {
  console.log(this, this === window)
}

myFunction()
// undefined, false


// Function inside an object
const myObj = {
  title: 'Atlas Shrugged',
  author: 'Ayn Rand',
  getBook: function() {
    // This refers to myObj
    // So, this.title is like myObj.title
    return `${this.title} by ${this.author}.`
  }
}

myObj.getBook()
// 'Atlas Shrugged by Ayn Rand.'
```

In case of arrow functions, the situation is different. Arrow functions don't have their own `this`. Arrow functions inherit `this` from the execution context in which there are used. When you in the default global environment, the execution context is also global, usually the `window` object.

```JavaScript
// This in non-strict mode
// Arrow function
let myArrowFunction = () => {
  console.log(this, this === window)
}

myArrowFunction()
// [object Window], true


///
// This in strict mode
'use strict'

let myArrowFunction = () => {
  console.log(this, this === window)
}

myArrowFunction()
// [object Window], true
```

When you are in a function, the execution context becomes the function. With arrow functions, there is no binding for `this`. Instead, `this` is inherited from its original context. If all there is is an object, the execution context will be global, the `window` object. This is a problem.

Imagine you have arrow function inside an object. When you use `this` inside that arrow function it will refer to global execution context, the `window`, not the object in which it is. This means that you then can't use `this` when you want to refer to some property inside that object.

Remember, `this` now refers to `window` and `window` doesn't have that property. So, if you try it, JavaScript will throw type error. The solution? Use regular function instead.

```JavaScript
// Arrow function inside an object
const myObj = {
  title: 'Atlas Shrugged',
  author: 'Ayn Rand',
  getBook: () => {
    // This refers to global object window
    // So, this.title is like window.title
    return `${this.title} by ${this.author}.`
  },
  getBookWithRegularFunction: function() {
    // This refers to myObj
    // So, this.title is like myObj.title
    return `${this.title} by ${this.author}.`
  }
}

myObj.getBook()
// TypeError: Cannot read property 'title' of undefined

myObj.getBookWithRegularFunction()
// 'Atlas Shrugged by Ayn Rand.'
```

This is one reason arrow functions are not the best choice for object methods. Also, it is arrow functions can't be used as constructors. If you try to do it, JavaScript will throw type error.

## Conclusion: JavaScript Arrow Functions

Hopefully this article helped you learn about JavaScript arrow functions, how they work and how to use them. In a recap, today you've learned about the basic of arrow functions and the syntax. Next, you've also learned about parameters and parentheses and curly brackets and when you can omit them and when not.

After that, you've also learned about implicit and explicit return,  when you can omit `return` statement and when not. Following that, you've learned how to create immediately invoked arrow functions. Lastly, you've also learned about the two main differences between arrow functions and functions. With that, thank you for your time.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[classes]: https://blog.alexdevero.com/javascript-classes-pt1/
[immediately invoked functions]: https://blog.alexdevero.com/javascript-functions-pt3/#immediately-invoked-functions
[arguments]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments
[reference error]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ReferenceError
[strict-mode]: https://developer.mozilla.org/en-US/docs/Glossary/strict_mode
[function constructor]: https://blog.alexdevero.com/javascript-functions-pt2/#function-constructor

<!--
### Meta:
-
-->

<!--
#### Resources:
-->
