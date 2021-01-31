# undefined and null in JavaScript Explained

`undefined` and `null` are two data types in JavaScript that can sometimes be confusing. This tutorial will help you learn about them. It will explain what `undefined` and `null` in JavaScript are. You will also learn what are some differences between these two and how to work with them.<!--more-->
<!--
Table of Contents:
-->

## The basics

Both, `undefined` and `null`, are primitive [data types] that exist in JavaScript. These data types are Boolean, Number, String, Symbol, Null and Undefined. The rest of values in JavaScript are objects. Another thing `undefined` and `null` have in common is that they are both [falsy] values.

This means that when you use `undefined` in a boolean context it will be considered `false`. Boolean context is a context which evaluates to boolean value, either `true` or `false`. One example of boolean context is condition in [if...else] statement. This is also why you should avoid testing for loose equality.

When you test for loose equality there is [type coercion] happening on the background. Both, `undefined` and `null`, are falsy and this is what they will be considered as. The result of test for [loose equality] will result in match. The result of this test will be `true`. However, this is not really correct.

These two data types are not the same. If you want to avoid many problems, avoid testing for loose equality. Instead of loose equality, test for strict equality. When you test for [strict equality] JavaScript doesn't perform type coercion. Strict check will compare not only the value but also the data type.

`undefined` and `null` in JavaScript are different data types. This means that strict equality test will tell you, correctly, that these two are not the same.

```JavaScript
// Testing for loose equality:
console.log(null == undefined)
// Output:
// true


// Testing for strict equality:
console.log(null === undefined)
// Output:
// false


// Other examples of loose equality:
console.log(null == 0)
// Output:
// false

console.log(null == 0n)
// Output:
// false

console.log(null == null)
// Output:
// true

console.log(null == false)
// Output:
// false

console.log(null == NaN)
// Output:
// false

console.log(null == '')
// Output:
// false


// Other examples of strict equality:
console.log(null === 0)
// Output:
// false

console.log(null === 0n)
// Output:
// false

console.log(null === null)
// Output:
// true

console.log(null === undefined)
// Output:
// false

console.log(null === false)
// Output:
// false

console.log(null === NaN)
// Output:
// false

console.log(null === '')
// Output:
// false
```

## The undefined

When you declare a variable but don't assign it a value, it will become `undefined`. This is one of the things that JavaScript does automatically. However, you can also assign variable `undefined` by yourself if you want. Although, this is not a common practice among JavaScript developers.

```JavaScript
// Declare variable without assigning it a value:
let car

// Log the value of "car":
console.log(car)
// Output:
// undefined


// Declare variable as undefined:
let house = undefined

// Log the value of "house":
console.log(house)
// Output:
// undefined
```

There are other scenarios when you will get `undefined`. Two examples of these scenarios are non-existing array elements, non-existing object properties. When you try to work with non-existing object property JavaScript will return undefined. The same with array element that doesn't exist.

```JavaScript
// Non-existing object properties and array elements:
const book = {
  title: 'Zero to One',
  author: ['Peter Thiel', 'Blake Masters'],
  publicationDate: 'September 18, 2014'
}

// Try to access non-existing property:
console.log(book.genre)
// Output:
// undefined


// Try to access non-existing array element:
console.log(book.author[2])
// Output:
// undefined


// Or:
const myObj = {}
const arr = []

// Log the value of myObj.prop:
console.log(myObj.prop)
// Output:
// undefined

// Log the value of first element:
console.log(arr[0])
// Output:
// undefined
```

Another scenario when you get an `undefined` is if you have a function that doesn't explicitly return anything. Then, it will implicitly return `undefined`. The same will happen if a function has a `return` statement, but without anything that follows it. It will also implicitly return `undefined`.

```JavaScript
// Create a function that doesn't return:
function myFunc() {}

// Call myFunc():
myFunc()
// Output:
// undefined


// Create a function that returns nothing:
function myFunc() {
  return
}

// Call myFunc():
myFunc()
// Output:
// undefined
```

One interesting thing is that `undefined` is not valid in JSON, `null` is. There is another interesting thing. If you try to get the type of a variable that is undefined JavaScript will return "undefined". In JavaScript, the the data type of undefined is a special value with its own type "Undefined".

```JavaScript
// Trying to use undefined in JSON
console.log(JSON.stringify({ name: undefined, age: null }))
// Output:
// '{"age":null}'

// Getting the data type of undefined:
console.log(typeof undefined)
// Output:
// 'undefined'
```

### undefined and default parameters values

[Default parameter values] are one handy feature that was introduced in ES6. This feature allows you to declare parameters with default values. You can use this feature with variables and with functions. By default, default parameters are used when the value is undefined. In case of functions, when the parameter is undefined, i.e. missing.

```JavaScript
// Create function with default parameter value:
function myFunc(name = 'Unknown') {
  return name
}

// Call myFunc without any argument (parameter being undefined):
myFunc()
// Output:
// Unknown

// Call myFunc with argument (parameter being defined):
myFunc('Jack')
// Output:
// 'Jack'
```

### undefined and destructuring assignment

[Destructuring assignment] is another feature introduced in ES6 that quickly became very popular. This feature allows you to extract values from arrays, and properties from objects, and assign them to variables. All this with a single line of code. One useful feature of destructuring is that it supports default values.

Imagine you have an array. What you want is to extract some items from this array and assign them to few variables. The problem is that you don't know if there is enough values for each variable. What you can do is to use default values. If some variable doesn't find a match in the array, it will use the default value.

This is because the value received from the array will be `undefined`. This will tell JavaScript that there is nothing to assign and that it should use the default value.

```JavaScript
// Create an array:
const myArray = ['1 is one', '2 is two', '3 is three']

// Use destructuring assignment
// to assign values from myArray:
const [one, two, three, four = 'Four doesn\'t exist'] = myArray

// Get the value of one:
console.log(one)
// Output:
// '1 is one'

// Get the value of two:
console.log(two)
// Output:
// '2 is two'

// Get the value of three:
console.log(three)
// Output:
// '3 is three'

// Get the value of four:
// four will be undefined because the array
// contains only three items.
// This will trigger default value 'Four doesn\'t exist'.
console.log(four)
// Output:
// "Four doesn't exist"
```

## The null

`null` in JavaScript can be hard to encounter. Unlike `undefined` it is not assigned automatically when some conditions happen. Due to tis, it has to be assigned by someone. This can happen quite often because many JavaScript developers like to use as a temporary value. It signals empty or non-existent value.

```JavaScript
// Variable automatically assigned undefined:
let name

// Log the value of "name":
console.log(name)
// Output:
// undefined


// Variable explicitly assigned null:
let position = null

// Log the value of "position":
console.log(position)
// Output:
// null
```

Do you remember that `undefined` has its own type "Undefined"? There is one interesting thing on `null` in JavaScript as well. It is actually an object. This object has a valid value, but no properties and it is non-mutable. You can easily test this by yourself with the [typeof] operator.

If you use the `typeof` operator with `null`, you will not get something like "null" for example. Instead, you will get "object". This has been in JavaScript since the very beginning. It is regarded as a mistake in the original implementation of JavaScript.

```JavaScript
// Test type of null:
console.log(typeof null)
// Output:
// 'object'

console.log(typeof null === 'object')
// Output:
// true
```

### null and default parameter values

As you know, default parameter values allow you to declare default value in case necessary value is `undefined`. Interestingly, this doesn't work with `null`. Let's say you create a function and use default parameter value. A bit later, you call that function with and pass in `null`.

What will happen in this case is not what you might expect. You will not get the default value you specified. What you will get instead is the `null`. Remember this if you like to use default parameters, or want to use them. Otherwise, you may get into some troubles.

```JavaScript
// Create function with default parameter value:
function myFunc(name = 'Unknown') {
  return name
}

// Call myFunc with null as an argument:
myFunc(null)
// Output:
// null
```

### null and garbage collection

In JavaScript, there is something called [garbage collection]. This is a process for freeing up memory allocated for your code, your objects. What this process does is it looks for unused existing objects in memory and removes them. JavaScript determines if object is in use or not if it is referenced.

When some object is no longer referenced JavaScript will assume it is no longer needed and remove it. This will free the memory allocated for that object. This process happens automatically and periodically on the background. This is one advantage of high-level languages such as JavaScript.

You don't have to allocate memory every time you create an object. Just as well you don't have to free that memory when you no longer need some object. JavaScript does this memory management for you. What about `null`? While JavaScript manages memory automatically you can tell it that some object can be garbage collected.

One way to do this is by assigning a variable, that stores the object, `null`. If there are no other references to that object JavaScript will remove it. This will not happen immediately. It will happen during the next cycle of garbage collection.

```JavaScript
// Create an object:
let myObj = { name: 'Stuart' }

// Assign the variable myObj to null
// to make { name: 'Stuart' } available for garbage collection:
myObj = null

// { name: 'Stuart' } can be garbage collected.


// Multiple references:
// First reference to { isAlive: true }:
let objOne = { isAlive: true }

// Second reference to { isAlive: true }:
let objTwo = objOne

// Remove all references to { isAlive: true }
// so the object can be garbage collected:
objOne = null
objTwo = null

// { isAlive: true } can be garbage collected.
```

## Simple checks for undefined and null in JavaScript

Checking for undefined and null in JavaScript can be easy and simple. You can use strict equality check and correct data type to check for. You can also use the `typeof` operator. However, you have to remember the thing about `null` being "object", not "null".

```JavaScript
// Check if value is null:
const myVar = null

console.log(myVar === null)
// Output:
// true


// Check if value is undefined:
let myVar

console.log(myVar === undefined)
// Output:
// true
```

Another option you can use to check for `null` is to use `typeof` operator and check if the value is falsy. `null` will be falsy, empty object will be `truthy`.

```JavaScript
// Check if value is null:
const myVar = null

console.log(typeof myVar === 'object' && !myVar)
// Output:
// true
```

## Conclusion: undefined and null in JavaScript explained

The `undefined` and `null` are two data types that can be sometimes confusing for beginners. This is especially thanks to some quirks and things one may not expect. I hope that this tutorial helped you understand how `undefined` and `null` in JavaScript work and also how to use them.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[data types]: https://blog.alexdevero.com/javascript-basics-data-types-pt1/
[falsy]: https://developer.mozilla.org/en-us/docs/Glossary/Falsy
[if...else]: https://blog.alexdevero.com/javascript-if-else-statement/
[type coercion]: https://blog.alexdevero.com/type-coercion-in-javascript/
[loose equality]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Equality
[strict equality]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Strict_equality
[Default parameter values]: https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt2/#default-parameters-and-values
[Destructuring assignment]: https://developer.mozilla.org/en-us/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment
[typeof]: https://developer.mozilla.org/en-us/docs/Web/JavaScript/Reference/Operators/typeof
[garbage collection]: https://blog.alexdevero.com/garbage-collection-in-javascript/

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
