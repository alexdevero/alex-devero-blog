The JavaScript event loop is one of the most important things to understand. It helps you understand how things work under the hood. You can then use this knowledge to write better JavaScript code, and also avoid problems. In this tutorial, you will learn what JavaScript event loop is and how it works.<!--more-->
<!--
Table of Contents:
-->

## Building blocks of JavaScript

In JavaScript, there are few fundamental building blocks. These blocks are [memory heap], [stack], [call stack], [web APIs], message queue and event loop. The memory heap is a place where JavaScript stores objects and functions. The stack is for storing static data, such as primitive data types values.

The call stack is a mechanism JavaScript uses to keep track of functions that needs to be executed. Web APIs are APIs built into your web browser. These APIs allow you to use features you could not otherwise. Some example are fetch API, geolocation API, WebGL API, Web Workers API and so on.

These APIs are not part of the JavaScript language itself. They are interfaces built on top of the core JavaScript language. This is also why they are available in all JavaScript environments. Another thing web APIs also handle are [async functions] and also `setTimeout` methods. Now, about the message queue and event loop.

## Message queue

The message queue is basically a storage. It is a place where JavaScript keeps "messages" it needs to proces. Each of these messages are basically callback functions used with async functions, such as `setTimeout`, and also events triggered by users. For example, clicks and keyboard events.

When any of these async functions gets executed, or events happen, JavaScript will first send them to the call stack. From here, JavaScript will send each function or event to appropriate web API to handle it. Once the API does what it needs to do, it will send a message with associated callback function to the message queue.

These messages are stored in message queue until the call stack is empty. When the call stack gets empty the first message in the queue, callback, will be pushed to the call stack. Call stack will execute that callback, and the code it contains.

There is one important thing about message queue. The call stack follows the LIFO principle. This means that first function pushed to the call stack will be processed as the last one. Message queue doesn't follow this principle. In case of message queue, it is the first message, or callback, that will be processed as the first.

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
-
-->

<!--
### Resources:
-
-->
