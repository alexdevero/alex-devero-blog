# ES6, ES7, ES8 & Writing Modern JavaScript Pt3 - Spread, Rest, Sets & Object Literal

ES6 brought many great features into JavaScript. In this part, you will learn about four of them, spread operator, rest parameter, sets and object literal. Understand what these features do and how to work with them so you can start using them in your projects with absolute confidence.

<!--
Table of Contents:
## Spread operator
## Rest parameter
## Sets
## Object literal
## Epilogue: ES6, ES7, ES8 & Writing Modern JavaScript Pt3
-->

ES6, ES7, ES8 & Writing Modern JavaScript [Part 1] (Scope, let, const, var).

ES6, ES7, ES8 & Writing Modern JavaScript [Part 2] (Template literals, Destructuring & Default Params).

## Spread operator

One small and handy goodie provided by ES6 specification of ECMAScript is spread operator. This feature allows you to take the content of objects such as array or object literal and copy it without using any arguments. Spread operator can be very useful, for example, when you don't know the concrete number of elements inside the array or object literal.

With spread operator, this doesn't matter. You don't need to use things such as loops or `length` and `size` properties to know the number of items, or properties. All you have to do is to use spread operator syntax and let JavaScript do the work for you. Another good use case for this ES6 feature is cloning arrays and objects. Cloning with spread operator is quick and simple (code example no.2 & no.4).

Spread operator also comes in handy when you want to concatenate arrays or object literals, and save the result into a new one (code example no.3 and no.5). Luckily, the syntax of spread operator is simple, unlike of some other features of ES6. It consists of three dots and the name of the variable you want to use, i.e.: the array or object literal, (`...variableName`).

One thing you should know about. You can use spread operator as many times as you want. Meaning, when you use it to pass arguments, concatenate arrays or anything else. There is no limit imposed by ES6 by default. Just remember to use commas to separate the operators.

```
///
// Spread example no.1: Array and printing the content
const arrOne = [5, 6, 'Josh', 'Tanner', 'Sweeney']

console.log(...arrOne)
// Outputs:
// 5
// 6
// 'Josh'
// 'Tanner'
// 'Sweeney'


///
// Spread example no.2: Array and cloning
const arrOne = [5, 6, 'Josh', 'Tanner', 'Sweeney']

const arrTwo = [...arrOne]

console.log(...arrTwo)
// Outputs:
// 5
// 6
// 'Josh'
// 'Tanner'
// 'Sweeney'


///
// Spread example no.3: Arrays and concatenating
const arrayOne = ['Hello.', 'This', 'could']
const arrayTwo = ['actually', 'work', 'in']
const arrayThree = ['the', 'end', '.']

// Concatenate arrays using spread operator
const arrayFour = [...arrayOne, ...arrayTwo, ...arrayThree]

console.log(arrayFour)
// Outputs:
// ["Hello.", "This", "could", "actually", "work", "in", "the", "end", "."]


///
// Spread example no.4: Objects and cloning
const objOne = {
  firstName: 'Stuart',
  lastName: 'Little',
  age: 11
}

// Create a clone of objOne
const objTwo = {...objOne}

console.log(objTwo)
// Outputs:
// [object Object] {
//   age: 11,
//   firstName: 'Stuart',
//   lastName: 'Little'
// }


///
// Spread example no.5: Objects and concatenating
const objOne = {
  firstName: 'Stuart'
}
const objTwo = {
  lastName: 'Little'
}
const objThree = {
  age: 11
}

// Create a clone of objOne
const objFour = {...objOne, ...objTwo, ...objThree}

console.log(objFour)
// Outputs:
// [object Object] {
//   age: 11,
//   firstName: 'Stuart',
//   lastName: 'Little'
// }

console.log(objTwo)
// Outputs:
// [object Object] {
//   age: 11,
//   firstName: 'Stuart',
//   lastName: 'Little'
// }

///
// Spread example no.6: Function and spread operator as an argument
const arrayOfNumbers = [8, 15, 99, 3523, 65]

function count(...numbers) {
  // Add all numbers inside the array and save the result in new variable
  const result = numbers.reduce((x, y) => x + y)

  console.log(result)
}

// Pass arrayOfNumbers using spread operator
count(...arrayOfNumbers)
// Outputs:
// 3710
```

## Rest parameter

The rest parameter looks and works similar to the previous ES6 feature spread operator. The difference is that you can use rest parameter, as the name suggests, only for function parameters. Rest will not work if you want to do operations such as cloning or concatenating arrays or object literals. Or viewing the content of these objects. However, the syntax is the same.

One useful thing you should know. Rest operator returns an array. This means that you can use indexes to access and use specific item inside the array, instead of all items. Since array is iterable object, it also means that you can use loops, `map` and `forEach` to iterate over it and work with its content. You can also use array methods such as `sort`, `pop`, etc.

```
///
// Rest example no.1:
// The ...words is the rest parameter.
function printAll(wordA, wordB, ...words) {
  console.log(wordA)
  console.log(wordB)
  console.log(words)
}

printAll('Hello', 'Smack', 'Dine', 'Work', 'Truth', 'Simplify', 'Future')
// Outputs:
// "Hello"
// "Smack"
// ["Dine", "Work", "Truth", "Simplify", "Future"]


///
// Rest example no.2: Rest parameter, array and map
function mapIt(wordA, wordB, ...words) {
  words.map((word) => console.log(word))
}

mapIt('Truth', 'Simplify', 'Future', 'Gang', 'China')
// Outputs:
// 'Future'
// 'Gang'
// 'China'


///
// Rest example no.3: Rest parameter, array and forEach
function useForEach(wordA, wordB, ...words) {
  words.forEach((word, index) => {
    console.log(`Word on index ${index} is ${word}.`)
  })
}

useForEach('Hello', 'Smack', 'Dine', 'Work', 'Future')
// Outputs:
// 'Word on index 0 is Dine.'
// 'Word on index 1 is Work.'
// 'Word on index 2 is Future.'


///
// Rest example no.4: Rest parameter, array and indexes
function restIndex(wordA, wordB, ...words) {
  console.log(words[0])
  console.log(words[1])
  console.log(words[4])
}

restIndex('Hello', 'Smack', 'Dine', 'Work', 'Truth', 'Simplify', 'Future')
// Outputs:
// 'Dine' - 1st element of words array (index 0)
// 'Work' - 2nd element of words array (index 1)
// 'Future' - 5th element of words array (index 4)


///
// Rest example no.5: Rest and spread
function restSpread(...params) {
  const arrayOfParameters = [...params]

  console.log(arrayOfParameters)
}

restSpread('Wayne', 'Stark', 'Woody', 'Storm')
// Outputs:
// ['Wayne', 'Stark', 'Woody', 'Storm']
```

## Sets

Sets are one of the less known features of ES6. While JavaScript developers talk a lot about many ES6 feature sets are almost ignored. This is almost sad because sets can be quite useful. Sets can help you easily solve some problems with a one-liner, problems that would otherwise require several lines of code.

Sets are look very similar to array. However, there is something special that makes them different. Like arrays, you can use sets to store values of any type, such as numbers, strings, booleans, etc. Unlike arrays, you can create a set only with Set constructor (`new Set()`). Also, sets can't contain duplicate values. Every value in a set must be unique.

What if you create a set and try to fill it with values, some of them being the same? JavaScript will add only the first instance of the value into the set. It will basically ignore all other duplicates. This can be very useful. Imagine you have a number of strings or numbers and you want to filter all duplicates.

You would have to write a custom short function to handle this. Or, you could use `array` along with `filter` method. After the release of ES6, you can simply add all those values into a set and let JavaScript automatically filter any duplicate values. This is the one-liner solution for some problems I mentioned above.

As I already mentioned, when you want to create a new set, you need to use set constructor. And, you must wrap all values you want to store in the set in square brackets, or you must put them inside an array (`new Set([value])`). This is one way. The second way is to create an empty set, use `new Set()` and then add values with `add()`.

The `add()` method is like an alternative to `push()` you would use in case of an array. So far, there is no other way to create sets in JavaScript that would not require you to use the set constructor. Maybe this will change with some future update. When you want to delete value from set, use `delete()` with the value inside the brackets.

ES6 also has method for removing all values from the set. You can achieve that using `clear()` method. Remember that when you use `clear()` the set as such will still exist. Only its content will be removed. You test this checking the `size` property of the set. It will return "0". There are few more things you need to know about sets.

Yes, they are very similar to arrays. However, you can't check for `length` or use `map`, as you can with arrays, when you work with sets. In case of sets, you can get the number of items with `size`. And when you want to iterate over the set you can use `forEach()` method.

```
///
// Set example no.1: Empty set and add()
const setExample = new Set()

// Add values to setExample set
setExample.add(5)
setExample.add('JavaScript')
setExample.add(true)
setExample.add('JavaScript') // Notice duplicate value
setExample.add('JavaScript') // Notice another duplicate value

// Iterate over the set and print its content
// Notice that there will be only one 'JavaScript' item
setExample.forEach(item => console.log(item))
// Outputs:
// 5
// 'JavaScript'
// true


///
// Set example no.2: Set initialized with values
const setExample = new Set([false, 13, 'string', {name: 'Tom', surname: 'Dextro', age: 29}])

// Iterate over the set and print its content
setExample.forEach(item => console.log(item))
// Outputs
// false
// 13
// 'string'
// [object Object] {
//   age: 29,
//   name: 'Tom',
//   surname: 'Dextro'
// }


///
// Set example no.3: Deleting individual values
const setExample = new Set([1, 5, 'thirteen', 'five'])

// Delete value 'thirteen'
setExample.delete('thirteen')

// Iterate over the set and print its content
setExample.forEach(item => console.log(item))
// Outputs:
// 1
// 5
// 'five'


///
// Set example no.4: Deleting all values
const setExample = new Set(['JavaScript', 'Ruby', 'Python', 'PHP'])

// Delete all values in the set
setExample.clear()

console.log(setExample.size)
// Outputs:
// 0
```

## Object literal

One of the ES6 features you may start using a lot is an object literal. Object literal is a list of name-value pairs separated by commas and wrapped in curly braces. It looks very similar to the JSON object. Just like with the JSON object, the usual use case for object literals is to encapsulate some data. These data can be any data types.

Object literal can store numbers, strings, arrays, functions and also nested object literals. This makes them very useful. For example, they can help you reduce the number of variables and keep your code more concise. You don't need to create variables for every piece of data. Instead, you can create one object literal, and store all the data inside it.

You can use variables names is the object literal keys and the data as values of these keys. The result will be one small and well-arranged package of data instead of multiple variables. Combine this with another two ES6 features, imports and exports, and you have a simple way to share big chunks of data across your code base.

As I mentioned, the syntax of object literal is very similar to JSON object. Object literal contains data in the form of key/value pairs. Every key and value is separated by a colon (`:`). Multiple key/value pairs are separated by comma.

Unlike sets, you don't have to use any constructor to create new object literal. You can either create it empty using `{}`, similar to creating an array, or initialize it with values (key/value pairs) `{key: value}`. You can add, modify or access the data inside the literal using either dot syntax `objLit.key` or square bracket syntax `objLit[key]`.

Which syntax will you use will depend on two conditions. First, if you want to add a multi-word key that contains space, or some special characters, you will have to use square bracket syntax `objLit['some multi-word value']`. Another use case for square bracket syntax is when the key is a variable.

For example, if you pass it as an argument to a function, access it in a loop you want to evaluate it as an expression. If none of these applies, you can safely use dot syntax. The second condition is your personal preference. What syntax to choose depends purely on your personal taste.

```
///
// Object literal example no.1: Stating with empty object literal
const objLitExample = {}

// Add pairs to objLitExample
objLitExample.one = 'First pair'
objLitExample.two = 'Second pair'
objLitExample.foo = 13

// Print the content of objLitExample
console.log(objLitExample)
// Outputs:
// [object Object] {
//   foo: 13,
//   one: 'First pair',
//   two: 'Second pair'
// }


///
// Object literal example no.2: Initialize object literal with values
const objLitExample = {
  one: 'First pair',
  two: 'Second pair',
  foo: 13
}

// Add another pair
objLitExample.bar = 'This is additional pair'

// Print the value of name key
console.log(objLitExample)
// Outputs:
// [object Object] {
//   bar: 'This is additional pair',
//   foo: 13,
//   one: 'First pair',
//   two: 'Second pair'
// }


///
// Object literal example no.3: Object literal and changing values
const objLitExample = {
  name: 'Don'
}

// Change the value of name key
objLitExample.name = 'Struck'

// Print the value of name key
console.log(objLitExample.name)
// 'Struck'

///
// Object literal example no.4: Object literal and key with space
const objLitExample = {}

// Add pairs to objLitExample
objLitExample['first name'] = 'John'
objLitExample['last name'] = 'Doer'

// Access the values
console.log(objLitExample['first name']) // 'John'
console.log(objLitExample['last name']) // 'Doer'

///
// Or, alternative using dot syntax
objLitExample.firstName = 'John'
objLitExample.lastName = 'Doer'

// Access the values
console.log(objLitExample.firstName)
// 'John'
console.log(objLitExample.lastName)
// 'Doer'


///
// Object literal example no.5: Object literal, bracket syntax and loops
const objLitExample = {}

for (let i = 0, l = 5; i < l; i++) {
  objLitExample['key' + i] = i
}

// Print the content of objLitExample
console.log(objLitExample)
// Outputs:
// [object Object] {
//   key0: 0,
//   key1: 1,
//   key2: 2,
//   key3: 3,
//   key4: 4
// }
```

## Epilogue: ES6, ES7, ES8 & Writing Modern JavaScript Pt3

Congratulations! You've just finished the third part of ES6, ES7, ES8 & Writing Modern JavaScript series. In this part, you've learned about four ES6 features, namely spread operator, rest parameter, sets and object literal. From now on, these features will no longer be a mystery for you. You will now be able to use them in your work with absolute confidence.

What's coming next? In the next part, you will learn about another set of ES6, ES7 and ES8 features. For example, array `includes()`, `padStart()` and `padEnd()`, new loops and much more. Until then, review what you've learned today and invest some of your time practice. Remember, the more you practice the better you can get in JavaScript.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Part 1]: https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt1/
[Part 2]: https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt2/
[]:

<!--
#### Meta:
-
-->

<!--
#### Inspiration:
- https://github.com/getify/You-Dont-Know-JS/blob/master/es6%20%26%20beyond/ch2.md
- https://github.com/lukehoban/es6features
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment
-->
