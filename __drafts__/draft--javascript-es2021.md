# Upcoming Interesting ES2021 JavaScript Features to Learn
<!--more-->
<!--
Table of Contents:
-->


## String.prototype.replaceAll()

Let's start with smaller JavaScript ES2021 feature, but still nice addition to the language, `replaceAll()` method. At this moment, when you want to replace multiple occurrences of a pattern in a [string] you can you [replace() method]. The problem? If you use a string, this will allow you to replace only the first occurrence of the pattern.

This doesn't mean the `replace()` method is useless if you want to replace all occurrences of a pattern. It can get this job done as well. However, you have to use a [regular expression]. If this is okay with you then no problem. For many developers, regular expressions are not their preferred choice. Far from it.

If you are one these developers, you are going to like the new `replaceAll()` method. This method works in a similar same way as the `replace()` method. The difference is that `replaceAll()` allows you to replace all occurrence of a pattern without having to use regular expression.

The `replaceAll()` method also accepts regular expressions. So, if regex is your thing you can use it as well. You can also use a function as the replacement. If you do, this function will be executed for each match in the string. You can read this proposal in the [official repository].

```JavaScript
// Declare a string:
let str = 'There are those who like cats, there those who like watching cats and there are those who have cats.'

// Replace all occurrences of "cats" with dogs:
str = str.replaceAll('cats', 'dogs')

// Log the new value of "str":
console.log(str)
// Output:
// 'There are those who like dogs, there those who like watching dogs and there are those who have dogs.'


// A simple alternative with replace():
str = str.replace(/cats/g, 'dogs')

// Log the new value of "str":
console.log(str)
// Output:
// 'There are those who like dogs, there those who like watching dogs and there are those have dogs.'
```

## Numeric separators

This is another very small JavaScript ES2021 feature that can make your day at least a bit better. Especially if you work with big numbers. Numeric separators provide you with an easy and simple way to make big numbers more readable and easier to work with. The syntax is just as easy. It is a underscore (`_`).

```JavaScript
// Number without numeric separators:
const num = 3685134689


// Number with numeric separators:
const num = 3_685_134_689
```

Remember that numeric separators are just visual aid. If you use them they will have no effect on the numeric values themselves. For example, if you try to log a number with numeric separators you will get the "raw" and "unedited" version.

```JavaScript
// Use numeric separators with a number:
const num = 3_685_134_689

// Log the value of "num":
console.log(num)
// Output:
// 3685134689
```

## Logical assignment operators

JavaScript allows to use logical operators generally in boolean contexts. For example, in [if...else statements] and [ternary operators] to test for truthfulness. This will change with ES2021 and logical assignment operators. These operators allow you to combine logical operators with assignment expression (`=`).

There are some [assignment operators] you can use that have been around for a while. For example, addition assignment (`+=`), subtraction assignment (`-=`), multiplication assignment (`*=`), and so on. Thanks to ES2021, you will be also able to use logical operators (`&&`, `||` and `??` ([nullish coalescing])) as well.

```JavaScript
//
// AND AND equals (&&=)
x &&= y

// Is equivalent to:
x = x && d

// Or:
if (x) {
  x = y
}

// Example 1:
let x = 3 // Truthy value.
let y = 0 // Falsy value.
x &&= y

// Log the value of "x":
console.log(x)
// Output:
// 0

// Example 2:
let x = 0 // Falsy value.
let y = 9 // Truthy value.
x &&= y

// Log the value of "x":
console.log(x)
// Output:
// 0

// Example 3:
let x = 3 // Truthy value.
let y = 15 // Truthy value.
x &&= y

// Log the value of "x":
console.log(x)
// Output:
// 15


//
// OR OR equals (||=):
x ||= y

// Is equivalent to:
x = x || y

// Or:
if (!x) {
  x = y
}

// Example 1:
let x = 3 // Truthy value.
let y = 0 // Falsy value.
x ||= y

// Log the value of "x":
console.log(x)
// Output:
// 3

// Example 2:
let x = 0 // Falsy value.
let y = 9 // Truthy value.
x ||= y

// Log the value of "x":
console.log(x)
// Output:
// 9

// Example 3:
let x = 3 // Truthy value.
let y = 15 // Truthy value.
x ||= y

// Log the value of "x":
console.log(x)
// Output:
// 3


//
// Nullish coalescing (??):
x ??= y

// Is equivalent to:
x = x ?? y

// Or:
if (x == null || x == undefined) {
    x = y
}

// Example 1:
let x = null // Null value.
let y = 'Hello' // Non-null value.
x ??= y

// Log the value of "x":
console.log(x)
// Output:
// 'Hello'

// Example 2:
let x = 'Jay' // Non-null value.
let y = 'Hello' // Non-null value.
x ??= y

// Log the value of "x":
console.log(x)
// Output:
// 'Jay'

// Example 3:
let x = 'Jay' // Non-null value.
let y = null // Null value.
x ??= y

// Log the value of "x":
console.log(x)
// Output:
// 'Jay'

// Example 4:
let x = undefined // Non-null value.
let y = 'Jock' // Null value.
x ??= y

// Log the value of "x":
console.log(x)
// Output:
// 'Jock'
```

Let's take a look at the example above. First, the `x &&= y`. This will assign `y` to `x` only if `x` is truthy. Otherwise, it will assign `y`. Second, the `x ||= y`. This will assign `y` to `x` only when `x` is a falsy value. If the `x` is truthy and `y` is falsy, the assignment will not happen.

The same will happen if both `x` and `y` are falsy. The last one, the `x ??= y`. This will assign `y` to `x` only if `x` is either `null` or `undefined`. If `x` is neither `null` nor `undefined` the assignment will not happen. The same if the `y` is either `null` or `undefined`.

## Promise.any()

When it comes to [JavaScript promises], last year or two were quite livid. The ES6 introduced `Promise.race()` and `Promise.all()` methods. After that, the ES2020 delivered `Promise.allSettled()`. ES2021 brings another method that can make working with promises even easier, the `Promise.any()` method.

The `Promise.any()` method takes multiple promises and returns a promise if any of the promises is fulfilled. The first promise that is fulfilled is the promise returned by the `Promise.any()`. If all promises you provided are rejected `Promise.any()` will return `AggregateError`. This contains the reasons of rejection.

```JavaScript
// Example 1: All resolve:
// Create promises:
const promise1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('promise1 is resolved.')
  }, Math.floor(Math.random() * 1000))
})

const promise2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('promise2 is resolved.')
  }, Math.floor(Math.random() * 1000))
})

const promise3 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('promise3 is resolved.')
  }, Math.floor(Math.random() * 1000))
})

;(async function() {
  // Await the result of Promise.any():
  const result = await Promise.any([promise1, promise2, promise3])

  // Log the value returned by Promise.any():
  console.log(result)
  // Output:
  // 'promise1 is resolved.', 'promise2 is resolved.' or 'promise3 is resolved.'
})()


// Example 2: Some resolve:
// Create promises:
const promise1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('promise1 is resolved.')
  }, Math.floor(Math.random() * 1000))
})

const promise2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject('promise2 was rejected.')
  }, Math.floor(Math.random() * 1000))
})

;(async function() {
  // Await the result of Promise.any():
  const result = await Promise.any([promise1, promise2])

  // Log the value returned by Promise.any():
  console.log(result)
  // Output:
  // 'promise1 is resolved.'
})()


// Example 3: None resolves:
// Create promises:
const promise1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject('promise1 was rejected.')
  }, Math.floor(Math.random() * 1000))
})

const promise2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject('promise2 was rejected.')
  }, Math.floor(Math.random() * 1000))
})

;(async function() {
  // Use try...catch to catch the AggregateError:
  try {
    // Await the result of Promise.any():
    const result = await Promise.any([promise1, promise2])
  }

  catch (err) {
    console.log(err.errors)
    // Output:
    // [ 'promise1 was rejected.', 'promise2 was rejected.' ]
  }
})()
```

## WeakRef

The last notable feature of ES2021 is a `WeakRefs`. In JavaScript, when you create a reference to an object, it prevents it from being collected by [garage collection]. This means that JavaScript can't remove the object and free its memory. This allows the object to live, as long as there is the reference to it, potentially forever.

ES2021 brings new class `WeakRefs`. This will allow developers create weak references to objects. With this, developers will be able to, for example, keep track of existing objects without preventing them from being garbage-collected. This can be useful for caches and objects mapping.

When you want to create new `WeakRef`, you have to use it with the `new` keyword. As an argument, you pass into the parentheses some object. When you want to read the reference, the referenced object, you can do so by calling `deref()` on the weak reference. Let's take a look at one very simple example.

```JavaScript
const myWeakRef = new WeakRef({
  name: 'Cache',
  size: 'unlimited'
})

// Log the value of "myWeakRef":
console.log(myWeakRef.deref())
// Output:
// { name: 'Cache', size: 'unlimited' }

// Log the value of "name" property:
console.log(myWeakRef.deref().name)
// Output:
// 'Cache'

// Log the value of "size" property:
console.log(myWeakRef.deref().size)
// Output:
// 'unlimited'
```

### Finalizers and FinalizationRegistry

Closely connected to `WeakRef`, there is another feature of ES2021 called finalizers, or `FinalizationRegistry`. This feature allows you to register callback functions that will be invoked when an object is garbage collected.

```JavaScript
// Create new FinalizationRegistry:
const reg = new FinalizationRegistry((val) => {
  // Print the value of "val" when invoked:
  console.log(val)
})

;(() => {
  // Create new object:
  const obj = {}

  // Register finalizer for the "obj" obj:
  // 1st argument: object to register finalizer for.
  // 2nd argument: value for callback function defined above.
  reg.register(obj, 'obj has been garbage-collected.')
})()
// Output when "obj" is garbage-collected:
// 'obj has been garbage-collected.'
```

One important thing about `WeakRef` and finalizers. The proposal for this feature itself advises not to use them. One reason is that they can be unpredictable. Another one is that they don't really help garbage collection do its job. They can actually make it job harder. You can read more about the reasons in the [proposal].

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
- https://codeburst.io/exciting-features-of-javascript-es2021-es12-1de8adf6550b
- https://backbencher.dev/javascript/es2021-new-features
-->
