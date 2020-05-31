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

When it comes to JavaScript generators `yield` keyword is very important. It is this `yield` keyword what pauses execution of a generator. It is also this keyword what can return some value when the generator is paused. You can think about `yield` keyword as a cousin of `return` statement.

Both can be used to return a value. One difference is that while `return` statement terminates function execution the `yield` doesn't. It only pauses the generator. The `yield` works more like a breakpoint. Another difference is that when `yield` returns a value only once.

When you resume the generator it will automatically move on to the next `yield` keyword. It will ignore the first one. The same if you resume the generator for the third time. It will ignore the previous two `yield` keywords and move on to the third one. If there is no third `yield`? The generator will return `undefined`.

The same will also happen if the generator doesn't contain any `yield` keyword. It will return `undefined` the first time you start it. Since we are talking about returned values. This is the third difference between `return` and `yield`. `yield` always returns an object.

This object always contains two key/value pairs. The first is for a `value` returned by `yield` from generator. If there is no `yield` or value returned, the value of `value` key is `undefined`. The second is for `done`. The value of `done` is always boolean. The `done` indicates if generator is finished or not.

A generator is finished when there is no `yield` to be processed. If generator contains one `yield` it will require two starts to complete it. First start will yield the value you specified after the `yield` keyword. The value of `done` with be `false`. Second start will return `undefined`. The value of `done` with be `true`.

If you don't add any `yield` keyword inside the generator it will return value set to `undefined` and `done` set to `true` on the first start.

```JavaScript
// Generator syntax
function *myGenerator() {
  // Yield, or return, a message when myGenerator is started
  yield 'Message from myGenerator.'
}

// Assign generator to a variable
const message = myGenerator()

// Call the generator and log the message (first start)
console.log(message.next())
// Call the generator and log the message (second start)
console.log(message.next())

// Output from the first start:
// { value: 'Message from myGenerator.', done: false }

// Output from the second start:
// { value: undefined, done: true }


// Generator with no yield
function *myGenerator() { }

// Assign generator to a variable
const message = myGenerator()

// Call the generator and log the message
console.log(message.next())

// Output from the first start:
// { value: undefined, done: true }
```

One thing about `yield` and pausing JavaScript generators. You use the `yield` keyword to pause the generator only from the inside of the generator. You can't use it from the outside. There is actually no way to pause a generator from the outside. Generator will pause itself only when it encounters a `yield` inside itself.

This also works in the opposite way for resuming a generator. Once it is paused generator can't resume itself on its own. The only way to resume it is by doing it from the outside. This brings us to the `next()` method.

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
