# JavaScript Basics - Understanding Basic JavaScript Data Types Pt.2
Data types are fundamental part of JavaScript language. If you want to get good at JavaScript, you have to know how these data types work and how to use them. This article will help you learn what you need to know about BigInt, boolean, null, undefined, symbols and objects.<!--more-->
<!--
Table of Contents:
## Data types
### BigInt
#### BigInt and arithmetic operations
#### BigInt type is not a Number type
#### From Number to BigInt and back
#### BigInt and booleans
### Boolean (logical type)
#### Truthy and falsy
### Null
### Undefined
### Symbols
#### Symbols as hidden object properties
#### Symbols and cloning objects
### Objects
#### Creating objects
#### Square brackets and computed properties
#### For...in loop, keys and values
#### Using "in" operator
#### Copying objects
#### Cloning objects
#### Merging objects
## Conclusion: Understanding Basic JavaScript Data Types
-->

## Data types

In the previous part, you've learned about the first two data types that exist JavaScript. These were strings and numbers. Now, let's take a look at the rest of them.

### BigInt

`BigInt` is one of the data types added to JavaScript language recently. The `BigInt` type allows you to work with numbers bigger than 2^53 - 1. Before `BigInt`, there was no way to work with such large numbers in JavaScript. The `number` primitive data type can't handle these numbers. There is a safe integer limit for `Number` type.

`BigInt` was created to bridge this gap. `BigInt` allows you to safely work and store with large integers, even integers exceeding the safe integer limit. Since the purpose of `BigInt` is to deal with very large numbers it is unlikely you will use it very often. That said, it is still good to know there is such data type, and how to work with it.

There are two ways to create a `BigInt`. The first way is by appending "n" to the end of an integer, such as `6562324949863231n`. The second way is by calling `BigInt()` function. In this case, you use the number as an argument-put it inside the parentheses-such as `BigInt(6562324949863231)`. This will create the same result as using the first way.

```js
// Create BigInt with 'n'
const bigIntExample1 = 6562324949863231n
typeof bigIntExample1 // 'bigint'


// Create BigInt with BigInt()
const bigIntExample2 = BigInt(6562324949863231)
bigIntExample2 // 6562324949863231n
typeof bigIntExample2 // 'bigint'
```

#### BigInt and arithmetic operations

Similarly to the `Number` type, you can do arithmetic operations with `BigInt` as well. You can add, subtract, multiply or divide them. When you want to do so, remember that you can do these operations only when all numbers are data type of `BigInt`. If you try to, for example, multiple a `Number` by `BigInt`, it will lead to an error.

Another thing to remember is that arithmetic operations with `BigInt` numbers will always return `BigInt` numbers. Arithmetic operations with `BigInt` will never return the decimal part. There will be no floats at the end because the results will always be rounded towards zero.

```js
// arithmetic operations
// addition
BigInt(3) + BigInt(9) // 12n

// subtraction
8n - 3n // 5n

// multiplication
5n * 15n // 75n

// division
12n / 4n // 3
64n / 3n // 21n <= no reminder

// modulo
74n % 6n // 2n

// exponentiation
12n ** 9n // 5159780352n

// Using BigInt
```

#### BigInt type is not a Number type

`BigInt` type is not a `Number` type. This is important to remember, especially for comparison. When you try to compare `BigInt` of zero with zero, it will work only if you use loose equal. Loose equal will result in `true`. On the other hand, if you use strict equal, it will result in `false`.

The reason is that strict equal compares both, the value as well as its data type. So, yes, the values are the same. Both are zero. However, the data types are different. One is `BigInt` and the other is `Number`. In order for things to be equal, both conditions must be "truthy". They are not. So, the result is `false`. Other than that, you can compare `BigInt` with `Number` as you want.

```js
// Comparison with loose equal
0n == 0
// true


// Comparison with strict equal
0n === 0
// false


// Comparing BigInt with number
3n < 65
// true

2n > 1
// true
```

#### From Number to BigInt and back

When you want to covert between these two data types you can use `BigInt()`, to convert number to `BigInt`, and `Number()`, to convert `BigInt` to number. Since `BigInt` allows to work with numbers larger than `Number` can handle, remember that if the `BigInt` is too big for the `Number` type, any extra bits will be cut off. So the precision will be lost.

When you want to convert some number to `BigInt` make sure the number is an integer. Otherwise, it will not work. When you try to convert float to `BigInt` JavaScript will throw an error. One more thing. As you know, it is possible to convert `string` to a `Number`. The same is also possible with `BigInt`. You can convert `string` to `BigInt`.

```js
// Convert number to BigInt
const someNumber = 13
BigInt(someNumber) // 13n


// Convert BigInt to number
const someBigInt = 35n
Number(someBigInt) // 35


// When BigInt is too big
// the number is rounded
// and precision is lost
const someBigNumber = BigInt(Number.MAX_SAFE_INTEGER)
const anotherBigNumber = BigInt(Number.MAX_SAFE_INTEGER)

someBigNumber * anotherBigNumber
// 81129638414606663681390495662081n
Number(someBigNumber * anotherBigNumber)
// 8.112963841460666e+31


// Try to convert float to BigInt
const someFloat = 35.8
BigInt(someFloat) // RangeError: The number 35.8 cannot be converted to a BigInt because it is not an integer


// Convert string to BigInt
const someString = '95'
BigInt(someString) // 95n
```

#### BigInt and booleans

One more thing about `BigInt` data type. When you use this data type in conditional statements, such as `if`, or other boolean operations, `BigInt` will behave like `Number`. For example, number zero is always "falsy". Numbers higher, or smaller, than zero are "truthy".

The same rule applies to `BigInt`. `BigInt` equal to `0n` is also "falsy". `BigInt` bigger or smaller than `0n` will be "truthy".

```js
// BigInt and booleans
if (-5) {
  console.log('Hello -5!')
}
// 'Hello -5!'

if (0) {
  console.log('Hello 0!')
}
// ... nothing

if (5) {
  console.log('Hello 5!')
}
// 'Hello 5!'


if (BigInt(-5)) {
  console.log('Hello -5!')
}
// 'Hello -5!'

if (BigInt(0)) {
  console.log('Hello 0!')
}
// ... also nothing

if (BigInt(5)) {
  console.log('Hello 5!')
}
// 'Hello 5!'
```

### Boolean (logical type)

`Boolean` is one of the simplest data types in JavaScript. It is a logical type that can be either `true` or `false`. You can think about `true` as "yes" and `false` as "no".

```js
// Boolean
const falsyBoolean = false
const truthyBoolean = true

// Boolean as a result of comparison
let comparison = 15 > 3
comparison // true

comparison = 7 > 21
comparison // false
```

#### Truthy and falsy

In JavaScript, when you use value in boolean context, such as `if` conditional statement, that value is converted to boolean. It can become either `true` or `false`. Which `boolean` it will is determined by the "type" of the value. Value can be either "truthy" or "false". Truthy value will become `true` and falsy `false`.

Fortunately, there is an easy way to remember which values are truthy and which are falsy. Values that are falsy are `0`, `0n` (0 `BigInt`), `""` or `''` or ` `` ` (empty string), `null`, `undefined`, `NaN` and of course `false`). Any other value is truthy.

```js
// Truthy values
42
-42
3.14
-3.14
12n
Infinity
-Infinity
"0"
'something'
`ticking`
"false"
[]
{}
new Date()
true


// Falsy values
0
0n
""
''
``
null
undefined
NaN
false
```

### Null

Next is `null`. This one is special. `Null` is a subtype of other default types that contains only the `null` value. In other programming languages, `null` is used as a reference to a non-existing object or null pointer. This is not the case in JavaScript.

In JavaScript, `null` represents "unknown value", "nothing" or "empty". In boolean context, `null` value is falsy. One more thing. Programmers sometimes use `null` as a value for variables whose values are "empty" or unknown.

```js
// Null
let balance = null
```

### Undefined

`undefined` is very similar to `null`. It is also special value, a subtype of other default types that contains only the `undefined` value. The meaning of `undefined` can be translated as "value is not assigned". The best example to illustrate this is declaring a variable without assigning it.

When you declare a variable, but you will not assign it any value, its value will automatically be `undefined`. Similarly to `null`, `undefined` is also falsy in boolean context. One more thing. You can assign `undefined` to a variable. However, this is not a recommended practice. It is better to assign it `null`.

```js
// Undefined
let player
typeof player // 'undefined'
console.log(player) // undefined
```

### Symbols

Similarly to `BigInt`, `Symbol` is also one of the data types that were recently added to JavaScript. The `Symbol` type represents a unique identifier. The main use of `Symbol` is creating unique identifiers for objects. For example, you can create hidden properties on objects.

When you want to create new `Symbol` it is by using `Symbol()`. You can also provide a description of the symbol, or name of the symbol. You can do this passing a `string` between the parenthesis. As we already discussed, symbols are always unique. This applies even if you specify a symbol name.

Even if you decide to create a couple of symbols, with the same name, they will still be different. The values will be different. That symbol name has no real effect for JavaScript itself, only for you. For example, for debugging.

```js
// Create new symbol
const newSymbol = Symbol()


// Create new symbol with name
const newSymbol = Symbol('id')


// Create multiple symbols
// with the same symbol name
const symbolA = Symbol('alpha')
const symbolB = Symbol('alpha')
const symbolC = Symbol('alpha')
const symbolD = Symbol('alpha')

// Check for equality
symbolA === symbolB // false
symbolC === symbolD // false
symbolA === symbolC // false
```

#### Symbols as hidden object properties

As we discussed, one common use case for using `Symbols` is to create hidden properties on objects. Hmm, hidden? When you create a property on object some 3rd party code can access it accidentally and re-write it. In case of a `Symbol`, this will not happen. They can't be accidentally accessed and re-written.

There are two reasons. First, 3rd party code is not very likely to see them. It is hard to re-write something you can't see. Second, `Symbol` are always unique. So, even if you look for a `Symbol` you still don't really know what you are looking for, what you are trying to find. This also applies to using [for...in loop].

When you use for...in loop, it will not reveal any `Symbol`. Not even `Object.keys()`, or `Object.values()`, will be able to reveal anything. If you can't find it, you can't access it and/or change it, even if you want. One thing, although `Symbols` will not be detected by `Object.keys()`, they will work with `Object.assign()`.

One thing to remember. When you want to use a `Symbol` in an object literal, to create a symbol property, you need to wrap that `Symbol` inside square brackets (`{ [someSymbol]: value }`).

```js
// Create a symbol
const id = Symbol('asin')

// Create object with symbol property (id)
// as a property for id
let book = {
  [id]: 'B00I0A6HUO', // <= use Symbol (id variable), with square brackets
  title: 'Hard Things About Hard Things',
  author: 'Ben Horowitz',
  pubDate: '2014'
}

// Access the symbol directly
// using correct name (of the variable)
book[id] // 'B00I0A6HUO'


// Try to find symbol with for...in (without success)
for (let property in book) {
  console.log(property)
}
// 'title'
// 'author'
// 'pubDate'


// Try to find the value of property
// created with symbol with for...in (without success)
for (let property in book) {
  console.log(book[property])
}
// 'Hard Things About Hard Things'
// 'Ben Horowitz'
// '2014'


// Try to find symbol with Object.keys() (without success)
Object.keys(book)
// [ 'title', 'author', 'pubDate' ]


// Try to find symbol with Object.values() (without success)
Object.values(book)
// [ 'Hard Things About Hard Things', 'Ben Horowitz', '2014' ]
```

#### Symbols and cloning objects

When you create a clone of an object, using `Object.assign()`, it will copy its whole content. This also includes any `Symbols` (symbol properties) inside it. This makes sense. When you want to create a clone of an object you want that clone to be a 1:1 copy.

It would not be a 1:1 copy if some properties were missing, those properties created with `Symbols`. It is 1:1 copy only when the content is 100% identical. This includes properties created with `Symbols`, or symbol properties.

```js
// Create symbol
const id = Symbol('asin')

// Create object with symbol property (id)
const book = {
  [id]: 'B00I0A6HUO', // <= use Symbol (id variable), with square brackets
  title: 'Hard Things About Hard Things',
  author: 'Ben Horowitz',
  pubDate: '2014'
}

// Access the symbol property of book object
book[id] // 'B00I0A6HUO'


// Crete clone of the book object
const bookClone = Object.assign({}, book)

// Access the symbol property of the clone
bookClone[id] // 'B00I0A6HUO'

// Equality check
book[id] === bookClone[id] // true
```

<!-- #### Symbols in the global context -->

### Objects

All the data types we discussed so far were "primitive". "Primitive" means that they can contain only one thing. For example, a `Number` can only contain one number while `String` can only contain one string. Objects are different. Objects can store more than just one "thing". What's more, they can store multiple "things" of multiple types.

#### Creating objects

There are two ways to create an `object`. The first one by using object literal syntax. In this case, you use curly brackets (`{}`) containing a list of properties, key/value pairs. This list of properties is optional. The second way is by using object constructor, or `new Object()`.

Which one you choose depends on your preference. That said, it is often easier, faster and more effective to use the object literal syntax. When you decide to go with object constructor you can then have to add properties (key/value pairs) using the dot notation (`obj.property = ...`). This works for object literal syntax as well.

However, when you use object literal syntax, adding properties (key/value pairs) is much faster. You don't have to create the object and then use dot notation. Instead, you can add properties (key/value pairs) right away, when you create the object.

In case of object literal, when you want to add property that contains multiple words, you must wrap that property, those words, with quotes (`{'some property': someValue }`). In case of object constructor, you have to wrap the property with quotes and square brackets (`obj['some property'] = someValue`).

When you want to access that multi-word property, you use quotes and square brackets again (`obj['some property']`). This also works for accessing one-word properties (`obj['property']`). Or, you can access the property using without brackets and quotes, using dot notation (`obj.property`).

Lastly, you can also delete existing properties. You can do this by using `delete` keyword followed by the object name and property (using dot notation).

```js
// Creating object with literal
const objOne = {}

// Creating object with literal
// and adding some properties (key/value pairs)
const objTwo = {
  name: 'Tony', // the 'name' is key and 'Tony' is a value
  age: 35 // the 'age' is key and 35 is a value
}


///
// adding new property using dot notation
objTwo.isAlive = true // the 'isAlive' is key and true is a value

// Check the object
console.log(objTwo)
// { name: 'Tony', age: 35, isAlive: true }


///
// Add multi-word property, using dot notation
objTwo['last job'] = 'programmer'


///
// Accessing multi-word property
console.log(objTwo['last job']) // 'programmer'


///
// Multi-word property with object literal
const objFive = {
  'some multi-word property': true,
  day: 'Monday'
}


///
// Delete name property in objTwo
delete objTwo.name

// Check the object
console.log(objTwo)
// { age: 35, isAlive: true }


///
// Creating object with object constructor
const objThree = new Object()


///
// Creating object with literal
// and adding some properties  (key/value pairs)
// using dot notation
const objFour = new Object()
objFour.name = 'Tony'
objFour.age = 35
objFour.isAlive = true

// Check the object
console.log(objFour)
// { name: 'Tony', age: 35, isAlive: true }


///
// Delete age property in objFour
delete objFour.age

// Check the object
console.log(objFour)
// { name: 'Tony', isAlive: true }


///
// Add multi-word property
objFour['happiness score'] = '92%'


///
// Accessing multi-word property
console.log(objFour['happiness score']) // '92%'
```

#### Square brackets and computed properties

As you know, adding multi-word properties works only when you use square brackets and quotes. This is due to a limitation in variable naming, i.e. it can't contain any spaces. So, remember to always use square brackets and quotes when you want to add multi-word property. Otherwise, you use camelCase, or something similar and remove spaces.

```js
// Square brackets and adding multi-word properties
let studentOne = {}
studentOne['can program'] = true

console.log(studentOne)
// { 'can read': true, 'can program': true }

// Access 'can program' property
console.log(studentOne['can program'])
// true


// camelCase and adding multi-word properties
let studentTwo = {}
studentTwo.canRead = true

console.log(studentTwo)
// { canRead: true }

// Access canRead property
console.log(studentTwo.canRead)
// true
```

When you use object literal, you can also use square brackets to reference a variable. When you do this, the value of that variable will be used as the name of the property. This, new, property is called computed property. Remember, when you use this approach, you have to use the value of that variable when you want to access the property, not the name of the variable.

When you use square brackets you can also use more complex property names. For example, you can combine, or concatenate, computed property with strings.

```js
// Declare and initialize variable
// for creating computed property
const example = 'title'

// Create object with computed property
const book = {
  [example]: 'Who knows' // [varOne] is computed property
}

// Access the property
// ! Use the value of the variable ('title'), not its name
console.log(book.title)
// 'Who knows'

// This will not work:
// Using variable name (example) to access the property
console.log(book.example)
// undefined


///
// Combine computed property with string
const itemOne = 'one'
const itemTwo = 'two'

let list = {
  ['item ' + itemOne]: 'phone',
  ['item ' + itemTwo]: 'computer'
}

console.log(list)
// { 'item one': 'phone', 'item two': 'computer' }

// Or
let obj = {}
let stuff = ['pencil', 'gum', 'computer', 'notepad', 'glass']

for (let i = 0; i < 5; ++i) {
  obj['item no.' + i] = i
}

console.log(obj)
// {
//   'item no.0': 'pencil',
//   'item no.1': 'gum',
//   'item no.2': 'computer',
//   'item no.3': 'notepad',
//   'item no.4': 'glass'
// }
```

#### For...in loop, keys and values

When you want to get all keys, or values, inside an `object` one thing you can use is `for...in` loop. Or, you can also use `Object.keys()` for getting all keys and `Object.values()` for getting all values. In case of `for...in` loop the syntax is simple. You specify variable for keys and what object you want to loop over.

When you use the key variable, inside the loop, you will get object key. You can also combine the key and object name to get the value.

```js
const user = {
  firstName: 'John',
  lastName: 'Doe',
  age: 28,
  occupation: 'scientist'
}

// Using for...in loop
// the 'key' variable specifies the key
// this variable doesn't have to be exactly 'key',
// just make sure to use the same variable name inside the loop
// for example: for (let blob in user) or for (let zig in user)
// the 'user' specifies the object to loop over
for (let key in user) {
  console.log('key: ' + key) // get all keys
  console.log('value: ' + user[key]) // get all values

  // This will also work - using dot notation
  // Note: Watch out! Multi-word properties
  // can cause issues with dot notation
  console.log('value: ' + user.key) // get all values
}
// 'key: firstName'
// 'value: John'
// 'key: lastName'
// 'value: Doe'
// 'key: age'
// 'value: 28'
// 'key: occupation'
// 'value: scientist'
```

#### Using "in" operator

When you want to check if specific property exists in an `object` there is a faster way. You can use `in` operator. The syntax is very simple. You use the property name in the form of a `string`, followed by the `in` operator, followed by the `object` you want to check. If the property exists, it will return `true`. Otherwise, it will return `false`.

```js
// in operator
const user = {
  firstName: 'John',
  lastName: 'Doe',
  age: 28,
  occupation: 'scientist'
}

console.log('firstName' in user) // true
console.log('occupation' in user) // true
console.log('wage' in user) // false
console.log('height' in user) // false
```

#### Copying objects

When you work with objects, there is one thing you have to remember. In JavaScript, objects themselves are not copied. What is being copied instead is the reference to the original object. This is called copying by reference. Or, creating a [shallow copy]. Put simply, no new object is created. There is still one object, but there are two variables referencing that object, the same object.

Why is this important? There is still only one object. So, when you change that object all its copies, all variables referencing that object, will be changed as well!

```js
// Copying objects, by reference
// Create object book
const book = {
  title: 'Zero to One',
  author: 'Peter Thiel'
}

// Create a copy of book object (copy by reference, shallow copy)
const newBook = book

// Check the newBook
console.log(newBook)
// { title: 'Zero to One', author: 'Peter Thiel' }

// Change the author in the ORIGINAL book object
book.author = 'Peter Thiel & Blake Masters'

// Check the ORIGINAL book object
console.log(book)
// { title: 'Zero to One', author: 'Peter Thiel & Blake Masters' }

// Check the COPY of the book object
console.log(newBook)
// { title: 'Zero to One', author: 'Peter Thiel & Blake Masters' }

// One more check
// Compare the original object with the copy - the same
console.log(book === newBook)
// true
```

This is not true for primitive data types we discussed, such as strings, numbers, etc. When you copy a string, new string is created. So, when you change the original string, it will not change the copy. The copy will remain untouched.

```js
// Copying strings
// Create a string
let hello = 'Hello!'

// Create a copy of the hello string
let newHello = hello

// Check the newHello string
console.log(newHello) // 'Hello!'

// Change the original string
hello = 'Hello world!'

// Check the original hello string
console.log(hello) // 'Hello world!'

// Check copy, newHello, string
console.log(newHello) // 'Hello!'

// One more check
// Compare the original string with the copy - different
console.log(hello === newHello) // false
```

#### Cloning objects

So, copying objects the old way doesn't duplicate the object itself. Is there a way to create a real, independent, copy of an object. Fortunately, yes. You can clone objects, create independent copies, with [Object.assign()]. When you use `Object.assign()` it will duplicate all properties inside the original and create new object.

So, if, in the future, you change the original object, the clone will not be affected. It will remain untouched. This `assign()` method accepts two parameters. First is `target` and second is `source`. When you want to create new object by copying another you use empty object as the `target` (`{}`) and the original object as the `source`, i.e. `Object.assign({}, originalObject)`. If you use some object as `target` it will be changed as well.

There are also other options for creating clones of objects, or of deep copies. One of them is library called [lodash] and its `_.cloneDeep()` method.

```js
// Create book object
const book = {
  title: 'Zero to One',
  author: 'Peter Thiel'
}

// Create a clone of book object
const newBook = Object.assign({}, book)

// Change the author in the ORIGINAL book object
book.author = 'Peter Thiel & Blake Masters'

// Check the ORIGINAL book object
console.log(book)
// { title: 'Zero to One', author: 'Peter Thiel & Blake Masters' }

// Check the COPY of the book object
console.log(newBook)
// { title: 'Zero to One', author: 'Peter Thiel' }

// One more check
// Compare the original object with the copy - different
console.log(book === newBook)
// false
```

#### Merging objects

One more thing. The `Object.assign()` can also be used for merging objects into a new one. The process is the same as when you create a copy. You use empty `object` as the `target` (`{}`). However, for the `source`, you now use all objects you want to merge into the new `object`, i.e. `Object.assign({}, objOne, objTwo, objThree)`.

```js
// Create one object
const bookPartOne = {
  author: 'Peter Thiel',
  title: 'Zero to One'
}

// Create another object
const bookPartTwo = {
  publisher: 'Currency',
  pubDate: '2014',
  numOfPages: 224
}

// Create one more object
const bookPartThree = {
  asin: '0804139296'
}

// Merge all three objects into new object
const newBook = Object.assign({}, bookPartOne, bookPartTwo, bookPartThree)

// Check the new object
console.log(newBook)
// {
//   author: 'Peter Thiel',
//   title: 'Zero to One',
//   publisher: 'Currency',
//   pubDate: '2014',
//   numOfPages: 224,
//   asin: '0804139296'
// }
```

<!-- https://javascript.info/object -->

## Conclusion: Understanding Basic JavaScript Data Types

Good job! You've just finished the second, and also last, part of this mini series. Now, you know about all seven data types that exist in JavaScript. You know how these data types work, how to use them, and what gotchas to pay attention to. Now, take time to review and practice what you've learned so far.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[for...in loop]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in
[lodash]: https://lodash.com/docs#cloneDeep
[Object.assign()]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign

<!--
#### Meta:
-
-->

<!--
#### Inspiration:
- https://javascript.info/number#tests-isfinite-and-isnan
-->
