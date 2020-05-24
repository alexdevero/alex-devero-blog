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

## Resolving and rejecting Promises

When you want the Promise to return some data, you pass those data into the `resolve`. For example, when your Promises makes a call to an API you pass into the `resolve` the data returned from the API. If some error occurs you can pass the data about the error to the `reject` callback. Or, some error message.

```JavaScript
// Promise syntax example
const myPromise = new Promise(function(resolve, reject) {
  // Resolving a Promise passing a message as a data
  resolve('Success: promise resolved.')

  // If some error happens
  if (error) {
    // Rejecting a Promise passing a message as a data
    reject('Failure: promise rejected')
  }
})

// Invoke the Promise
myPromise


// Promise syntax example using an arrow function
const myPromise = new Promise((resolve, reject) => {
  // Resolving a Promise passing a message as a data
  resolve('Success: promise resolved.')

  // If some error happens
  if (error) {
    // Rejecting a Promise passing a message as a data
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
  // Resolving a Promise passing a message as a data
  resolve('Success: promise resolved.')

  // If some error happens
  if (error) {
    // Rejecting a Promise passing a message as a data
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
    // Resolving a Promise passing a message as a data
    resolve('Success: promise resolved.')

    // If some error happens
    if (error) {
      // Rejecting a Promise passing a message as a data
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

## Handling JavaScript Promises

You know how to create a Promise and the four states in which it can be. What you need to next is how to handle Promise. You need to know how you can work with the data returned by a Promise, data passed into `resolve` and `reject` callbacks. This is where `then()`, `catch()` and `finally()` comes into game.

The `then()`, `catch()` and `finally()` are handler function you can attach to a Promise. These handlers are important. When you invoke a Promise and the promise is settled (resolved or rejected) one of these handlers will be automatically invoked. When there are some data returned from a Promise it is passed into these handlers.

If you want to work with the data returned by a Promise these handlers are the place where to do it. For example, you could put logic for updating your app with the data you received from API into these handlers. What if you don't use any of these handlers?The Promise would still run after you invoke it.

However, there would be nothing processing the data it returns. The data would be basically locked inside the Promise object. This is why these handlers are important. They are like messengers that transport the message from Promise further down the chain.

## Promise methods

### Promise.all()

Promise.all will immediately reject if any of the promises fail to resolve, wherease Promise.allSettled will await the completion of all promises.

Promise.all() is passed an iterable (usually an array of other promises) and will attempt to resolve all of them. If any of these promises throws an exception or rejects, Promise.all will immediateley invoke its reject.

### Promise.allSettled()

Promise.allSettled() is also passed an iterable (usually an array of other promises) and will attempt to resolve all of them. If any of these promises throws an exception or rejects, its status is set to rejected.

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
