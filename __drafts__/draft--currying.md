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

## Currying made simple

Functions are first-class citizens. A function can return another function. You can pass arguments between those functions. Now, let's talk about currying. What is currying? Currying is a process of taking a function with multiple arguments and transforming it into a sequence of functions, each function taking a single argument.

The result is that instead of having `myFunc(arg1, arg2, arg3)` you have `myFunc(arg1)(arg2)(arg3)`. In case of the `sum()` function, instead of `sum(num1, num2)`, the syntax would now look like this: `sum(num1)(num2)`. If you use more arguments, you add more parentheses. Have you noticed something interesting on this syntax?

```JavaScript
// Simple example of calling syntax
// Create curried function
function myCurriedFunc(arg1) { /* ... */ }

// Call curried function
// One pair of parentheses for each returned function
myCurriedFunc(arg1)(arg2)(arg3)(arg4)(arg5)
```

You are also adding second pair parentheses after the function call, or more pairs. This looks very similar to what you saw on the example number 3, where you invoked the returned function immediately. So, this is how currying looks like when you invoke a curried function. Now, let's take a look under the hood.



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
