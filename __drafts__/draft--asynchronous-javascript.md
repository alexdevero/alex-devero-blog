
JavaScript is a single-threaded programming language. Only one thing can happen at a time. That said, there are ways to do multiple things without blocking the main thread. You can write asynchronous JavaScript code. In this tutorial, you will learn three ways that will help you do this.<!--more-->
<!--
Table of Contents:
-->

## A quick introduction to asynchronous JavaScript

By nature, JavaScript is a single-threaded programming language. It runs on a single thread. This thread is based on something called [event loop]. This thread responds to events when they occur. As a single-threaded language JavaScript can process only one thing at the time, one statement. During this, the thread is blocked.

This has some upsides. It makes it easier to write code. For example, you don't have to worry about problems related to [concurrency]. Your code will run sequentially, in the order in which you wrote it. You also don't have to worry about multiple tasks being executed at the same time.

There are also downsides. Probably the biggest is that there can be only one thing being executed at the time. Anything that follows after it has to wait until that thing is finished. This may not be a problem, until it is. For example, let's say you have an app that needs to get data from some API.

When you make a call to the API, in a synchronous way, this call will block the main thread until it is finished. During this time, the rest of your code has to wait until the call stop blocking the main thread. Until the, your app will stop responding.

```JavaScript
// Function to make an API call
function makeAPICall() {
  // Show notification about API call
  console.log('Calling some API.')
}

// Function to process the API data
function processAPIData() {
  // Show notification about processing data
  console.log('Data processed.')
}

// Another app function
// This function has to wait until
// the makeAPICall() and processAPIData() are finished
function someOtherFunction() {
  console.log('Some other function not related to API.')
}

// Make the API call
makeAPICall()

// Process data from API
processAPIData()

// Run some other function
someOtherFunction()

// Output:
// 'Calling some API.'
// 'Data processed.'
// 'Some other function not related to API.'
```

Opposite problem is when there is a delay. In that case, your code can run in a different order than you would want it to. As a result, part of your program may want to use data that is not available yet.

```JavaScript
// Function to process the API data
function processAPIData() {
  // Simulate a delay
  setTimeout(() => {
    // Show notification about processing data
    console.log('Data processed.')
  }, 2000)
}

// Function to make an API call
function makeAPICall() {
  // Show notification about API call
  console.log('Calling some API.')
}

// Function to read the API data
function readTheData() {
  console.log('Reading the data.')
}

// Another app function
// This function has to wait until
// the processAPIData(), makeAPICall()
// and readTheData() are done
// and stop blocking the main thread
function someOtherFunction() {
  console.log('Some other function not related to API.')
}

// Make the API call
makeAPICall()

// Process the data
processAPIData()

// Read the data
readTheData()

// Output:
// 'Calling some API.'
// 'Reading the data.'
// 'Data processed.'
```

Solution for this is writing asynchronous JavaScript code, making that API call asynchronous. When you write asynchronous JavaScript code multiple tasks can run concurrently, at the same time. When you run some asynchronous task it is put into event queue and so it is not blocking the main thread.

If the main thread is not blocked it can execute other tasks that follows. It can work on the rest of your code. When the asynchronous task in the event queue is finished it will return its result so you can work with it. There are three ways to achieve this: callbacks, promises and async/await.

## Callbacks

The first and oldest way to write asynchronous JavaScript code is by using callbacks. A callback is an asynchronous function that is passed as argument to other function when you call it. When that function you called finishes its execution it "calls back" the callback function.

Until this happens, the callback function is not executed. It is not doing anything. Most importantly, that callback function is not blocking the main thread so the main thread can take care of other things. One example where callbacks are still often used are [event listeners].

The `addEventListener()` method accepts three parameters. The first is the type of an event you want to listen to. The second is the callback function you want to execute when specific event occurs. The third, and optional, is an object with options. When the event occurs the callback function you provided will be executed.

```JavaScript
// Find a button in the dom
const btn = document.querySelector('#btn')

// Create handler function
function handleBtnClick() {
  console.log('Click!')
}

// Attach event listener to the btn,
// add pass in the handler function as a callback
// that will be executed when someone clicks the button
btn.addEventListener('click', handleBtnClick)

// Alternative:
// Write the callback function directly
btn.addEventListener('click', function() {
  console.log('Click!')
})
```

Callbacks are especially useful when you can't predict when some data will be available. Take the example with API call, data processing and delay. It can be impossible to predict when the API is finished. It can just as impossible to predict when the data processing is finished.

With callback functions you don't have to try to predict anything. What you have to do is to compose your functions in the order you need. For example, if processing the API data takes time, you can pass the function to read those data as a callback and execute it when the data are ready. Until then, it will not block anything.

```JavaScript
// Function to process the API data
function processAPIData() {
  // Simulate a delay
  setTimeout(() => {
    // Show notification about processing data
    console.log('Data processed.')

    readTheData()
  }, 2000)
}

// Function to make an API call
function makeAPICall() {
  // Show notification about API call
  console.log('Calling some API.')

  // Process received data
  processAPIData()

  // Show confirmation message
  console.log('API call finished.')
}

// Function to read the API data
function readTheData() {
  console.log('Reading the data.')
}

// Another app function
// This function will be executed
// before the processAPIData()
// and readTheData() are finished
function someOtherFunction() {
  console.log('Some other function not related to API.')
}

// Make the API call
makeAPICall()

// Run some other function
someOtherFunction()

// Output:
// 'Calling some API.'
// 'API call finished.'
// 'Some other function not related to API.'
// 'Data processed.'
// 'Reading the data.'
```

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
