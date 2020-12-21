# The JavaScript Event Loop Explained

The JavaScript event loop is one of the most important things to understand. It helps you understand how things work under the hood. In this tutorial, you will learn what JavaScript event loop is and how it works. You will also learn about a bit about call stack, web APIs and message queue.<!--more-->
<!--
Table of Contents:
## Building blocks of JavaScript
## Message queue
### A simple example of how message queue works
## Call stack, message queue and priorities
## Message queue processing and zero delays
## The JavaScript event loop
## A note about promises and async functions
## Conclusion: The JavaScript event loop explained
-->

## Building blocks of JavaScript

In JavaScript, there are few fundamental building blocks. These blocks are [memory heap], [stack], [call stack], [web APIs] (browser APIs), message queue and event loop. The memory heap is a place where JavaScript stores objects and functions. The stack is for storing static data, such as primitive data types values.

The call stack is a mechanism JavaScript uses to keep track of functions that needs to be executed. Web APIs are APIs built into your web browser. These APIs allow you to use features you could not otherwise. Some example are fetch API, geolocation API, WebGL API, Web Workers API and so on.

These APIs are not part of the JavaScript language itself. They are interfaces built on top of the core JavaScript language. This is also why they are not available in all JavaScript environments. Another thing web APIs also handle are async methods such as the `setTimeout` and also event. Now, about message queue and event loop.

## Message queue

The message queue is basically a storage. It is a place where JavaScript keeps "messages" it needs to proces. Each of these messages are basically callback functions used with async functions, such as `setTimeout`, and also events triggered by users. For example, clicks and keyboard events.

When any of these async functions gets executed, or events happen, JavaScript will first send them to the call stack. From here, JavaScript will send each function or event to appropriate web API to handle it. Once the API does what it needs to do, it will send a message with associated callback function to the message queue.

These messages are stored in message queue until the call stack is empty. When the call stack gets empty the first message in the queue, callback, will be pushed to the call stack. Call stack will execute that callback, and the code it contains.

There is one important thing about message queue. The call stack follows the LIFO principle. This means that last function pushed to the call stack will be processed as the first one. Message queue doesn't follow this principle. In case of message queue, it is the first message, or callback, that will be processed as the first.

### A simple example of how message queue works

Let's demonstrate this on the `setTimeout` method. When you use the `setTimeout` method JavaScript will send it to the call stack that will execute it. Executing it will create new timer. This timer will be send to appropriate web API. This API will then start the countdown.

When the countdown reaches zero, API will send the callback for the `setTimeout` method to the message queue. The callback will wait in the message queue until the call stack is empty. When the call stack is empty, JavaScript will take the callback in the message queue and push it to the call stack, which will then execute it.

```JavaScript
// Use setTimeout method to delay
// execution of some function
setTimeout(function cb() {
  console.log('Hello.')
}, 500)

// Step 1:
// Add to call stack: setTimeout(function cb() { console.log('Hello.') }, 500)

// Call stack                                         //
// setTimeout(function cb() { console.log('Hello.') } //
//                                                    //

// Step 2:
// Send cb() to web API
// and remove setTimeout from call stack
// and create timer: 500

// Call stack //
//            //
//            //

// web API     //
// timer, cb() //
//             //

// Step 3:
// When timer is up, send cb() to message queue
// and remove it from web API

// web API     //
//             //
//             //

// message queue //
// cb()          //
//               //

// Step 4:
// When call stack is empty, send cb() to call stack
// and remove it from message queue

// message queue //
//               //
//               //

// Call stack //
// cb()       //
//            //
```

## Call stack, message queue and priorities

In JavaScript, both call stack and message queue have different priorities. The priority of call stack is higher than the priority of message queue. As a result, the message queue has to wait until the call stack is empty before it can push anything from the queue to the call stack.

Only when the call stack is empty the message queue can push in the first message, or callback. When does this situation happen? The call stack will get empty when all function calls inside it, and call stacks of these calls, are executed. When this is happens, the call stack will be empty and available for message queue.

## Message queue processing and zero delays

Message queue can process only one message at the time. What's more, if message queue contains multiple messages each message has to be processed before any other message can. Processing of every message depends on the completion of the previous message. If one message takes more time to process other messages has to wait.

This principle is called [run-to-completion]. This has another implication called [zero delays]. Let's say you use `setTimeout` method and set the delay to 0. The idea is that the callback passed into this timeout should be executed immediately. The reality is that this might not happen.

As you know, message queue can process only one message at the time. Each message has to be completed before the queue can process another one. So, if you use `setTimeout` with delay set to 0 its callback will be executed immediately only if it is the first message in the message queue. Otherwise, it will have to wait.

## The JavaScript event loop

This is how JavaScript handles async operations. This is how operations are passed between call stack, web APIs and message queue. Even though JavaScript itself is single-threaded it can do this because the web APIs run on separate threads. What has the JavaScript event loop to do with this?

It is the JavaScript event loop what takes care of this cycle. It is the job of the JavaScript event loop to continuously check the call stack if it is empty or not. If it is empty, it will take the first message from the message queue and push it to the call stack.

If the call stack is not empty, event loop will not let any message from the queue in. Instead, it will let the call stack process call inside it. Each of these cycles, or iterations, of the event loop is called "tick".

## A note about promises and async functions

Async methods such as `setTimeout` and events are handled by web APIs and message queue. This doesn't apply to [async functions] and [promises]. Async functions and promises are handled by a different queue. This queue is called the job queue. Another name for this queue is microtask queue.

So, when you use promise, or async function, and `setTimeout` they will be handled differently. First, promises and async functions will be handled by the job queue. The `setTimeout` will be handled by the message queue. Second, job queue has a higher priority than message queue. This has one important implication.

Let's say you have a promise and also a `setTimeout`. The promise resolves immediately and that `setTimeout` has delay set to 0. So, it should also execute +/- immediately. To make this more interesting, let's also add another regular function. This function will be at the end. What will be the result of this?

The first function that will be executed will be the regular we put as the last one. As next will be executed any callback for the promise. The callback for the `setTimeout` will be executed as the last. It doesn't matter that the `setTimeout` method is placed above the promise in the code.

What does matter is that the job queue has a higher priority than message queue. As a result, when there is a race between promise and `setTimeout` it is the promise who will be the winner.

```JavaScript
// Create a function
function myFuncOne() {
  console.log('myFuncOne in setTimeout.')
}

// Create another function
function myFuncTwo() {
  console.log('myFuncTwo after the promise.')
}

// Delay the myFuncOne() by 0 seconds
setTimeout(myFuncOne, 0)

// Create a promise and resolve it immediately
new Promise((resolve, reject) => {
  resolve('Message from a promise')
})
  .then(res => console.log(res))

// Call the myFuncTwo()
myFuncTwo()

// Output:
// 'myFuncTwo after the promise.'
// 'Message from a promise'
// 'myFuncOne in setTimeout.'
```

## Conclusion: The JavaScript event loop explained

Understanding how the JavaScript event loop helps you understand how JavaScript works under the hood. To understand this you also need to understand topics such as call stack, web APIs and message queue. I hope that this tutorial helped you understand all these topics and, most importantly, the JavaScript event loop.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[stack]: https://blog.alexdevero.com/memory-life-cycle-heap-stack-javascript/#the-stack
[memory heap]: https://blog.alexdevero.com/memory-life-cycle-heap-stack-javascript/#the-memory-heap
[call stack]: https://blog.alexdevero.com/memory-life-cycle-heap-stack-javascript/#the-call-stack
[web APIs]: https://developer.mozilla.org/en-US/docs/Web/API
[async functions]: https://blog.alexdevero.com/javascript-async-await/#async-functions
[run-to-completion]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop#Run-to-completion
[zero delays]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop#Zero_delays
[promises]: https://blog.alexdevero.com/javascript-promises/

<!--
### Meta:
-
-->

<!--
### Keywords:
- JavaScript Event Loop
- Event Loop
-->

<!--
### Resources:
-
-->
