# How JavaScript Async/Await Works and How to Use It

[Promises] made dealing with asynchronous code became easier. ES8 introduced one feature that makes this even easier. This feature is async/await. This tutorial will help you learn about what async/await is and how it works. You will also learn how to use async/await to write  JavaScript.

<!--more-->
<!--
Table of Contents:
-->

## Synchronous vs asynchronous code

JavaScript is a synchronous single-threaded programming language. What this means that it can perform only one operation at the time. When one operation is executed other operations are blocked and have to wait. They can be executed only when the currently executed operation is finished. This is also called blocking.

Now, what if code is asynchronous? It works in the opposite way. When asynchronous code is executed it doesn't block other code. Other code can still be executed while the asynchronous operation is being executed. That asynchronous code is basically running in the background making space for other operations to take place.

You may not need to execute asynchronous operation all the time. However, there are situations when performing some operations asynchronously will be better, maybe even necessary. One example is fetching data from server. This may sound like something that is easy to do. Well, there is at least one problem.

When you fetch data from a server you never really know how fast you get them. Let's say you fetch these data in synchronous way. This means that you are blocking the [main thread]. When this happens other operations has to wait until the fetching is done and the main thread is available to use.

This will not happen if you fetch these data in asynchronous way. If the response from server is not immediate it doesn't block the main thread. In this case, you data fetching is moved to the siding until it is finished, metaphorically speaking. Any other code that needs to be executed can be executed right away.

It is only when that data fetching is complete, either with success or failure, when that operation moves to the main thread again. This doesn't mean you should re-write all your synchronous code to asynchronous. All it means is that there are some situations when asynchronous code can be quite useful.

Async/await are one way to make writing and working with asynchronous code. Let's take a look how it works and how you can use it.

## Async functions

There are two fundamental building blocks of async/await. The first are async functions. Let's take a look at how can you create a new async function.

### The async keyword

The most important part of an async function is `async` keyword. This is will tell JavaScript that you are want to declare an async function instead of regular. It is also this `async` keyword what will allow you to use `await` keyword inside that async function. Otherwise, JavaScript will throw SyntaxError. More about this later.

When you want to create an async you put the `async` keyword before the `function` keyword and its name, `async function myAsyncFunc() {}`. This is [function declaration]. In case of [function expression] the `async` keyword goes between the equal sign and `function` keyword, `const myAsyncFunc = async function() {}`. This is all you need to create an async function.

```JavaScript
// Create async function with function declaration
async function myAsyncFunc() {
  // some code
}

// Create async function with function expression
const myAsyncFunc = async function() {
  // some code
}

// Create async function with arrow function
const myAsyncFunc = async () => {
  // some code
}
```

### Returning a value from async function

Creating async functions s very similar creating a regular [functions]. One difference is the `async` keyword. Another, and more important, is that async functions always return a promise. This doesn't mean that you should not use `return` statement inside async functions. You still can.

When you use `return` statement to return a value from an async function that function will still return resolved promise. The value of this promise will be the value you returned. You can also return resolved promise directly. To do this you can use `Promise` object and `resolve()` method, the value being passed as a parameter to `resolve()`.

This also means one thing. If a function returns a promise you have to handle that returned promise in the right way. This means using `then()` method to get and process the returned value from that promise. Since you are working with promise you can also use other [handler functions], such as `catch()` and `finally()`.

```JavaScript
// Example no.1: using return statement
// Create async function
async function myAsyncFunc() {
  // Return some value using 'return' statement
  return 'There will be dragons.'
}

// Invoke the async function
// and get and process the returned promise
// to get the value
myAsyncFunc()
  .then(res => console.log(res))
  // Optionally catch and log any errors
  .catch(err => console.log(err))

// Output:
// 'There will be dragons.'


// Example no.2: using Promise.resolve()
// Create async function
async function myAsyncFunc() {
  // Return some value using 'return' statement
  return Promise.resolve('There will be dragons.')
}

// Invoke the async function
// and get and process the returned promise
// to get the value
myAsyncFunc()
  .then(res => console.log(res))
  // Optionally catch and log any errors
  .catch(err => console.log(err))


// Or assign the result to variable
async function myAsyncFunc() {
  // Return some value using 'return' statement
  return Promise.resolve('There will be dragons.')
}

// Invoke the async function
// and get and process the returned promise
// to get the value
// and assign the result to variable
const result = myAsyncFunc()
  .then(res => console.log(res))
  // Optionally catch and log any errors
  .catch(err => console.log(err))

// Output:
// 'There will be dragons.'


// What not to do: not using then()
async function myAsyncFunc() {
  // Return some value using 'return' statement
  return Promise.resolve('There will be dragons.')
}

console.log(myAsyncFunc())

// Or
const result = myAsyncFunc()
console.log(result)

// Output:
// [object Promise] { ... }
```

## The await keyword

The second fundamental building block of async/await is the `await` keyword. This keyword is inseparable from async functions. You can use `await` only inside an async function. You can't use it outside it, [yet]. You also can't use it inside regular functions. If you try it JavaScript will throw SyntaxError.

The `await` keyword tells JavaScript to wait until a promise, that follows this keyword, settles and returns some result. The `await` keyword is what moves the executed code the siding until it is finished. In the meantime, other operations can take space in the main thread be executed.

```JavaScript
// Create async function
async function myAsyncFunction() {
  // Create new promise
  const messagePromise = new Promise((resolve, reject) => {
    // Wait for 0.5s
    setTimeout(() => {
      // Resolve the promise
      resolve('There will be dragons.')
    }, 500)
  })

  // Invoke messagePromise and wait until it is resolved
  // Once it is resolved assign the resolved promise to a variable
  const messageResult = await messagePromise
  // NOTE: await will cause myAsyncFunction() to pause here
  // until the messagePromise is settled (resolved or rejected)

  // Log the result
  console.log(messageResult)
}

// Invoke the myAsyncFunction() function
myAsyncFunction()

// Output:
// 'Promise is finished.'
```

### Await and promise.then()

Notice one thing on the example above. You are creating a promise that resolves after 0.5s. Next, you are using `await` to invoke this promise, the `messagePromise`. At the same time you are assigning the resolved promise to a variable `messageResult`. After that, you are logging the value of that variable.

There is one thing missing, one thing that should be there and it is not. This thing that is missing is the `then()` function. This function is supposed to get the value from the returned promise. Yet, the code still works. When you invoke the `myAsyncFunction()` function you will still see the message logged in console.

This is another thing `await` does for you. It replaces the `then()` function. When you use `await` to assign some resolved Promise to a variable it will automatically "extract" the resolved value. You don't need to use `then()`. The work `then()` would do has been already done by `await`.

This is why you didn't need to use `then()` function on `messageResult` variable. Yet, you still managed to get the message, the value returned by resolved promise. So, remember, when you use `await` to wait for resolved promise you don't to use `then()`function.

```JavaScript
// This:
// Create async function
async function myAsyncFunction() {
  // Create new promise
  const messagePromise = new Promise((resolve, reject) => {
    // Wait for 0.5s
    setTimeout(() => {
      // Resolve the promise
      resolve('There will be dragons.')
    }, 500)
  })

  // Wait until messagePromise is resolved
  // NOTE: await will cause myAsyncFunction() to pause here
  // until the messagePromise is settled (resolved or rejected)
  const messageResult = await messagePromise

  // Log the result
  console.log(messageResult)
}

// Invoke the myAsyncFunction() function
myAsyncFunction()


// Is the same as:
// Create async function
async function myAsyncFunction() {
  // Create new promise
  const messagePromise = new Promise((resolve, reject) => {
    // Wait for 0.5s
    setTimeout(() => {
      // Resolve the promise
      resolve('There will be dragons.')
    }, 500)
  })
    // Use then() to process resolved promise
    // and get the returned value
    .then(res => {
      console.log(res)
    })
}

// Invoke the myAsyncFunction() function
myAsyncFunction()
// 'There will be dragons.'
```

## Async await and error handling

```JavaScript
```

## Async await and parallelism

## Conclusion: [...] ...

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Promises]: https://blog.alexdevero.com/javascript-promises/
[function]: https://blog.alexdevero.com/javascript-functions-pt1/
[main thread]: https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Concepts#Threads
[handler functions]: https://blog.alexdevero.com/javascript-promises/#handling-javascript-promises-with-handler-functions
[function declaration]: https://blog.alexdevero.com/javascript-functions-pt1/#function-declaration-and-function-expression
[function expression]: https://blog.alexdevero.com/javascript-functions-pt1/#function-declaration-and-function-expression
[yet]: https://github.com/tc39/proposal-top-level-await

<!--
### Meta:
-
-->

<!--
### Keywords:
- javascript switch statement
- switch statement
-->

<!--
### Resources:
- https://medium.com/javascript-in-plain-english/async-await-javascript-5038668ec6eb
- https://javascript.info/async-await
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function
- https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt7/
- https://dev.to/shoupn/javascript-fetch-api-and-using-asyncawait-47mp
- https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Introducing
- https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Concepts
-->
