# undefined and null in JavaScript Explained
<!--more-->
<!--
Table of Contents:
-->

## The basics

Both, `undefined` and `null`, are primitive [data types] that exist in JavaScript. These data types are Boolean, Number, String, Symbol, Null and Undefined. The rest of values in JavaScript are objects. Another thing `undefined` and `null` have in common is that they are both [falsy] values.

This means that when you use `undefined` in a boolean context it will be considered `false`. Boolean context is a context which evaluates to boolean value, either `true` or `false`. One example of boolean context is condition in [if...else] statement. This is also why you should avoid testing for loose equality.

When you test for loose equality there is [type coercion] happening on the background. Both, `undefined` and `null`, are falsy and this is what they will be considered as. The result of test for [loose equality] will result in match. The result of this test will be `true`. However, this is not really correct.

These two data types are not the same. If you want to avoid many problems, avoid testing for loose equality. Instead of loose equality, test for strict equality. When you test for [strict equality] JavaScript doesn't perform type coercion. Strict check will compare not only the value but also the data type.

`undefined` and `null` in JavaScript are different data types. This means that strict equality test will tell you, correctly, that these two are not the same. Let's take a look at each data type separately.

```JavaScript
// Testing for loose equality:
console.log(null == undefined)
// Output:
// true


// Testing for strict equality:
console.log(null === undefined)
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

One interesting thing is that `undefined` is not valid in JSON, `null` is. If you try to get the type of a variable that is undefined JavaScript will return "undefined". This is another interesting thing. In JavaScript, the the data type of undefined is a special value with its own type "Undefined".

```JavaScript
// Getting the data type of undefined:
console.log(typeof undefined)
// Output:
// 'undefined'
```

## Conclusion: undefined and null in JavaScript Explained

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[data types]: https://blog.alexdevero.com/javascript-basics-data-types-pt1/
[falsy]: https://developer.mozilla.org/en-us/docs/Glossary/Falsy
[if...else]: https://blog.alexdevero.com/javascript-if-else-statement/

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