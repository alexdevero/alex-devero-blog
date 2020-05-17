# Error Handling in JavaScript for Beginners
<!--more-->
<!--
Table of Contents:
## Two main types of errors
### Syntax errors
### Runtime errors
## Error handling and try...catch statement
### Catch
### Try, catch and control
### Using multiple try...catch statements
### Finally
### Somewhat optional catch
### Try...catch statement inside functions
## Creating and throwing errors
### Creating simple errors
### Creating errors with JavaScript built-in error constructors
### Creating custom errors with Function constructor and class
## Error handling globally
## Conclusion: Error Handling in JavaScript
-->

## Two main types of errors

When it comes to error handling in JavaScript there are two types of errors you can stumble upon. The first type of errors are syntax errors. The second type are runtime errors.

### Syntax errors

Syntax errors are also called parsing errors. This is errors occur when JavaScript parser interprets your code. When one of these errors occurs it only affect the code that in the same thread. The rest of code is left unaffected. An example of syntax error can be forgotten opening or closing parenthesis or bracket.

Another example can be missing coma or colon in object. Any of these errors will cause the syntax to be invalid and break your program. There are some ways to avoid these types of errors. One is checking your code and looking for them. This is not effective and can take a lot of time.

Another option is using some tool or IDE plugin. These tools will automatically scan your code and look for any syntax issues for you. Three most popular tools that will help you catch syntax errors are [eslint], [jshint] and [jslint]. Eslint is my favorite. I use in almost all my projects.

These tools are so popular, and developers don't like repetitive tasks. This makes it likely there is a plugin for each of these tools you can install in IDE you are using. If you find some I highly recommend installing it and using it. It can save you a lot of headaches.

### Runtime errors

The second type of errors are runtime errors. These errors are also called exceptions. These errors occur during execution of your code, when you run it. One simple example can be calling a method that doesn't exist. Another can be passing string to a function instead of number, or the other way around.

Important is that each of these errors is valid in the view of JavaScript. Yes, you may misspell some variable or function name. However, the syntax itself is still valid. There are no missing colons or brackets. If this is true JavaScript will let your code compile. You run into these errors only when you run your code.

This is also what makes runtime errors more difficult to handle. It is also why it is a very good idea to write and also run [unit tests]. Aside to that, there is no plugin that would help you spot these errors before they occur. Well, this is true only partially. You can use a JavaScript superset, such as [TypeScript].

If your IDE has support for one of these supersets, it it will help you detect runtime errors. For example, when you use TypeScript in VS Code it will warn you when some function or variable you want to use is undefined. It will also suggest methods and variables you previously defined while you write your code.

Aside to this, there are some JavaScript built-in tools that will make error handling easier for you. Let's take a look at these tools.

## Error handling and try...catch statement

The first tool for error handling is a `try...catch` statement. This statement might look similar to `if...else` statement. It also contains two blocks of code, wrapped with curly braces. However, there are no parenthesis before the first block, the `try` block. This `try` block contains the code you want to try to run.

```JavaScript
try {
  // some code
}
```

That said, your whole code doesn't have to defined in one giant `try` block. Instead, you put into the `try` block only what you want to run. For example, let's say you want to declare some [function]. You can declare this function somewhere outside the `try` block, but you invoke the function inside it.

```JavaScript
// Declare function outside try block
function myFunction() {
  // do something
}

// Create try block
try {
  // And invoke the function inside it
  myFunction()
}
```

### Catch

When you do this, the `try` block will call that function. If your function runs without any errors nothing will happen. If there are some runtime errors? This is where `catch` block comes into play. The `catch` block looks similar to `try`. One difference is that there are parenthesis after the `catch` keyword and before opening curly brace.

Inside these parenthesis is defined one parameter. This parameter is a error object. This object contains information about the error that occurred. It contains name of the error, the error message and current call stack. The `catch` block is a place where you define what to do when an error occurs.

```JavaScript
// Create try...catch statement
try {
  // Run some code
}
catch(error) { // error is the error object, you can use a different name
  // Do something when an error occurs
}


// Example:
// Create try...catch statement
try {
  // Try to invoke function that doesn't exist
  myFunc()
}
catch(error) {
  console.log('Error name: ', error.name)
  console.log('Error message: ', error.message)
  console.log('Error stack: ', error.stack)
  console.log('Error: ', error)
}

// Outputs:
// 'Error name: ' 'ReferenceError'

// 'Error message: ' 'myFunction is not defined'

// 'Error stack: ' `ReferenceError: myFunction is not defined
//     at eval (eval at <anonymous> (:7:47), <anonymous>:4:3)
//     at <anonymous>:7:47
//     at <anonymous>:15:9`
//     ...

// 'Error: ' ReferenceError: myFunction is not defined
    // at eval (eval at <anonymous> (:7:47), <anonymous>:4:3)
    // at <anonymous>:7:47
    // at <anonymous>:16:9
    //     ...
```

The parenthesis and error object after the `catch` keyword, and before opening curly brace, are optional. It is used to pass the information about error. If you don't want to use these information, you can omit both, the parenthesis and error object. The `try...catch` statement will still work.

```JavaScript
// Create try...catch statement
try {
  // Try to invoke function that doesn't exist
  myFunction()
}
catch { // Omit parenthesis and error object
  // Show some custom error message
  console.log('An error occurred.')
}

// Outputs:
// 'An error occurred.'
```

### Try, catch and control

The code inside `catch` block is execute immediately when some runtime error occurs. This is important remember. If some code you execute in `try` block leads to an error any code that follows, inside the same `try` block, will not be execute. The `catch` block will automatically assumes control and processes the error.

```JavaScript
// Create function that leads to an error
function myFuncWithError() {
  throw 'Error'
}

// Create another function that doesn't lead to an error
function myFunc() {
  console.log('Hello.')
}

// Create try...catch statement
try {
  // Invoke the myFuncWithError function
  // If this function causes error...
  myFuncWithError()

  // Invoke the myFunc function
  // ...this function will never be invoked
  myFunc()
}
catch(error) {
  // Log any error message
  console.log(error)
}

// Outputs:
// 'Error'

// Note:
// Only myFuncWithError() function was invoked
// then control shifted to catch block
// and myFunc() function was never invoked
```

### Using multiple try...catch statements

There is a way to fix this. In JavaScript, there is no limit to how many `try...catch` statements you can use. There is also no rule that you have to use one for all your code. If anything, you should actually do the opposite. Using multiple `try...catch` statements allows you to isolate errors and not let it affect the rest of your code.

If you want to invoke both functions, the easiest thing you can do is to create two `try...catch` statements. Then, you can invoke one function in the first statement and another function in the second.

```JavaScript
// Create function that leads to an error
function myFuncWithError() {
  throw 'Error'
}

// Create another function that doesn't lead to an error
function myFunc() {
  console.log('Hello.')
}

// Create first try...catch statement
try {
  // Invoke the myFuncWithError function
  myFuncWithError()
}
catch(error) {
  // Log any error message
  console.log(error)
}

// Create second try...catch statement
try {
  // Invoke the myFunc function
  myFunc()
}
catch(error) {
  // Log any error message
  console.log(error)
}

// Outputs:
// 'Error'
// 'Hello.'

// Note: both functions were successfully invoked
// because error that occurred in the first
// was caught by the first try...catch statement
// and had no effect on the second function
```

The example would work with any number of function, or code, you want to invoke or execute. You could create tens or more `try...catch` statements each to handle one specific use case. Then, any error that would occur would not affect the rest of your code, invoked or executed in other `try...catch` statements.

As you can see, the `try...catch` statement is really powerful tool for error handling. It allows you to run pieces of your code without letting it crash other pieces, or your whole application. That said, there is more.

### Finally

The `try...catch` statement can help you make error handling easy.However, there is also `finally` block you can use. The `try` invokes the code inside the block. The `catch` is invoked when error occurs. The `finally` is invoked at the end of each `try...catch...finally` statement.

The important thing is that the `finally` is invoked in all cases. It doesn't matter if there is an error or not. The `finally` will be invoked. This can be useful when you do something at the end of each block. The syntax of `finally` is the same as the syntax for `try`.

There is the `finally` keyword followed by block of code to execute wrapped with curly braces. There are no parenthesis, even optional.

```JavaScript
// Create try...catch...finally statement
try {
  // Run some code
}
catch(err) {
  // Log any error message
  console.log(err)
}
finally {
  // Do something whether is an error or not
}


// Example:
try {
  // Try to invoke non-existing function
  myFunc()
}
catch(err) {
  // Log any error message
  console.log(err.message)
}
finally {
  // Log a message at the end of execution of the try...catch...finally statement
  console.log('The end of try...catch...finally statement.')
}

// Outputs:
// 'myFunc is not defined'
// 'The end of try...catch...finally statement.'
```

### Somewhat optional catch

So far, we always did error handling using all blocks of `try...catch` or `try...catch...finally` statement. One thing you should know is that the `catch` is, similarly to the `finally`, also optional. Having said that, that doesn't mean it is a good idea to omit it.

When you omit the `catch` block any error that occurs during execution of `try` block will "leak" outside. Without the `catch` block, there is nothing that catch any error and process it. So, can you omit it? Yes. You can use only `try` or `try...finally`. Both, will works. However, no errors will be caught.

```JavaScript
// Create try statement
try {
  myFunc()
}


// Create try...finally statement
try {
  myFunc()
}
finally {
  console.log('try...finally is finished.')
}
```

### Try...catch statement inside functions

All previous show error handling sing `try...catch` in a global scope, outside any functions. This doesn't mean `try...catch` statement is restricted to global scope. It is not. You can use in a global scope or a local scope, created by a function for example. It will work just as well.

```JavaScript
// Declare new function that takes one parameter
function myFunction(name) {
  // Add try...catch statement
  try {
    // If value passed as name parameter is not a string
    if (typeof name !== 'string') {
      // Throw a TypeError
      throw new TypeError('The name value of parameter must be a string!')
    } else {
      console.log(`Hello ${name}.`)
    }
  }
  catch(err) {
    // Log
    console.log(err)
  }
}

myFunction(11)
// Outputs:
// TypeError: The name value of parameter must be a string!
//     at myFunction (eval at <anonymous> (:7:47), <anonymous>:6:13)
//     at eval (eval at <anonymous> (:7:47), <anonymous>:13:1)
//     at <anonymous>:7:47
//     at <anonymous>:19:23
//     ...

myFunction('Jack')
// Outputs:
// 'Hello Jack.'
```

## Creating and throwing errors

For error handling you can use either built-in JavaScript errors or you can define your own. With both approaches, you will use `throw` statement. This statement specifies the value you want to throw as an error. You already used this statement in example in the "Try, catch and control" section, inside the `declaration myFuncWithError() function`.

### Creating simple errors

Let's take a look at the first way to create a custom error. This will be a very simple error. You will do it by using `throw` statement with a string, number or any other [data type]. For example, let's create a simple function that when you invoke it it will throw a custom error. This custom error will be a string.

```JavaScript
// Create function
function myFunc() {
  // Throw a custom error
  throw 'My custom error.'
}

// Create try...catch statement
try {
  // Invoke the myFunc() function
  myFunc()
}
catch(err) {
  // Log the error
  console.log('Error: ', err)
  console.log('Error name: ', err.name)
  console.log('Error message: ', err.message)
  console.log('Error stack: ', err.stack)
}

// Outputs:
// 'Error: ' 'My custom error.'
// 'Error name: ' undefined
// 'Error message: ' undefined
// 'Error stack: ' undefined
```

As you can see, creating a simple error is easy. The downside of creating errors this way is that these custom errors will not have `name`, `message` and `stack` properties. There is a way to fix this. A simple way to do it is by using an object instead of a primitive data type.

So, instead of throwing a string or other primitive, you will throw an object. Inside this object, you will define all the properties that would normally exist in an error object, the `name`, `message` and `stack`. Now, when this custom error occurs you can also access its `name`, `message` and `stack`.

```JavaScript
// Create function
function myFunc() {
  // Throw a custom error object
  throw {
    name: 'MyCustomError',
    message: 'An error occurred.',
    stack: 'myFunc()'
  }
}

try {
  // Invoke the myFunc() function
  myFunc()
}
catch(err) {
  // Log the error
  console.log('Error: ', err)
  console.log('Error name: ', err.name)
  console.log('Error message: ', err.message)
  console.log('Error stack: ', err.stack)
}

// Outputs:
// 'Error: ' {
//   name: 'MyCustomError',
//   message: 'An error occurred.',
//   stack: 'myFunc()'
// }
// 'Error name: ' 'MyCustomError'
// 'Error message: ' 'An error occurred.'
// 'Error stack: ' 'myFunc()'
```

### Creating errors with JavaScript built-in error constructors

Another option for creating new errors is by using JavaScript built-in error constructors, such as `Error`, `TypeError`, `ReferenceError`, `SyntaxError`, `RangeError`, `EvalError`, `InternalError` and `URIError`. You will use `throw` statement to throw these custom errors as well. You will also have to use keyword `new` along with one the constructor's names.

The `new` keyword says that you are creating a new instance of a constructor. In this case, some error constructor. When you use one of these constructors the `name` property inside the `error` object will be the constructor you used. The `message` will be the string you pass as an argument when you instantiate the constructor.

```JavaScript
// Create function
function myFunc() {
  // Throw a custom error using Error constructor
  // The Error will be the "name" property in error object
  // The 'An error occurred.' will be the "message" property in error object
  throw new Error('An error occurred.')
}

try {
  myFunc()
}
catch(err) {
  console.log('Error: ', err)
  console.log('Error name: ', err.name)
  console.log('Error message: ', err.message)
  console.log('Error stack: ', err.stack)
}

// Outputs:
// 'Error: ' Error: An error occurred.
//     at myFunc (eval at <anonymous> (:7:47), <anonymous>:4:9)
//     at eval (eval at <anonymous> (:7:47), <anonymous>:8:3)
//     at <anonymous>:7:47
//     at <anonymous>:20:9
//     ...

// 'Error name: ' 'Error'

// 'Error message: ' 'An error occurred.'

// 'Error stack: ' `Error: An error occurred.
//     at myFunc (eval at <anonymous> (:7:47), <anonymous>:4:9)
//     at eval (eval at <anonymous> (:7:47), <anonymous>:8:3)
//     at <anonymous>:7:47
```

### Creating custom errors with Function constructor and class

Along with JavaScript built-in error constructors you can also create custom errors with [Function constructor] or [class]. Here is how. You have to use function constructor to create a new custom error. This function constructor will take one parameter when you use it. This will be the error message.

Inside this constructor, you will add three properties, `name`, `message` and `stack`. The `name` property will contain the name of your custom error. The `message` will refer to the value passed as `message` parameter. The `stack` will use `stack` property from newly instantiated `Error` constructor.

When you have this you have to set the `prototype` property of this new Function constructor to error constructor. Finally, you also have to set the `constructor` property of the Function constructor under `prototype` property to the Function constructor. When you have this, you use `throw` and `new` statements to create new errors based on your custom error constructor.

```JavaScript
// Create new custom error using Function constructor
const MyCustomError = function(message) {
  // Add name property with some custom name
  this.name = 'MyCustomError'
  // Add message property referencing the value passed as "message" parameter
  this.message = message
  // Add stack property from Error constructor
  this.stack = (new Error()).stack
}

// Set "prototype" property of custom error constructor to Error constructor
MyCustomError.prototype = new Error()

// Set the "constructor" property of custom error constructor to the custom error constructor
MyCustomError.prototype.constructor = MyCustomError


// Usage:
// Create function
function myFunc() {
  // Use custom error constructor to create new error
  throw new MyCustomError('An error occurred.')
}

// Create try...catch statement
try {
  // Invoke function with custom error
  myFunc()
}
catch(err) {
  // Log error data
  console.log('Error: ', err)
  console.log('Error name: ', err.name)
  console.log('Error message: ', err.message)
  console.log('Error stack: ', err.stack)
}

// Outputs:
// 'Error: ' Error
//     at new MyCustomError (eval at <anonymous> (:7:47), <anonymous>:6:16)
//     at myFunc (eval at <anonymous> (:7:47), <anonymous>:13:9)
//     at eval (eval at <anonymous> (:7:47), <anonymous>:17:3)
//     at <anonymous>:7:47
//     at <anonymous>:26:9
//     ...

// 'Error name: ' 'MyCustomError'

// 'Error message: ' 'An error occurred.'

// 'Error stack: ' `Error
//     at new MyCustomError (eval at <anonymous> (:7:47), <anonymous>:6:16)
//     at myFunc (eval at <anonymous> (:7:47), <anonymous>:13:9)
//     at eval (eval at <anonymous> (:7:47), <anonymous>:17:3)
//     at <anonymous>:7:47
//     at <anonymous>:28:9
//     ...
```

With JavaScript class creating custom error constructor is even easier. First, you have to create new class for your custom error constructor. This class will `extend` the `Error` class. Inside the class, you will add `constructor` with one parameter. this will be the error message.

Inside the `constructor`, you have to call `super` with `message` passed as argument. This will call the constructor of parent class `Error`. After that, still inside the `constructor`, you will override the `name` property by adding your own `name` property with name for your custom constructor.

```JavaScript
// Create new error constructor with JavaScript class
class MyCustomError extends Error {
  constructor(message) {
    // Call constructor of parent class Error
    super(message)

    // Set your custom error name
    this.name = 'MyCustomError'
  }
}

// Create try...catch statement
try {
  // Throw new custom error
  throw new MyCustomError('An error occurred')
}
catch(err) {
  console.log('Error name: ', err.name)
  console.log('Error message: ', err.message)
  console.log('Error stack: ', err.stack)
}

// Outputs:
// 'Error name: ' 'MyCustomError'

// 'Error message: ' 'An error occurred'

// 'Error stack: ' `MyCustomError: An error occurred
//     at eval (eval at <anonymous> (:7:47), <anonymous>:12:9)
//     at <anonymous>:7:47
//     at <anonymous>:23:9
//     ...
```

## Error handling globally

The `try...catch` and `try...catch...finally` statements are powerful. These two can make error handling very easy. One problem might be if you can't isolate code you want to execute with `try` block. For example, when some code is executed in a global scope from a place where you cannot access it.

In this case, you can use `onerror()` method. This is an error event handler. You can use it to catch and process errors occurring in a global scope. Aside to `window` object you can also use it with elements in the DOM. Alternatively, you can attach new event listener for `error` event, either on `window` or some element.

```JavaScript
// Option no.1: onerror() method
window.onerror = function(message, url, lineNumber, columnNumber, error) {
  console.log(`
    error message: ${message},
    error URL: ${url},
    line with error: ${lineNumber},
    column with error: ${columnNumber}
  `)
}


// Option no.2: listening to 'error' event
window.addEventListener('error', function(event) {
  console.log(`
    error message: ${event.message},
    error URL: ${event.filename},
    line with error: ${event.lineno},
    column with error: ${event.colno},
    error object: ${JSON.stringify(event.error)}
  `)
})
```

## Conclusion: Error Handling in JavaScript

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[eslint]: https://eslint.org/
[jshint]: http://www.jshint.com/
[jslint]: http://www.jslint.com/
[TypeScript]: https://www.typescriptlang.org
[unit tests]: https://medium.com/welldone-software/an-overview-of-javascript-testing-7ce7298b9870
[function]: https://blog.alexdevero.com/javascript-functions-pt1/
[data type]: https://blog.alexdevero.com/javascript-basics-data-types-pt1/
[Function constructor]: https://blog.alexdevero.com/javascript-functions-pt2/#function-constructor
[class]: https://blog.alexdevero.com/javascript-classes-pt1/

<!--
### Meta:
-
-->

<!--
### Resources:
- https://javascript.info/error-handling
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Control_flow_and_error_handling
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch
- https://www.sitepoint.com/proper-error-handling-javascript/
- https://medium.com/@iaincollins/error-handling-in-javascript-a6172ccdf9af
- https://www.tutorialspoint.com/javascript/javascript_error_handling.htm
-->
