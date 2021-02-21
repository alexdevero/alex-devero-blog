# X JavaScript ES2020 Features You Should Know
<!--more-->
<!--
Table of Contents:
-->

## BigInt

The first of ES2020 features, new data type called `BigInt`, can seem like like a minor. It might be for many JavaScript developers. However, it will be big for developers who have to deal with large numbers. In JavaScript, there is a [limit] for the size of a number you can work with. This limit is 2^53 – 1.

Before the `BigInt` type, you could not go above this limit because the `Number` data type just can't handle these big numbers. With `BigInt` you can create, store and work with these large numbers. This includes even numbers that exceed the safe integer limit. There are two ways to create a `BigInt`.

The first way is by using `BigInt()` constructor. This constructor takes a number you want to convert to `BigInt` as a parameter and returns the `BigInt`. The second way is by adding "n" at the end of an integer. In both cases, JavaScript will add the "n" to the number you want to convert to `BigInt`.

This "n" tells JavaScript that the number at hand is a `BigInt` and it should not be treated as a `Number`. This also means one thing. Remember that `BigInt` is not a `Number` data type. It is `BigInt` data type. Strict comparison with `Number` will always fail.

```JavaScript
// Create the largest integer
let myMaxSafeInt = Number.MAX_SAFE_INTEGER

// Log the value of "myMaxSafeInt":
console.log(myMaxSafeInt)
// Output:
// 9007199254740991

// Check the type of "myMaxSafeInt":
console.log(typeof myMaxSafeInt)
// Output:
// 'number'

// Create BigInt with BigInt() function
let myBigInt = BigInt(myMaxSafeInt)

// Log the value of "myBigInt":
console.log(myBigInt)
// Output:
// 9007199254740991n

// Check the type of "myBigInt":
console.log(typeof myBigInt)
// Output:
// 'bigint'


// Compare "myMaxSafeInt" and "myBigInt":
console.log(myMaxSafeInt === myBigInt)
// Output:
// false


// Try to increase the integer:
++myMaxSafeInt
// Output:
// 9007199254740992

++myMaxSafeInt
// Output:
// 9007199254740992

++myMaxSafeInt
// Output:
// 9007199254740992


// Try to increase the BIgInt:
++myBigInt
// Output:
// 9007199254741007n

++myBigInt
// Output:
// 9007199254741008n

++myBigInt
// Output:
// 9007199254741009n
```

## String.prototype.matchAll()

The `matchAll()` is another smaller item on the list of ES2020 features. However, it can be handy. What this methods does is it helps you find all matches of a [regexp] pattern in a string. This methods returns an iterator. When you have this iterator, there are at least two things you can do.

First, you can use a `for...of` loop to iterate over the iterator and get individual matches. The second option is to convert the iterator to an array. Individual matches and corresponding data will become one individual items in the array.

```JavaScript
// Create some string:
const myStr = 'Why is the answer 42, what was the question that led to 42?'

// Create some regex patter:
const regexp = /\d/g

// Find all matches:
const matches = myStr.matchAll(regexp)

// Get all matches using Array.from():
Array.from(matches, (matchEl) => console.log(matchEl))
// Output:
// [
//   '4',
//   index: 18,
//   input: 'Why is the answer 42, what was the question that led to 42?',
//   groups: undefined
// ]
// [
//   '2',
//   index: 19,
//   input: 'Why is the answer 42, what was the question that led to 42?',
//   groups: undefined
// ]
// [
//   '4',
//   index: 56,
//   input: 'Why is the answer 42, what was the question that led to 42?',
//   groups: undefined
// ]
// [
//   '2',
//   index: 57,
//   input: 'Why is the answer 42, what was the question that led to 42?',
//   groups: undefined
// ]


// Get all matches using for...of loop:
for (const match of matches) {
  console.log(match)
}
// Output:
// [
//   '4',
//   index: 18,
//   input: 'Why is the answer 42, what was the question that led to 42?',
//   groups: undefined
// ]
// [
//   '2',
//   index: 19,
//   input: 'Why is the answer 42, what was the question that led to 42?',
//   groups: undefined
// ]
// [
//   '4',
//   index: 56,
//   input: 'Why is the answer 42, what was the question that led to 42?',
//   groups: undefined
// ]
// [
//   '2',
//   index: 57,
//   input: 'Why is the answer 42, what was the question that led to 42?',
//   groups: undefined
// ]
```

## globalThis

JavaScript developers working with difference environments have to remember that there are different global objects. For example, there is the `window` object in the browser. However, in Node.js, there is `global` object. In case of web workers, there is the `self`. One of the ES2020 features that aims to make this easier is `globalThis`.

The `globalThis` is basically a way to standardize the global object. You will no longer have to detect the global object on your own and then modify your code. Instead, you will be able to use `globalThis`. This will always refer to the global object for the environment you are working with at the moment.

```JavaScript
// In Node.js:
console.log(globalThis === global)
// Output:
// true


// In browser:
console.log(globalThis === window)
// Output:
// true
```

## Dynamic import

One thing every JavaScript developer has to deal with are various imports and growing amount of scripts. Until now, when you wanted to import any module you had to do it no matter the conditions. Sometimes, you had to import a module that was not actually used, based on the dynamic conditions of your application.

One of the ES2020 features, quite popular, are dynamic imports. What dynamic imports do is simple. They allow you to import modules when you need them. For example, let's say you know you need to use some module only under certain condition. Then, you can use [if...else statement] to test for this condition.

If the condition is met you can tell JavaScript to import the module so you can use it. This means putting a dynamic import inside the statement. The module will be loaded only when condition is met. Otherwise, if the condition is not met, no module is loaded and nothing is imported. Less code, smaller memory usage, etc.

When you want to import some module using dynamic import you use the
`import` keyword as you normally would. However, in case of dynamic imports, you use it as a function and call it. The module you want to import is what you pass into the function as an argument. This import function returns a [promise].

When the promise is settled you can use the [then()] handler function to do something with the imported module. Another option is to use the [await] keyword and assign the returned value, the module, to variable. You can then use that variable to work with the imported module.

```JavaScript
// Dynamic import with promises:
// If some condition is true:
if (someCondition) {
  // Import the module as a promise
  // and use then() to process the returned value:
  import('./myModule.js')
    .then((module) => {
      // Do something with the module
      module.someMethod()
    })
    .catch(err => {
      console.log(err)
    })
}


// Dynamic import with async/await:
(async() => {
  // If some condition is true:
  if (someCondition) {
    // Import the module and assign it to a variable:
    const myModule = await import('./myModule.js')

    // Do something with the module
    myModule.someMethod()
  }
})()
```

## Promise.allSettled()

Sometimes, you have a bunch of promises and don't care if some resolve and some reject. What you want to know is if and when all those promises are settled. This is exactly when you might want to use the new `allSettled()` method. This method accepts a number of promises in the form of an array.

It is only when all promises in the array are settled this method resolves. It doesn't matter if some, or all, promises are resolved or rejected. The only thing that matters is that they are all settled. When they are, the `allSettled()` method will return a new promise.

This value of this promise will be an array with statuses for each promise. It will also contain value for every fulfilled promise and reason for every rejected.

```JavaScript
// Create few promises:
const prom1 = new Promise((resolve, reject) => {
  resolve('Promise 1 has been resolved.')
})

const prom2 = new Promise((resolve, reject) => {
  reject('Promise 2 has been rejected.')
})

const prom3 = new Promise((resolve, reject) => {
  resolve('Promise 3 has been resolved.')
})

// Use allSettled() to wait until
// all promises are settled:
Promise.allSettled([prom1, prom2, prom3])
  .then(res => console.log(res))
  .catch(err => console.log(err))
// Output:
// [
//   { status: 'fulfilled', value: 'Promise 1 has been resolved.' },
//   { status: 'rejected', reason: 'Promise 2 has been rejected.' },
//   { status: 'fulfilled', value: 'Promise 3 has been resolved.' }
// ]
```

## Optional chaining

As a JavaScript developer you probably often work with objects and their properties and values. One good practice is to check if specific property exists before you try to access it. This okay if the structure of the object is shallow. It can quickly become a pain if it is deeper.

When you have to check for properties on multiple levels you quickly end up with long conditionals that can't fit the whole line. You may no longer need this with one of the ES2020 features called optional chaining. Optional chaining allows you to access deeply nested object properties without having to worry if the property exists.

If the property exists, you will get its value. If it doesn't exist, you will get `undefined`, instead of an error. What's also good about optional chaining is that it also works on function calls and arrays.

```JavaScript
// Create an object:
const myObj = {
  prop1: 'Some prop.',
  prop2: {
    prop3: 'Yet another prop.',
    prop4: {
      prop5: 'How deep can this get?',
      myFunc: function() {
        return 'Some deeply nested function.'
      }
    }
  }
}


// Log the value of prop5 no.1: without optional chaining
// Note: use conditionals to check if properties in the chain exist.
console.log(myObj.prop2 && myObj.prop2.prop4 && myObj.prop2.prop4.prop5)
// Output:
// 'How deep can this get?'


// Log the value of prop3 no.2: with optional chaining:
// Note: no need to use conditionals.
console.log(myObj.prop2?.prop4?.prop5)
// Output:
// 'How deep can this get?'


// Log non-existent value no.1: without optional chaining
console.log(myObj.prop5 && myObj.prop5.prop6 && myObj.prop5.prop6.prop7)
// Output:
// undefined


// Log non-existent value no.2: with optional chaining
// Note: no need to use conditionals.
console.log(myObj.prop5?.prop6?.prop7)
// Output:
// undefined
```

## Nullish coalescing operator

This feature, nullish coalescing operator, is also among the ES2020 features that caught a lot of attention. You know that with optional chaining you can access nested properties without having to worry if they exist. If not, you will get undefined. Nullish coalescing operator is often used with along with optional chaining.

What nullish coalescing operator does is it helps you check for "nullish" values and act accordingly. What is the point of "nullish" values? In JavaScript, there are two types of values, falsy and truthy. Falsy values are empty strings, 0, `undefined`, `null`, `false`, `NaN`, and so on.

The problem is that this makes it harder to check if something is only either `null` or `undefined`. Both `null` and `undefined` are falsy and they will be converted to `false` in boolean context. The same will happen if you use empty string or 0. They will also end up `false` in boolean context.

You can avoid this by checking for `undefined` and `null` specifically. However, this will require more code. Another option is the nullish coalescing operator. If the expression on the left side of the nullish coalescing operator evaluates to `undefined` or `null`, it will return the right side. Otherwise, the left.

One more thing. The syntax. The syntax of nullish coalescing operator is quite simple. It is composed of two question marks `??`. If you want to learn a lot more about nullish coalescing operator take a look at [this tutorial].

```JavaScript
// Create an object:
const friend = {
  firstName: 'Joe',
  lastName: undefined, // Falsy value.
  age: 0, // falsy value.
  jobTitle: '', // Falsy value.
  hobbies: null // Falsy value.
}

// Example 1: Without nullish coalescing operator
// Note: defaults will be returned for every falsy value.

// Log the value of firstName (value is 'Joe' - truthy)
console.log(friend.firstName || 'First name is unknown.')
// Output:
// 'Joe'

// Log the value of lastName (value is undefined - falsy)
console.log(friend.lastName || 'Last name is unknown.')
// Output:
// 'Last name is unknown.'

// Log the value of age (value is 0 - falsy)
console.log(friend.age || 'Age is unknown.')
// Output:
// 'Age is unknown.'

// Log the value of jobTitle (value is '' - falsy)
console.log(friend.jobTitle || 'Job title is unknown.')
// Output:
// 'Job title is unknown.'

// Log the value of hobbies (value is null - falsy)
console.log(friend.hobbies || 'Hobbies are unknown.')
// Output:
// 'Hobbies are unknown.'

// Log the value of non-existing property pets (falsy)
console.log(friend.pets || 'Pets are unknown.')
// Output:
// 'Pets are unknown.'


// Example 2: With nullish coalescing operator
// Note: defaults will be returned only for null and undefined.

// Log the value of firstName (value is 'Joe' - truthy)
console.log(friend.firstName ?? 'First name is unknown.')
// Output:
// 'Joe'

// Log the value of lastName (value is undefined - falsy)
console.log(friend.lastName ?? 'Last name is unknown.')
// Output:
// 'Last name is unknown.'

// Log the value of age (value is 0 - falsy)
console.log(friend.age ?? 'Age is unknown.')
// Output:
// 0

// Log the value of jobTitle (value is '' - falsy)
console.log(friend.jobTitle ?? 'Job title is unknown.')
// Output:
// ''

// Log the value of hobbies (value is null - falsy)
console.log(friend.hobbies ?? 'Hobbies are unknown.')
// Output:
// 'Hobbies are unknown.'

// Log the value of non-existing property pets (falsy)
console.log(friend.pets ?? 'Pets are unknown.')
// Output:
// 'Pets are unknown.'
```

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
