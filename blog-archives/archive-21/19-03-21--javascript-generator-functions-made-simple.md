# JavaScript Generator Functions Made Simple

Generator functions are one of those things you may not see as often. However, they can be handy in some situations. This tutorial will help you understand them. You will learn about what generator functions are. You will also learn about `yield` and `next()` and also how to delegate execution.<!--more-->
<!--
Table of Contents:
## From regular functions to generator functions
## The syntax
## The generator object
## The yield and next()
### Yield, next, value and done
### Yield and return
### Example of generator function with a loop
## Yield* and execution delegation
### Yield* and return statement
## Yield, next() and passing arguments
## Conclusion: JavaScript Generator Functions Made Simple
-->

## From regular functions to generator functions

Regular [functions] has been around since the beginning of JavaScript. Functions are one of the fundamental building blocks of this programming language. This is not true if we talk about generator functions. These special functions have been introduced to JavaScript quite recently.

Functions have been working very well. Aside to regular functions, there are now also arrow functions. So far, arrow functions proved to be beneficial in some cases. They are often also preferred by JavaScript developers over the regular. One may ask, why add something new?

Both regular and arrow functions are great when you want to encapsulate a piece of code to make it re-usable. They are also allow you to return a single value or nothing. A single can be also an array or an object that contains multiple values. Nonetheless, there is still one thing you want to return.

This is where generator functions are different. Unlike regular functions, generators are capable of returning multiple values. That said, they don't return all of them at the same time. Instead, they returned one after another, only when you want it. Until then, generator will wait while remembering the last value.

## The syntax

One nice thing about generators is that they have a friendly syntax. There is a lot to learn, especially if you already know something about regular [functions]. At this monument, there are two ways to create a generator function. The first one is with the help of [GeneratorFunction constructor].

This approach is not very common and you will see it very rarely. The second, and more common approach, is by using function [declaration]. Yes, you can also create generators with function expression. In both cases, the `function` keyword is followed by asterisk (`*`).

This symbol is what tells JavaScript that you want to create a generator function, not a regular function. Except this small change, the rest of the syntax is the same as for function. There is the function name, parentheses for parameters, and function body with code to execute.

```JavaScript
// Create generator function:
function* myGenerator() {
  // Function body with code to execute.
}
```

## The generator object

One thing that may surprise you is that generators don't run the code inside them when you call them. Calling a generator function doesn't execute the code inside it. Instead, the generator function will return a special object called "generator object". This object allows you to work with the generator.

It allows you to tell the generator to return new value when you need it, by referencing this object. Because of this, when you call a generator function you should assign the returned generator object to some variable. Otherwise, it will be lost.

```JavaScript
// Create generator function:
function* myGenerator() {
  // Function body with code to execute.
}

// Assign the generator object to variable:
const myGeneratorObj = myGenerator()

// Log the generator object:
console.log(myGeneratorObj)
// Output:
// Iterator [Generator] {}
```

## The yield and next()

When it comes to generator functions, there are two important things. The first is [yield] keyword, along with some expression. The second is `next()` method. The `yield` keyword is like a breakpoint. You can use it only in a generator function. It does two things. First, it returns a value from the generator.

The second thing it does is it pauses execution of the generator. This happens right after the generator returns the value. You can think about the `yield` as a `return` statement. The difference is that while the `return` returns and terminates a function, `yield` returns and only pauses a generator.

As you know, calling a generator function returns a generator object. The `next()` is the main method of this generator object. This method allows you to run the generator, execute the code inside, and return some value. The value it returns is specified by the `yield` keyword. It is preceded by it.

So, to sum it up. The `yield` allows you to return a value from the generator, when you execute it, and then pause the generator. The `next()` method allows you to execute the generator, return the value that follows after the `yield`. Remember that `next()` will return only the value after the first `yield`.

If you use five `yield` keywords in a generator, you will have to call the `next()` method five times. One call for one `yield`. With every yield the execution of a generator will be paused, waiting for another call of `next()` method.

```JavaScript
// Create generator function:
function* myGenerator() {
  // Use yield to return values:
  yield 1
  yield 2
  yield 3
  yield 4
  return 5
}

// Assign the generator object to variable:
const myGeneratorObj = myGenerator()

// Return the first value:
console.log(myGeneratorObj.next())
// Output:
// { value: 1, done: false }

// Return the second value:
console.log(myGeneratorObj.next())
// Output:
// { value: 2, done: false }

// Return the third value:
console.log(myGeneratorObj.next())
// Output:
// { value: 3, done: false }

// Return the fourth value:
console.log(myGeneratorObj.next())
// Output:
// { value: 4, done: false }

// Return the fifth value:
console.log(myGeneratorObj.next())
// Output:
// { value: 5, done: true }
// The generator is finished.

// Try to return one more time:
console.log(myGeneratorObj.next())
// Output:
// { value: undefined, done: true }
```

### Yield, next, value and done

When you call the `next()` method JavaScript will always return an object. This object will contain two properties with some values. One property will be `value`. This is the actual value returned by the generator. It is the value that follows after the `yield` keyword in your code.

If there is no value to return, the value of this property will be `undefined`. The second property is `done`. This property says if the generator function is finished or not. "Finished" means that there are no more `yield` keywords in the generator functions and no more values to return.

The value of `done` will always be a boolean, either `true` or `false`. It will be `false` until the generator reaches the last `yield`. When it does, it will return the last value, after the last `yield`, along with `done` set to `true`. After this, calling `next()` again will be useless.

```JavaScript
// Create generator function:
function* myGenerator() {
  // Use yield to return values:
  yield 'a'
  yield 'b'
  return 'omega'
}

// Assign the generator object to variable:
const myGeneratorObj = myGenerator()

// Return the first value:
console.log(myGeneratorObj.next())
// Output:
// { value: 'a', done: false }

// Return the second value:
console.log(myGeneratorObj.next())
// Output:
// { value: 'b', done: false }

// Return the third value:
console.log(myGeneratorObj.next())
// Output:
// { value: 'omega', done: true }
// This is the last value returned
// and the generator is finished.
```

### Yield and return

Just because generators use `yield` to return values doesn't mean there is no place for `return` statement. There still is. In the context of generator functions, a `return` statement, is another thing that specifies if the generator is finished. Generator will finish under two conditions.

First, there are no more `yield` keywords. Second, the execution encounters a `return` statement. These two will change the value of `done` in the returned object from `false` to `true`. Returning a value with return works like `yield`. Any value after the `return` will be the value of `value` property in the returned object.

Three things to remember. First, `return` will finish the generator whether there are other `yield` or not. Let's say you declare four `yields` in a generator, but put `return` after the second. The result will that the generator will return three values. Two values for the first two `yield` and one for the `return`.

The last two `yield` after the return statement will never be executed because the `return` will finish the generator prematurely. Second thing to remember is that you don't necessarily have to use the `return` statement. The generator will finish when it encounters the last `yield`.

The third to remember. If you don't use `return`, the value of `done` after the last `yield` will be still set to `false`. It will change only if you try to return a value one more time. With `return`, `done` will be set to `true` right with the last call of `next()` method.

```JavaScript
// Generator function without return:
// NOTE: last yield will not change "done" to "true".
// It will change only after another call of "next()".
function* myGeneratorOne() {
  // Use yield to return values:
  yield 'a'
  yield 'b'
}

// Assign the generator object to variable:
const myGeneratorOneObj = myGeneratorOne()

// Return the first value:
console.log(myGeneratorOneObj.next())
// Output:
// { value: 'a', done: false }

// Return the second value:
console.log(myGeneratorOneObj.next())
// Output:
// { value: 'b', done: false }

// Try to return value again:
console.log(myGeneratorOneObj.next())
// { value: undefined, done: true }
// The generator is finished.


// Generator function ending with return:
// NOTE: the return will change "done" to "true" right away.
function* myGeneratorOne() {
  // Use yield to return values:
  yield 'a'
  return 'b'
}

// Assign the generator object to variable:
const myGeneratorOneObj = myGeneratorOne()

// Return the first value:
console.log(myGeneratorOneObj.next())
// Output:
// { value: 'a', done: false }

// Return the second value:
console.log(myGeneratorOneObj.next())
// Output:
// { value: 'b', done: true }
// The generator is finished.


// Generator function with return in the middle:
function* myGeneratorOne() {
  // Use yield to return values:
  yield 'a'
  yield 'b'
  return 'End'
  yield 'c'
  yield 'd'
}

// Assign the generator object to variable:
const myGeneratorOneObj = myGeneratorOne()

// Return the first value:
console.log(myGeneratorOneObj.next())
// Output:
// { value: 'a', done: false }

// Return the second value:
console.log(myGeneratorOneObj.next())
// Output:
// { value: 'b', done: false }

// Return the third value (the return):
console.log(myGeneratorOneObj.next())
// Output:
// { value: 'End', done: true }
// The generator is finished.

// Try to return the fourth value:
console.log(myGeneratorOneObj.next())
// Output:
// { value: undefined, done: true }
```

### Example of generator function with a loop

This ability to return a value on demand can be useful for example when you want to generate a series of numbers with loop. Normally, the loop would return all numbers right away. This will not happen if you use generator functions. Generators will allow you to return all numbers one by one.

There are only few things you need to create this number generator. First, is a generator function. Inside this generator will be a loop. Inside this loop will be the `yield` keyword returning current number in the series. This will create a loop that will pause after every iteration, waiting for the next call of `next()`.

```JavaScript

// Example of generator with for loop:
function* myGenerator() {
  for (let i = 0; i < 5; i++) {
    yield i
  }
}

// Assign the generator object to variable:
const myGeneratorObj = myGenerator()

// Return the first number:
console.log(myGeneratorObj.next())
// Output:
// { value: 0, done: false }

// Return the second number:
console.log(myGeneratorObj.next())
// Output:
// { value: 1, done: false }

// Return the third number:
console.log(myGeneratorObj.next())
// Output:
// { value: 2, done: false }

// Return the fourth number:
console.log(myGeneratorObj.next())
// Output:
// { value: 3, done: false }

// Return the fifth number:
console.log(myGeneratorObj.next())
// Output:
// { value: 4, done: false }

// Try to return another number:
console.log(myGeneratorObj.next())
// Output:
// { value: undefined, done: true }
// The generator is finished.
```

## Yield* and execution delegation

The `yield` keyword can do more than just return a value. It also allows you to delegate the execution of generator to another generator. You can use it to start a second generator from the first. This second generator will run until it is finished. Then, the execution will resume to the first generator.

This allows you to connect multiple generators together. Then, you can run them in a series you can control, each as long as necessary. When you want to use the `yield` to do this, just remember to add the asterisk symbol (`*`) right after the `yield` keyword (`yield*`). Then add a call to the generator you want to execute.

```JavaScript
// Create first generator function:
function* myGeneratorOne() {
  yield 1
  yield* myGeneratorTwo() // Delegate to myGeneratorTwo() generator.
  yield 3
}

// Create second generator function:
function* myGeneratorTwo() {
  yield 'a'
  yield 'b'
  yield 'c'
}

// Assign the first generator object to variable:
const myGeneratorObj = myGeneratorOne()

// Return the first value (myGeneratorOne):
console.log(myGeneratorObj.next())
// Output:
// { value: 1, done: false }

// Return the second value (myGeneratorTwo):
console.log(myGeneratorObj.next())
// Output:
// { value: 'a', done: false }

// Return the third value (myGeneratorTwo):
console.log(myGeneratorObj.next())
// Output:
// { value: 'b', done: false }

// Return the fourth value (myGeneratorTwo):
console.log(myGeneratorObj.next())
// Output:
// { value: 'c', done: false }

// Return the fifth value (myGeneratorOne):
console.log(myGeneratorObj.next())
// Output:
// { value: 3, done: false }

// Return the sixth value (myGeneratorOne):
console.log(myGeneratorObj.next())
// Output:
// { value: undefined, done: true }
```

### Yield* and return statement

When you use delegation careful with `return` statements. This applies especially to generators somewhere in the series. Don't worry. The `return` statement will not finish, or terminate, the whole chain. It will only finish the generator at which it is. However, it will not return any value.

When you use `return` statement in a generator it will finish the generator. It will also return a value that follows it. This doesn't applies to delegated execution and chain of generators. In this case, `return` will only finish the current generator and resume execution to the previous one. It will not return a value.

```JavaScript
// Create first generator function:
function* myGeneratorOne() {
  yield 1
  yield* myGeneratorTwo() // Delegate to myGeneratorTwo() generator.
  yield 3
}

// Create second generator function:
function* myGeneratorTwo() {
  yield 'a'
  yield 'b'
  return 'c' // This returned value will not show up.
}

// Assign the first generator object to variable:
const myGeneratorObj = myGeneratorOne()

// Return the first value (myGeneratorOne):
console.log(myGeneratorObj.next())
// Output:
// { value: 1, done: false }

// Return the second value (myGeneratorTwo):
console.log(myGeneratorObj.next())
// Output:
// { value: 'a', done: false }

// Return the third value (myGeneratorTwo):
console.log(myGeneratorObj.next())
// Output:
// { value: 'b', done: false }

// Return the fourth value (myGeneratorOne):
console.log(myGeneratorObj.next())
// Output:
// { value: 3, done: false }

// Return the fifth value (myGeneratorOne):
console.log(myGeneratorObj.next())
// Output:
// { value: undefined, done: true }
```

## Yield, next() and passing arguments

There is one interesting thing about the `next()` method. It allows you to pass arguments to generator functions. When you pass something as an argument to the `next()`, that value will become the value of `yield` in the generator. That said, if you want to pass some argument, do it for the second call of `next()`, not the first.

The reason for this is simple. The first call of `next()` method starts the execution of the generator. The generator is then paused when it reaches the first `yield`. There is no `yield` between the start of the generator execution and the first `yield`. So, any argument you pass will be lost.

```JavaScript
// Create generator function:
function* myGenerator() {
  console.log(yield + 1)
  console.log(yield + 2)
  console.log(yield + 3)
  console.log(yield + 4)
  return 5
}

// Assign the first generator object to variable:
const myGeneratorObj = myGenerator()

// Return the first value (no argument passing):
console.log(myGeneratorObj.next())
// Output:
// { value: 1, done: false }
// '1x' // <= value from console.log(yield + ...)

// Return the second value:
console.log(myGeneratorObj.next('1x'))
// Output:
// { value: 2, done: false }
// '2x' // <= value from console.log(yield + ...)

// Return the third value:
console.log(myGeneratorObj.next('2x'))
// Output:
// { value: 3, done: false }
// '3x' // <= value from console.log(yield + ...)

// Return the fourth value:
console.log(myGeneratorObj.next('3x'))
// Output:
// { value: 4, done: false }
// '4x' // <= value from console.log(yield + ...)

// Return the fifth value:
console.log(myGeneratorObj.next('4x'))
// Output:
// { value: 5, done: true }
```

## Conclusion: JavaScript Generator Functions Made Simple

Generator functions may not be used as often, but they can be useful. For example, when you want to generate some data on demand. Or, when you want to have more control over iteration over some data. I hope that this tutorial helped you understand what generator functions are and how to work with them.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[functions]: https://blog.alexdevero.com/javascript-functions-pt1/
[arrow functions]: https://blog.alexdevero.com/javascript-arrow-functions/
[GeneratorFunction constructor]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/GeneratorFunction
[declaration]: https://blog.alexdevero.com/javascript-functions-pt1/#function-declaration-and-function-expression
[yield]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/yield

<!--
### Meta:
-
-->

<!--
### Keywords:
- generator functions
-->

<!--
### Resources:
-
-->
