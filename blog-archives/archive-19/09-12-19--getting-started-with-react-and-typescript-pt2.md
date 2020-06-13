# Getting Started With React and TypeScript Pt.2 - Basic Types
If you ever wanted to learn how to use React and TypeScript, you are on the right place. This tutorial will help you understand all types you can expect in TypeScript and how to work with them. Learn about these basic types so you can start using React and TypeScript today.<!--more-->
<!--
Table of Contents:
## Types
### Number
### BigInt
### String
### Boolean
### The "null" value
### The "undefined" value
### Symbol
### Object
### Array
### Tuple
### Enum
### Void
### Never
### Any
## Type inference
## Conclusion: Getting Started With React and TypeScript Pt.2
-->

Getting Started With React and TypeScript [Part 1].

## Types

Before you start using React and TypeScript you should get familiar with types you can use in TypeScript. TypeScript supports all types that exist in JavaScript. On top of it, TypeScript adds some new types. Here is an overview of the types you can expect and use when you work with React and TypeScript together, or just with TypeScript.

### Number

Like in JavaScript the `number` type represents both, integer and floating point numbers. In other words, there is no one specific type for integers and other for floats. Both are united under the same type, `number`. These numbers also include hexadecimal and decimal literals, and [binary and octal] literals introduced in ECMAScript 2015.

```ts
// The ': number' after variable name
// and before equal sign specifies number type
// Declare new variable of type number
let numberExample: number

// Assign a value to 'numberExample'
numberExample = 979


// Declare and initialize variable of type number
const numberInteger: number = 13 // number type is not necessary here due to type inference
const numberFloat: number = 8.12 // number type is not necessary here due to type inference
const numberHex: number = 0xf00d // number type is not necessary here due to type inference
const numberBinary: number = 0b111110111 // number type is not necessary here due to type inference
const numberOctal: number = 0o767 // number type is not necessary here due to type inference
```

### BigInt

The `BigInt` type is a new type that was recently added to the JavaScript language specification. Why? In JavaScript, the `number` type cannot represent integer values larger than 2^53, or less than -2^53 for negatives. This means that you can work with numbers of up to around 16 decimal digits.

Sometimes, this may not be enough. You may need something that can handle numbers even bigger than that. In that case, you can use the new `BigInt` value. You can use the `BigInt` to represent a number of arbitrary value. When you want to create `BigInt` you do that by appending `n` to the end of the number.

When it comes to working with React and TypeScript, you will probably not need to use `BigInt` so often. Maybe never. Nonetheless, it is still good to know what it is.

```ts
// The ': bigint' after variable name
// and before equal sign specifies bigint type
// Declare new variable of type bigint
let bigIntExampleTwo: bigint

// Assign a value to 'bigIntExampleTwo'
bigIntExampleTwo = 987654321987654321987654321987654321000n

// Try to change the value of 'bigIntExampleTwo' to different type
bigIntExampleTwo = 159 // error: Type '159' is not assignable to type 'bigint'.


// Declare and initialize variable of type bigint
const bigIntExample: bigint = 1234567890123456789012345678901234567890n // bigint type is not necessary here due to type inference
```

### String

In JavaScript, strings represent some textual data, an array of characters if you want. When you want to create a string you can use single quotes, double quotes or [template literals], or template strings. Strings in TypeScript work in the same way.

```ts
// The ': string' after variable name
// and before equal sign specifies string type
// Declare new variable of type string
let stringExample: string

// Assign a value to 'stringExample'
stringExample = 'This is the initial value.'

// Try to change the value of 'stringExample' to different type
stringExample = 33 // error: Type '33' is not assignable to type 'string'.


// Declare and initialize variable of type string'
const singleQuoteString: string = 'This is a single quote string.' // string type is not necessary here due to type inference
const doubleQuoteString: string = "This is a double quote string." // string type is not necessary here due to type inference
const templateLiteralString: string = `This is a template literal string.` // string type is not necessary here due to type inference
```

### Boolean

Boolean are very simple, logical, type. It has only two values: `true` and `false`.

```ts
// The ': boolean' after variable name
// and before equal sign specifies boolean type
// Declare new variable of type boolean
let booleanExampleTwo: boolean

// Assign a value to 'booleanExampleTwo'
booleanExampleTwo = false

// Try to change the value of 'booleanExampleTwo' to different type
booleanExampleTwo = 'false' // error: Type '"false"' is not assignable to type 'boolean'.


// Declare and initialize variable of type boolean
const booleanExample: boolean = true // boolean type is not necessary here due to type inference
```

### The "null" value

The `null` is special value. It is a subtype of other default types. In JavaScript, null represents "empty", "unknown value" or "nothing". Unlike in other languages, `null` is not a reference to a non-existing object. In TypeScript, if you disable `strictNullChecks` rule/option in `compilerOptions` (or flag) you can assign `null` to types such as number, string, etc.

When you keep the `strictNullChecks` rule enabled, which is the recommended practice, you can assign only to `any`.

```ts
// The ': null' after variable name
// and before equal sign specifies null type
// Declare and initialize variable of type null
const unknownVariable: null = null


// with 'strictNullChecks' rule disabled
// Create 'numberExample' variable of type number
// and initialize it with value of 13
let numberExample: number = 13; // number type is not necessary here due to type inference

// reassign the value of 'numberExample' to null
numberExample = null

// reassign the value of 'numberExample' to a number
numberExample = 15


// with 'strictNullChecks' rule enabled
// Create 'numberExample' variable of type number
// and initialize it with value of 13
let numberExample: number = 13; // number type is not necessary here due to type inference

// reassign the value of 'numberExample' to null
numberExample = null // error: Type 'null' is not assignable to type 'number'.


// with any ('strictNullChecks' doesn't matter now)
// Create 'something' variable of type any
let something: any = 7

something = null // no error
```

### The "undefined" value

The `undefined` is another special value, similar to the `null`. The meaning of undefined is "value is not assigned". For example, if you declare a variable, but not assign any value to it, its value will be `undefined`. The `undefined` works in a similar way to `null`.

```ts
// The ': undefined' after variable name
// and before equal sign specifies undefined type
// Declare and initialize variable of type undefined
let unknownVar: undefined = undefined


// with 'strictNullChecks' rule disabled
// Create 'numberExample' variable of type number
// and initialize it with value of 7
let numberExample: number = 7; // number type is not necessary here due to type inference

// reassign the value of 'numberExample' to undefined
numberExample = undefined

// reassign the value of 'numberExample' to a number
numberExample = 99


// with 'strictNullChecks' rule enabled
// Create 'numberExample' variable of type number
// and initialize it with value of 11
let numberExample: number = 11; // number type is not necessary here due to type inference

// reassign the value of 'numberExample' to undefined
numberExample = undefined // error: Type 'undefined' is not assignable to type 'number'.


// with any ('strictNullChecks' doesn't matter now)
// Create 'something' variable of type any
let something: any = 8888

something = undefined // no error
```

### Symbol

Similarly to `BigInt`, `Symbol` is another new type that was added to JavaScript language specification. A `Symbol` is a unique and immutable (unchangeable) primitive value, something like a unique ID. Symbols are used as unique identifiers for objects.

```ts
// The ': symbol' after variable name
// and before equal sign specifies symbol type
// Declare new variable of type symbol
let symbolExample: symbol

// Assign a value to 'symbolExample'
symbolExample = Symbol('Two')

// Try to change the value of 'symbolExample' to different type
symbolExample = 'some text' // error: Type '"some text"' is not assignable to type 'symbol'.


// Declare and initialize variable of type symbol
let symbolExample: symbol = Symbol('One') // symbol type is not necessary here due to type inference


// Create new variable of type symbol
const SECRET_KEY: symbol = Symbol() // symbol type is not necessary here due to type inference

// Use a computed property key to make the value of SECRET_KEY the key of a property, by putting the 'SECRET_KEY' in square brackets.
let myObj = {
    [SECRET_KEY]: 123
}
```

### Object

The `object` type is another special type. Unlike the other types, `object` can contain collections of various types. In TypeScript, `object` represents anything that is not `number`, `BigInt`, `string`, `boolean`, `null`, `undefined` or `symbol`. This is also one of the types you will encounter fairly often as you work with React and TypeScript.

```ts
// The ': object' after variable name
// and before equal sign specifies object type
// Declare new variable of type object
let objectExample: object

// Assign a value to 'objectExample'
objectExample = {
    firstName: 'Tony',
    lastName: 'Wayne'
}

// Try to change the value of 'objectExample' to different type
objectExample = 'Tony'// error: Type '"Tony"' is not assignable to type 'object'.

// Try to change the value of 'objectExample' to array
objectExample = ['Tony', 'Wayne'] // This is okay (array is an object)


// Declare and initialize variable of type object
let myObj: object = {} // object type is not necessary here due to type inference


// Create object with one key/value pair
// where the key is 'someKey' and its value is type of number
let myObj: { someKey: number } = {
    someKey: 123
}
```

### Array

JavaScript types end with the previous eight types. TypeScript goes farther. In TypeScript, you can use `Array` type. You will probably use this type a lot when you work with React and TypeScript. Arrays are often used to store collections of data and React component. The `Array` type can be written in two ways.

First, you use the type of the elements inside the array followed by `[]` to specify an array of that element type. The second way is about using a generic array type `Array<elementType>`. The `elementType` specifies the type of the elements inside the array.

```ts
// The ': string[]' after variable name
// and before equal sign specifies array type containing strings
// Declare new variable of type array (the first way with '[]')
let names: string[]

// Assign a value to 'names'
names = ['Axel', 'Timothy', 'Jane']

// Try to change the value of 'names' to different type
names = 'Jane'// error: Type '"Jane"' is not assignable to type 'string[]'.


// Declare and initialize variable of type array containing numbers (the first way with '[]')
let ages: number[] = [28, 37, 24] // number[] type is not necessary here due to type inference


// Declare new variable of type array containing strings (the second way with 'Array<elementType>')
let hobbies: Array<string>

// Assign a value to 'names'
hobbies = ['Programming', 'Meditation', 'Reading']


// Declare and initialize variable of type array containing numbers (the second way with 'Array<elementType>')
let mensaNumbers: Array<number> = [658, 983, 4421] // Array<number> type is not necessary here due to type inference
```

### Tuple

The `tuple` types is the first type specific to TypeScript. Although this type doesn't exist in JavaScript, you may find it handy in your projects built with React and TypeScript. It can be interesting alternative to arrays. The `tuple` type allows you to declare an array with a fixed number of elements and known types.

```ts
// The ': [elementType]' after variable name
// and before equal sign specifies tuple type
// Declare a new variable of type tuple with two values, both numbers
let tupleExample: [number, number]

// Assign a value to 'tupleExample'
tupleExample = [59, 62]


// Declare and initialize variable of type tuple with two values, both strings
let tupleExampleTwo: [string, string] = ['Axel', 'Smith'] // tuple type is not necessary here due to type inference


// Try to assign different types to tuple
let tupleExampleThree: [number, string]

// Assign a value to 'names'
// switch the order of values - string, number instead of number, string
tupleExampleThree = ['alphabet', 1]
// error 1 ('alphabet'): Type 'string' is not assignable to type 'number'.
// error 2 (1): Type 'number' is not assignable to type 'string'.
```

### Enum

The `enum` type is another specific to TypeScript. It is also a type you may use often if your work with React and TypeScript. The `enum` type is defined as a collection of values. It is similar to `object` and `array`. Values are separated by commas. It allows you give more friendly names to numeric values.

There are two differences. The first one is that it doesn't contain key/value pairs, only values. The second is that there is no equal sign (`=`) before the curly brackets (`{}`). Similarly to `arrays`, `enum` also start with `index` of 0. So, when you want reference one of the values, you can use this index, like when you work with an `array`.

This index is not set in stone. You can change it if you want. You can do this by using equal sign (`=`) followed by number (the index) in during enum declaration.

```ts
// Create enum
enum Languages {
  JavaScript,
  C,
  Java,
  Ruby,
  PHP
}

// Declare and initialize variable
// using one language from Languages enum using index
const favoriteLanguage: Languages = Languages.JavaScript

// Log the value of favoriteLanguage
console.log(favoriteLanguage) // 0


// Get the name of the value on index 0
const favoriteLanguage: Languages = Languages[0]

// Log the value of favoriteLanguage
console.log(favoriteLanguage) // JavaScript


// Create enum with custom indexes, using '= number'
enum Names {
  One = 1, // set index to 1
  Two = 3, // set index to 3
  Three = 8 // set index to 8
}

// Declare and initialize variables using Names enum
const enumExOne: Names = Names.One
const enumExTwo: Names = Names.Two
const enumExThree: Names = Names.Three

// Log variable values
console.log(enumExOne) // 1
console.log(enumExTwo) // 3
console.log(enumExThree) // 8
```

### Void

The `void` type is specifies that there is no type, or absence of any type. This type is often used as the return type of functions that don't return any value. In case of React and TypeScript, `void` is commonly used as the return type of functions for handling events. In case of variables, `void` is not useful at all.

When you declare some variable of type `void` you can assign to it only assign `null` or `undefined`. This is only possible if you disable the `strictNullChecks` rule/option (or flag).

```ts
// The ': void' after variable name and parenthesis
// and before equal sign specifies void type
// Create function with return type of void
// (function doesn't return any value)
function sayHi(): void {
  console.log('There is no return statement here.')
}


// Declare and initialize variable of type void as undefined
let thisWillNotBeUsed: void = undefined

// This will work if you disable strictNullChecks
thisWillNotBeUsed = null


// Create onChange event handler function that accepts
// one argument (event) and doesn't return any (return of type void)
const handleInput = (event: React.ChangeEvent): void => {
    setName(event.target.value) // Update state with value
}
// some code
<input onChange={handleInput} />


// Create click event handler function that accepts
// one argument (event) and doesn't return any (return of type void)
const handleClick = (): void => {
    console.log('Click')
}
// some code
<Button onClick={handleClick}>Click</Button>


// Try to create function with return type of void
// that returns a string
function sayHi(): void {
  return 'Looks like return.' // error: Type '"Looks like return."' is not assignable to type 'void'.
}
```

### Never

The `never` type is one of the types you are not likely to use with React and TypeScript. This type is where the code which uses it should never be reachable, or when return value never occur. In case of functions, a function that never returns, or always throws an exception, returns `never`. For example, a function with infinite `while` loop.

When you create such a function, with infinite loop, TypeScript will let your code compile. However, TypeScript will infer that function as having return type of `never`. In case of variables, similarly to `void`, `never` is also not very useful.

When you declare some variable of type `never` you can't assign any other type to it. You can use only the `never` type. TypeScript will also infer the `never` when you narrow the type guards so that it can never be true.

```ts
// The ': never' after variable name and parenthesis
// and before equal sign specifies never type
// Create function with one parameter that throws an exception,
// returns type of never
function throwError(message: string): never {
  throw new Error(message)
}


// Create function with infinite loop,
// returns type of never
function getStuck(): never {
  while (true) {
    console.log('Infinite loop.')
  }
}


// Declare variable of type never
let neverOne: never

// Try to change the value of neverOne
neverOne = 'Some thing' // error: Type '"Some thing"' is not assignable to type 'never'.


// Never and narrowing type guards
function processThis(value: any) {
  // Check for impossible type of value
  // such as string, number and object at the same time
  if (typeof value === 'string' && typeof value === 'number' && typeof value === 'object') {
    // This will never happen
    value // TypeScript will infer type never
  }
}
```

### Any

The `any` type is the last type you can encounter, and use, in TypeScript. It is also the most used, or abused, type by TypeScript beginners. The `any` is commonly used when you either don't know the type of a variable or you don't need to specify it. One example can be when your program doesn't require some specific type.

Another example is when you work with 3rd party packages, modules and APIs and you don't know what to expect. Or, if you know only partially what to expect. For example, you know the value will be an `array`, but you know nothing about its content. In these cases, `any` will tell TypeScript to skip the type check and let your code compile.

The `any` type is also very handy when you want to gradually rewrite your JavaScript code to TypeScript. Or, when you migrate from React to React and TypeScript. The way `any` works is simple. It tells TypeScript that the value can be of any type. It can be string, number, boolean, array, object, whatever. So, there is nothing to complain about.

```ts
// The ': any' after variable name
// and before equal sign specifies any type
// Declare variable of type any
let anyExample: any

// Assign a number to anyExample
anyExample = 19 // This is okay

// Change the value of anyExample and also its type
anyExample = 'The power of any' // This is okay

// Change the value of anyExample and also its type again
anyExample = false // This is okay


// Using any with partially known data
// Create function to fetch some API
function fetchApi() {
  fetch('endpoint')
    .then(res => {
      // Data will be an array with something inside,
      // but we don't know what is the type of data
      const fetchedData = res.data

      console.log(fetchedData)
    })
    .catch(error => console.log(error))
}

fetchApi()
```

## Type inference

Throughout the examples, I add comments saying that the type is not necessary in that place due to type inference. What is type inference? It is not necessary to annotate type every time. In some situations, TypeScript will do this for you. It will automatically infer types of variables and parameters based on the default values.

There are three situations when this will happen. First, TypeScript will infer type of variable when the variable is declared and also initialized. Second, TypeScript will infer type of parameter when you set default values for that parameter. Fourth, TypeScript will infer return type when function returns some value.

If you find yourself any of these three situations you don't have to annotate, or specify, types. What if you forget to annotate some variable or parameter? TypeScript will automatically use type of `any`. If you enable `noImplicitAny`, or `strict`, option TypeScript will automatically warn you when this implicit `any` occurs.

```ts
// Declare and initialize value
let userAge = 46
// TypeScript will infer: let userAge: number

let isAlive = true
// TypeScript will infer: let isAlive: boolean

let username = 'Stan Wayne'
// TypeScript will infer: let username: string

let arr = [59, 890, 563]
// TypeScript will infer: let arr: number[]

let userData = {
    name: 'axel',
    age: 28,
    isAlive: true
}
// TypeScript will infer:
// let userData: {
//     name: string;
//     age: number;
//     isAlive: boolean;
// }


// Function with parameter(s) with default value
function greetUser(name = 'anonymous') {
    return `Welcome back ${name}`
}
// TypeScript will infer: function greetUser(name?: string): string
// function greetUser with optional parameter type of string and return type of string


// Function returning value
function greetUser() {
  return 'Welcome back!'
}
// TypeScript will infer: function greetUser(): string
// function greetUser with return type of string

// Function with return type of void
function noReturn() {
  console.log('This is void.')
}
// TypeScript will infer: function noReturn(): void
// function noReturn with return type of void


// Only declaring a variable
let something
// TypeScript will infer: let something: any
```

What if you some data collections with values of different types? Will TypeScript infer types here as well? Yes, it will. TypeScript will correctly infer all types for you.

```ts
// Array with number, string and boolean
let arrOne = [15, 'Tony Grand', false]
// TypeScript will infer: let arrOne: (string | number | boolean)[]


// Array with numbers and boolean
let arrTwo = [165, 98956, 9494, true]
// TypeScript will infer: let arrTwo: (number | boolean)[]


// Object with number, strings, boolean and array
let userObj = {
    firstName: 'Arthur',
    lastName: 'Bailey',
    age: 35,
    isMarried: false,
    skills: [
        'design',
        'programming'
    ]
}
// TypeScript will infer:
// let userObj: {
//     firstName: string;
//     lastName: string;
//     age: number;
//     isMarried: boolean;
//     skills: string[];
// }
```

## Conclusion: Getting Started With React and TypeScript Pt.2

Congratulations! You've just finished the second part of this series about getting started with React and TypeScript. Today you've learned about what types can you expect, and work with, in TypeScript. Knowing these types and how to work with them will make it easier to start with React and TypeScript.

What's coming in the next part of this getting started with React and TypeScript series? You will get into the practical side of working with React and TypeScript. You will learn about types and interfaces. After that, you will learn how to write class and functional components and use hooks in TypeScript, and how to annotate your code.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Part 1]: https://blog.alexdevero.com/react-and-typescript-pt1/
[binary and octal]: https://babeljs.io/docs/en/learn/#binary-and-octal-literals
[template literals]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals

<!--
### Meta:
-
-->
