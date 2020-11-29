# What is Currying In JavaScript and How to Use It

Currying is a very popular concept in functional programming, but it might sound confusing. This tutorial will help you understand what currying is and how it works. You will also learn how to use currying in JavaScript to help you make your code more readable and simpler.

<!--more-->
<!--
Table of Contents:
## h2
### h3
### h3
## h2
## Conclusion: [...] ...
-->

## A quick word about functions

Before we get to currying in JavaScript there is something important about functions you should know. In JavaScript, functions are treated as [first-class citizens]. This allows you to do some interesting things with them. You can assign functions to variables and you can also pass them as arguments.

Another thing you can also do is to return them. You can return functions from other functions. Not only you can return functions. You can also pass arguments into those returned functions. This all may sound trivial, but it is very important. It is thanks to this currying is possible.

```JavaScript
// Create a function that returns a function
function sumNumbers(num1, num2) {
  // Pass the second argument
  // to the returned function
  return function() {
    // Return the sum of all arguments
    return num1 + num2
  }
}

sumNumbers(5, 15)()
// Output:
// 20


// Alternatively
function sumNumbers(num1, num2) {
  return function() {
    return num1 + num2
  }
}

const sum = sumNumbers(5, 15)
sum()
// Output:
// 20
```

## h2

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
