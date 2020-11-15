
JavaScript is a single-threaded programming language. Only one thing can happen at a time. That said, there are ways to do multiple things without blocking the main thread. You can write asynchronous JavaScript code. In this tutorial, you will learn three ways that will help you do this.<!--more-->
<!--
Table of Contents:
-->

## A quick introduction to asynchronous JavaScript

By nature, JavaScript is a single-threaded programming language. It runs on a single thread. This thread is based on something called [event loop]. This thread responds to events when they occur. As a single-threaded language JavaScript can process only one thing at the time, one statement. During this, the thread is blocked.

This has some upsides. It makes it easier to write code. For example, you don't have to worry about problems related to [concurrency]. Your code will run sequentially, in the order in which you wrote it. You also don't have to worry about multiple tasks being invoked at the same time.

There are also downsides. Probably the biggest is that there can be only one thing being invoked at the time. Anything that follows after it has to wait until that thing is finished. This may not be a problem, until it is. For example, let's say you have an app that needs to get data from some API.

When you make a call to the API, in a synchronous way, this call will block the main thread until it is finished. During this time, the rest of your code has to wait until the call stop blocking the main thread. Until the, your app will stop responding.

```JavaScript
// Function to make an API call
function makeAPICall() {
  // Show notification about API call
  console.log('Calling some API.')

  // Get the data
  console.log('Data received from the API.')
}

// Function to process the API data
function processAPIData() {
  // Show notification about processing data
  console.log('Data processed.')
}

// Function to read the API data
function readTheData() {
  console.log('Reading the data.')
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

// Read the data
readTheData()

// Run some other function
someOtherFunction()

// Output:
// 'Calling some API.'
// 'Data received from the API.'
// 'Data processed.'
// 'Reading the data.'
// 'Some other function not related to API.'
```

Opposite problem is when there is a delay. In that case, your code can run in a different order than you would want it to. As a result, part of your program may want to use data that is not available yet.

```JavaScript
// Function to make an API call
function makeAPICall() {
  // Show notification about API call
  console.log('Calling some API.')
  // Simulate a delay
  setTimeout(() => {
    // Get the data
    console.log('Data received from the API.')

    // Show confirmation message
    console.log('API call finished.')
  }, 2000)
}

// Function to process the API data
function processAPIData() {
  // Show notification about processing data
  console.log('Data processed.')
}

// Function to read the API data
function readTheData() {
  console.log('Reading the data.')
}

// Another app function
function someOtherFunction() {
  console.log('Some other function not related to API.')
}

// Make the API call
makeAPICall()

// Process the data
processAPIData()

// Read the data
readTheData()

// Do some other stuff
someOtherFunction()

// Output:
// 'Calling some API.'
// 'Data processed.'
// 'Reading the data.'
// 'Some other function not related to API.'
// 'Data received from the API.'
// 'API call finished.'
```

Solution for this is writing asynchronous JavaScript code, making that API call asynchronous. When you write asynchronous JavaScript code multiple tasks can run concurrently, at the same time. When you run some asynchronous task it is put into event queue and so it is not blocking the main thread.

If the main thread is not blocked it can execute other tasks that follows. It can work on the rest of your code. When the asynchronous task in the event queue is finished it will return its result so you can work with it. There are three ways to achieve this: callbacks, Promises and async/await.

## Callbacks

The first and oldest way to write asynchronous JavaScript code is by using callbacks. A callback is an asynchronous function that is passed as argument to other function when you call it. When that function you called finishes its execution it "calls back" the callback function.

Until this happens, the callback function is not invoked. It is not doing anything. Most importantly, that callback function is not blocking the main thread so the main thread can take care of other things. One example where callbacks are still often used are [event listeners].

The `addEventListener()` method accepts three parameters. The first is the type of an event you want to listen to. The second is the callback function you want to execute when specific event occurs. The third, and optional, is an object with options. When the event occurs the callback function you provided will be invoked.

```JavaScript
// Find a button in the dom
const btn = document.querySelector('#btn')

// Create handler function
function handleBtnClick() {
  console.log('Click!')
}

// Attach event listener to the btn,
// add pass in the handler function as a callback
// that will be invoked when someone clicks the button
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
// Function to make an API call
function makeAPICall() {
  // Show notification about API call
  console.log('Calling some API.')

  // Simulate a delay
  setTimeout(() => {
    // Get the data
    console.log('Data received from the API.')

    // Process received data
    processAPIData()

    // Show confirmation message
    console.log('API call finished.')
  }, 2000)
}

// Function to process the API data
function processAPIData() {
  // Show notification about processing data
  console.log('Data processed.')

  readTheData()
}

// Function to read the API data
function readTheData() {
  console.log('Reading the data.')
}

// Another app function
// This function will be invoked
// right after the makeAPICall() function
// and before all other functions
function someOtherFunction() {
  console.log('Some other function not related to API.')
}

// Make the API call
makeAPICall()

// Run some other function
someOtherFunction()

// Output:
// 'Calling some API.'
// 'Some other function not related to API.'
// 'Data received from the API.'
// 'Data processed.'
// 'Reading the data.'
// 'API call finished.'
```

## Promises

The second way to write asynchronous JavaScript code are Promises. Promises are a newer feature, introduced to JavaScript with the [ES6 specification]. They provide a very easy way to deal with asynchronous JavaScript code. This one reason why many JavaScript developers, if not almost all, started using them instead of callbacks.

A [Promise] is an object that represents some value. This value is not known at the time you create the Promise. It will be known somewhere in the future. Promise returns this value by being either "fulfilled" or "rejected". "Fulfilled" means that Promise is successful. "Rejected" means that Promise failed, for some reason.

Promise that is either "fulfilled" or "rejected" is "settled". Until a Promise is "settled" it is pending. These are the four states a Promise can exist in: pending, "fulfilled", "rejected" and "settled". There are three [handler functions] you can use to get the value returned by a Promise.

These handler functions are `then()`, `catch()` and `finally()`. The way to use these handlers is by attaching them to a Promise object. Depending on the state of a Promise, one of these handlers will be invoked. The `then()` will be invoked when Promise is "fulfilled", but you can also use it to handle "rejected" state.

The `catch()` will be invoked only when Promise is "rejected". The last one, `finally()`, will be invoked when Promise is "settled". This also means that `finally()` will be invoked every time, no matter if Promise is "fulfilled" or "rejected". To learn more about Promises take a look at this [tutorial].

```JavaScript
// Create new Promise to make the API call
const makeAPICall = new Promise((resolve, reject) => {
  // Show notification about API call
  console.log('Calling some API.')

  setTimeout(() => {
    // Get the data
    console.log('Data received from the API.')

    // Process received data
    resolve('API call finished.')
  }, 2000)
})

// Create a function to process the API data
function processAPIData() {
  // Show notification about processing data
  console.log('Data processed.')
}

// Create a function to read the API data
function readTheData() {
  // Process received data
  console.log('Reading the data.')
}

// Add some additional function
// This function will be able to run
// right after the makeAPICall Promise
// and before all other functions
function someOtherFunction() {
  console.log('Some other function not related to API.')
}

// Make the API call
makeAPICall
  // And handler for fulfilled state of the Promise
  .then(resOne => {
    // Log the message from makeAPICall Promise
    console.log(resOne)

    // Process the data
    processAPIData()

    // Read the data
    readTheData()
  })
  // And handler for rejected state of the Promise
  .catch(error => {
    console.log(`There has been an error during the API call: ${error}.`)
  })
  // Optionally, you could add finally() here
  // .finally(() => {})

// Run some other function
someOtherFunction()

// Output:
// 'Calling some API.'
// 'Some other function not related to API.'
// 'Data received from the API.'
// 'API call finished.'
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
