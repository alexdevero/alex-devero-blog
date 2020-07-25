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

### Canceling setTimeout

Every time you use the `setTimeout` method it returns something called "timer identifier". This identifier is useful when you want to cancel existing timeout that didn't execute yet. You can do this with `clearTimeout` method. This method accepts only one parameter, the timer identifier of a timeout you want to cancel.

In order to clear a timeout you have to store its reference somewhere. To do this, you assign the timeout to a variable. Since the `setTimeout` returns the identifier when it is declared that  identifier will be assigned to that variable. You can then use that variable to cancel the timeout.

```JavaScript
// Create timeout and assign it to a variable
const newTimeout = setTimeout(() => {
  console.log('I was supposed to run after 3 seconds.')
}, 3000)

// Log the timer identifier of newTimeout
console.log(newTimeout)
// Output:
1

// Use clearTimeout() to cancel the "newTimeout" timeout
clearTimeout(newTimeout)
```

When you assign timeout to a variable you don't have to call it, like you would have a function. When you assign it, the timer will run automatically after the delay. Or, it will run immediately if there is no delay, and no other code to execute.

```JavaScript
// Create timeout and assign it to a variable
const newTimeout = setTimeout(() => {
  console.log('I will run automatically.')
}, 3000)

// Output:
'I will run automatically after 3 seconds.'
```

### Intervals with nested setTimeout method

One interesting thing you can do with `setTimeout` methods is nesting them. This means that you can put one timeout inside another. This can be useful if you want to execute some code in different intervals. When it comes to nesting, there are two thing you have to know about.

The first thing is that browser can start to penalize your timeouts. This will happen if you create five or more nested timeouts. In that case, browser will automatically force the delay to be at least four milliseconds. If all your nested intervals use delay bigger than four milliseconds you nothing will happen.

The second thing is that it is not guaranteed your nested intervals will be executed precisely on the schedule. The precision of execution delays depends on CPU load, function execution, and other tasks that are running on your device at the moment. If your computer is busy, the schedule might have some small additional delays.

```JavaScript
// Extreme example of nested timeouts
setTimeout(() => {
  console.log('Timeout number 1.')

  setTimeout(() => {
    console.log('Timeout number 2.')

    setTimeout(() => {
      console.log('Timeout number 3.')

      setTimeout(() => {
        console.log('Timeout number 4.')

        setTimeout(() => {
          console.log('Timeout number 5.')

          setTimeout(() => {
            console.log('Timeout number 6.')
          }, 150)
        }, 350)
      }, 250)
    }, 150)
  }, 200)
}, 100)

// Output:
'Timeout number 1.'
'Timeout number 2.'
'Timeout number 3.'
'Timeout number 4.'
'Timeout number 5.'
'Timeout number 6.'
```

## The setInterval method

The `setInterval` method is useful when you want to execute some code repeatedly in same intervals. The `setInterval` method has the same syntax as the `setTimeout` method. It accepts some callback functions, a delay and additional optional arguments. This delay is the time `setInterval` method waits until it executes the first, or another, interval.

The `setInterval` method works in a similar way to the `setTimeout` method. It runs automatically once you declare it. Unlike the `setTimeout` method, it runs until you stop it, or cancel it. If you don't stop it will run forever.

```JavaScript
// Create an interval that will run every 5 seconds
setInterval(() => {
  console.log('I will show up every 5 seconds.')
}, 5000) // Delay is in milliseconds

// Output:
'I will show up every 5 seconds.'
'I will show up every 5 seconds.'
```

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
