# How JavaScript Spread Operator and Rest Parameters Work

Rest Parameters and Spread Operator are two quite popular features introduced in ES6. Thi tutorial will help you understand them. You will learn what rest parameters and spread operator are and how they work. You will also learn how to use them in the right way.

<!--more-->
<!--
Table of Contents:
-->

## Spread Operator

The spread operator is a feature that allows you to access content of an iterable object. Iterable object is an object, or data structure, that allows to access its content with [for...of] loop. The most popular example of an iterable is an array. Another example of an iterable can be objects literals or [strings].

When you wanted to access all content an some iterable before spread operator you had to use some kind of a loop, such as the mentioned `for...of` loop, or method, such as [forEach()]. Another option were indexes. Spread Operator allows you to do this much faster and with much less code. About the syntax.

The syntax of spread operator is simple and easy to remember. It consists of three dots (`...`). These three dots are followed by the iterable (`...someIterable`), which content you want to access.

```JavaScript
// Create array
const myArray = ['Venus', 'Ares', 'Mars']

// Use spread operator to access content of "myArray" variable
// Syntax: ...someIterable
console.log(...myArray)
// Output:
// 'Venus' 'Ares' 'Mars'
```

## Conclusion: [...] ...

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[for...of]: https://blog.alexdevero.com/javascript-loops/#for8230of-loop
[strings]: https://blog.alexdevero.com/javascript-basics-data-types-pt1/#strings
[forEach()]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach

<!--
### Meta:
-
-->

<!--
### Keywords:
- spread operator
- rest parameters
-->

<!--
### Resources:
- https://javascript.info/rest-parameters-spread
-->
