# JavaScript Promises - An Introduction
<!--more-->
<!--
Table of Contents:
-->

## Introduction

What are JavaScript promises? Promises are objects that represent some value. You don't know that value when you create a promise. You will get this value in the future when a promise is resolved or rejected. Code that follows the promise is not block by it. This makes writing asynchronous code much easier and more manageable.

Imagine you have an app. When you start this app it needs to fetch data from some API. The problem is that you don't know whn you will receive this data. Sometimes, you get them quickly. Sometimes, it might take more time. How can you write your app in a way so it takes this uncertainty into account?

One option could be checking the data in specific intervals. You would do this until you finally get the data you need. This is neither effective nor clean. Another option is to use a Promise. You can use a Promise to make that API call. When this Promises is settled, that is it is resolved or rejected, you can update your app.

How is this easier? When JavaScript Promise is settled, resolved or rejected, it automatically triggers events you listen to with specific handler methods. So, unlike in the first solution, you don't have to regularly check the status of Promises. The Promise will automatically execute any code you want at the right moment.

I hope this makes a bit sense. If not, let's try more real-life like example. Let's say you are washing your clothes. The problem is that your washing machine doesn't show the time it will take to complete its job. What can you do? One, you can regularly check if it is done, and if you can take your clothes out and put them in a dryer.

Another option is to set this in a way that when your washing machine finishes, there will be something that will automatically take your clothes from the washing machine and put it into dryer, and start drying your clothes. Ideally, it would also put your clothes in a closet when drying is finished. That something, the "bridge" between washing machine and dryer, is a Promise.

## Creating a Promise

That was the theory. Now, to the practice. When you want to create a Promise you use Promise constructor. In the terms of syntax, this means using keyword `new` followed by `Promise()`. The constructor takes one parameter. This parameter is a function called executor. The executor is invoked automatically when you create a Promise.

The executor function takes two parameters, both of which are callbacks. These parameters are `resolve` and `reject`. When Promise is resolved the `resolve` callback is invoked. This is when the job a Promise is supposed to do is successful. When it is not, when there is some error, Promise is rejected and the `reject` callback is invoked.

```JavaScript
// Promise syntax example
const myPromise = new Promise(function(resolve, reject) {
  // ... some code
})


// Promise syntax example using an arrow function
const myPromise = new Promise((resolve, reject) => {
  // ... some code
})
```

## Resolving and rejecting Promises with static methods

When you want the Promise to return some data, you pass those data into the `resolve`. For example, when your Promises makes a call to an API you pass into the `resolve` the data returned from the API. If some error occurs you can pass the data about the error to the `reject` callback. Or, some error message.

```JavaScript
// Promise syntax example
const myPromise = new Promise(function(resolve, reject) {
  // Resolve the Promise passing a message as a data
  resolve('Success: promise resolved.')

  // If some error happens
  if (error) {
    // Reject the Promise passing a message as a data
    reject('Failure: promise rejected')
  }
})

// Invoke the Promise
myPromise


// Promise syntax example using an arrow function
const myPromise = new Promise((resolve, reject) => {
  // Resolve the Promise passing a message as a data
  resolve('Success: promise resolved.')

  // If some error happens
  if (error) {
    // Reject the Promise passing a message as a data
    reject('Failure: promise rejected')
  }
})

// Invoke the Promise
myPromise
```

When you do this, Promise will be able to pass these data to handler functions you attached to that Promise. Two more things about creating JavaScript Promises you need to know. One, you can assign Promise to a variable and then invoke it. This is similar to a [function expression].

```JavaScript
// Creating Promise no.1: assigning to a variable
const myPromise = new Promise((resolve, reject) => {
  // Resolve the Promise passing a message as a data
  resolve('Success: promise resolved.')

  // If some error happens
  if (error) {
    // Reject the Promise passing a message as a data
    reject('Failure: promise rejected')
  }
})

// Invoke the Promise
myPromise
```

Another option is to return a Promise from a function. Then, when you want to invoke that Promise, you call the function that returns it. This will work in the same way is the first way. Remember that when you want to return a Promise you still have to use the `new` keyword before Promise constructor.

```JavaScript
// Creating Promise no.2: returning it from a function
function myFunc() {
  // Return new Promise
  return new Promise(function(resolve, reject) {
    // Resolve the Promise passing a message as a data
    resolve('Success: promise resolved.')

    // If some error happens
    if (error) {
      // Reject the Promise passing a message as a data
      reject('Failure: promise rejected')
    }
  })
}

// Invoke myFunc() to invoke the Promise inside it
myFunc()
```

## Four states of JavaScript Promises

On the lines above you read about Promises being resolved or rejected. These two are related to states JavaScript Promises have. These states describe in which state Promise is, and if any handler function should attached to that Promise should be invoked. JavaScript Promises have four states.

The first state is called `pending`. This is the initial state when you create a Promise and invoke it. This state says that the Promise is neither fulfilled (resolved) nor rejected. The second state is called `fulfilled`. This means that Promise was successfully resolved.

The third state is called `rejected`. When this happens it means there was some problem that prevented the Promise from being successfully fulfilled (resolved). The fourth and last state is called `settled`. This means that the job of the Promise is finished and the Promise was either fulfilled or rejected.

## Handling JavaScript Promises with prototype methods

You know how to create a Promise and the four states in which it can be. What you need to next is how to handle Promise. You need to know how you can work with the data returned by a Promise, data passed into `resolve` and `reject` callbacks. This is where `then()`, `catch()` and `finally()` comes into game.

The `then()`, `catch()` and `finally()` are handler function you can attach to a Promise. These handlers are important. When you invoke a Promise and the promise is settled (resolved or rejected) one of these handlers will be automatically invoked. When there are some data returned from a Promise it is passed into these handlers.

If you want to work with the data returned by a Promise these handlers are the place where to do it. For example, you could put logic for updating your app with the data you received from API into these handlers. What if you don't use any of these handlers?The Promise would still run after you invoke it.

However, there would be nothing processing the data it returns. The data would be basically locked inside the Promise object. This is why these handlers are important. They are like messengers that transport the message from Promise further down the chain.

### The then() handler function

Let's stat with the first handler function, the `then()`. This handler is usually used to handle `fulfilled` state of JavaScript Promises. In order to use the `then()`, or any other handler, you have to attach it after the Promise when you invoke it. This means referencing the Promise by its name and then adding `.then()`

When the Promise is settled (resolved or rejected) the data will be passed to the `then()` handler. These data are the data passed into the `resolve()` handler inside the Promise. When you want to access this data all you need to do is to pass a callback function to the `then()` handler.

This callback function should accept one parameter. Any data returned by the Promise (resolved) will then be available through this parameter.

```JavaScript
// Create a Promise
const myPromise = new Promise((resolve, reject) => {
  // Fake a delay
  setTimeout(function() {
    // Resolve the Promise with a simple message
    resolve('Promise has been resolved!')
  }, 1000)
})

// Invoke the myPromise and attach then() handler
// Pass a callback function to the then() handler
// Make that callback function accept one parameter
myPromise.then((receivedData) => {
  // Log the data received by Promise
  console.log(receivedData)
})

// Output:
// 'Promise has been resolved!'
```

There is one interesting thing on `then()` handler. You can use this handler also to handle `rejected` state of Promise. Well, to handle both states. This is because the primary function of this handler is to handle `fulfilled` state. When you want it to handle `rejected` state you need to pass a second callback function to it.

This second callback should also accept one parameter. Through this parameter you will be able to access any error data passed by the Promise. This is why the `then()` handler is primarily used for `fulfilled` state and not `rejected`. It is hard to pass a second callback to handle the `rejected` state without passing the first to handle the `fulfilled` state first.

```JavaScript
// Create a Promise
const myPromise = new Promise((resolve, reject) => {
  // Fake a delay
  setTimeout(function() {
    // Reject the Promise with a message
    reject('Promise has been rejected...')
  }, 1000)
})

// Invoke the myPromise and attach then() handler
// Pass a callback function to the then() handler
// Make that callback function accept one parameter
myPromise.then((receivedData) => {
  // This is the first callback, for 'fulfilled' state
  // Log the data received by Promise
  console.log(receivedData)
}, (error) => { // <= Remember to separate handlers with comma
  // This is the second callback, for 'rejected' state
  console.log(error)
})

// Output:
// 'Promise has been rejected...'
```

*Note: Remember to separate handlers for `fulfilled` and `rejected` state with comma if you decide to use `then()` handler function for both.*

### The catch() handler function

Another way, the usual, for handling `rejected` states of JavaScript Promises is by using `catch()` handler. Using tis handler and accessing any data passed into it is the same as with `then()`. When you attach it to a Promise it is a good practice to attach it after the `then()` handler.

When you attach it, you pass in a callback function that accepts one parameter. When Promise gets rejected any data passed into the `reject()` handler inside the Promise will be available through parameter.

```JavaScript
// Reject example no.1: without then()
// Create a Promise
const myPromise = new Promise((resolve, reject) => {
  // Fake a delay
  setTimeout(function() {
    // Reject the Promise with a message
    reject('Promise has been rejected...')
  }, 1000)
})

// Invoke the myPromise and attach catch() handler
// Pass a callback function to the catch() handler
// Make that callback function accept one parameter
myPromise.catch((error) => {
  // Log the error message received by Promise
  console.log(error)
})

// Output:
// 'Promise has been rejected...'


// Reject example no.2: with then()
// Create a Promise
const myPromise = new Promise((resolve, reject) => {
  // Fake a delay
  if (error) {
    // Resolve the Promise with a message
    reject('Promise has been rejected...')
  } else {
    resolve('Promise has been resolved.')
  }
})

// Invoke the myPromise and first attach then() handler
// with a callback function to that accepts one parameter
// then attach catch() handler also with a callback function
// that accepts one parameter
myPromise
  .then((receivedData) => {
    // Log the data received by Promise
    console.log(receivedData)
  })
  .catch((error) => {
    // Log the error message received by Promise
    console.log(error)
  })
```

### The finally() handler function

The `finally()` is the last handler function you can use. What's special on this handler is that it will be invoked every time the Promise is `settled`. It will be invoked whether the Promise is `fulfilled` or `rejected`. This can be useful when you want to do something regardless of the final state of a Promise.

The `finally()` handler is used in the same way as the `then()` and `catch()`. You attach it to the Promise when you invoke it. The  `finally()` is usually attached as the last, after `then()` and `catch()` handlers. Unlike the previous two, this handler doesn't require any parameter because there is nothing passed into it.

```JavaScript
const myPromise = new Promise((resolve, reject) => {
  // Fake a delay
  setTimeout(function() {
    // Resolve the Promise with a message
    resolve('Promise has been resolved.')
  }, 1000)
})

// Invoke the myPromise and attach then() handler
// then attach catch() handler
// and then attach finally() handler
myPromise
  .then((receivedData) => {
    // Log the data received by Promise
    console.log(receivedData)
  })
  .catch((error) => {
    // Log the error message received by Promise
    console.log(error)
  })
  .finally(() => {
    // Log some notification message
    console.log('Promise is done.')
  })

// Output:
// 'Promise has been resolved.'
// 'Promise is done.'
```

## Promise methods

Working with JavaScript Promises is easy when you have to handle just one or two. What if you have to handle more Promise at once? Fortunately, JavaScript offers some methods that will make this easier for you. These methods are `all(),` `allSettled(),` `race()` and `any()`.

All these methods accept an iterable object such as an array. This object contains Promises you want to invoke. The difference is that each of these methods works in a different way and leads to different results. So, let's take a look at each.

### Promise.all()

When you pass Promises into `Promise.all()` it will try to resolve all of them. When all Promises you passed are resolved `Promise.all()` will return one Promise that contains all values. You can than access this value by attaching `then()` handler to the `Promise.all()`, along with callback function.

When something happens and one of those Promises gets rejected the `Promise.all()` will immediately return the rejected value. This is important to remember. If one Promise "fails" `Promise.all()` will return only the rejected value. It will not return data from any previously resolved Promise(s).

```JavaScript
// Example no.2: all Promises resolve
// Create first Promise that resolves
const myPromiseOne = new Promise((resolve, reject) => {
  // Fake a delay
  setTimeout(function() {
    // Resolve the Promise with a message
    resolve('myPromiseOne has been resolved.')
  }, 500)
})

// Create second Promise that resolves
const myPromiseTwo = new Promise((resolve, reject) => {
  // Fake a delay
  setTimeout(function() {
    // Resolve the Promise with a message
    resolve('myPromiseTwo has been resolved.')
  }, 1000)
})

// Use Promise.all() to process all Promises
Promise.all([myPromiseOne, myPromiseTwo])
  .then((data) => {
    // Log data when all Promises are resolved
    console.log(data)
  })
  .catch((error) => {
    // Log error message when some Promise is rejected
    console.log(error)
  })

// Output:
// [
//   'myPromiseOne has been resolved.',
//   'myPromiseTwo has been resolved.'
// ]


// Example no.2: the middle Promise rejects
// Create first Promise that resolves
const myPromiseOne = new Promise((resolve, reject) => {
  // Fake a delay
  setTimeout(function() {
    // Resolve the Promise with a message
    resolve('myPromiseOne has been resolved.')
  }, 500)
})

// Create second Promise that rejects
const myPromiseTwo = new Promise((resolve, reject) => {
  // Fake a delay
  setTimeout(function() {
    // Reject the Promise with a message
    reject('myPromiseTwo has been rejected.')
  }, 1000)
})

// Create third Promise that resolves
const myPromiseThree = new Promise((resolve, reject) => {
  // Fake a delay
  setTimeout(function() {
    // Resolve the Promise with a message
    resolve('myPromiseThree has been resolved.')
  }, 1500)
})

// Use Promise.all() to process all Promises
Promise.all([myPromiseOne, myPromiseTwo, myPromiseThree])
  .then((data) => {
    // Log data when all Promises are resolved
    console.log(data)
  })
  .catch((error) => {
    // Log error message when some Promise is rejected
    console.log(error)
  })

// Output:
// 'Error: myPromiseTwo has been rejected'

// !! Notice that the data from myPromiseOne that was resolved
// before the myPromiseTwo was rejected are missing
```

### Promise.allSettled()

Promise.allSettled() is also passed an iterable (usually an array of other promises) and will attempt to resolve all of them. If any of these promises throws an exception or rejects, its status is set to rejected.

wherease Promise.allSettled will await the completion of all promises.

An important note is that Promise.allSettled can never throw. You do not need to wrap it with try/catch - it will always resolve.

### Promise.race()

The Promise.race() method returns a promise that fulfills or rejects as soon as one of the promises in an iterable fulfills or rejects, with the value or reason from that promise. 1

### Promise.any()

## Conclusion: [...] ...

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[function expression]: https://blog.alexdevero.com/javascript-functions-pt1/#function-declaration-and-function-expression

<!--
### Meta:
-
-->

<!--
### Resources:
- https://blog.jonlu.ca/posts/promises
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
-->