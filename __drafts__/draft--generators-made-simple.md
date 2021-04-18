# Blog post title [...]
<!--more-->
<!--
Table of Contents:
-->

## From regular functions to generator functions

Regular [functions] has been around since the beginning of JavaScript. Functions are one of the fundamental building blocks of this programming language. This is not true if we talk about generator functions. These special functions have been introduced to JavaScript quite recently.

Functions have been working very well. Aside to regular functions, there are now also arrow functions. So far, arrow functions proved to be beneficial in some cases. They are often also preferred by JavaScript developers over the regular. One may ask, why to add something new?

Both regular and arrow functions are great when you want to encapsulate a piece of code to make it re-usable. They are also allow you to return a single value or nothing. A single can be also an array or an object that contains multiple values. Nonetheless, there is still one thing you want to return.

This is where generator functions are different. Unlike regular functions, generators are capable of returning multiple values. That said, they don't return all of them at the same time. Instead, they returned one after another, only when you want it. Until then, generator will wait while remembering the last value.

## The syntax

One nice thing about generator functions is that they have a friendly syntax. There is a lot to learn, especially if you already know something about regular [functions]. At this monument, there are two ways to create a generator function. The first one is with the help of [GeneratorFunction constructor].

This approach is not very common and you will see it very rarely. The second, and more common approach, is by using function [declaration]. Yes, you can also create generators with function expression. In both cases, the `function` keyword is followed by asterisk (`*`).

This symbol is what tells JavaScript that you want to create a generator function, not a regular function. Except this small change, the rest of the syntax is the same as for function. There is the function name, parentheses for parameters, and function body with code to execute.

```JavaScript
// Create generator function:
function* myGenerator() {
  // Function body with code to execute.
}
```

## The generator object

One thing that may surprise you is that generators don't rune the code inside them when you call them. Calling a generator function doesn't execute the code inside it. Instead, the generator function will return a special object called "generator object". This object allows you to work with the generator.

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

The second thing it does is it pauses execution of the generator. This happens right after the generator returns the value. You can thing about the `yield` as a `return` statement. The difference is that while the `return` returns and terminates a function, `yield` returns and only pauses a generator.

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

// Try to return one more time:
console.log(myGeneratorObj.next())
// Output:
// { value: undefined, done: true }
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
