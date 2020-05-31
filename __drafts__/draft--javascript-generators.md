# How JavaScript [Generators] Work and How to Use Them

JavaScript generators, or generator functions, are one of the lesser known features of ECMAScript 6 (ES6). They can look a bit strange. This tutorial will help you wrap you head around them and understand the basics. You will learn about what JavaScript generators are, how they work and how to use them.
<!--more-->
<!--
Table of Contents:
-->

## What are generators

Generators sit somewhere between [iterators] and [functions]. The way normal functions work is very simple. When you invoke a function it will run until it completion. It will execute all code inside it or until it encounters `return` statement. Iterators work in a similar way. Let's take `for` loop for example.

Imagine you have an array with some data and you want to use `for` loop to iterate over it. When the `for` loop start it will run until it is stopped by the condition you specified. Or, it will run infinitely. This is what distinguishes JavaScript generators from functions and iterators.

The first difference is that generators will not execute their code when you invoke them. Instead, they will return a special object called `Generator`. The second difference is that, unlike loops, you will not get all values at once when you use generator. Instead, you get each value only if you want it.

This means that you can suspend, or pause, the generator for as long as you want.  When you decide to resume the generator it will start right where you suspended it. It will remember the last value and continue from that point, instead of from the beginning. In short, generators are like function you can pause and resume.

You can do this, starting and pausing and starting, as many times as you want. Interesting fact. You can create generator that never finishes, something like an infinite loop. Don't worry, infinite generator will not cause a mess like infinite loop. What's more, generator can communicate with the rest of code with each start and restart.

What I meaning is that you can pass a data to generator when you start it, or restart it. You can also return, or yield data, when you pause it. Wrapping one's head around generators can be difficult. Let's take a look at the code. That might give you a better picture.

## Generator syntax

The syntax of generators is very simple. You define a generator in a similar way you would define a function. The difference is that you put asterix (`*`) right before the name of the function, or generator, such as `function *myGen() { }`. This asterix is a signal for JavaScript that the function a type of generator function.

Another option you may have seen is to put the asterix right after the `function` keyword, such as `function* myGen() { }`. Both ways are valid, but JavaScript developers tend to use more often the former, with asterix right before the name. I think that asterix right before the name is more readable.

```JavaScript
// Generator syntax
function *myGenerator() {
  // ... some code
}

// Or
function* myGenerator() {
  // ... some code
}
```

What about the content? Well, generators are very similar to normal JavaScript functions. What you do inside normal functions you can also do inside generators. So, there are special or required things you would have to learn. Maybe except one thing called `yield`.

## Yield

## next() method

## Return

## Yield*

## Conclusion: [...] ...

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[iterators]: https://blog.alexdevero.com/javascript-loops/
[functions]: https://blog.alexdevero.com/javascript-functions-pt1/

<!--
### Meta:
-
-->

<!--
### Keywords:
- generators
- JavaScript generators
-->

<!--
### Resources:
-
-->
