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

### Under the hood, part 1

Let's keep it simple, just enough. Imagine you have a function. This function returns a function. When you want to call both functions you add additional pair of parentheses after the first when you call the outer most function. This second pair of parentheses is for the second function, the function you return.

Simple way to think about this in a way that the second pair is another function call. In this case, it is calling the returned function. Here is the interesting thing. If the returned function also returns a function, all you just repeat the process. You add third pair of parentheses.

What if you return function event more times? All you have to do is to repeat the same process again and again. You add parentheses as many times as there are returned functions. One parentheses is for each returned function. This is the first part, how the additional parentheses work.

```JavaScript
// Example of calling a function
// that returns one function
function myFunc() {
  return function() {
    return 'Hello'
  }
}

// Calling the function
// One pair of parentheses
// for the outer function
// and one for each returned function
myFunc()()
// Output:
// 'Hello'


// Example of calling a function
// that returns two functions
function myFunc() {
  return function() {
    return function() {
      return 'Hello'
    }
  }
}

// Calling the function
// One pair of parentheses
// for the outer function
// and one for each returned function
myFunc()()()
// Output:
// 'Hello'


// Example of calling a function
// that returns four functions
function myFunc() {
  return function() {
    return function() {
      return function() {
        return 'Hello'
      }
    }
  }
}

// Calling the function
// One pair of parentheses
// for the outer function
// and one for each returned function
myFunc()()()()
// Output:
// 'Hello'
```

### Under the hood, part 2

The second part is about how to transform those arguments. Until now, you passed all arguments to a single function call, the first. This might be okay for now, but it can quickly become messy. Distributing those arguments to the function calls can help you make your code cleaner and easier to read, theoretically.

The best part is that this transformation is very easy. There are only two changes you have to make. First, you have to stop defining all parameters in the first, outermost, function. Second, what you have to do instead, is to define those parameters for every returned function. Each of these function will take one of these parameters.

This small and quick change will allow you to pass all required arguments individually to each function call, one argument for each pair of parentheses. That's it. This is all the mystery there is about currying in JavaScript and in general.

```JavaScript
// Example with two arguments
function myFunc(arg1) {
  return function(arg2) {
    return arg1 + arg2
  }
}

// Calling the function
myFunc(15)(59)
// Output:
// 74


// One-line alternative
const myFunc = (arg1) => (arg2) => arg1 + arg2


// Example with three arguments
function myFunc(arg1) {
  return function(arg2) {
    return function(arg3) {
      return arg1 * arg2 * arg3
    }
  }
}

// Calling the function
myFunc(3)(5)(7)
// Output:
// 105


// One-line alternative
const myFunc = (arg1) => (arg2) => (arg3) => arg1 * arg2 * arg3


// Example with four arguments
function myFunc(arg1) {
  return function(arg2) {
    return function(arg3) {
      return function(arg4) {
        return arg1 + arg2 + arg3 + arg4
      }
    }
  }
}

// Calling the function
myFunc(56)(23)(13)(89)
// Output:
// 181


// One-line alternative
const myFunc = (arg1) => (arg2) => (arg3) => (arg4) => arg1 + arg2 + arg3 + arg4
```

Do you remember the `sumNumbers()` function from the beginning of this article? Let's rewrite it to a curried function. Since this function is very closed to a curried version this rewrite will be quick. The only thing you have to do is to distribute the parameters between the calls.

You have to take the `num2` parameter from the outer function and use it as a parameter for the returned function. That's it. Now, you have a curried version of the `sumNumbers()` function.

```JavaScript
// Before
function sumNumbers(num1, num2) {
  return function() {
    return num1 + num2
  }
}

sumNumbers(52, 77)()
// Output:
// 129


// After
function sumNumbers(num1) {
  return function(num2) {
    return num1 + num2
  }
}

sumNumbers(52)(77)
// Output:
// 102
```


So far, you've worked with examples that always used only one argument per call. This doesn't mean you have to always use only one argument. If you want to use more, you can. In that case, all you need to do is to decide which of your functions will accept those additional arguments.

When you decide, you have to add necessary new parameters to that function and you are ready to go. After this, when you call your curried function, you will be able to pass multiple arguments into specific function calls, pair of parentheses. If you do this, remember to use correct amount of parameters for each call.

```JavaScript
// Example of multiple arguments per call
// This function will accept one parameter
function myFunc(arg1) {
  // This function will also accept one parameter
  return function(arg2) {
    // This function will accept three parameters
    return function(arg3, arg4, arg5) {
      // This function will accept one parameter
      return function(arg6) {
        return arg1 * arg2 * arg3 * arg4 * arg5 * arg6
      }
    }
  }
}

// Call myFunc
myFunc(1)(3)(5, 7, 9)(11)
// Output:
// 10395
```

## Order of arguments matters

There is one thing you need to know about currying. The order of arguments matters. This may sound like a no-brainer, but it is still good to mention it. If you change the order of arguments you pass into individual function calls you also change which value will each function receive.

Depending on your curried function, this may change the result you will get. If you pass arguments of wrong [data types] you can also break your code. So, double-check you pass correct argument(s) to correct call. Also, double-check you are using correct number of arguments. That, too, can cause a lot of troubles.

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
