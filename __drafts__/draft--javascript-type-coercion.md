# How Type Coercion in JavaScript Works

In JavaScript, you can convert a value from one type to another. This is called type coercion. Type coercion is one of the topics that can be hard to understand. This tutorial will help you with it. It will show you what it is, how it works, and how to use it to become a better JavaScript developer.

<!-- Type coercion in Javascript Explained -->
<!--more-->
<!--
Table of Contents:
## h2
## Conclusion: [...] ...
-->

## Introduction

JavaScript is an interesting language. It allows you to convert value of one [type] into another. This process of type conversion is called "type coercion", when it is done implicitly. When it is done explicitly, it is called "type casting". This process applies to primitive types such as `number`, `string`, `boolean`, `null`, `undefined` and `Symbol`. It also applies to objects.

When type coercion or type casting happens, the result is always some primitive type, like `string`, `number`, or `boolean`. It will never happen that the result of type coercion, or casting, will be either object or a function.

## Implicit and explicit type coercion

As you know, type coercion refers to implicit type conversion while type casting to explicit. When JavaScript developers talk about type coercion, they usually refer to both types, implicit and explicit. The main difference between these two is that one is usually done on purpose while the other automatically, by the language.

JavaScript as a programming language is weakly and dynamically typed. This means few things. Weakly means you don't have to specify what type some value is before you can use it. For example, you don't have to tell that a function requires string as a parameter or that some variable is, or will be, an integer.

JavaScript allows you to change types as you go. You can declare a variable and assign it a string. Later, you can decide to change it to a number. You can also declare a variable leave it empty and assign it a value later, without specifying its type. This is what it means when some programming language is dynamically typed.

### Implicit coercion

One advantage, or disadvantage, of weakly typed languages is that it allows for implicit type coercion to happen. This usually happens in two situations. The first one is when you use some operator along with two or more different values. Here, JavaScript will take those values and convert them as needed to make that operation happen.

For example, let's say you try to add a string to a number. In this case, JavaScript will take the number, convert it to a string. After that, it will concatenate that converted number, now string, with the string you wanted to add.

```JavaScript
// Implicit conversion of a number to string
13 + '14' // '1314'
123 + '' // '123
7 + ' roses' // '7 roses'
```

Another example can be when you try to compare a number with another number that is defined as a string. In this case, JavaScript will first convert that number defined as a string to a number. After that, it will convert the real number with the converted. The same happens if you try to multiply those numbers.

```JavaScript
// Implicit conversion of a string to number
4 < '5' // true
6 > '15' // false
95 * '15' // 1425
```

The second situation when implicit type coercion happens is when you use `if...else` statement or ternary operator. It doesn't matter what you use as the condition. The result will always be a boolean, either `true` or `false`. This is also why it is important to remember what are [falsy] and [truthy] values in JavaScript.

```JavaScript
// Implicit conversion and truthy and falsy values

// Some truthy values
if (5) true // true
if ('test') true // true
if ({}) true // true
if ([]) true // true


// Some falsy values
'' ? true : false // false
if (!'') true // true
0 ? true : false // false
if (!0) true // true
null ? true : false // false
if (!null) true // true
NaN ? true : false // false
if (!NaN) // true
```

## Explicit coercion

That was about implicit coercion. Now, let's talk about explicit, or type casting. This will be quick. Explicit coercion happens when JavaScript developers decide to convert value from another using specific object or method. For example, you can use `Number()` object to convert some type to a number, or `String()` to a string.

```JavaScript
// Using explicit coercion to convert types to a number
Number('55') // 55
Number('dwarf') // Nan
Number(false) // 0
Number(true) // 1
Number([]) // 1
Number({}) // NaN
Number(null) // 0
Number(undefined) // NaN

// Use explicit coercion to convert types to a string
String(99) // '99'
String(true) // 'true'
String(false) // 'false'
String([]) // ''
String(['one', 'two']) // 'one,two'
String({}) // '[object Object]'
String(Infinity) // Infinity
String(null) // 'null'
String(undefined) // 'undefined'
```

## Conclusion: [...] ...

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[type]: https://blog.alexdevero.com/javascript-basics-data-types-pt1/
[falsy]: https://developer.mozilla.org/en-US/docs/Glossary/Falsy
[truthy]: https://developer.mozilla.org/en-US/docs/Glossary/Truthy

<!--
### Meta:
-
-->

<!--
### Resources:
- https://github.com/getify/You-Dont-Know-JS/blob/1st-ed/types %26 grammar/ch4.md
- https://www.freecodecamp.org/news/js-type-coercion-explained-27ba3d9a2839/
- https://2ality.com/2019/10/type-coercion.html
- https://codeburst.io/javascript-quickie-what-is-type-coercion-74f19df6d16f
- https://levelup.gitconnected.com/javascript-the-weird-parts-part-i-data-types-type-coercion-pbr-3ecc751ad62
- https://exploringjs.com/deep-js/ch_type-coercion.html
- https://hackernoon.com/understanding-js-coercion-ff5684475bfc
- https://developer.mozilla.org/en-US/docs/Glossary/Type_coercion
- https://stackoverflow.com/questions/19915688/what-exactly-is-type-coercion-in-javascript/19915864
- https://www.w3schools.com/js/js_type_conversion.asp
-->
