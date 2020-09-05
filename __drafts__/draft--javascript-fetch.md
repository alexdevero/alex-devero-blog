# Getting Started With the JavaScript Fetch API

In the past, there were two ways to make requests. One was with `XMLHttpRequest`. The other was with jQuery, namely the `ajax()` method. Fortunately, JavaScript now offers a third way, the Fetch API.
In this tutorial, you will learn all you need to know to get started with JavaScript Fetch API.

<!--more-->
<!--
Table of Contents:
-->

## A quick introduction

The Fetch API is a newer addition to JavaScript standard. What this API does is it provides an easier and cleaner way to make server request. What's even better is that this API is based on [promises]. This makes it easier and more friendly to use. It is also what makes it preferable to both, `XMLHttpRequest` and also jQuery's `ajax()`.

## The basics of JavaScript Fetch API

When you want to make requests with fetch API you will mostly need two things. The first one is `fetch()` method. This method is what makes the request. This method requires one argument, the path or URL you want to make request to. Aside to this argument, you can also provide this method with config object.

This config object is optional. It allows you to set various settings for the request. For example, you can add headers, body with some data, set mode for cross-origin requests, enable cache, allow or disallow redirect, specify referrers and referrerPolicy, and so on. You can find all available options on [MDN].

```JavaScript
// Fetch syntax
fetch(someURL, {})

// or with optional config object
fetch(someURL, {/* settings go here */})
```

### Handling fetch with promise handler functions

The second thing you will need are [promise handler functions]. As we briefly discussed, the fetch API is based on promises. This means that every time you make a request the result, the data returned by `fetch()` method, will be a promise. In order to process this promise you will need to use one of the promise handler functions.

Two handler functions you will probably use the most often are `then()` and `catch()`. The `then()` handler function helps you handle fulfilled state of a promise. This applies to both, resolved and rejected promises. Another way to handle rejected promises is by using the `catch()`.

Both, the `then()` and `catch()` can handle rejected promises. However, only the `then()` can handle resolved promises. So, make sure to use the `then()` at least to handle resolved state of a promise. For handling the rejected state, decide if you want to use either `then()` and `catch()`.

When the fetch promise gets fulfilled, the data it received are automatically passed to handler functions attached to it. When you want to work with those data, you have to do it from the inside of those handler functions. If you want to make those data available outside them, you can assign the data to some outside variable.

```JavaScript
// Use fetch() method with promise handler functions
fetch(someUrl)
  .then(data => {
    // When promise gets resolved
    // log received data to console
    console.log(data)
  })
  .catch(error => {
    // If promise gets rejected
    // log the error to console
    console.log(error)
  })
```

As you can see on the example above, you can chain promise handler functions one after another. It is a good practice to put the `then()` function(s) as first and the `catch()` as second. If you also use `finally()`, it is a good practice to put that one as the last.

## Making request with fetch

## Conclusion: Getting Started With the JavaScript Fetch API

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[promises]: https://blog.alexdevero.com/javascript-promises/

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
