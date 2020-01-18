# ES6, ES7, ES8 & Writing Modern JavaScript Pt2 - Template literals, Destructuring & Defaults

ES6 added many great features to JavaScript. Among these features are template literals, destructuring and default parameters and values. These are also the features you will learn about in this part. Improve your knowledge of ES6 and learn how to write modern JavaScript. Become a better JavaScript programmer!

<!--
Table of Contents:
## Template literals
## Destructuring
## Default parameters and values
## Epilogue: ES6, ES7, ES8 & Writing Modern JavaScript Pt2
-->

ES6, ES7, ES8 & Writing Modern JavaScript [Part 1] (Scope, let, const, var).

## Template literals

Before there was ES6 (ECMAScript 2015), it was possible for web developers to create strings in only two ways. They could use either single or double quotes. This way of writing code what not very effective. This was especially true if the developer also wanted to include one or more variables inside the string.

In this case, he had to use string concatenation. This is not a problem if the string you are working with is short, and the amount of variables is low. However, what if you have a lot of text and the amount of variables you need to use is high? Then, it is a different story and the result can be a disaster. Messy and barely readable code.

Fortunately, this is no longer something you should worry about. One of the features introduced by ES6 were template literals. Template literals are like strings on steroids. Some developers also call them a syntactic sugar. Well, this can be said about many other features of ES6, and later specifications, as well.

Template literals allow you to create strings and include pieces of your code such as variables. These are called placeholders. This is called [string interpolation]. Another thing template literals allow is creating multi-line strings. Meaning, you don't need to use special encoded character for line break. When you want to add a line-break you just hit "Enter".

The syntax of template literals is very simple. Instead of quotes, you wrap the text, or any content, with back-ticks (``` `` ```). When you want to add some variable or just any expression into the content, you use dollar sign followed by curly braces. The expression goes inside the curly braces (`${expression}`). For multi-line, just hit "Enter".

One interesting thing. When you try the code below, or any code that uses back-ticks, notice what will you get. There will be no back-ticks in the console. The reason? JavaScript will compile the back-ticks into good old quotes.

```
///
// Template literal example no.1: Basic text
// Notice that there are no back-ticks in the output.
console.log(`Some random text`)

// Outputs:
// 'Some random text'

// Template literal example no.2: Multi-line text
// Notice that there are again no back-ticks in the output.
console.log(`This text
should be printed
on multiple lines.`)

// Outputs:
// `This text
// should be printed
// on multiple lines.`

// Using quotes:
console.log('This text\n' + ' should be printed\n' + ' on multiple lines.')

// Outputs:
// 'This tex'
//  should be printed
//  on multiple lines."

///
// Template literal example no.3: Using placeholders (such as variables)
const username = 'johndoe'
const age = 32

console.log(`The name of the user is ${username} and his age is ${age}.`)
// Outputs:
// 'The name of the user is johndoe and his age is 32.'

// Using quotes:
const username = 'johndoe'
const age = 32

console.log('The name of the user is ' + username + ' and his age is ' + age + '.')
// Outputs:
// 'The name of the user is johndoe and his age is 32.'

///
// Template literal example no.4: Other expressions
const x = 3
const y = 11

console.log(`X plus Y is ${x + y > 20 ? 'bigger' : 'smaller'} than 20.`)
// Outputs:
// 'X plus Y is smaller than 20.'

// Using quotes:
const x = 3
const y = 11

console.log('X plus Y is ' + (x + y > 20 ? 'bigger' : 'smaller') + ' than 20.')
// Outputs:
// 'X plus Y is smaller than 20.'
```

_A note on syntactic sugar: I mentioned that some developers like to call template literals, and other features of ES6 and later JavaScript specifications, a syntactic sugar. This is actually not so far from the truth. Under the hood, JavaScript is passing the content of back-ticks into a function and concatenating its parts into one string. In other words, JavaScript does what you saw on the examples with quotes._

## Destructuring

The destructuring is also called destructuring assignment. This is a JavaScript feature that makes it easier for you to create a number of different variables from values stored inside arrays or properties stored inside objects. All this with a single line. Meaning, you no longer have to declare all variables one by one.

Well, I should be more precise. "Easier" is not the correct word. A better word to use, in this context, is "possible" because you couldn't do this before ES6. There was nothing similar to destructuring in older specifications of JavaScript.

As you know, there are two ways to declare variables, with (code example no.2) or without an initial value (code example no.1). The only [exception] is `const`, which must be always declared with value. These two ways work also when you want to use destructuring. When you want to declare variables or assign values to them using destructuring wrap the variables with square brackets (`[]`) in case of an array.

When you want to destructuring with an object use curly braces (`{}`) (code example no.3). Also, remember to use correct name for your variables when you work with objects. Variable names must match the name of properties inside the object. Otherwise, the variable will be declared as `undefined` (code example no.4).

Fortunately, ES6 provides a way to bypass this. You can use destructuring to extract values from objects and declare variables with different names than the names of those properties. The way to do this is by changing the left side of the assignment. You will again use variable names that match the name of properties.

Then, these names will be followed by colons (`:`) and the new names. It will look like you are creating a new object (code example no.5). Another good use case for destructuring is when you want to quickly swap values of variables. Before ES6, you would have to use a temporary variable. With destructuring you can do this with a single line of code (code example no.6).

One great thing about destructuring is that it supports default values. This is another very useful feature in ES6. This means that you can provide a default value for a variable. This can be useful when you want to declare more variables than there is items in an array or properties in an object (code example no.7).

If there is a corresponding item or property, it will be assigned to the variable. Otherwise, variable will use the default value. What if you declare more variables than there is items in the array or properties in the object and forget default values? JavaScript will initialize the variable will set its value to `undefined` (code example no.8).

What if the opposite is true? Let's say that you want to declare two variables. However, there are four items in the array. What's more, you want to use only the first and third item. This is not a problem. Destructuring allows you to skip or ignore the array item, or object property. You use empty space instead of variable (`[a, , b]`) (code example no.9).

```
///
// Destructuring example no.1: No initial values and array
let x
let y
let z

// Assign values to x, y, z
[x, y, z] = ['one', true, 13]

console.log(x)
// Outputs: 'one'
console.log(y)
// Outputs: true
console.log(z)
// Outputs: 13

///
// Destructuring example no.2: With initial values and array
let [x, y, z] = ['one', true, 13]

console.log(x)
// Outputs: 'one'
console.log(y)
// Outputs: true
console.log(z)
// Outputs: 13

// the same as
let array = ['one', true, 13]

let [x, y, z] = array

console.log(x)
// Outputs: 'one'
console.log(y)
// Outputs: true
console.log(z)
// Outputs: 13

///
// Destructuring example no.3: Objects
let {name, surname, age} = {name: 'John', surname: 'Doe', age: 35}

console.log(name)
// Outputs: 'John'
console.log(surname)
// Outputs: 'Doe'
console.log(age)
// Outputs: 35

///
// Destructuring example no.4: Objects the wrong way
let {a, b, c} = {name: 'John', surname: 'Doe', age: 35}

console.log(a)
// Outputs: undefined
console.log(b)
// Outputs: undefined
console.log(c)
// Outputs: undefined

///
// Destructuring example no.5: Objects and changing variable names
// Notice the left side of the assignment.
// Here is where you change the variable names: name to a, surname to b, age to c
let {name: a, surname: b, age: c} = {name: 'John', surname: 'Doe', age: 35}

console.log(a)
// Outputs: 'John'
console.log(b)
// Outputs: 'Doe'
console.log(c)
// Outputs: 35

///
// Destructuring example no.6: Swapping variable values
let y = 'Jack';
let z = 35;

[y, z] = [z, y]
console.log(y)
// Outputs: 35
console.log(z)
// Outputs: 'Jack'

///
// Destructuring example no.7: Default values
// The 'foo', 'bar' and 'bazz' are default values for a, b and c.
let [a = 'foo', b = 'bar', c = 'bazz'] = [13, 14]

console.log(a)
// Outputs: 13 - first item in the array
console.log(b)
// Outputs: 14 - second item in the array
console.log(c)
// Outputs: 'baz' - default value because array has only 2 items

///
// Destructuring example no.8: More variables and no defaults
let [a, b, c, d] = [true, 'world', 'falsy']

console.log(a)
// Outputs: true
console.log(b)
// Outputs: 'world'
console.log(c)
// Outputs: 'falsy'
console.log(d)
// Outputs: undefined

///
// Destructuring example no.9: Ignoring item
// Notice the empty space between 'j' and 'k'
let [j, , k] = ['first', 'second', 'third']

console.log(j)
// Outputs: 'first'
console.log(k)
// Outputs: 'third'
```

There is one important thing about destructuring you need to know. The order of variables and values matters. There is no way to specify what value should be assigned to what variable when you use destructuring. JavaScript solves this puzzle by simply assigning the first value (item, or property) to the first variable, second to the second and so on.

This means one thing. When you want to change the order in which values are assigned you must change the order in which you declare variables. For example, let's say you want to declare variable `x` with the second value and variable `y` with the first. Then, you must declare the variable `y` as first and variable `x` as second.

## Default parameters and values

In ES6, and later versions of JavaScript, you can declare parameters with default values. Then, if there is no value, or the value is `undefined`, JavaScript will automatically use the default value you provided. You already saw default values in action, with variables, in the previous section about destructuring (code example no.7).

However, default values goes beyond variables. You can use them also with parameters when you work with functions, or methods. This can be very useful because it can help you avoid unnecessary errors. Imagine you have a function that requires one parameter. What will happen if you forget to pass it when you call the function?

It will fail, unless you declared a variable with some fallback inside that function. This is how you would solve this potential issue in the old days. Now, with ES6, you can skip that fallback variable and use default parameter instead. Then, if you forget to call the function with required argument it not fail. It will use the default value.

When you want to use default parameters, you use the same syntax as you saw in the example with destructuring (code example no.7 and code example no.1 below). You specify the name of the parameter and follow it by equal sign (`=`) followed by the default value - `function foo(parameter = 'default value')` (code example no.2).

```
///
// Default parameters and values example no.1: Variable and destructuring
// The 'foo' and 'bar' are default values for a and b.
let [a = 'foo', b = 'bar'] = ['Tom']

console.log(a)
// Outputs: 'Tom' - first item in the array
console.log(b)
// Outputs: 'Bar' - default value because array has only 1 item

///
// Default parameters and values example no.2: Functions
// Set the default value of name parameter to 'Anonymous'
function greet(name = 'Anonymous') {
  console.log(`Hello ${name}. How are you doing?`)
}

// Calling with argument
greet('Anthony')
// Outputs: 'Hello Anthony. How are you doing?'

// Calling without argument
greet()
// Outputs: 'Hello Anonymous. How are you doing?'

// The old way
function greet(name) {
  // Ensure there is always something to be used as a name
  var fallback = (typeof name === 'undefined') ? 'Anonymous' : name

  console.log('Hello ' + fallback + '. How are you doing?')
}

// Calling with argument
greet('Anthony')
// Outputs: Hello Anthony. How are you doing?

// Calling without argument
greet()
// Outputs: Hello Anonymous. How are you doing?
```

## Epilogue: ES6, ES7, ES8 & Writing Modern JavaScript Pt2

Congratulations! You've just finished the second part of ES6, ES7, ES8 & Writing Modern JavaScript series. This means that you now know everything you need about template literals, destructuring and default parameters and values. These ES6 features will no longer puzzle you. From now, you will use them in your projects with absolute confidence.
What's next?

In the next part, you will learn about features such as spread and rest operators, object literals, new loops and much more. This will help you get one step closer to mastering ES6, ES7, ES8 and writing modern JavaScript. Until then, walk through what you've learned today and invest some of your time in practice. Remember, the best way to learn anything is by doing. So, now go and write some code!

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Part 1]: https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt1/
<!-- [Part 3]: (https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt3/) -->
[string interpolation]: https://en.wikipedia.org/wiki/String_interpolation#JavaScript
[exception]: https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt1/
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
