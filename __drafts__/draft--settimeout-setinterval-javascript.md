# setTimeout, setInterval and How to Schedule Tasks in JavaScript

The `setTimeout()` and `setInterval()` are two methods you can use to schedule tasks in JavaScript. This tutorial will show you how to do it. It will introduce you both methods. It will show you how these methods work. It will also show you how to use them to schedule execution of your code.

<!--more-->
<!--
Table of Contents:
-->

## A quick introduction

Usually, you want to execute your code as you write it. That said, there will be situations when you will want to delay the execution. Or, you may want to repeat the execution in specific intervals. JavaScript provides two methods, one for each of these goals. The `setTimeout()` to delay execution and `setInterval()` to repeat it.

There is one interesting thing about these two methods to schedule tasks. None of them is a part of JavaScript language specification. These methods are actually part of [HTML Living Standard specification], defined as "timers". Fortunately, they are supported in all browsers, even in Node.js. So, we can use them safely. Let's take a look at them.

## The setTimeout method

The `setTimeout()` method allows you to execute your code after a delay. You set this delay, in milliseconds, as one the parameters this method accepts. When the `setTimeout()` method executes your code, after the delay, it executes it only once. So, no need to worry about your code being executed multiple times.

The `delay` parameter is optional. You can use it, but don't have to. You will soon learn why. Another parameter this method accepts is a callback function. When the delay runs out, the `setTimeout()` method executes the callback function you passed as an argument, and whatever content you put inside it.

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

As you just learned, the delay parameter is optional. When you omit it the `setTimeout()` method will execute the callback function immediately. Well, almost. The callback function will be executed immediately only if there is no more code to execute. Otherwise the callback will be executed after the rest of code is executed.

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

Every time you use the `setTimeout()` method it returns something called "timer identifier". This identifier is useful when you want to cancel existing timeout that didn't execute yet. You can do this with `clearTimeout()` method. This method accepts only one parameter, the timer identifier of a timeout you want to cancel.

In order to clear a timeout you have to store its reference somewhere. To do this, you assign the timeout to a variable. Since the `setTimeout()` returns the identifier when it is declared that  identifier will be assigned to that variable. You can then use that variable to cancel the timeout.

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

One interesting thing you can do with `setTimeout()` methods is nesting them. This means that you can put one timeout inside another. This can be useful if you want to execute some code in different intervals. When it comes to nesting, there are two thing you have to know about.

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

The `setInterval()` method is useful when you want to execute some code repeatedly in same intervals. The `setInterval()` method has the same syntax as the `setTimeout()` method. It accepts some callback functions, a delay and additional optional arguments. This delay is the time `setInterval()` method waits until it executes the first, or another, interval.

The `setInterval()` method works in a similar way to the `setTimeout()` method. It runs automatically once you declare it. Unlike the `setTimeout()` method, it runs until you stop it, or cancel it. If you don't stop it will run forever.

```JavaScript
// Create an interval that will run every 5 seconds
setInterval(() => {
  console.log('I will show up every 5 seconds.')
}, 5000) // Delay is in milliseconds

// Output:
'I will show up every 5 seconds.'
'I will show up every 5 seconds.'
```

### Canceling setInterval

In order to stop the `setInterval()` method from running again you have to use the `clearInterval()` method. The `clearInterval()` method works in the same way as the `clearTimeout()` method. It also accepts only one parameter, the timer identifier of an interval you want to cancel.

The `setInterval()` method also returns timer identifier you can than pass to the `clearInterval()`. Since the `setInterval()` method runs forever, and requires canceling manually, it is usually assigned to a variable. When you assign it to a variable, the identifier it returns is assigned to that variable.

Now, you can pass that variable to the `clearInterval()` method as an argument to cancel the interval.

Another

```JavaScript
// Example no.1: using setTimeout method to cancel interval
const myInterval = setInterval(() => {
  // Log some message
  console.log('I will be stopped soon.')
}, 500)

// Create timeout to stop the interval after 1 second
setTimeout(() => {
  clearInterval(myInterval)
}, 1000)

// Output:
'I will be stopped soon.'
'I will be stopped soon.'


// Example no.2: using clearInterval() inside setInterval method
// Create an interval and assign it to a variable
const myInterval = setInterval(() => {
  // Log some message
  console.log('I will run once.')

  // Cancel the interval
  clearInterval(myInterval)
}, 1000)

// Output:
'I will run once.'
```

As you can see on the example above, you can also use the `clearInterval()` method inside the interval you want to stop. Well, you can also use it inside the `setTimeout()` method, but since it runs only once it doesn't make sense. In case of `setInterval()` method this can be handy.

For example, you can let the interval run only once. To do that you just put the `clearInterval()` method somewhere in the callback function. Then, the `setInterval()` method will execute the code inside the callback function and terminate itself. Another option is to use it with [if...else] statement.

You can use these two together to cancel the interval only under specific condition. Otherwise, if the condition is not met, you can let the interval run another iteration.

```JavaScript
// Create an interval and assign it to a variable
const myInterval = setInterval(() => {
  // Log some message
  console.log('Still running.')

  // Cancel the interval only if condition is met
  if (Math.floor(Math.random() * 5) === 3) {
    clearInterval(myInterval)

    // Log confirmation message
    console.log('Interval cleared.')
  }
}, 500)

// Output:
'Still running.'
'Still running.'
'Still running.'
'Still running.'
'Still running.'
'Still running.'
'Still running.'
'Still running.'
'Still running.'
'Still running.'
'Still running.'
'Interval cleared.'
```

## Combining setTimeout and setInterval

Both, `setTimeout` and `setInterval`, are very useful tools to schedule tasks. They can be even more useful when you combine them. For example, you can use `setInterval` to observe something in specific intervals, like changes in the DOM or answer from the server, if you can't use [async/await] or [promises].

Along with that, `setTimeout` as something like a fallback. If there is no change in DOM after some time, or response from a server, you can use the `setTimeout` method to cancel the interval.

```JavaScript
// Create interval to watch for change every .15 milliseconds
const myInterval = setInterval(function() {
  // If change happens
  if (/* some condition is true */) {
    // Cancel the interval
    clearInterval(myInterval)
  }
}, 150)

// Create a fallback to cancel the interval
// if change doesn't happen after
setTimeout(function() {
  // Clear the interval
  clearInterval(myInterval)
}, 6000)
```

You can also combine these two method to schedule tasks the other way around. For example, you can create an interval with `setInterval` method and put it inside the `setTimeout` method to delay it. Then, you can also use another `setTimeout` method as a fallback to cancel the interval after some time.

```JavaScript
// Declare unassigned variable for interval
let myInterval

// Use timeout to delay first interval
setTimeout(function () {
  // Create interval and assign it to "myInterval" variable
  myInterval = setInterval(function () {
    // If change happens
    if (something) {
      // Cancel the interval
      clearInterval(myInterval)
    }
  }, 1000)
}, 2000)

// Create a fallback to cancel the interval
// if change doesn't happen after 9 seconds
setTimeout(function () {
  // Clear the interval
  clearInterval(myInterval)
}, 9000)
```

## Conclusion: setTimeout, setInterval and how to schedule tasks in JavaScript

The `setTimeout()` and `setInterval()` are two useful methods that can help you schedule tasks and execute your code according to your schedule. These methods might look simple, but they can be very powerful, especially when you combine them. I hope this tutorial helped you understand how these methods work, how to use them and to watch out for.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[HTML Living Standard specification]: https://html.spec.whatwg.org/multipage/timers-and-user-prompts.html#timers
[normal function]: https://blog.alexdevero.com/javascript-functions-pt1/
[arrow function]: https://blog.alexdevero.com/javascript-arrow-functions/
[https://blog.alexdevero.com/javascript-if-else-statement/]: https://blog.alexdevero.com/javascript-if-else-statement/
[async/await]: https://blog.alexdevero.com/javascript-async-await/
[promises]: https://blog.alexdevero.com/javascript-promises/

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
