# setTimeout, setInterval and How to Schedule Tasks in JavaScript

The `setTimeout` and `setInterval` are two methods you can use to schedule tasks in JavaScript. This tutorial will show you how to do it. It will introduce you both methods. It will show you how these methods work. It will also show you how to use them to schedule execution of your code.

<!--more-->
<!--
Table of Contents:
-->

## A quick introduction

Usually, you want to execute your code as you write it. That said, there will be situations when you will want to delay the execution. Or, you may want to repeat the execution in specific intervals. JavaScript provides two methods, one for each of these goals. The `setTimeout` to delay execution and `setInterval` to repeat it.

There is one interesting thing about these two methods. None of them is a part of JavaScript language specification. These methods are actually part of HTML Living Standard specification, defined as "timers". Fortunately, they are supported in all browsers, even in Node.js. So, we can use them safely. Let's take a look at them.

## setTimeout

The `setTimeout` method allows you to execute your code after a delay. You set this delay, in milliseconds, as one the parameters this method accepts. When the `setTimeout` method executes your code, after the delay, it executes it only once. So, no need to worry about your code being executed multiple times.

The `delay` parameter is optional. You can use it, but don't have to. You will soon learn why. Another parameter this method accepts is a callback function. When the delay runs out, the `setTimeout` method executes the callback function you passed as an argument, and whatever content you put inside it.

Aside these two parameters, you can also pass an infinite number of additional arguments. There are two things you have to remember if you want to pass any additional arguments. First, these will not work in versions of Internet Explorer below 9. This is probably not a problem nowadays.

The second might be more important. If you want to access these additional arguments you have to add parameters to your callback function. You can then use these parameters inside the callback function to access the data you want. One last thing. As a callback function, you can use either [normal function] or [arrow function], both will work.

```JavaScript
// setTimeout method syntax
setTimeout(callbackFunction, delay, argument1, argument2, ...)


// setTimeout method example no.1: with normal function
// Create a setTimeout method that waits for 2 seconds
// and then prints a message to console
setTimeout(function() {
  console.log('The time is up.')
}, 2000) // Delay is specified in milliseconds

// Output (after 2 seconds):
'The time is up.'


// setTimeout method example no.2: with arrow function
setTimeout(() => {
  console.log('The time is up.')
}, 2000) // Delay is specified in milliseconds

// Output (after 2 seconds):
'The time is up.'


// setTimeout method example no.3: additional arguments
// The "name" parameter is for accessing the 'John Doe'
// The "message" parameter is for accessing the 'Welcome back'
setTimeout((name, message) => {
  console.log(`${message} ${name}.`)
}, 2000, 'John Doe', 'Welcome back')
// Output (after 2 seconds):

'Welcome back John Doe.'
```

### (Sometimes) immediate setTimeout

As you just learned, the delay parameter is optional. When you omit it the `setTimeout` method will execute the callback function immediately. Well, almost. The callback function will be executed immediately only if there is no more code to execute. Otherwise the callback will be executed after the rest of code is executed.

```JavaScript
// Example no.1: setTimeout method that executes immediately
setTimeout(() => {
  console.log('I will be printed right away.')
}) // Omit the delay parameter

// Output (immediate):
'I will be printed right away.'


// Example no.2: setTimeout method that execute (almost) immediately
setTimeout(() => {
  console.log('I was supposed to be printed right away...')
})

console.log('I will be printed as first.')

function printMessage() {
  console.log('I will be printed as second.')
}

printMessage()

// Output:
'I will be printed as first.' // First console.log
'I will be printed as second.' // log in printMessage function
'I was supposed to be printed right away...' // Log in setTimeout
```

### Immediate setTimeout

## setInterval

## Combining setTimeout and setInterval

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
- setTimeout in JavaScript
- setInterval in JavaScript
- setTimeout
- setInterval
-->

<!--
### Resources:
-
-->
