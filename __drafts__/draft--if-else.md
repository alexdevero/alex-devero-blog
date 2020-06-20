# JavaScript If Else Statement Made Simple

JavaScript if else statement is the most frequently used tools to execute code based on different conditions. This tutorial will help you understand how it works and how to use it. You will learn how to use `if`, `else`, `else if` and nested if else. You will also learn about ternary operator.
<!--more-->
<!--
Table of Contents:
-->

## The if statement

JavaScript if else statement makes it very easy to execute your code if specific conditions is truthy. Its syntax is just as a easy. It is composed of three parts. First part is `if` keyword. You use this keyword to tell JavaScript that you are about to create an if else statement.

The second part is a condition you want to test for. Condition is wrapped with parentheses and it follows the `if` keyword. This can condition can range from very simple to very complex expressions. The only thing that matters is if the result of that expression is [boolean], either `true` or `false`.

The third part is a block of code you want to execute. This block of code is surrounded by curly brackets. It follows right after the condition. Remember that this block of code will be executed only if the condition evaluates to `true`, is truthy. If it evaluates to `false`, it is falsy, the block of code will not be executed.

```JavaScript
// If else statement syntax
if (condition) {
  // block of code to execute
  // if condition is truthy
}


// Example of if statement: truthy condition
// Create a variable and assign it a number
const num = 10

// Create an if statement that checks
// if the value of num variable is bigger than 5
// this is the condition
if (num > 5) {
  // If num is bigger than 5 run the code below
  console.log('The value of num is bigger than 5.')
}

// Output:
// 'The value of num is bigger than 5.'


// Example of if statement: falsy condition
// Create a variable and assign it a string
const name = 'Rick'

// Create an if statement that checks
// if the value of name variable starts with 'A'
// this is the condition
if (name[0] === 'A') {
  // If the value of name starts with 'A' run the code below
  console.log('The value of name starts with \'A\'.')
}

// Output:
// ... nothing
```

There is one thing about if statement, and the condition, worth mentioning. You can quickly make any condition truthy or falsy, by using [logical NOT operator] (`!`). This logical operator will negate any boolean expression. It will transform `true` to `false` and `false` to `true`.

```JavaScript
// Example of if statement: using logical NOT operator
// Create a variable and assign it a number
const num = 10

// Create an if statement that checks
// if the value of num variable is NOT bigger than 5
if (!num > 5) { // <= the '!' negates the who condition
  // If num is bigger than 5 run the code below
  console.log('The value of num is bigger than 5.')
}

// Output:
// ... nothing


// Or
// Create a variable and assign it a string
const name = 'Rick'

// Create an if statement that checks
// if the value of name variable doesn't start with 'A'
// this is the condition
if (name[0] !== 'A') { // or (!(name[0] === 'A'))
  // If the value of name doesn't start with 'A' run the code below
  console.log('The value of name doesn\'t start with \'A\'.')
}

// Output:
// 'The value of name doesn\'t start with \'A\'.'
```

## The if else statement

## The else if

## Nested if else statement

## From if else statement to ternary operator

## Conclusion: [...] ...

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[boolean]: https://blog.alexdevero.com/javascript-basics-data-types-pt2/#boolean-logical-type
[logical NOT operator]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_NOT

<!--
### Meta:
-
-->

<!--
### Keywords:
- javascript if else statement
- if else statement
- javascript if else
- if else
-->

<!--
### Resources:
-
-->
