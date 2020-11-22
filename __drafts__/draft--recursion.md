# Introduction to Recursion in JavaScript: How It Works and How to Use It

Recursion is one of those programming topics that can sound intimidating. This is especially true if you are new to programming. In this tutorial, you will learn all you need to know about it. You will learn what recursion is, how recursion in JavaScript works and also how to implement it.<!--more-->
<!--
Table of Contents:
## A quick introduction
## Base case
## How to choose the best base case
## How it actually works: A quick introduction to call stack
### Recursive factorial function, call stack and analysis
## Another two examples of recursion in JavaScript
### Recursive function for countdown
### Recursive function for reversing string
## Conclusion: Introduction to recursion in JavaScript
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
  // Add base case
  if (/* condition */) {
    // Call the recursive function again
    recursiveFunction()
  } else {
    // Return something instead of calling
    // the recursive function again
  }
}

// Call the recursive function
recursiveFunction()
```

JavaScript will terminate function execution when it encounters a `return` statement. This mean that you don't really have to use `if...else` statement. You need just the `if` part. If something, return something. Otherwise, you can let JavaScript skip the `if...else` and continue.

```JavaScript
// Recursive function with shorter condition
function recursiveFunction() {
  // Add base case
  if (/* condition */) {
    // If condition evaluates to true
    // terminate this function call
    // by returning something
    return /* some value */
  }

  // Otherwise, call the recursive function again
  recursiveFunction()
}

// Call the recursive function
recursiveFunction()
```

This is actually not the shortest version. You can make the base condition, and the whole function, even shorter. You can replace the `if...else` statement with [ternary operator]. This way, you can reduce the whole recursive function almost a one-liner. If you use an [arrow function] than literally to a one-liner.

```JavaScript
// Recursive function with ternary operator
function recursiveFunction() {
  // Add base case
  return (/* condition */) ? /* some value */ : recursiveFunction()
}

// Call the recursive function
recursiveFunction()
```

## How to choose the best base case

What is the best candidate for the base case? This depends on what you want to achieve with your recursive function. For exampled, let's say you want to use recursion to calculate factorial. This is the most popular example for recursion. In case of a factorial, think about what is the lowest number you can use.

For factorial, the lowest number is 1. Factorial of 1 (1!) will always result to one. This makes 1 the best candidate for base case because it the smallest number, or level, you can get to. If you want to count numbers from X down to 0, 0 will be the lowest number. It will also be the best candidate for base case.

If you want to do the opposite and count upwards, the base will be the highest number you want to reach. Another example could be reversing a simple string. In that situation, the base case would be that the length of the string must be more than 0. It doesn't make sense to continue reversing an empty string.

## How it actually works: A quick introduction to call stack

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

### Recursive factorial function, call stack and analysis

Now, let's use this information about call stack to understand how recursion in JavaScript works. To illustrate this better let's take a recursive function to calculate a factorial. This function will accept a single parameter, a number for which it will calculate a factorial.

The base case for this function will be that the number you passed as argument must be equal to 1. When this situation happens, the function will return that number. It will return 1. Otherwise, it will return the number multiplied by the result of calling itself with the number decreased by 1 passed as an argument.

```JavaScript
// Recursive function to calculate factorial
function calculateFactorial(num) {
  // Base case
  if (num === 1) {
    // The value of "num" here will be 1
    return num
  }

  return num * calculateFactorial(num - 1)
}

// Shorter version with ternary operator
function calculateFactorial(num) {
  // Base case
  return (num === 1) ? num : num * calculateFactorial(num - 1)
}

// Test the calculateFactorial()
calculateFactorial(4)
// Output:
// 24

// Test the calculateFactorial() again
calculateFactorial(9)
// Output:
// 362880

// Test the calculateFactorial() one more time
calculateFactorial(1)
// Output:
// 1
```

Let's analyze the execution of the `calculateFactorial()` function. To keep this short, let's use 4 as the number for which we want to calculate the factorial. When you call the function with number 4 as an argument JavaScript will add it to the call stack. Since 4 is not equal to 1 `calculateFactorial()` will be called again.

At this moment, `calculateFactorial()` will be called not with number 4, but number 3 passed as an argument. Subsequent calls are always with number decreased by 1. JavaScript will add that second call to the call stack as well. It will add it on the top of the previous call of `calculateFactorial()` with number 4.

The number is still not equal to 1. So another call of `calculateFactorial()` function will be executed. The number passed in as an argument will now be 2. JavaScript will add this call at the top of the call stack and call `calculateFactorial()` function again. The number will be now 1.

This number meets the base case so the `calculateFactorial()` function will now return the number and it will not call itself again. The chain of calls is now over and we are at the top of the call stack.

```JavaScript
// Recursive function to calculate factorial
function calculateFactorial(num) {
  // Base case
  return (num === 1) ? return num : num * calculateFactorial(num - 1)
}

// Test the calculateFactorial()
calculateFactorial(4)

// Call stack after calling calculateFactorial(4):
// calculateFactorial(1) - top of the stack, first out
// calculateFactorial(2)
// calculateFactorial(3)
// calculateFactorial(4) - bottom of the stack, last out
```

What happens next? When we are at the top of the stack and there are no more calls, JavaScript will start moving to the bottom of the stack. During this, JavaScript will also start returning values of all function calls in the stack. With each returned value one function call will be removed from the stack.

The most interesting part are the values returned from all those calls. Do you remember the `num * calculateFactorial(num - 1)` line in the code for the `calculateFactorial()` function? Those values returned by calls in the stack will basically replace the `calculateFactorial(num - 1)` part.

The line will now look something like `num * "num" (returned by the previous call)`. For each call in the stack, the `num` will be multiplied by the result of the previous call. The `calculateFactorial(1)` is the last call at the top of the stack and its return value will be returned as first.

There is no previous call and the function says that this number should be returned. This is the `(num === 1) ? return num :` part. So, the first returned value is 1. The next call is in the call stack is `calculateFactorial(2)`. This is not the last call so the `(num === 1) ? return num :` line doesn't apply here.

Instead, we have to apply the `num * calculateFactorial(num - 1)`. The first `num` is the number passed as parameter to the current call: 2. The `calculateFactorial(num - 1)` is the number returned by the last call: 1. So, `num * calculateFactorial(num - 1)` will result in `2 * 1`.

The next call in the call stack is `calculateFactorial(3)`. Just like in the previous case, we have to apply the `num * calculateFactorial(num - 1)`. The first `num` is again the number passed to the current call: 3. The `calculateFactorial(num - 1)` is the number returned by the last call: 2.

The result of last call was `2 * 1`. That's why `calculateFactorial(num - 1)` now translates to 2. So, `num * calculateFactorial(num - 1)` will translate to `3 * 2`. The `calculateFactorial(4)` call was the last call, at the bottom of the stack. The `num` passed to the current call is 4.

The result of `calculateFactorial(num - 1)` returned by the previous call, `calculateFactorial(3)`, was 6 (result of `3 * 2`). So, now, `num * calculateFactorial(num - 1)` translates to `4 * 6`. This makes the value returned by the current and last call 24. This is also the final result of your factorial calculation.

```JavaScript
// Recursive function to calculate factorial
function calculateFactorial(num) {
  // Base case
  return (num === 1) ? return num : num * calculateFactorial(num - 1)
}

// Test the calculateFactorial()
calculateFactorial(4)

// Call stack after calling calculateFactorial(4):
// calculateFactorial(1)
//  - returns 1

// calculateFactorial(2)
// - returns 2 * 1 (1 is value returned from calculateFactorial(1))

// calculateFactorial(3)
//  - returns 3 * 2 (2 is value returned from calculateFactorial(2))

// calculateFactorial(4)
//  - returns 4 * 6 (6 is value returned from calculateFactorial(4))
```

## Another two examples of recursion in JavaScript

Before we end this tutorial, let's take a look at few examples of recursion in JavaScript. You already know how to use recursion to calculate factorial of any given number. Let's take a quick look at another two examples of recursive functions.

### Recursive function for countdown

One good example to demonstrate implementation of recursion in JavaScript can be a function that counts down to 0, and prints number for each recursive call. The base case for this recursive function will be if the number passed, when decreased by one, is bigger than 0.

Only if the number is is bigger than 0 the function will be called again. Otherwise, there will be nothing more to do so the function will terminate itself.

```JavaScript
// Recursive function for countdown
function countdown(num) {
  // Print the number passed
  // to the current recursive call
  console.log(num)

  // Base case
  if (num - 1 > 0) {
    // If current number decreased by 1
    // is higher than 0 call countdown() again
    // with number decreased by 1
    return countdown(num - 1)
  }
}

// Call the countdown() function
countdown(11)
// Output:
// 11
// 10
// 9
// 8
// 7
// 6
// 5
// 4
// 3
// 2
// 1
```

### Recursive function for reversing string

The second example of an implementation of recursion in JavaScript will be a function that reverses a string. This function will accept string as a parameter. The base case will be if the length of the string is bigger than 1. If this condition is true, the function will call itself.

The string for this subsequent call will be the string from the current call without the first character. In addition, this first character will be added to end of the value returned by the next call.

```JavaScript
// Recursive function for reversing string
function reverseString(str) {
  // Base case
  if (str.length >= 1) {
    // If the length of the string is bigger than 1
    // call the reverseString() function again,
    // pass in pass in the string without the first character
    // and then add the character and the end
    return reverseString(str.substring(1)) + str.charAt(0)
  }

  // Otherwise, return the string
  return str
}

// Call the reverseString() function
reverseString('Hello')
// Output:
// 'olleH'
```

## Conclusion: Introduction to recursion in JavaScript

Recursion is an advanced topic that can be very hard to fully grasp. However, it is worth the time to learn to learn about it. Recursion can be a very useful tool to solve some problems better and faster. I hope that this tutorial helped you understand recursion in JavaScript works and what it is in general.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[if...else]: https://blog.alexdevero.com/javascript-if-else-statement/
[call stack]: https://blog.alexdevero.com/memory-life-cycle-heap-stack-javascript/#the-call-stack
[LIFO principle]: https://www.i-programmer.info/babbages-bag/263-stacks.html
[ternary operator]: https://blog.alexdevero.com/javascript-if-else-statement/#ternary-operator
[arrow function]: https://blog.alexdevero.com/javascript-arrow-functions/

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
