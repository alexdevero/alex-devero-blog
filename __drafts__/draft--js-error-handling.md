# Error handling in JavaScript
<!--more-->
<!--
Table of Contents:
-->

## Two types of errors

When it comes to error handling in JavaScript there are two types of errors you can stumble upon. The first type of errors are syntax errors. The second type are runtime errors.

### Syntax errors

Syntax errors are also called parsing errors. This is errors occur when JavaScript parser interprets your code. When one of these errors occurs it only affect the code that in the same thread. The rest of code is left unaffected. An example of syntax error can be forgotten opening or closing parenthesis or bracket.

Another example can be missing coma or colon in object. Any of these errors will cause the syntax to be invalid and break your program. There are some ways to avoid these types of errors. One is checking your code and looking for them. This is not effective and can take a lot of time.

Another option is using some tool or IDE plugin. These tools will automatically scan your code and look for any syntax issues for you. Three most popular tools that will help you catch syntax errors are [eslint], [jshint] and [jslint]. Eslint is my favorite. I use in almost all my projects.

These tools are so popular, and developers don't like repetitive tasks. This makes it likely there is a plugin for each of these tools you can install in IDE you are using. If you find some I highly recommend installing it and using it. It can save you a lot of headaches.

## Throw statement

## Try...catch

### Finally

## Errors and Promises

## onerror() method

## Conclusion: [...] ...

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[eslint]: https://eslint.org/
[jshint]: http://www.jshint.com/
[jslint]: http://www.jslint.com/

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
