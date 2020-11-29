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
// Example no.2:
// Alternative
function sumNumbers(num1, num2) {
  // Pass the second argument
  // to the returned function
  return function() {
    // Return the sum of all arguments
    return num1 + num2
  }
}

const sum = sumNumbers(11, 91)
sum()
// Output:
// 102


// Example no.2:
// Or, as a one-liner
const sumNumbers = (num1, num2) => () => num1 + num2

const sum = sumNumbers(52, 25)
sum()
// Output:
// 77


// Example no.3:
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
```

Note: Just calling the `sum()` function with some numbers passed as arguments would not give you the result you are looking for. That function call would return the function that is returned from `sum()`. In order to get the result, the sum, you need to call the returned function as well.

One way to do this is by calling the function and assigning the returned value to variable. This returned value will be the returned function. Now, you can call that variable, that returned function and get the result, the sum of numbers you passed. You can see this on the example number 1 and 2.

An alternative is to invoke, or call, both function. To do this, you add additional parentheses (`()`) after the first call. This is when you call the `sum()` function and assign it to a variable. This will call the `sum()` function, return the return function, and then call it as well. You can see this approach on the example number 3.


An alternative is to invoke, or call, both function. To do this, you add additional parentheses (`()`) after the first call. This is when you call the `sum()` function and assign it to a variable. This will call the `sum()` function, return the return function, and then call it as well. You can see this approach on the example number 1.


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
