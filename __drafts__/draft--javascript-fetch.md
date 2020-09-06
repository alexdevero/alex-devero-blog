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
  .then(response => {
    // When promise gets resolved
    // log received data to console
    console.log(response)
  })
  .catch(error => {
    // If promise gets rejected
    // log the error to console
    console.log(error)
  })


// Real-world example
fetch('https://sv443.net/jokeapi/v2/joke/Programming')
  // Convert response to JSON format
  .then(response => response.json())
  // Log the response JSON
  .then(jsonData => console.log(jsonData))
  .catch(error => {
    // If promise gets rejected
    // log the error to console
    console.log(error)
  })

// Output:
// {
//   error: false,
//   category: 'Programming',
//   type: 'twopart',
//   setup: 'Programming is like sex.',
//   delivery: 'Make one mistake and you end up supporting it for the rest of your life.',
//   flags: {
//     nsfw: true,
//     religious: false,
//     political: false,
//     racist: false,
//     sexist: false
//   },
//   id: 8,
//   lang: 'en'
// }
```

As you can see on the example above, you can chain promise handler functions one after another. It is a good practice to put the `then()` function(s) as first and the `catch()` as second. If you also use `finally()`, it is a good practice to put that one as the last.

### Handling fetch with await

Another option, if you don't want to use promise handler functions, is [await]. The `await` does two things. First, it pauses the execution of surrounding code until a promise that follows this keyword is fulfilled. The second thing `await` does is it replaces the `then()` function. It automatically extracts and assigns the data returned by a promise to a variable.

There are two things to remember if you want to use `await`. First, use it inside [try...catch] statement. The await supplements the `then()` function. However, it doesn't supplement the `catch()`. If you want to catch any error that can arise you can catch with the `try...catch` statement.

The second thing is that until [top-level await] is released, you can use `await` only in [async functions]. This is what you can do. Use `fetch()` along with `await`. Then, wrap these two with `try...catch` statement and put it all inside `async` function.

```JavaScript
// Create async function
async function makeRequest() {
  // Use try...catch statement
  try {
    // Use await and make fetch request
    const responseData = await fetch('https://sv443.net/jokeapi/v2/joke/Any')
    // Convert the response to JSON format
    const responseJSON = await responseData.json()

    // Log the converted JSON
    console.log(responseJSON)
  }
  catch (error) {
    // Log any error
    console.log(error)
  }
}

// Call the makeRequest()
makeRequest()
// Output:
// {
//   error: false,
//   category: 'Miscellaneous',
//   type: 'twopart',
//   setup: "Mom asked me where I'm taking her to go out to eat for mother's day.",
//   delivery: 'I told her, "We already have food in the house".',
//   flags: {
//     nsfw: false,
//     religious: false,
//     political: false,
//     racist: false,
//     sexist: false
//   },
//   id: 89,
//   lang: 'en'
// }
```

### Processing the response

When you make a request the promise returned by `fetch()` returns a response in the form of a object. This object contains information received from the server and also various methods. We can use these methods to work with the data. These methods are `clone()`, `redirect()`, `arrayBuffer()`, `formData()`, `blob()`, `text()` and `json()`.

The `clone()` method creates a clone of the response. The `redirect()` method creates a new response, but with a different URL. The `arrayBuffer()` returns the response as [ArrayBuffer]. The `formData()` returns the response as [FormData] object. The `blob()` returns returns the response as a Blob.

The `text()` returns the response as a string, or text. The last one, the `json()`, returns the response as a JSON. Which of these methods you should use to parse the response depends on what type of data you expect. For example, if you expect to receive data in the form of a JSON then use `json()`, if text use `text()` and so on.

The nice thing about these method is that you don¨t necessarily need to know what response should you expect. These methods that parses the response, such as the `text()` and `json()` will often work even if you pick wrong method for the job. For example, let's say you use the `text()` method, but response will be a JSON.

In that case, the `text()` method will be able to pick that JSON and parse it as a string. The result will be basically stringified JSON. That said, the same will not work with text response and `json()`. The `json()` expects specific syntax. If the response is a plain text, and you use `json()`, you will get syntax error.

So, if you are not sure what type of response you should expect, use `text()`. In the worst case, you will get some stringified JSON and you will know that you should use `json()` instead. If you expect other format, use corresponding method: `response.formData()`, `response.blob()` or `response.arrayBuffer()`.

```JavaScript
// Example no.1:
// Parsing response as a text
async function makeRequest() {
  // Use try...catch statement
  try {
    // Make fetch request
    const responseData = await fetch('https://sv443.net/jokeapi/v2/joke/Programming')

    // Parsing as Text happens here:
    // Parse the response as a text
    const responseText = await responseData.text()

    // Log the text
    console.log(responseText)
  }
  catch (error) {
    // Log any error
    console.log(error)
  }
}

// Call the makeRequest()
makeRequest()
// Output:
// '{
//   error: false,
//   category: 'Programming',
//   type: 'single',
//   joke: 'Programming is 10% science, 20% ingenuity, and 70% getting the ingenuity to work with the science.',
//   flags: {
//     nsfw: false,
//     religious: false,
//     political: false,
//     racist: false,
//     sexist: false
//   },
//   id: 37,
//   lang: 'en'
// }'

// Alternative:
fetch('https://sv443.net/jokeapi/v2/joke/Programming')
  .then(response => response.text())
  .then(responseText => console.log(responseText))
  .catch(err => console.log(err))


// Example no.2:
// Parsing response as a text
async function makeRequest() {
  // Use try...catch statement
  try {
    // Make fetch request
    const responseData = await fetch('https://sv443.net/jokeapi/v2/joke/Programming')

    // Parsing as JSON happens here:
    // Parse the response as a JSON
    const responseJSON = await responseData.json()

    // Log the JSON
    console.log(responseJSON)
  }
  catch (error) {
    // Log any error
    console.log(error)
  }
}

// Call the makeRequest()
makeRequest()
// Output:
// {
//   error: false,
//   category: 'Programming',
//   type: 'twopart',
//   setup: 'How do you generate a random string?',
//   delivery: 'Put a Windows user in front of Vim and tell him to exit.',
//   flags: {
//     nsfw: false,
//     religious: false,
//     political: false,
//     racist: false,
//     sexist: false
//   },
//   id: 129,
//   lang: 'en'
// }

// Alternative:
fetch('https://sv443.net/jokeapi/v2/joke/Programming')
  .then(response => response.json())
  .then(responseJSON => console.log(responseJSON))
  .catch(err => console.log(err))
```

### Processing already processed response

When you process the response with one method, to parse it in one format you can't process it again, and parse it to another format. If you parse the response as a text, you can't then take the response and parse it again as a JSON. After you parse the response for once it will be locked. Parsing it again will lead to TypeError.

```JavaScript
async function makeRequest() {
  // Use try...catch statement
  try {
    // Make fetch request
    const responseData = await fetch('https://sv443.net/jokeapi/v2/joke/Programming')

    // Parse the response as a text
    const responseText = await responseData.text()

    // This will not work after the first parsing
    // Try to parse the response again as a JSON
    const responseJSON = await responseData.json()

    // Log the text
    console.log(responseText)

    // Log the JSON
    console.log(responseJSON)
  }
  catch (error) {
    // Log any error
    console.log(error)
  }
}

makeRequest()
// Output:
// TypeError: Failed to execute 'json' on 'Response': body stream is locked
```

## Making request with fetch

The default type of request the `fetch()` method makes is `GET`. If you want make a different type of request you can change it. You can chang the type of request through the optional config object you can pass as the second argument to the `fetch()` method. For example, you can set `method` to `POST` to make a `POST` request and so on.

### The GET request

If you use the `fetch()` method as it is and provide it only with URL, it will automatically execute `GET` request.

```JavaScript
// GET request example
async function makeGetRequest() {
  // Use try...catch statement
  try {
    // Make GET fetch request
    const responseData = await fetch('https://sv443.net/jokeapi/v2/joke/Programming')

    // Parse the response as a JSON
    const responseJSON = await responseData.json()

    // Log the JSON
    console.log(responseJSON)
  }
  catch (error) {
    // Log any error
    console.log(error)
  }
}

// Call the makeGetRequest()
makeGetRequest()
// Output:
// {
//   error: false,
//   category: 'Programming',
//   type: 'single',
//   joke: "Knock knock.
// Who's there?
// Recursion.
// Recursion who?
// Knock knock.",
//   flags: {
//     nsfw: false,
//     religious: false,
//     political: false,
//     racist: false,
//     sexist: false
//   },
//   id: 182,
//   lang: 'en'
// }


// Alternative with promise handler functions:
fetch('https://sv443.net/jokeapi/v2/joke/Programming')
  .then(response => response.json())
  .then(responseJSON => console.log(responseJSON))
  .catch(err => console.log(err))
```

### The POST request

Another popular type of request is `POST`. You can make this type of request with fetch API if you change the `method` on config object. This object is the second, optional, argument you can pass to `fetch()`. If you set the `method` to `POST` the `fetch()` method will execute a `POST` request.

When you make a `POST` request you will need to send some data. You can add these data through `body` option. This option is also in the config object. In addition, you may also want to change the `Content-Type`. You can do this via `headers` option. However, for a simple `POST` just the `method` and `body` might be enough.

```JavaScript
// Some data to send
const userData = {
  firstName: 'Tom',
  lastName: 'Jones',
  email: 'tom@jones.ai'
}

// Make POST request
async function makePostRequest() {
  // Use try...catch statement
  try {
    // Make fetch request
    const responseData = await fetch('/users/register', {
      method: 'POST', // Change the request method
      headers: { // Change the Content-Type
        'Content-Type': 'application/json;charset=utf-8'
      },
      body: JSON.stringify(userData) // Add data you want to send
    })

    // Parse the response as a JSON
    const responseJSON = await responseData.json()

    // Log the JSON
    console.log(responseJSON)
  }
  catch (error) {
    // Log any error
    console.log(error)
  }
}

// Call the makeRequest()
makePostRequest()


// Alternative with promise handler functions:
fetch('/users/register', {
  method: 'POST', // Change the request method
  headers: { // Change the Content-Type
    'Content-Type': 'application/json;charset=utf-8'
  },
  body: JSON.stringify(userData) // Add data you want to send
})
  .then(response => response.json())
  .then(responseJSON => console.log(responseJSON))
  .catch(err => console.log(err))
```

## Conclusion: Getting Started With the JavaScript Fetch API

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[promises]: https://blog.alexdevero.com/javascript-promises/
[MDN]: https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/fetch
[promise handler functions]: https://blog.alexdevero.com/javascript-promises/#handling-javascript-promises-with-handler-functions
[await]: https://blog.alexdevero.com/javascript-async-await/
[try...catch]: https://blog.alexdevero.com/error-handling-javascript/#error-handling-and-try8230catch-statement
[top-level await]: https://github.com/tc39/proposal-top-level-await
[async functions]: https://blog.alexdevero.com/javascript-async-await/
[ArrayBuffer]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer
[FormData]: https://developer.mozilla.org/en-US/docs/Web/API/FormData

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
