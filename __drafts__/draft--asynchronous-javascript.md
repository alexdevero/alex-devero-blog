
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
