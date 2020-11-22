# Introduction to Recursion in JavaScript - How It Works and How to Use It

Recursion is one of those programming topics that can sound intimidating. This is especially true if you are new to programming. In this tutorial, you will learn all you need to know about it. You will learn how recursion in JavaScript works and also how to implement it in your code.<!--more-->
<!--
Table of Contents:
-->

## A quick introduction

The simplest way to describe what recursion is by saying that it is a function that calls itself. This type of function is called "recursive function". It doesn't matter if it is recursion in JavaScript or any other language. The main idea is that you have a function and this function calls itself, at least once.

```JavaScript
// Simple recursive function
function recursiveFunction() {
  // Call the recursive function again
  recursiveFunction()
}

// Call the recursiveFunction()
recursiveFunction()
```

That said, recursive function is not just any function. There are some conditions every recursive function has to meet. This is not necessary just so you can call that function a recursion. It is also necessary to make that recursion work properly. Here is the potential problem.

Let's say you have a function. This function calls itself. What happens when you call this function? Well, it will call itself. What happens next? When that function calls itself it will call itself again, and again and again. The problem is that there is no point at which the function is terminated. The result is an infinite loop.

For example, this will happen if you try to run the function in the example above. When you run that function, you will get an error `Uncaught RangeError: Maximum call stack size exceeded`. You can avoid this problem, creating an infinite loop, by adding a base case to the recursive function.

## Base case

A base case is a fancy name for a specific condition. It is also called "base condition". This condition will force the function to do one of two things. If the condition evaluates to `false`, the recursive function will call itself again. If the condition evaluates to `true`, the recursive function will return a value.

The easiest way to create this base case is by using simple [if...else] statement. Inside one block, either `if` or `else` depending on the condition, you will return some value. Inside the other block, you will call the recursive function again. This will allow you to terminate the function at the right time.

```JavaScript
// Simple recursive function
function recursiveFunction() {
  if (/* condition */) {
    // Call the recursive function again
    recursiveFunction()
  } else {
    // Do something instead of calling
    // the recursive function again
  }
}

recursiveFunction()
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
