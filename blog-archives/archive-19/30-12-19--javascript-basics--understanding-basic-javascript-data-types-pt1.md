# JavaScript Basics - Understanding Basic JavaScript Data Types Pt.1
Data types are one of the things every JavaScript developer, and web developer, should know. This article will help you learn all you need to know about the first two, strings and numbers. It will help you understand how these data types work and how you can use them.<!--more-->
<!--
Table of Contents:
## Data types
### Strings
#### Length, characters, and cases
#### Searching strings
#### Getting a substring
#### Template literals
#### From string to number
### Strings... arrays?
### Numbers
#### From number to string
#### Doing some Math
#### Testing for integers and floats
#### One gotcha
## Conclusion: Understanding Basic JavaScript Data Types
-->

## Data types

Data types are fundamental blocks of every programming language. Data types are basically a classification, or an attribute, that says what kind of data specific value can have. In some cases, this applies not only to values but also to variables. In JavaScript, there are currently eight data types. Let's take a look at each.

### Strings

The first of data types is a `string`. It is also one of the most commonly used data types. A string is something surrounded by either single or double quotes. Between the quotes can be almost anything, characters, numbers, etc. In some sense, string can contain any other data types.

```js
// Single-quote string
let a = 'Some sentence.'
let a2 = 'Year 2020.'

// Double-quote string
let b = "notes"
let b2 = "Wait for 1984."

// Also valid strings
let c = ''
let d = ""
```

Whatever is there between the quotes, JavaScript will treat it as a piece of text. This also applies to quotes themselves. If you create a string with single quotes you can use single quote characters inside the string only if you escape it with slash (`\'` or (`\"`)). Otherwise, JavaScript will think that quote ends the string.

```js
// This is safe - using different strings
let a = "We're coding something."

// This is safe - correctly escaped string
let b = 'You\'re doing well.'
let c = "He said, \"this will be fun\", few hours later."

// This is NOT safe - using the same, unescaped, strings
let d = 'You're break this string.'
let e = "Citation says, "it will break", and I agree."
```

You can also add (or concatenate) two or more strings together. In this case, it doesn't matter if one string uses single quotes and the other(s) double. This is also useful when you want to include some expression in that string.

```js
// Concatenating strings
let a = 'Some '
let b = "string"
let c = ' to be '
let d = "added."
let e = a + b + c + d
e // 'Some string to be added.'


// or
let f = 'Some ' + "string" + ' to be ' +  "added."
f // 'Some string to bea dded.'


// Including variable in a string
let age = 13
let message = 'This is ' + age + ' years old.'
message // 'This is 13 years old.'

// or
let message2 = 'This is ' + 13 + ' years old.'
message2 // 'This is 13 years old.'
```

#### Length, characters, and cases

Now, what are some things you can do with data types such as `strings`? When you want to check the size of the `string`, you can use `length` property. When you want to access some character, based on its index, you can use `charAt()` method. For changing the case, there are `toLowerCase()` and `toUpperCase()` methods.

```js
// Checking the size of a string
let a = 'This is around 29 characters.'
a.length // 29

// or
'This is around 29 characters.'.length // 29


// Accessing character
let b = 'Makes sense.'
b.charAt(7) // 'e'

// or
'Makes sense.'.charAt(7) // 'e'

// Changing case
let c = 'Something is happening.'
c.toUpperCase() // 'SOMETHING IS HAPPENING.'
c.toLowerCase() // 'something is happening.'

// or
'Something is happening.'.toUpperCase() // 'SOMETHING IS HAPPENING.'
'Something is happening.'.toLowerCase() // 'something is happening.'
```

#### Searching strings

You can also search for a substring in a `string`, or a piece of that string, using `indexOf()` method. This method will return the index at which the first occurrence of the substring begins. If it doesn't exist, it will return `-1`. You can also add optional parameter to specify the index at which the method should begin its search.

Alternative to `indexOf()` is `lastIndexOf()`. While the `indexOf()` starts at the beginning and go to the end, the `lastIndexOf()` starts at the end and goes to the beginning. Remember that both, `indexOf()` and `lastIndexOf()`, will return index of only the first occurrence of the string you are looking for.

```js
let a = 'Something to be found.'

// Using indexOf()
a.indexOf('be') // 13

a.indexOf('hoax') // -1 - not found

a.indexOf('e') // 3

// Start from index 8 (7th letter)
a.indexOf('e', 8) // 14


// Using LastIndexOf()
let b = 'Welcome to the Paradise'
b.lastIndexOf('a') // 18

// Start from index 17 (18th letter) and move to the beginning
b.lastIndexOf('a', 17) // 16
```

Another options for searching strings are `includes()`, `startsWith()` and `endsWith()` methods. The names of these methods say pretty much everything you need to know about how they work. The `includes()` returns `true` if string includes the substring you are looking for. The `startsWith()` returns `true` if it starts with the substring.

The last one, `endsWith()`, returns `true` if the string ends with the substring. Remember that all these methods, including the `indexOf()` and `lastIndexOf()` are case sensitive. So, pay attention to use the correct case for all characters of the substring you are looking for.

```js
let x = 'There will be dragons!'

// includes()
x.includes('will') // true
x.includes('Be') // false

// startsWith()
x.startsWith('There') // true
x.startsWith('Is') // false

// endsWith()
x.endsWith('!') // true
x.endsWith('.') // false
```

#### Getting a substring

When you want to get a substring of a string, based on index, you can use `substring`, `substr` or `slice`. The `substring` returns a substring between the start and end indices. The `slice` returns a substring from start to end, not including the end index. Lastly, the `substr` returns a substring, from start, of a length you specified.

The last one, `substr`, is not recommended to be used. It is still in JavaScript mainly for historical reasons. Out of these three, the best choice is probably the `substring` since you don't have to remember that it indeed includes the end index in the substring.

```js
let a = 'Hello from JavaScript.'

// substring - get substring starting on 5th index
// and ending on 12th index
a.substring(5, 12) // ' from J'

// slice - get substring starting on 4th index
// and ending on 9th index (including the 9th index, or 8th character)
a.slice(4, 10) // 'o from'

// substr - get substring starting on 3rd index,
// 7 characters long
a.substr(3, 7) // 'lo from'
```

#### Template literals

When you want to include some JavaScript expression in a string, you don't have to add strings. There is a better, faster and cleaner way to do this since the release of ES2015. It is called [template literals], or template strings. Template literals are very similar to strings. However, they are much more powerful.

With string literals you can embed expressions and even unicode codes and hexadecimal and octal literal in the string. You can also use create multi-line strings without the need to use special line-break characters. Template literal is created by using back-tick characters (` `), instead of quotes.

When you want to include some expression, you wrap the expression with `${}`, or `${some code}`. When you want to create multi-line string, just hit enter key when you need it. It looks almost like magic. Under the hood is JavaScript joining things, such as strings and variables and expressions, and returning strings.

```js
// Using template literal as a string
let a = `Some text`
a // 'Some text'


// Embedding variable inside template literal
let name = 'Joe'
let b = `This is ${name} calling.`
b // 'This is Joe calling.'


// Embedding expression inside template literal
let c = `The answer is ${7 * 9 / 2}.`
c // 'The answer is 31.5.'


// Multi-line text with template literal
let d = `Todo:
- write code
- write more code
- write even more code
`
d
// `Todo:
// - write code
// - write more code
// - write even more code
// `

// with regular string
let e = 'Todo:\n- write code\n- write more code\n- write even more code'
e
// 'Todo
// - write code
// - write more code
// - write even more code'


// Template literal is technically still a string
`Is it?` === 'Is it?' // true
```

#### From string to number

Numbers and strings are two different data types. However, that doesn't mean you can't play around with these data types. For example, by changing one into another. In JavaScript, there are built-in methods that will help you "convert" these data types. When you want to convert some `string` that contains number into a `number` there are some ways to do it.

First, you can use `parseInt()`. This will convert the `string` into an integer. On the other hand, `parseFloat()` will convert the `string` into a float (decimal). Next, you can use methods provided by `Math` object, such as `floor()`, `round()` and `ceil()`. All these method accept number in the form of a `string` and return an integer.

The downside of these three is that it will round the number. If you have a decimal and it in that form, these three may not be as useful. Lastly, you can also use [unary operator] and multiplying the `string` by 1. Or, you can simply use `Number` object.

```js
// Using parseInt()
let a = parseInt('156')
typeof a // 'number'
a // 156


// Using parseFloat()
let b = parseFloat('6.18')
typeof b // 'number'
b // 6.18


// Using Math.floor()
let c = Math.floor('5.16')
typeof c // 'number'
c // 5

// Using Math.round()
let d = Math.round('98')
typeof d // 'number'
d // 98

// Using Math.ceil()
let e = Math.ceil('91.3')
typeof e // 'number'
e // 92


// Using unary operator
let f = '216'
f = +f // <= the magic (+)
typeof f // 'number'
f // 216

// or
+'59' // 59, number


// Using multiplication by 1
let g = '980'
g = g * 1 // 'number'
typeof g // 980
g // 980

// or
'15' * 1 // 15, number


// Using Number object
let g = new Number('918.85')
typeof g // object - correct (Number is object)
g // {918.85}
```

One thing to remember for `parseInt()` and `parseFloat()`. When you convert string to number, and that string contains some non-numerical characters, JavaScript will remove them. It will return only the integer or float.The `floor()`, `round()` and `ceil()` will not work at all. JavaScript will return `NaN`.

The same applies to unary operator, multiplication by 1 and `Number` object. All these will `NaN`. So, if you want to convert a string with numbers, and it contains non-numerical characters, use either `parseInt()` and `parseFloat()`. Otherwise, modify the `string`.

```js
// This will work
let a = parseInt('1 world')
a // 1

let b = parseFloat('15.8 hours on wheels')
b // 15.8


// This will not work
let c = Math.floor('15.8 hours on wheels')
c // NaN

let d = Math.round('15.8 hours on wheels')
d // NaN

let e = Math.ceil('15.8 hours on wheels')
e // NaN

+'15.8 hours on wheels' // NaN

'15.8 hours on wheels' * 1 // NaN
```

### Strings... arrays?

In some languages, such as C, strings are thought of as `arrays` of characters. This is not exactly true in JavaScript. In JavaScript, `strings` and `arrays` might be similar, but they are not the same. For example, both, `strings` and `arrays` have `length` property, `indexOf()` and even `concat()` methods.

Both, `strings` and `arrays`, also work with indices. In case of `strings`, this was not always the case. For `strings`, it is better to use `charAt()` method. Another difference is that `strings` are immutable while `arrays` are mutable. Meaning, you can change the value of an array "in-place".

In case of `strings`, you have to create new `string`, modify it and then return it. So, no `strings` are not just `arrays` of characters. Although similar in many ways, there are differences between `strings` and `arrays`.

```js
// String are immutable and can't be changed in-place
// This doesn't work
let a = 'something'

// Try to change the original string
a.toUpperCase() // 'SOMETHING'

// Check the original array
a // 'something'


// This also doesn't work
let x = 'twenty'
let y = x.toUpperCase()

x === y // false
x // 'twenty'
y // 'TWENTY'


// Neither this
let r = 'text'
r[2] = '2' // TypeError: Cannot assign to read only property '2' of string 'text'
r


// This will work
let a = 'something'

// Create new string, modify it,
// return it and assign it to a
a = a.toUpperCase() // 'SOMETHING'

// Check the original array
a // 'SOMETHING'


// Arrays are mutable - can be changed in place
// This will work
let arr = [1, 2, 3]

// Add and remove items
arr.push(4) // [ 1, 2, 3, 4 ]
arr.shift() // 1

// Check the original array
arr // [ 2, 3, 4 ]


// This will work
let arr2 = [false, false, false]
arr2[1] = true
arr2 // [ false, true, false ]


// Accessing characters - string
let a = 'World'

// using charAt() method
a.charAt(3) // // 'l'

// Using index also works
a[3] // 'l'

// Accessing characters - array and index
let b = ['w', 'x', 'y', 'z']
b[3] // 'z'
```

`Strings` might belong to basic data types. However, that doesn't change the fact that they can be quite powerful. If you want to learn about more other methods you can use with `string`, take a look at the documentation at [MDN]. Here, you will find a lot of things to learn and try, not just about `strings`, but about other data types as well.

### Numbers

Next is a `number`. This is another of wildly used data types. In JavaScript, the `number` type represents both kinds of numbers, integers and floating point numbers. In other languages, such as C, there are multiple types for numbers, integers, shorts, longs, floats, doubles, etc. This makes working with numbers in JavaScript much easier.

In general, number are in JavaScript expressed as base-10 decimals. When you define some number with a leading zero, i.e. floating point number smaller than zero, the leading zero is optional. The same applies to trailing zero. It is also optional.

You can also end the floating point number with the floating point. However, this is neither recommended nor a good practice as it can confuse some people reading your code, even you yourself. There is one interesting thing in JavaScript. You can shorten the number by appending letter "e" to the number and specifying the zeroes count.

You can use the same also for decimal numbers. In this case, you need to add minus "-" after the letter "e" and specify the number of zeros. This includes the zero before the floating point.

```js
// integer
let x = 15

// float
let y = 89.3

// float with leading 0(s) (optional)
let y = 0.72
let o = 00000000.72

// the same as - float without leading 0(s)
let w = .72

// float with trailing 0(s) (optional)
let q = 82.230000
let s = 82.230

// the same as - float without trailing 0(s)
let p = 82.23


// hexadecimal number
let i = 0xf00d


// binary number
let f = 0b111110111


// octal number
let g = 0o767


// also valid, float ending with floating point '.'
let u = 78.


// Shortening a positive number
let a = 8000000000
// is the same as
let b = 8e9
// test
a === b // true

// or
let c = 987500000
// is the same as
let d = 9875e5
// test
c === d // true


// Shortening a decimal number
let e = 0.00000002
// is the same as
let f = 2e-8
// test
e === f // true


// also valid float - float ending with floating point '.'
let u = 78.
```

#### From number to string

As you know, it is possible to "switch" between data types. Or, to convert one data type to another. When you've learned about `strings`, you've learned how to convert strings to numbers. Now, let's take a look at how to convert numbers to strings.

There are at least four ways to do that. The first one is using `.toString()` method. The benefit of using this method is that you can also specify which [base] it should use to represent that number. The second option is using `String()` object.

Third option is using template literals you learned about above, in the section about `strings`. The fourth and last option is concatenating the number with an empty string.

```js
let a = 56

// Using .toString()
a.toString() // '56'

// or
935 .toString() // '935', note: the space between number and '.' is necessary

13.8 .toString() // '13.8', note: the space between number and '.' is necessary

(935).toString() // '935', note: or use parenthesis

(13.8).toString() // '13.8', note: or use parenthesis

// using radix to specify base
(935).toString(2) // '1110100111'


// Using String()
String(a) // '56'

// or
String(890) // '890'


// Using template literals
let str = `${a}` // '56'

let str2 = `${3.589}` // '3.589'


// Concatenating the number with an empty string
let b = '' + 659 // '659'
let c = 9863 + '' // '9863'
```

#### Doing some Math

Every number supports standard arithmetic operations, such as addition (`+`), subtraction (`-`), multiplication (`*`), division (`/`), remainder (`%`) and exponentiation (`**`). The `numbers` data type also includes hexadecimal and decimal literals as well as binary and octal literals. These were introduced later in ECMAScript 2015.

In addition to these, `number` also includes special numeric values such as `Infinity`, `-Infinity` and `NaN`. The `Infinity` is the same infinity you know from [Mathematics]. The `NaN` stands for a computational error. You will encounter it when you try to do some incorrect or an undefined mathematical operation.

When you need to perform rounding operations, there is the previously mentioned `Math` object with `floor()`, `round()` and `ceil()` methods. The `floor()` always rounds numbers down. Tip to remember: floor is down. The `ceil()` always rounds numbers up. Tip to remember, ceil(ing) is up. The last, `round()`, rounds to the nearest integer.

Aside to these, there is also `toFixed()` method. This method rounds the number to number of digits you specify inside the parenthesis. The number of digits refers to digits after the floating point. One thing to keep in mind. The `toFixed()` method return `string`, not `number`.

```js
// arithmetic operations
// addition
85 + 15 // 100

// subtraction
65 - 12 // 53

// multiplication
78 * 2236 // 174,408

// division
953 / 3 // 317.6666666667

// remainder
92 % 5 // 2

// exponentiation
5 ** 6 // 15625


// Rounding
Math.floor(3.89) // 3
Math.floor(-3.89) // -4

Math.round(4.5) // 5
Math.round(-4.5) // -4

Math.ceil(36.2) // 37
Math.ceil(-36.2) // -36


// toFixed
8.95932791.toFixed(3) // '8.959'

let a = 698.232657891.toFixed(5)
typeof a // 'string'
a // '698.23266'
```

#### Testing for integers and floats

There are a couple of ways to test if some number, or anything, is an integer or a float. In case of integer, the best approach is using `Number` object and its `isInteger()` method. Another option is `isSafeInteger()`. This method will check if the provided value is a number that is a safe integer.

```js
// test for integer
Number.isInteger(50) // true

Number.isInteger(-900) // true

Number.isInteger(75.0) // true

Number.isInteger(0.75) // false

Number.isInteger(Infinity) // false

Number.isInteger(NaN) // false

Number.isInteger(true) // false

Number.isInteger('hello') // false
```

Testing for floats is not that straightforward. There is no built-in way to test for this type of number. Here are two quick ways you can test for floats.

```js
// No.1
someNumber !== parseInt(someNumber)

5 !== parseInt(5) // false - is not a float
3.14 !== parseInt(3.14) // true - is a float

// No.2
Math.ceil(parseFloat(someNumber)) !== someNumber

Math.ceil(parseFloat(87)) !== 87 // false - is not a float
Math.ceil(parseFloat(92.11)) !== 92.11 // true - is a float
```

#### One gotcha

There are some gotchas even in data types. The `number` data type, especially floats are a good example. This is not true only for JavaScript, but also for other programming languages. The problem is that not all decimal representations are exact. So, when you try to compare them, they will not be equal.

```js
// Gotcha with decimals
0.4 + 0.2 === 0.6 // false?

// What is the result of this?
0.4 + 0.2 // 0.6000000000000001
// hence 0.6 !== 0.6000000000000001
```

## Conclusion: Understanding Basic JavaScript Data Types

This is all for this part. In a recap, today, you've learned about the two first JavaScript data types, namely, strings and numbers. You've learned how these two data types work and how you can use them. Now, take some time to review and practice what you've learned here. Doing so will help you remember it better.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Mathematics]: https://en.wikipedia.org/wiki/Infinity
[template literals]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals
[MDN]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String
[unary operator]: https://scotch.io/tutorials/javascript-unary-operators-simple-and-useful
[base]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toString

<!--
#### Meta:
-
-->
