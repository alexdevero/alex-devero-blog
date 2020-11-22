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

## How to choose the best base case

What is the best candidate for the base case? This depends on what you want to achieve with your recursive function. For exampled, let's say you want to use recursion to calculate factorial. This is the most popular example for recursion. In case of a factorial, think about what is the lowest number you can use.

For factorial, the lowest number is 1. Factorial of 1 (1!) will always result to one. This makes 1 the best candidate for base case because it the smallest number, or level, you can get to. If you want to count numbers from X down to 0, 0 will be the lowest number. It will also be the best candidate for base case.

If you want to do the opposite and count upwards, the base will be the highest number you want to reach. Another example could be reversing a simple string. In that situation, the base case would be that the length of the string must be more than 0. It doesn't make sense to continue reversing an empty string.

## How it actually works

You know what recursion is and how it looks like so you can recognize it when you see it. You also know what is a base case. Now, let's take a look at how it actually works. Especially, how it works in JavaScript, since this will be the programming language you are most familiar with.

To understand how recursion works, you need to know at least a little about about [call stack]. Call stack is mechanism that is built in JavaScript. JavaScript uses it to keep track of all function calls. Let's say you call a function. When you do this, JavaScript will add that function to the call stack.

When that function call is finished, JavaScript will automatically remove that function call from the call stack and goes to another one below, if there is any. However, if the function you called calls another function, something different happens. When that second function is called, JavaScript will add it to the call stack as well.

If that second function also calls a function, JavaScript will also add it at the top of the call stack. This repeats as long as there are function calls in the current chain of function. There are three important things you need to know. The first thing is that JavaScript will put that second call above the first.

JavaScript will add that function call on top of it, on top of the whole call stack. The second thing is that JavaScript executes calls in the call stack from the top to the bottom. This means that the first function call that was added to the call stack will be executed as last.

Conversely, the the last function call that was added to the call stack will be executed as first. This is called [LIFO principle] (Last-In-First-Out). The third thing is that when JavaScript encounters function call it will stop executing the current call, execute that new call, and anything inside the newly called function.

Only when that newly called function is executed JavaScript will return to the previous call and finish executing that one. This will repeat for each function in the call stack.

```JavaScript
function funcFour() {
  // some code to execute
}

function funcThree() {
  funcFour()
  // Execution of funcThree() is paused on the line above
  // until funcFour() is finished
}

function funcTwo() {
  funcThree()
  // Execution of funcTwo() is paused on the line above
  // until funcThree() is finished
}

function funcOne() {
  funcTwo()
  // Execution of funcOne() is paused on the line above
  // until funcTwo() is finished
}

// Call the funcOne()
funcOne()

// Call stack at this moment:
// funcFour() - executed as first (top of the stack)
// funcThree() - waiting for funcFour() to finish
// funcTwo() - waiting for funcThree() to finish
// funcOne() - waiting for funcTwo() to finish

// README:
// funcFour() is at the top of the stack
// and its function call will be finished as first
// after that execution will return to funcThree()
// when funcThree() is finished execution will return to funcTwo()
// when funcTwo() is finished execution will return to funcOne()
// when funcOne() is finished the call stack will be empty
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
