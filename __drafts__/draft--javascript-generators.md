# An Introduction to JavaScript [Generators]

JavaScript generators, or generator functions, are one of the lesser known features of ECMAScript 6 (ES6). They can look a bit strange. This tutorial will help you wrap your head around them and understand the basics. You will learn about what JavaScript generators are, how they work and how to use them.
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

## Assigning to a variable

When you create a generator, and call it, will not execute the code inside it. Instead, it will return `Generator` object. What you need to do with this Generator object is to assign it to a variable. When you want to work with the generator, that is start it, pause it and start it again, you reference the variable.

What if you don't assign the generator to a variable? It will always yield, or return, only the value that follows the first `yield` keyword. This will happen every time you resume it using `next()`. The generator will not remember the last value it returned, or the last yield it encountered. It will always start from the beginning.

So, always assign a generator to a variable, unless you want the generator to always start and resume from the begging. Remember that the variable you assign the generator is what stores the last value returned by the generator. This variable is basically the memory of the generator. Make sure to use it

```JavaScript
// Example no.1: without variable assignment
// Create generator
function *myGenerator() {
  yield 1
  yield 2
  yield 3
}

// Call the generator without assigning it to a variable
console.log(myGenerator().next())
// Output:
// { value: 1, done: false }

// Call the generator for the second time
console.log(myGenerator().next())
// Output:
// { value: 1, done: false }

// Call the generator for the third time
console.log(myGenerator().next())
// Output:
// { value: 1, done: false }

// Call the generator for the fourth time
console.log(myGenerator().next())
// Output:
// { value: 1, done: false }


// Example no.2: with variable assignment
// Example no.1: without variable assignment
// Create generator
function *myGenerator() {
  yield 1
  yield 2
  yield 3
}

// Assign generator to a variable
const myGeneratorVariable = myGenerator()

// Call the generator referencing 'myGeneratorVariable' variable
console.log(myGeneratorVariable.next())
// Output:
// { value: 1, done: false }

// Call the generator for the second time
console.log(myGeneratorVariable.next())
// Output:
// { value: 2, done: false }

// Call the generator for the third time
console.log(myGeneratorVariable.next())
// Output:
// { value: 3, done: false }

// Call the generator for the fourth time
console.log(myGeneratorVariable.next())
// Output:
// { value: undefined, done: true }
// Since the 'done' is true the generator is done
```

*Note: Don't worry about what `yield` keyword and `next()` method are. You will learn about both in this tutorial.*

## Yield

When it comes to JavaScript generators `yield` keyword is very important. It is this `yield` keyword what pauses execution of a generator. After you start it, the generator will run until it encounters `yield`. When it does it will pause itself. It is also this keyword what can return some value when the generator is paused.

You can think about `yield` keyword as a cousin of `return` statement. Both can be used to return a value. One difference is that while `return` statement terminates function execution the `yield` doesn't. It only pauses the generator. The `yield` works more like a breakpoint.

Another difference is that when `yield` returns a value only once. When you resume the generator it will automatically move on to the next `yield` keyword. It will ignore the first one. The same if you resume the generator for the third time. It will ignore the previous two `yield` keywords and move on to the third one.

What if there is no third `yield`? The generator will return `undefined`. The same will also happen if the generator doesn't contain any `yield` keyword. It will return `undefined` the first time you start it. Since we are talking about returned values. This is the third difference between `return` and `yield`. `yield` always returns an object.

This object always contains two key/value pairs. The first is for a `value` returned by `yield` from generator. If there is no `yield` or value returned, the value of `value` key is `undefined`. The second is for `done`. The value of `done` is always boolean. The `done` indicates if generator is done or not.

A generator is done when there is no `yield` to be processed. If generator contains one `yield` it will require two starts to complete it. First start will yield the value you specified after the `yield` keyword. The value of `done` with be `false`. Second start will return `undefined`. The value of `done` with be `true`.

If you don't add any `yield` keyword inside the generator it will return value set to `undefined` and `done` set to `true` on the first start.

```JavaScript
// Create generator
function *myGenerator() {
  // Yield, or return, a message when myGenerator is started
  yield 'Message from myGenerator.'
}

// Assign generator to a variable
const message = myGenerator()

// Call the generator and log the message (the first start)
console.log(message.next())
// Output:
// { value: 'Message from myGenerator.', done: false }

// Call the generator and log the message (the second start)
console.log(message.next())
// Output:
// { value: undefined, done: true }


// Create generator with no yield
function *myGenerator() { }

// Assign generator to a variable
const message = myGenerator()

// Call the generator and log the message
console.log(message.next())
// Output:
// { value: undefined, done: true }
```

One thing about `yield` and pausing JavaScript generators. You use the `yield` keyword to pause the generator only from the inside of the generator. You can't use it from the outside. There is actually no way to pause a generator from the outside. Generator will pause itself only when it encounters a `yield` inside itself.

This also works in the opposite way for resuming a generator. Once it is paused generator can't resume itself on its own. The only way to resume it is by doing it from the outside. This brings us to the `next()` method.

## The next() method

You know that when you call a generator it will not execute its code. You also know that `yield` keyword is used to pause a generator. One question is, how can start a generator? Another one is, how can you resume paused one? The answer for both question is `next()` method.

When you assign a generator to a variable you start the generator using the `next()` method. When generator encounters `yield` keyword and pauses itself it is also the `next()` method what will resume it. When it is resumed, the generator will run until it encounters another `yield` keyword, `return` or end of its code block.

From this point of view, calling `next()` is like asking the generator for a value that's on the right side of next `yield` keyword. The important word here is "next". Remember that calling `next()` will always return the next yield inside the generator that follows the previous.

If it is the first start of the generator, after you assigned it to a variable, `next()` will return the first yield.

```JavaScript
// Create generator
function *myGenerator() {
  // Yield a number when myGenerator is started
  yield 1
  yield 2
  yield 3
}

// Assign generator to a variable
const message = myGenerator()

// Call the generator and log the number (the first start)
// This call returns the first yield
console.log(message.next())
// Output:
// { value: 1, done: false }

// Call the generator and log the number (the second start)
// This call returns the second yield
console.log(message.next())
// Output:
// { value: 2, done: false }

// Call the generator and log the number (the third start)
// This call returns the third yield
console.log(message.next())
// Output:
// { value: 3, done: false }

// Call the generator and log the number (the fourth start)
// This call doesn't return any yield because there is no fourth
// And since there is no other yield the generator is done
console.log(message.next())
// Output:
// { value: undefined, done: true }
```

Once the generator is done, once there are no more `yield` keywords the `next()` will always return the same. it will return object where value will be set to `undefined` and `done` to true. This will also happen generator reaches the end of its block.

```JavaScript
// Create generator
function *myGenerator() {
  // Yield a number when myGenerator is started
  yield 1
  yield 2
}

// Assign generator to a variable
const message = myGenerator()

// Call the generator and log the number (the first start)
console.log(message.next())
// Output:
// { value: 1, done: false }

// Call the generator and log the number (the second start)
console.log(message.next())
// Output:
// { value: 2, done: false }

// Try to call the generator and log the number (the third start)
// Generator is done and calling next() will always return the same value
console.log(message.next())
// Output:
// { value: undefined, done: true }

// Try to call the generator and log the number (the fourth start)
// The same value as after previous call
console.log(message.next())
// Output:
// { value: undefined, done: true }
```

Since we are talking about `next()` this is worth repeating. If you don't assign generator to a variable, calling `next()` will always return the first yield. The generator will not remember previous calls and values. We discussed this in the "Assigning to a variable" section.

## Yield and return

JavaScript generators are very similar to normal JavaScript functions. One of these similarities is that you can also use `return` statement inside them. When you do this, the generator will still pause with every `yield` it encounters. However, it will do so only with those that precede the `return` statement.

When generator encounters `return` statement it stops its execution,forever. If you return some value, the `return` statement will cause the generator to return that value. Otherwise, it will return `undefined` as a `value` of the returned object. At the same time, it will also return the `done` set to `true`.

This means that `return` statement will cause the generator to finish immediately. When you try to resume the generator you will get the same result as if the generator reached the last yield or end of the block. The `value` of returned object will be set to `undefined` and `done` will be set to `true`.

This also means that if there is any `yield` after `return` statement generator will never get to it.

```JavaScript
// Create generator
function *myGenerator() {
  // Yield a number when myGenerator is started
  yield 1
  // Return some value, and terminate the generator
  return 'The end.'
  // This second yield will never be reached
  yield 2
}

// Assign generator to a variable
const message = myGenerator()

// Call the generator and log the number (first start)
console.log(message.next())
// Output:
// { value: 1, done: false }

// Call the generator and log the message returned by return statement (second start)
console.log(message.next())
// Output:
// { value: 'The end.', done: true }

// Try to call the generator and log the second yield (third start)
// Generator is finished and calling next() will now always return the same value
console.log(message.next())
// Output:
// { value: undefined, done: true }
```

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
