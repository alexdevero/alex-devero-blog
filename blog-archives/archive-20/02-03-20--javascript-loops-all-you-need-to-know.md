# JavaScript Loops - All You Need to Know
JavaScript loops are a great way to execute a block of code repeatedly. In this tutorial, you will learn about all loops, the `for`, `while`, `do...while`, `for...in` and `for...of`, and how to use each of them. You will also learn about the problem with infinite loops and what to watch out for.
<!--more-->
<!--
Table of Contents:
## Introduction to JavaScript loops
## For loop
### i++ vs ++i
## While loop
## Do...while loop
## For...in loop
## For...of loop
## Infinite Loops
## Conclusion: JavaScript Loops
-->

## Introduction to JavaScript loops

When you write code, there are times when you want to do something repeatedly. You can this done in many ways. For example, you can write that block of code over and over again. The downside of this approach is that it is neither scalable nor effective. It can also make maintenance a nightmare.

Another option is to put the code you want to execute repeatedly inside [functions]. Then, you can invoke these functions whenever you want or need. This approach is much better than the first one. It is scalable, effective and also quite easy to maintain. That said, there might be a better, native, option.

This option are JavaScript loops. There are many types of JavaScript loops. All of them do basically the same thing. They help you execute code as many times as you need. All you need is to specify the code you want to execute and how many times it should be executed. Then, just pick one of the available JavaScript loops.

As I mentioned, all JavaScript loops do basically the same thing. They do specific task X times. What is different for some of these loops is the syntax. Some of these loops also use different loop mechanism. This can make some loops a better choice at specific situations. So, let's take a look at each loop so you know which one to choose.

## For loop

The `for` loop has been around for a long time. It is one of the most popular JavaScript loops, if not the most. When JavaScript developers need a loop, `for` loop is usually one of the top options. The syntax of `for` loop can be difficult to remember at the beginning. This will get better with practice. Soon, you will remember it like your name.

The syntax of `for` loop consists of a few parts. First, there is the `for` keyword that is at the beginning of the loop, and line. Next, there are parenthesis, or "head", that contains three expressions that are separated by semicolons (`;`): `initialize expression`, `condition expression` and `increment expression`. The increment expression is also called "final expression".

The `initialize expression` is used to define counters and also [variables]. Put simply, here is when you usually define the starting point of the loop, a number. For example, you can use the `initialize expression` to define a counter with value of `0`. This means that the loop will start at "0". You can use any name for this counter.

When you want to define some variables, along with the counter, you separate them, and also the counter, with comas: `let counter = 0, let myVar = 5`. You can use as many variables as you want. Next, the `condition expression` specifies condition under which the loop should run, or iterate/repeat.

This condition works like [if...else] statement. As long as this condition evaluates to `true` the `for` loop will run, unless you terminate it from the inside. You can use the `condition expression` to say that loop should run only six times, i.e. condition like `counter < 7` (if counter starts at `0`).

The `increment expression` is used to specify how the loop is supposed to update the counter(s) you specified in the `initialize expression`. `for` loop will execute this update at the end of each iteration. For example, you can use the `increment expression` to tell the `for` loop to increase the counter with each iteration, or to decrease it.

It is good to know that all these expressions are optional. So, yes, you could create a `for` loop with an empty head, without any of these expression. One thing to remember is that when you decide to omit some expression you still need to add a semicolon. In other words, `for` loop will always contain two semicolons, regardless of how many expressions are there.

After the head of `for` loop, the parenthesis with expressions, come curly brackets. The code you want the loop to execute belongs between those brackets. That's for the theory. Let's take a look at some code examples.

```JavaScript
// For loop syntax
// 1) the "for" keyword
// 2) then head with 3 expressions inside parenthesis:
// initializeExpression; conditionExpression; incrementExpression
// 3) curly braces with code that should be executed
// if condition is true
// NOTE: Remember to separate
// each expression with semicolons
for (initializeExpression; conditionExpression; incrementExpression) {
  // code to execute
}


// A simple for loop to iterate from 1 to 5
// 1) the "i" is a counter, starting point of the loop
// it says that the loop should start at 0
// 2) the "i < 6" condition says that loop will run as along
// as the "i" counter is smaller than 6 (< 6: "i" starts on 0, not 1)
// 3) the "i++" says that "i" counter should increment
// at the end of each iteration
for (let i = 0; i < 6; i++) {
  // log the current value of "i" counter
  console.log(i)
}
// 0
// 1
// 2
// 3
// 4
// 5


// Simple for loop to iterate from 5 to 1
// 1) the "x" is a counter, starting point of the loop
// it says that the loop should start at 5
// 2) the "x >= 0" condition says that loop will run as along
// as the "x" counter is bigger or equal to 0
// (>= 0: "x" starts on 5, we want 5 iterations so 0 must be included)
// 3) the "x--" says that "x" counter should decrement
// at the end of each iteration
for (let x = 5; x >= 0; x--) {
  // log the current value of "x" counter
  console.log(x)
}
// 5
// 4
// 3
// 2
// 1
// 0


// Use for loop to iterate over an array
// 1) the "y" is a counter, starting point of the loop
// it says that the loop should start at 0
// 2) the "arrLength" is a variable (optional)
// 3) the "y < myArray.length" condition says that loop will run as along
// as the "y" counter is smaller length of the array
// smaller? array starts on index 0, array with 1 item has length of 1, not 0
// 4) the "y++" says that "y" counter should increment
// at the end of each iteration
const myArray = ['loops', 'statements', 'keywords', 'variables', 'scope']

for (let y = 0; y < myArray.length; y++) {
  // log the current value of "y" counter
  // and also item inside the myArray at current index
  console.log(y, myArray[y])
}
// 0 'loops'
// 1 'statements'
// 2 'keywords'
// 3 'variables'
// 4 'scope'


// Use for loop to iterate over an array and using variables
// 1) the "c" is a counter, starting point of the loop
// it says that the loop should start at 0
// 2) the "arrLength" is a variable
// that will store the length of "myArray"
// 3) the "c < arrLength" condition says that loop will run as along
// as the "c" counter is smaller length of the array
// instead of "myArray.length" we can now use the "arrLength" variable
// 4) the "c++" says that "c" counter should increment
// at the end of each iteration
const myArray = ['loops', 'statements', 'keywords', 'variables', 'scope']

for (let c = 0, let arrLength = myArray.length; c < arrLength; c++) {
  // log the current value of "y" counter
  // and also item inside the myArray at current index
  console.log(c, myArray[c])
}
// 0 'loops'
// 1 'statements'
// 2 'keywords'
// 3 'variables'
// 4 'scope'


// Omitting some expressions no.1: no initialization expression
// Create variable for initialization expression
let d = -5

// 1) Omit the initialization expression, BUT add the semicolon
// before the condition expression as usually
// 2) the "d < 4" condition says that loop will run as along
// as the "d" counter is smaller than 4
// 3) the "d++" says that "d" counter should increment
// at the end of each iteration
for (; d < 4; d++) {
  // Log the current value of "d" counter
  console.log(d)
}
// -5
// -4
// -3
// -2
// -1
// 0
// 1
// 2
// 3


// Omitting some expressions no.2: no condition expression
// 1) the "f" is a counter, starting point of the loop
// it says that the loop should start at 6
// 2) Omit the condition expression, BUT add the semicolon
// at the end of initialization and before the increment expression as usually
// 3) the "f--" says that "f" counter should decrement
// at the end of each iteration
for (let f = 6;; f--) {
  // Log the current value of "f" counter
  console.log(f)

  // Terminate the loop when "f" counter reaches 0
  // If you don't terminate loop without condition
  // or with condition that never happens
  // it will create an infinite loop, i.e. the loop will run forever
  if (f === 0) break
}
// 6
// 5
// 4
// 3
// 2
// 1
// 0


// Omitting some expressions no.3: no increment expression
// 1) the "g" is a counter, starting point of the loop
// it says that the loop should start at 0
// 2) the "g < 8000" condition says that loop will run as along
// as the "g" counter is smaller than 8000
// 3) Omit the increment expression, BUT add the semicolon
// at the end of condition as usually
// NOTE: This will also create an infinite loop
// because the loop doesn't update the counter
// i.e. counter will always be smaller than 8000
for (let g = 0; g < 8000;) {
  // Log the current value of "g" counter
  console.log(g)
}
// 0
// 0
// 0
// 0
// 0
// 0
// 0
// ... infinite loop
```

### i++ vs ++i

One more thing about `for` loops. You may have heard that there is a difference between using `i++` and `++i` as the increment expression. Well, sort of. Some JavaScript developers think that there is a difference in performance. There is none. In programming languages such as C, there is a difference in performance when you use `i++` and `++i`.

This doesn't apply to JavaScript. It doesn't make any performance difference if you use `i++` and `++i` in JavaScript loops, namely `for` loops. The only difference between `i++` and `++i` is that `i++` returns the value of `i` before it increments it, while `++i` returns the value of `i` after it increments it.

From the view of functionality, there is also no difference. Whether you use `i++` or `++i`, `for` loop will work the same in both cases. So, choosing between `i++` and `++i` is basically a matter of personal taste. It will neither improve nor break your code. The same applies to `i +=`. It doesn't matter.

```JavaScript
// For loop with "i++"
for (let i = 0; i < 4; i++) {
  console.log(i)
}
// 0
// 1
// 2
// 3


// For loop with "++i"
for (let i = 0; i < 4; ++i) {
  console.log(i)
}
// 0
// 1
// 2
// 3


// For loop with "i += 1"
for (let i = 0; i < 4; i += 1) {
  console.log(i)
}
// 0
// 1
// 2
// 3
```

## While loop

The `while` loop is another member of JavaScript loops. The `while` loop might be more interesting for some JavaScript developers because their syntax is much easier. This is especially true if you compare it with the syntax of `for` loops, we discussed previously. About the syntax of `while` loops.

Every `while` loop starts with `while` keyword. This keyword is followed by parenthesis that contains condition under which the `while` loop should be executed. Similarly to `for` loop, `while` loop is executed as long as the condition you specified evaluates to `true`. Once it evaluates to `false`, the `while` loop is terminated.

These parenthesis, with condition, are followed by curly braces that contains the code you want to execute. And, that's it. The syntax of `while` loop is really that simple. Let's take a look at some code examples to better illustrate how `while` loops look and work.

```JavaScript
// While loop syntax
// 1) the "while" keyword
// 2) then parenthesis with condition
// 3) curly braces with code
// that should be executed if condition is true
while (someCondition) {
  // code to execute if someCondition is true
}


// A simple while loop
// Declare variable with number of iterations
let numOfIterations = 0

// Create while loop
// Use "numOfIterations" in a condition:
// Iterate if "numOfIterations" is smaller or equal 4
// This means the while loop will run 5x
while (numOfIterations <= 4) {
  console.log('While...')

  // Increase the value of "numOfIterations"
  // It is necessary to change the "numOfIterations" variable
  // used in condition so there is moment when the while will stop
  ++numOfIterations
}
// 'While...'
// 'While...'
// 'While...'
// 'While...'
// 'While...'


// While loop and iterating over an array
// Declare variable with array of names
const arrOfNames = ['Sandy', 'Tony', 'Timothy', 'Andrew']

// Declare variable with number of iterations
let numOfIterations = 0


// Create while loop
// Use "numOfIterations" and length of "arrOfNames" in a condition:
// iterate if numOfIterations is smaller or equal 4
while (numOfIterations < arrOfNames.length) {
  // Log name on an index matching the current value of "numOfIterations"
  console.log(arrOfNames[numOfIterations])

  // increase the value of "numOfIterations"
  ++numOfIterations
}
// 'Sandy'
// 'Tony'
// 'Timothy'
// 'Andrew'
```

## Do...while loop

The third member of JavaScript loops is `do...while` loop. This loop is very similar to the `while` loop we just discussed. There are two differences. First, there is a new `do` keyword. The block of code for the while loop follows after this keyword. Then, there is the `while` keyword and condition wrapped with parenthesis.

There is no block of code after the `while` loop. The second difference is that the code inside the block, that follows after the `do`, is evaluated before the `while` condition is evaluated. In other words, the code in block will always run at least once, even if the condition for the `while` loop evaluates to `false`.

If the `while` condition evaluates to `true`, the loop will run again and execute the code block after the `do`. This behavior makes the `do...while` loop a good choice if you need to execute some code at least once, no matter the condition. Let's take a look at some examples.

```JavaScript
// Do...while syntax
do {
  // code to execute
} while (condition)


// A simple do...while loop
// This loop will run, and execute the code,
// once even though the condition is false right from the start
// Declare "myCounter" variable
let myCounter = 0

// Create do...while loop
do {
  // Log the value of "myCounter" variable
  console.log(myCounter)
} while (myCounter < 0) // run if "myCounter" is smaller than 0
// 0
```

## For...in loop

The fourth member of JavaScript loops is `for...in` loop. This loop is usually used to through properties of [objects]. The syntax is somewhere between `for` and `while`. It starts with `for` keyword. This is then followed by parenthesis containing a variable, `in` keyword and name of an object you want to iterate over.

During each iteration, one property from the object, you specified, is assigned to the variable and the code inside the block is executed. This loop continues until all properties of the object are "processed".

```JavaScript
// For...in syntax
for (myVariable in myObj) {
  // code to execute
}


// A simple for...in
// Create an object with some data
const user = {
  firstName: 'Johny',
  lastName: 'Zane',
  education: 'college',
  job: 'programmer'
}

// Create for...in loop
// 1) "prop" is the variable each property
// will be assigned to during every iteration
// 2) "user" is the name of the object we want to loop through
for (let prop in user) {
  console.log(`key is: ${prop}; value is: ${user[prop]}.`)
}
// 'key is: firstName; value is: Johny.'
// 'key is: lastName; value is: Zane.'
// 'key is: education; value is: college.'
// 'key is: job; value is: programmer.'
```

## For...of loop

The `for...of` is the last of JavaScript loops we will talk about in the tutorial. The `for...of` looks and works almost like the `for...in`. There are two main differences between these two loops. The first difference is that the `for...of` uses `of` instead of `in` keyword inside the parenthesis.

The second difference is that the `for...of` loop is designed to loop through iterable objects. It is important to mention that "iterable object" is not the same as "objects". Objects are objects, "things" with properties, key/value pairs. Iterable objects are arrays, maps, sets, `arguments` object inside functions and methods, strings, etc.

So, while the `for...in` loop works objects, the `for...of` loop works with arrays, maps, sets, strings, arguments atc. When you need to loop thorough any of these use `for...of`, not `for...in`. Or, use other JavaScript loops, such as `for` loop. Other than these two differences, `for...of` and `for...in` are the identical.

About the variable. Let's say you want to use `for...of` loop to iterate over some iterable object, like an array. Then, during each iteration, one item from that array will be assigned to the variable you specify before the `of` keyword. And, as usually, the code inside the block is executed. `for...of` loop continues until there are no items inside the iterable object left to be processed.

```JavaScript
// For...of loop syntax
for (myVariable of myArray) {
  // code to execute
}


// A simple for...of loop no.1: iterate over an array
// Create an object with some data
const languages = ['JavaScript', 'C++', 'Java', 'Python', 'Perl']

// Create for...of loop
// 1) "item" is the variable each item
// will be assigned to during every iteration
// 2) "languages" is the name of the iterable object, now array,
//  we want to loop through
for (let item of languages) {
  console.log(`Current item is: ${item}.`)
}
// 'Current item is: JavaScript.'
// 'Current item is: C++.'
// 'Current item is: Java.'
// 'Current item is: Python.'
// 'Current item is: Perl.'


// A simple for...of loop no.2: iterate over a string
const myWord = 'Camel'

for (let char of myWord) {
  console.log(char)
}
// 'C'
// 'a'
// 'm'
// 'e'
// 'l'
```

## Infinite Loops

When it comes to JavaScript loops, there is always some chance of creating an infinite loop. Put simply, infinite loop is a loop that never ends. This happens when the condition used in a loop always evaluates to `true`, never to `false`. The only way to avoid this is by paying a good attention every time you work with JavaScript loops.

This is especially true for `while` loops. The `while` loop makes it very easy to forget to ensure the condition will sooner or later evaluate to `false` and the loop will stop. So, pay attention to the code you write and watch for typos. Or, lower the chance of running into infinite loops by replacing `while` loop with other JavaScript loops.

```JavaScript
// WRONG: missing update of variable used in condition
// This will create infinite loop
let numOfIterations = 0

// Create while loop
while (numOfIterations < 10) {
  // Log current value of "numOfIterations"
  console.log(numOfIterations)
  /* <= problem */
}


// CORRECT: update variable used in condition
// Infinite loop
let numOfIterations = 0

// Create while loop
while (numOfIterations < 10) {
  // Log current value of "numOfIterations"
  console.log(numOfIterations)

  // Update "numOfIterations"
  numOfIterations++ /* <= fixed */
}


// WRONG: wrong increment expression (i-- instead of i++)
// This will create infinite loop
for (let i = 0; i < 10; i-- /* <= problem */) {
  // Log current value of "i"
  console.log(i)
}


// CORRECT: use correct increment expression,
// based on the desired result
for (let i = 0; i < 10; i++ /* <= fixed */) {
  // Log current value of "i"
  console.log(i)
}
```

## Conclusion: JavaScript Loops

JavaScript loops offer a great way to run block of code multiple times. This tutorial helped you learn about all JavaScript loops you can use, and how to use them. These loops are `for`, `while`, `do...while`, `for...in` and `for...of`. You've also learned about the problem with infinite loops and what to watch out for. I hope you enjoyed this tutorial and learn something new.

[xyz-ihs snippet="thank-you-message"]

<!-- ## Links -->
[functions]: https://blog.alexdevero.com/javascript-functions-pt1/
[if...else]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/if...else
[variables]: https://blog.alexdevero.com/javascript-variables-introduction/
[objects]: https://blog.alexdevero.com/javascript-objects-pt1/

<!--
### Meta:
-
-->

<!--
### Resources:
-
-->
