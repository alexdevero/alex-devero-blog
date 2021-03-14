# 7 JavaScript ES2017 Features to Learn

The JavaScript ES2017 specification (ES8) has been around for a while. Many of the features introduced in this spec are very useful. Most of them are also well supported and safe to use. In this tutorial, you will learn about what are the ES2017 features, how they work, and how to use them.<!--more-->
<!--
Table of Contents:
-->

## String padding with padStart() and padEnd()

Two smaller ES2017 features added to strings are `padStart()` and `padEnd()`. These two methods allow you to easily add characters to a string so it reaches a specific length. The `padStart()` adds characters at the beginning of the string. The `padEnd()` adds characters at the end.

Both methods accept two parameters. The first parameter is the length of the string you want to reach. The second parameter is the character you want to add. This character will be added repeatedly as long as is needed to reach the target length. If the string is already at the target length, or beyond it, nothing will happen.

This second parameter, the character to add, is optional. If you specify it, both methods will add it if necessary. If you omit it, both methods will add default character

```JavaScript
// padStart() example:
// Add '-' character at the beginning
// until the string reaches length of 9 characters.
'Hello'.padStart(9, '-')
// Output:
// '----Hello'

// Add 'A' character at the beginning
// until the string reaches length of 3 characters.
// Note: the string is already beyond this length
// so nothing will happen.
'Hello'.padStart(3, 'A')
// Output:
// 'Hello'

// Increase the length of a string to 11,
// but don't specify the character to add.
'Hello'.padStart(15)
// Output:
// '          Hello'


// padEnd() example:
// Add '-' character at the beginning
// until the string reaches length of 9 characters.
'Bye'.padEnd(9, '.')
// Output:
// 'Bye......'

// Add 'A' character at the beginning
// until the string reaches length of 3 characters.
// Note: the string is already beyond this length
// so nothing will happen.
'Bye'.padEnd(1, '?')
// Output:
// 'Bye'


// Increase the length of a string to 11,
// but don't specify the character to add.
'Bye'.padEnd(11)
// Output:
// 'Bye        '
```

## Object.values()

Another nice and useful addition to JavaScript language is `Object.values()` method. This method returns values from all object's own properties. It returns these values in the form of an array. This method accepts one parameter. This parameter is the object whose values you want to get.

One interesting thing is that this method also works with arrays. This means that you can pass an array as an argument, instead of an object. As a result, you will get a new array of values, the items from the original array.

```JavaScript
// Object.values() with objects:
// Create an object:
const joshuaObj = { name: 'Joshua', hobbies: 'programming' }

// Get all values from "joshuaObj":
console.log(Object.values(joshuaObj))
// Output:
// [ 'Joshua', 'programming' ]


// Object.values() with arrays:
// Create an array:
const languagesArr = ['C', 'C++', 'Rust', 'Python', 'JavaScript']

// Get all values from "languagesArr":
console.log(Object.values(languagesArr))
// Output:
// [ 'C', 'C++', 'Rust', 'Python', 'JavaScript' ]
```

## Object.entries()

Another addition for objects is the `entries()` method. The previous method `Object.entries()` returned only values of own properties. This method returns both, values of own properties as well as those own properties. You will get this data, these properties and values, in the form of nested [multidimensional arrays].

You will get one array for each own property. Each of these arrays will contain two items. The first one is the property. The second one is the value. The way to use this method is the same as for the `Object.entries()` method. You pass the object, whose entries you want to get, as an argument.

Similarly to the `Object.values()` method the `Object.entries()` also works with arrays. If you pass in an array, you will also get a multidimensional array. There will be one nested array for every item in the array. Each of these arrays will contain two items, the index of the item and the item itself.

```JavaScript
// Object.entries() with objects:
// Create an object:
const jackObj = { name: 'Jack', age: 44 }

// Get all entries from "jackObj":
console.log(Object.entries(jackObj))
// Output:
// [ [ 'name', 'Jack' ], [ 'age', 44 ] ]


// Object.entries() with arrays:
// Create an array:
const hobbiesArr = ['Reading', 'Writing', 'Sport', 'Programming']

// Get all entries from "hobbiesArr":
console.log(Object.entries(hobbiesArr))
// Output:
// [
//   [ '0', 'Reading' ],
//   [ '1', 'Writing' ],
//   [ '2', 'Sport' ],
//   [ '3', 'Programming' ]
// ]
```

## Object.getOwnPropertyDescriptors()

In JavaScript, objects have a number of properties. All these properties have their [descriptors]. These descriptors are attributes of these properties. These attributes include "value": value associated with the property and "writable": says if property can be read/written to, or if it is read-only.

Third attribute is "configurable": says if you can modify the descriptor and delete the property. Fourth is "enumerable": says if the property will shows up when you enumerate (loop over) the object. Last two are "get" and "set": getter and setter function for the property.

One of the ES2017 features is the `Object.getOwnPropertyDescriptors()` method. This method is here to help you work with these descriptors. It does so in two ways. First, it helps you get all own properties of an object along with all existing descriptors for these properties.

Second, it also helps you copy these descriptors. This will be very useful when you want to clone objects. When you try to copy an object, for example with [Object.assign()], you will encounter one problem. It will not copy properties with non-default attributes correctly. It will also leave out getter setter functions.

You can avoid this issue by using the `Object.getOwnPropertyDescriptors()` method, along with `Object.create()` and [Object.getPrototypeOf()]. This combination will allow you to create a [shallow copy] of an object that also contains  descriptors with non-default values.

```JavaScript
// Create an object:
const pet1 = {}

// Add property 'species' that is read-only
// and has custom getter function:
Object.defineProperty(pet1, 'species', {
  configurable: false,
  enumerable: true,
  writeable: false,
  get: function() {
    return 'It\'s a bird!'
  }
})

// Log the "pet1" object:
console.log(pet1)
// Output:
// { species: 'bird' }

// Log the value of "species" property:
// Note: this will invoke getter for this property.
console.log(pet1.species)
// Output:
// "It's a bird!"

// Get all properties and their descriptors:
Object.getOwnPropertyDescriptors(pet1)
// Output:
// {
//   species: {
//     get: ƒ get(),
//     set: undefined,
//     enumerable: true,
//     configurable: false
//   }
// }


// Try to clone the "pet1" object:
const pet2 = Object.assign({}, pet1)

// Log the value of "species" property of "pet2":
// Note: this will show an actual value.
// It will not trigger getter function
// because there is no getter function in "pet2".
console.log(pet2.species)
// Output:
// "It's a bird!"

// Get all properties of "pet2" and their descriptors:
Object.getOwnPropertyDescriptors(pet2)
// Output:
// {
//   species: {
//     value: "It's a bird!", // This is not supposed to be here.
//     writable: true, // This is supposed to be false.
//     enumerable: true,
//     configurable: true // This is supposed to be false.
//     // There is supposed to be custom getter function.
//   }
// }


// Try to clone the "pet1" object again
// using getOwnPropertyDescriptors(), create()
// and the prototype of "pet1":
const pet3 = Object.create(
  Object.getPrototypeOf(pet1),
  Object.getOwnPropertyDescriptors(pet1)
)

// Log the value of "species" property:
// Note: this will actually invoke getter for this property.
console.log(pet3.species)
// "It's a bird!"

// Get all properties and their descriptors:
Object.getOwnPropertyDescriptors(pet1)
// Output:
// {
//   species: {
//     get: ƒ get(), // Here is the custom getter.
//     set: undefined,
//     enumerable: true,
//     configurable: false // This is false as it should be.
//     // There is no "value", which is correct.
//   }
// }
```

## Async functions

Async functions are one of the most popular ES2017 features. This is not a surprise since they make writing asynchronous JavaScript even easier than [promises]. That said, async functions are really not that far from promises. One interesting fact. Async functions are actually built on top of promises.

When you use async functions, under the hood, JavaScript is still using promises. With that in mind, what's the point of using async functions and not promises? The main reason for using async functions is simpler and easier to read syntax. Promises made it easier to escape from the callback hell.

However, async functions took it one step further. I already wrote an extensive tutorial on both, [async functions] as well as [asynchronous JavaScript]. So, to learn more about async functions and asynchronous JavaScript, take a look at these two tutorials. They cover all you need to know.

Now, the big picture. Async functions are actually about two features. The first one is the `async` keyword. When you put this keyword at the beginning of a function declaration you create an async function. The second feature is the [await] operator. This operator can be used only inside an async function.

This operator pauses the execution of the async function in which it is placed. The execution is paused until a promise that follows this operator is resolved, until it is either fulfilled or rejected. When the promise is resolved, `await` extracts the value returned by the promise and allows to work with it, or assign it to a variable.

```JavaScript
// Syntax of async function:
async function myAsyncFunc() {
  // Syntax of await:
  // Assign the value returned by promise to a variable:
  const val = await somePromise()

  // Log the value returned by the promise:
  console.log(val)
}


// Example of promise and its handler methods and async function:
// Promise example:
// Use fetch to get data from API:
fetch('https://currencyapi.net/api/v1/rates?key=7zq3xkh2qeZcnvFhfyDyFlvqx4EmQ7R3N1qq')
  // Convert the response to JSON:
  .then(res => res.json())
  // Log the JSON to console:
  .then(data => console.log(data))
  // Log any errors:
  .catch(err => console.log(err))
// Output:
// {
//   valid: true,
//   updated: 1615723207,
//   base: 'USD',
//   rates: {
//     AED: 3.67338,
//     AFN: 77.705,
//     ALL: 103.255,
//     // ...
//   }
// }

// Async function example:
async function getCurrencies() {
  // Use fetch to get data from API
  // and assign it to a variable:
  const data = await fetch('https://currencyapi.net/api/v1/rates?key=7zq3xkh2qeZcnvFhfyDyFlvqx4EmQ7R3N1qq')
  // Convert the response to JSON
  // and assign it to a variable:
  const json = await data.json()

  // Log the JSON to console:
  console.log(json)
}

// Call the getCurrencies() function:
getCurrencies()
// Output:
// {
//   valid: true,
//   updated: 1615723207,
//   base: 'USD',
//   rates: {
//     AED: 3.67338,
//     AFN: 77.705,
//     ALL: 103.255,
//     // ...
//   }
// }


// Async with try...catch:
async function getCurrencies() {
  try {
    const data = await fetch('https://currencyapi.net/api/v1/rates?key=7zq3xkh2qeZcnvFhfyDyFlvqx4EmQ7R3N1qq')
    const json = await data.json()

    console.log(json)
  }
  catch(err) {
    // Log any errors:
    console.log(err)
  }
}

getCurrencies()


// Promise with async function:
// Create function that returns a promise:
function myPromiseFunc() {
  // Return a promise:
  return new Promise((resolve) => {
    // Resolve the promise after 2.5s:
    setTimeout(() => {
      resolve('Job done!')
    }, 2500)
  })
}

// Create async functions:
async function myAsyncFunction() {
  // Call the "myPromiseFunc()" function
  // and log returned value to console:
  console.log(await myPromiseFunc())
}

// Call the "myAsyncFunction()" function:
myAsyncFunction()
console.log('This will actually appear before the promise.')
console.log('This will also appear before the promise.')
// Output:
// 'This will actually appear before the promise.'
// 'This will also appear before the promise.'
// 'Job done!'
```

## Trailing commas

This is a small feature that can make working with git, or another source control, easier. The purpose of this feature is simple. It allows you to end the list of parameter of a function with a trailing coma. This may sound weird, but consider this. Imagine you have a function that accepts multiple parameters.

To make the code more readable, each parameter is on a separate line. You commit this code, add it to your source control. Then, someone else comes and adds new parameter. What happens? Source control will annotate the line with new parameter. However, it will also annotate the line above.

The reason is simple. In order to add new parameter, it is necessary to add a new comma after the last existing parameter. Source control will notice this change and annotate two lines that changed, one with old parameter and one with new. The purpose of trailing comma allows is to avoid this.

You add the trailing comma after the last parameter. Then, when someone else adds new parameter, it is not necessary to add new comma after the last parameter. The result? Source control annotates only one line that changed.

```JavaScript
// Before adding new parameter:
function myFunc(
  parOne,
  parTwo,
  parThree
) {}

// Before adding new parameter:
function myFunc(
  parOne,
  parTwo,
  parThree, // First change: new ",".
  parFour // Second change: new parameter.
) {}


// With trailing comma:
// Before adding new parameter:
function myFunc(
  parOne,
  parTwo,
  parThree, // Trailing comma is now valid here.
) {}

// Before adding new parameter:
function myFunc(
  parOne,
  parTwo,
  parThree,
  parFour, // First and only change: new parameter.
) {}
```

## Shared Memory and atomics

The first, shared memory, uses [SharedArrayBuffer] to create a memory you can then share between agents, web workers, and threads. The second, atomics, goes hand in hand with shared memory. There is one problem with `SharedArrayBuffer`. It can be unpredictable. You don't really know when the data will be synchronized between agents.

One reason for this is that the speed of synchronization depends on the system on which it is running. It depends on the resources that are available. Atomics provide you with static functions that help you make [atomic operations] more predictable. If you want to learn more about shared memory and atomics, take a look at [this tutorial].

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
