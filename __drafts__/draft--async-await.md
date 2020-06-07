# How JavaScript Async/Await Works and How to Use It

[Promises] made dealing with asynchronous code became easier. ES8 introduced one feature that makes this even easier. This feature is async/await. This tutorial will help you learn about what async/await is and how it works. You will also learn how to use async/await to write  JavaScript.

<!--more-->
<!--
Table of Contents:
## Synchronous vs asynchronous code
## Async functions
### The async keyword
### Returning a value from async function
## The await keyword
### Await and promise.then()
### Top-level await
## Async/await and error handling
## Word of caution
## A real world example
## Conclusion: How JavaScript Async/Await Works and How to Use It
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

The `await` keyword tells JavaScript to pause the execution of the async function in which it is. This function is then paused until a promise, that follows this keyword, settles and returns some result. So, it is  this `await` keyword what moves the executed code the siding until it is finished. In the meantime, other operations can take space in the main thread be executed.

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

### Top-level await

At the time of writing this tutorial, it is not possible to use `await` keyword in a global scope. As you know, `await` keyword can be used only inside async function. One good news is that there as a [proposal] for top-level `await`. This proposal is at stage three so it might be too long until it is part of JavaScript.

Second good news is that you don't have to wait for top-level `await` to happen. There is a workaround you can use today. What you can do is to create top-level async [IIFE] (Immediately-invoked function expression).

Since this function is async you can use `await` inside it. When top-level `await` is part of JavaScript specification you can remove the async IIFE and. Until then, it will do the job.

```JavaScript
// Pseudo-top-level await
// Create async function
(async () => {
  // Create new promise
  const myPromise = new Promise((resolve, reject) => {
    // Resolve the promise
    resolve('Promise resolved!.')
  })

  // Await the promise
  // and assign the result to a variable
  const message = await myPromise

  // Log the message from resolved promise
  console.log(message)
})()

// Output:
// 'Promise resolved!.'
```

## Async/await and error handling

When it comes to async/await and errors, there are two ways to deal with them. One way is by using `catch()` function. Async function returns a promise. When promise gets rejected it is `catch()` function what allows you to catch and handle this error. This works also for Async/await.

```JavaScript
// Create async function
async function myAsyncFunc() {
  // Create promise that rejects
  // and wait for its completion
  await new Promise((resolve, reject) => {
    reject('Promise rejected!')
  })
}

// Invoke myAsyncFunc and catch the error
myAsyncFunc()
  .catch(err => {
    console.log(`error: ${err}`)
  })
// 'error: Promise rejected!'
```

The second option is to use `try...catch` statement. In this case, you use `try` block to wrap the part of your code that contains `await`. Next, you use the `catch` block to handle any error that occurs.

```JavaScript
// Create async function
async function myAsyncFunc() {
  // Create new promise that rejects
  const myPromise = new Promise((resolve, reject) => {
    reject('Promise rejected!')
  })

  // Create try...catch statement
  try {
    // Await the promise to get rejected
    const message = await myPromise
  }
  catch(err) {
    // Catch any error and log it
    console.log(`error: ${err}`)
  }
}

// Invoke the myAsyncFunc() function
myAsyncFunc()
// 'error: Promise rejected!'
```

## Word of caution

As you know, `await` pauses execution of async function in which it is. This is good. It means you don't have worry about when your promise will be settled, resolved or rejected. However, this has some consequences. Since the `await` paused the async function this function can't finish its execution until the promise is settled.

This may not be a problem if you await one promise and the response is fast. What if you await multiple promises? What if getting some responses takes more time than others? Then, the execution of that async function will also take more time. Let's take a look at one example of an async function with three awaited promises.

```JavaScript
// Create async function
async function myAsyncFunc() {
  // Create timestamp when function is invoked
  const dateStart = Date.now()

  // Create new promise and await its completion
  // Until then, pause execution of this function
  await new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve('Promise 1 is done.')
    }, 450)
  })

  // Create new promise and await its completion
  // Until then, pause execution of this function
  await new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve('Promise 2 is done.')
    }, 750)
  })

  // Create another promise and also await its completion
  // Until then, pause execution of this function
  await new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve('Promise 3 is done.')
    }, 1250)
  })

  // Create timestamp when all promises are resolved
  const dateFinished = Date.now()

  // Return a message a the end of function execution
  // with time it took to execute it
  return `All promises are done. Time: ${(dateFinished - dateStart) / 1000}s.`
}

// Invoke the myAsyncFunc() function
myAsyncFunc()
  // Process the resolved promise returned by myAsyncFunc() function
  .then(res => {
    // Log the message from myAsyncFunc() function
    console.log(res)
  })
// 'All promises are done. Time: 2.468s.'
```

As you can see, when the function waited for all promises to settle it took it around 2 seconds to execute the whole block. This is because all promises in the example above that are preceded by `await` keyword are executed in a sequence. So, when one awaited promise is being executed other promises that follow it has to wait.

It is only when the first one is settled the other can be executed. This applies to all awaited promises in the "chain". The second has to wait for the first. The third has to wait for the second. This repeats until all awaited promises are settled. During this time the async function is paused with each `await` keyword.

Fortunately, there is a way to make this faster. You can run all those promises in parallel and await only the final result of of those promises. To do that you can use `Promise.all()` method. This method accepts an iterable object of promises, like an array. When all promises are settled it returns one promise withe all values.

So, what you need to do is to take those promises and put them inside the `Promise.all()`. Then, instead of awaiting all those promises you will await only the `Promise.all()`.

```JavaScript
// Create async function
async function myAsyncFunc() {
  // Create timestamp when function is invoked
  const dateStart = Date.now()

  // Use Promise.all() to wrap all promises and await its completion
  await Promise.all([
    // Create new promise and await its completion
    // Until then, pause execution of this function
    new Promise((resolve, reject) => {
      setTimeout(() => {
        resolve('Promise 1 is done.')
      }, 450)
    }),
    // Create new promise and await its completion
    // Until then, pause execution of this function
    new Promise((resolve, reject) => {
      setTimeout(() => {
        resolve('Promise 2 is done.')
      }, 750)
    }),
    // Create another promise and also await its completion
    // Until then, pause execution of this function
    new Promise((resolve, reject) => {
      setTimeout(() => {
        resolve('Promise 3 is done.')
      }, 1250)
    })
  ])

  // Create timestamp when all promises are resolved
  const dateFinished = Date.now()

  // Return a message a the end of function execution
  // with time it took to execute it
  return `All promises are done. Time: ${(dateFinished - dateStart) / 1000}s.`
}

// Invoke the myAsyncFunc() function
myAsyncFunc()
  // Process the resolved promise returned by myAsyncFunc() function
  .then(res => {
    // Log the message from myAsyncFunc() function
    console.log(res)
  })
// 'All promises are done. Time: 1.264s.'
```

As you can see, the updated `myAsyncFunc()` function ran almost twice as fast, thanks to `Promise.all()` method and running all promises in parallel. Remember this the next time you will want to use `await` and make you use it properly.

## A real world example

You've learned a lot about async functions, `await` and asynchronous code. How about to put all this knowledge to practice? Let's create a function that will fetch GitHub API and return data for one specific user. This function will be async. It will use JavaScript `fetch()` API to fetch the GitHub API and wait for the response.

When the response arrives, the async function will translate received data to JSON format and return the result. Since this is an async function the data will be returned in the form of a promise. To get the data from the resolved promise will need to use `then()` method. Then, we will log these data to console.

Now, use what you've learned today to do this exercise. If you get stuck, need a hint, or just want to compare your solution, take a look one possible solution in the example below.

```JavaScript
// Create async function to fetch GitHub API
async function asyncFetchGitHub(name) {
  // Fetch GitHub API and wait until the request is settled
  const serverResponse = await fetch(`https://api.github.com/users/${name}`)

  // Translate the response to JSON format
  const serverData = serverResponse.json()

  // Return the translated data
  return serverData
}

// Invoke the asyncFetchGitHub() function
asyncFetchGitHub('alexdevero')
  .then(data => {
    // Log the data to console
    console.log(data)
  })

// Output:
// {
//   login: 'alexdevero',
//   url: 'https://api.github.com/users/alexdevero',
//   html_url: 'https://github.com/alexdevero',
//   followers_url: 'https://api.github.com/users/alexdevero/followers',
//   ...
// }
```

## Conclusion: How JavaScript Async/Await Works and How to Use It

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Promises]: https://blog.alexdevero.com/javascript-promises/
[function]: https://blog.alexdevero.com/javascript-functions-pt1/
[main thread]: https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Concepts#Threads
[handler functions]: https://blog.alexdevero.com/javascript-promises/#handling-javascript-promises-with-handler-functions
[function declaration]: https://blog.alexdevero.com/javascript-functions-pt1/#function-declaration-and-function-expression
[function expression]: https://blog.alexdevero.com/javascript-functions-pt1/#function-declaration-and-function-expression
[yet]: https://github.com/tc39/proposal-top-level-await
[proposal]: https://github.com/tc39/proposal-top-level-await
[IIFE]: https://blog.alexdevero.com/javascript-functions-pt3/#immediately-invoked-functions

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
