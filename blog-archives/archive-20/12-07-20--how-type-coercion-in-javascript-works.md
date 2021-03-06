# How Type Coercion in JavaScript Works

In JavaScript, you can convert a value from one type to another. This is called type coercion. Type coercion is one of the topics that can be hard to understand. This tutorial will help you with it. It will show you what it is, how it works, and how to use it to become a better JavaScript developer.

<!-- Type coercion in Javascript Explained -->
<!--more-->
<!--
Table of Contents:
## Introduction
## Implicit and explicit type coercion
### Implicit coercion
## Explicit coercion
## Three types of type Coercion
### Coercion to number
### Coercion to string
### Coercion to boolean
## Strict and loose equality
## Conclusion: How Type Coercion in JavaScript Works
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

That was about implicit coercion. Now, let's talk about explicit, or type casting. This will be quick. Explicit coercion happens when JavaScript developers decide to convert value from another using specific function. For example, you can use `Number()` function to convert some type to a number, or `String()` to a string.

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
String(Infinity) // 'Infinity'
String(null) // 'null'
String(undefined) // 'undefined'
```

## Three types of type Coercion

In JavaScript, there are only three types of type conversion. These conversion types are to number, to string and to boolean. Let's take a look at each.

### Coercion to number

Explicit conversion, or type casting, to a type of number is simple and can be done quickly. The easiest way to do this is by using the `Number()` function. Implicit, or type coercion, is more tricky. There are multiple ways in which it can be triggered. The first one are comparison operators, the `>`, `<`, `<=` and `>=`.

When you use any of these operators JavaScript will automatically coerce the values you used with one of these operators to number. Implicit coercion to number will also happen when you use bitwise operators, the `|`, `&`, `^` and `~`. It will also happen if you use arithmetic operators, the `-`, `+`, `*`, `/` and `%`.

One exception here is the binary `+` operator. This operator will not trigger coercion to number if any of the values is type of a string. What will happen instead is coercion to a string. Lastly, implicit coercion will happen if you use the loose equality operator `==`. This also includes the loose not equal `!=`.

Another exception here. JavaScript will not do implicit coercion to a number if you use `==` or `!=` and both values are strings. This probably makes sense, but it is still worth mentioning, just in case. One last thing about coercion to number. When you want to convert a string to a number, JavaScript will first remove any leading and trailing white space.

JavaScript will also remove any new line (`\n`) and tab (`\t`) characters in the string. If the remaining string doesn't contain a valid number it will be coerced to `NaN`. Otherwise, it will be coerced into a number. If the remaining string will be empty it will be coerced to 0. This will also happen with `null`.

```JavaScript
// Implicit coercion to number
7 > '10' // false => becomes: 7 > 10
+'88' // becomes 88
65 != '56' // true, => becomes: 65 != 56
15 / null // infinity
false | 0 // 0


// Explicit coercion to number
Number('678') // 678
Number('13m') // NaN
Number(' 51 ') // 51
Number('-65.9') // -65.9
Number('\n') // 0
Number('\n13') // 13
Number('\t') // 0
Number('\t695') // 695
Number([]) // 0
Number(null) // 0
Number(undefined) // NaN
```

### Coercion to string

Explicit coercion to a string is just as easy as coercion to a number. All you have to do is use `String()` function. Implicit coercion to a string is just as easy. When you want to trigger implicit coercion you have to use the binary `+` operator, along with at least one string.

```JavaScript
// Implicit coercion to string
56 + ' words' // '56 words'
'number ' + 17 // 'number 17'
7 + ' dwarfs and ' + 1 + ' Snow White' // '7 dwarfs and 1 Snow White'
'' + 15 // '15'


// Explicit coercion to string
String(true) // 'true'
String(false) // 'false'
String(15.5) // '15.5'
String(-650) // '-650'
String(Infinity) // 'Infinity'
String([]) // ''
String(['Jacket', 15]) // 'Jacket,15'
String(null) // 'null'
String(undefined) // 'undefined'
String({}) // '[object Object]'
```

Aside to the `String()` there is also `toString()` method. This method also allows you to coerce various types to strings. You can use this method with numbers, booleans, arrays, objects, dates and also Symbols. Don't use it with `null` or `undefined`. If you want to use it to convert a number, or an object, you have to wrap it with parentheses to avoid syntax errors.

One more thing for numbers. You can also specify radix parameter. The method will then convert the number to the base according to the radix parameter and then into a string.

```JavaScript
// Coercing types to string with toString() method
58.toString() // SyntaxError: Identifier directly after number
(58).toString() // '58'
true.toString() // 'true'
false.toString() // 'false'
['JS', 'TS'].toString() // 'JS,TS'
undefined.toString() // TypeError: Cannot read property 'toString' of undefined
null.toString() // TypeError: Cannot read property 'toString' of null
({name: 'Joe'}).toString() // '[object Object]'
Symbol('name').toString() // 'Symbol(name)'


// Using toString() with radix parameter
(15).toString(2) // '1111'
(15).toString(8) // '30'
(15).toString(16) // 'f'
```

### Coercion to boolean

When you want to explicitly convert something in boolean you can do that with `Boolean()` function. Implicit coercion will happen in two situations. The first situations is a logical context. For example, inside the `if...else` statement. The second situation is when you use one of the logical operators, the `||`, `&&` or `!`.

```JavaScript
// Implicit coercion to boolean

if (0) {/* Do something */} // logical context
!!7 // true
99 || 'JS' // 99
!!0 // false (0 is falsy value)
!!'' // false (empty string is falsy value)
!!null // false (null is falsy value)
!!undefined // false (null is falsy value)

// Explicit coercion to boolean
Boolean(15) // true
Boolean(-15) // true
Boolean('') // false
Boolean('Syntax') // true
Boolean(true) // true
Boolean(0) // false
Boolean(-0) // false
Boolean(Infinity) // true
Boolean(-Infinity) // true
Boolean(null) // false
Boolean(undefined) // false
Boolean(NaN) // false
Boolean([]) // true
Boolean({}) // true
Boolean(Symbol()) // true
Boolean(function() {}) // true
```

## Strict and loose equality

One topic related to type coercion is equality. In JavaScript, there are two types of eventuality. The first one is loose equality, either `==` or `!=`. The second one is strict equality, either `===` or `!==`. The difference between those is that one allows for type coercion to happen while the other doesn't.

The first one, loose equality, is the one that allows for type coercion to happen. When you use loose equality to check if some values are equal, JavaScript will do two things. First, it will check if the two values are the same type. If not, it will coerce one into another. Then, it will check if those values are the same.

When you use strict equality, JavaScript will not try to coerce one value into another. Instead, it will do two checks. First, it will check if those values are the same. Second, it will check if their types are the same. Only if both conditions are true, the result will be `true`. Otherwise, the result will be `false`.

```JavaScript
// Loose equality and coercion
0 == false // true (0 is falsy value) - coerced to false == false
0 == true // false - coerced to false == false
1 == true // true (1 is truthy value) - coerced to true == true
1 == false // false - coerced to true == false
'15' == 15 // true - coerced to '15' == '15'
15 == '15' // true - coerced to '15' == '15'
null == undefined // true - coerced to false == false
undefined == null // true - coerced to false == false


// Strict equality and coercion
0 === false // false - number is not a boolean
0 === true // false - number is not a boolean
1 === true // false - number is not a boolean
1 === false // false - number is not a boolean
'15' === 15 // false - string is not a number
15 === '15' // false - number is not a string
null === undefined // false - null is not undefined
undefined === null // false - undefined is not null
```

As you can see, loose equality can lead to results you might not expect. The best way to avoid this, and also to create more reliable equality checks, is to use strict equal. With strict equal, JavaScript will not be able to use type coercion. It will also always compare the types of values, instead of only the values.

## Conclusion: How Type Coercion in JavaScript Works

Type coercion in JavaScript is one of the topics that can be tricky. It is also one of the topics every JavaScript developer has to learn and understand. I hope this tutorial made this easier. I hope it helped you understand what type coercion in JavaScript is and how it works. I also hope it showed you how to use it to your advantage.

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
-
-->
