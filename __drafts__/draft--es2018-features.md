# Blog post title [...]
<!--more-->
<!--
Table of Contents:
-->

## Asynchronous iteration

Asynchronous iteration is one of the lesser discussed ES2018 features. While there is a lot of talk about other ES2018 features such rest and spread, there is almost none about asynchronous iteration. What is this about? With asynchronous iteration we get asynchronous iterables and iterators.

Well, this might not be helpful. One thing this means is that asynchronous iteration allows you to use the [await] keyword with for...of loops. You can use these loops to iterate over iterable objects. Examples of iterable objects include arrays, Maps, Sets, NodeLists, function arguments, TypedArray, etc.

Before ES2018 `for...of` loops worked synchronously. If you tried to iterate over iterable that involved asynchronous operations and await it, it would not work. The loop itself would remain synchronous, basically ignore the `await`, and complete the iteration before asynchronous operation inside it could finish.

```JavaScript
// This would not work pre-ES2018
// because the loop remains synchronous.
// Create an async function:
async function processResponses(someIterable) {
  // Try to iterate over iterable
  for (let item of someIterable) {
    // Process item via asynchronous operation, like promise:
    await processItem(item)
  }
}
```

With asynchronous iteration `for...of` loops also work with asynchronous code. This means that if you want to iterate over iterable and do some asynchronous operation you can. The `for...of` loop will now be asynchronous and let you await for asynchronous operations to complete.

What you have to remember is where to use the `await` keyword. You don't put it inside the loop. Instead, you put it at the beginning of the `for...of` loop, after the `for` keyword. Now, when you use the `next()` method to get the next value of the async iterator, you will get a Promise. If you want to know more, you can find the proposal on [GitHub].

```JavaScript
// Create an async function:
async function processResponses(someIterable) {
  // Iterate over iterable and await the result
  // of an asynchronous operation
  for await (let item of someIterable) {
    processItem(item)
  }
}
```

## Rest/Spread properties

The rest and spread are not really new features. Both introduced in ES6. They quickly rose in popularity and usage. It is safe to say that JavaScript developers loved them. The only problem was that they worked only with arrays and parameters. ES2018 introduced these two features also for objects. Let's quickly discuss both.

### The rest operator for objects

The first one, rest operator, allows you to extract all remaining object properties properties of an object onto a new object. Note that these properties must be enumerable. If you already used destructuring for some properties, the rest operator will extract only properties that remained.

```JavaScript
// Rest example:
// Create an object:
const daysObj = {
  one: 'Monday',
  two: 'Tuesday',
  three: 'Wednesday',
  four: 'Thursday',
  five: 'Friday'
}

// Use destructuring to assign
// first two properties to variables.
// Then, use rest to assign rest of properties
// to the third variable.
const { one, two, ...restOfDays } = daysObj
// The rest will extract only "three", "four"
// and "five" because we already extracted
// the "one" and "two" vie destructuring.

// Log the value of "one":
console.log(one)
// Output:
// 'Monday'

// Log the value of "two":
console.log(two)
// Output:
// 'Tuesday'

// Log the value of "restOfDays":
console.log(restOfDays)
// Output:
// { three: 'Wednesday', four: 'Thursday', five: 'Friday' }
```

If you want to use rest operator for objects, remember two things. First, you can use it only once. Exception is if you use it with nested objects. Second, you must use it at the last one. This is why, in the example above, you saw it after destructuring the first two properties, not before.

```JavaScript
// This will not work - rest operator as first:
const { ...all, one, two } = { one: 1, two: 2, three: 3 }

// This will work - rest operator as last:
const { one, two, ...all } = { one: 1, two: 2, three: 3 }


// This will not work - multiple rest operators on the same level:
const { one, ...some, ...end } = { /* some properties */ }

// This will work - multiple rest operators on multiple levels:
const { one, {...secondLevel }, ...firstLevel } = { /* some properties */ }
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
