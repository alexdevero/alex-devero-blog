# JavaScript Switch Statement - All You Need to Know

Switch statement is one of the oldest features of JavaScript. Yet, it is not used as often as `if...else`. This is unfortunate. Switch statement can sometimes do a better job and make your code more readable. This tutorial will teach you what JavaScript switch statement is, how to use it and when.
<!--more-->
<!--
Table of Contents:
## Introduction to switch statement
## The case block
### The default case
### Grouping cases
## The break statement
### Omitting break statement
## When to use switch statement
## Conclusion: JavaScript Switch Statement
-->

## Introduction to switch statement

Every JavaScript switch statement must have three things in order to work. The first thing is the `switch` keyword. Every switch statement has to start with this keyword. The second thing is an expression you want to compare with case value. You will learn more about case blocks in "Case blocks" section.

The expression goes between the parenthesis, that follow after the `switch` keyword. What follows next are curly braces with block of code. This block of code is the body of a switch statement.

```JavaScript
// Switch statement syntax
switch (expression) {
  // body with block of code
}
```

## The case block

JavaScript switch statement works in a similar way to `if....else` statement. In case of `if....else`, there is some condition and you "test" if that condition is either `true` or `false`. Then, you can execute code specific for each boolean value, or one of them. Switch statement uses different syntax, but the result is same.

What JavaScript switch statement does is it operates with two parts. The first one is the expression you want to check. The second part is a case block. This, the case block, is also the third thing you need to make switch work. Every case block you add to a switch statement should have some value.

A bit how it works. When you execute a switch statement, it will do two things. First, it will take the expression you passed in parenthesis, that follow after the `switch` keyword. Second, it will compare this expression with values you specified for each statement. Now, let's talk about the case blocks.

A case block consists of two parts. First, there is the `case` keyword. This keyword defines a case block. This keyword is then followed by some value, colons and code you want to execute if switch expression matches the value a case. This can be a little bit confusing.

Case blocks don't use curly braces. There are only colons at the end of the line. Then, on the next line is the code you want to execute if the case is used. That is, if the switch expression matches the value you specified after the `case` keyword.

When you want to add a new case block you add it to the body of switch statement, inside the curly braces. When it comes to case blocks, there is no limit to how many of them you can use. You can add as many case blocks as you want.

```JavaScript
// Switch statement with one case block
switch (expression) {
  case value:
    // Do something if 'value' matches the 'expression'
    break // Stop the execution of switch statement
}


// Switch statement with multiple case blocks
switch (expression) {
  case value:
    // Do something if 'value' matches the 'expression'
    break // Stop the execution of switch statement
  case firstDifferentValue:
    // Do something if 'firstDifferentValue' matches the 'expression'
    break // Stop the execution of switch statement
  case secondDifferentValue:
    // Do something if 'secondDifferentValue' matches the 'expression'
    break // Stop the execution of switch statement
  case thirdDifferentValue:
    // Do something if 'thirdDifferentValue' matches the 'expression'
    break // Stop the execution of switch statement
}


// Example with calendar
// Create expression to check
const today = 'Wednesday'

// Create a switch statement
// and pass value of 'today' variable as an argument
switch (today) {
  case 'Monday':
    // If value of today is 'Monday' do following
    console.log('It\'s Monday.')
    break // Stop the execution of switch statement

  case 'Tuesday':
    // If value of today is 'Tuesday' do following
    console.log('It\'s Tuesday.')
    break // Stop the execution of switch statement

  case 'Wednesday':
    // If value of today is 'Wednesday' do following
    console.log('It\'s Wednesday.')
    break // Stop the execution of switch statement

  case 'Thursday':
    // If value of today is 'Thursday' do following
    console.log('It\'s Thursday.')
    break // Stop the execution of switch statement

  case 'Friday':
    // If value of today is 'Friday' do following
    console.log('It\'s Friday.')
    break // Stop the execution of switch statement

  case 'Saturday':
    // If value of today is 'Saturday' do following
    console.log('It\'s Saturday.')
    break // Stop the execution of switch statement

  case 'Sunday':
    // If value of today is 'Sunday' do following
    console.log('It\'s Sunday.')
    break // Stop the execution of switch statement
}

// Output:
// 'It\'s Wednesday.'


// Note 1:
// Empty lines between case blocks
// are just to improve readability of the code.


// Note 2:
// You could also pass the string
// to switch statement directly: switch ('Monday') { ... }
```

### The default case

We discussed that every case block should have some value. There is one exception to this rule. The only exception here is a default case. This default case doesn't need any value. This also means one thing. If any preceding case either fails or doesn't stop the execution of the switch statement the default will be executed.

The purpose of default case is to serve as a backup. It should be executed when, for whatever reason, neither of cases in a switch match the expression passed to switch as an argument. One thing to remember. The default case will be also applied if any other case matches the expression, but it didn't stop the execution of switch statement.

So, make sure you know what is the result you want. Do you want to use the default case only when no other case matches the expression passed to switch as an argument? Or, do you want to use it regardless? If you want the first to happen, then make sure to stop the switch statement right after it executes the code you want it to execute (more about this in "Break statement" section).

Creating a default case is similar to a normal case with value. In case of default case, you start with `default` keyword, instead of `case`. This keyword is then followed by colons and block of code. Remember that this code will be executed by default, either if no case matches or if no case block stops the execution of switch statement.

```JavaScript
// Create switch statement
switch (expression) {
  case value:
    // Do something if 'value' matches the 'expression'
    break // Stop the switch statement

  default:
    // Do something if either no case value matches the 'expression'
    // or if none of the cases stops the execution of switch statement
}


// Example with calendar and default case
// Create expression to check
const today = 'Who knows.'

// Create a switch statement
// and pass value of 'today' variable as an argument
switch (today) {
  case 'Monday':
    // If value of today is 'Monday' do following
    console.log('It\'s Monday.')
    break // Stop the execution of switch statement

  case 'Tuesday':
    // If value of today is 'Tuesday' do following
    console.log('It\'s Tuesday.')
    break // Stop the execution of switch statement

  case 'Wednesday':
    // If value of today is 'Wednesday' do following
    console.log('It\'s Wednesday.')
    break // Stop the execution of switch statement

  case 'Thursday':
    // If value of today is 'Thursday' do following
    console.log('It\'s Thursday.')
    break // Stop the execution of switch statement

  case 'Friday':
    // If value of today is 'Friday' do following
    console.log('It\'s Friday.')
    break // Stop the execution of switch statement

  case 'Saturday':
    // If value of today is 'Saturday' do following
    console.log('It\'s Saturday.')
    break // Stop the execution of switch statement

  default:
    // If no other case matches the expression
    // use the default and assume the day is Sunday
    console.log('It\'s Sunday.')
}

// Output:
// 'It\'s Sunday.'
```

Notice that `break` statement is not necessary in `default` case. This is because the purpose of `break` statement is to stop the execution of switch. The `default` case is the last case that will be executed. When switch encounters the `default` case it will stop executing itself automatically. So, there is no need for `break`.

### Grouping cases

One interesting thing on JavaScript switch statement cases is that you can group them together. This can be helpful when you want to check for two different conditions and execute the same code. Otherwise, you would have to create two cases and copy and paste your code from one case to another.

Grouping two or more cases is simple and quick. First, you have to put these cases together, literally. All items must go in sequence, one after the other. Second, you must omit the case block in all cases that precede the last in the group. Only the last case in the group will have a case block.

```JavaScript
// Example of switch statement with grouped cases
const language = 'JavaScript'

// Create switch statement
switch (language) {
  // This is the beginning of the first group of cases
  // The 'This is a loosely typed language.' message
  // will be printed for if language is equal to 'JavaScript',
  // 'Pearl', 'Python' or 'Ruby'
  case 'JavaScript':
  case 'Pearl':
  case 'Python':
  case 'Ruby':
    console.log('This is a loosely typed language.')
    break
  // This is the end of the first group of cases

  // This is the beginning of the second group of cases
  // The 'This is a strongly typed language.' message
  // will be printed for if language is equal to 'C',
  // 'Go' or 'Java'
  case 'C':
  case 'Go':
  case 'Java':
    console.log('This is a strongly typed language.')
    break
  // This is the end of the second group of cases

  // This is a normal separate case block
  case 'English':
    console.log('This is not a programming language.')
    break

  default:
    console.log('This language is unknown.')
}

// Output:
// 'This is a loosely typed language.'
```

## The break statement

By default the switch statement will stop only after it executed all code inside it. This may not be what you want. You may to stop it right after a value of some case matches the expression you passed to switch and its code block is executed. You don't want the switch to continue to other case, including the default.

The easiest way to do this is by using `break` statement. You've already seen this statement a couple of times on previous examples. Now, it's time to finally talk about it. Let's say that value of some case matches the expression you passed to switch. Then, switch will automatically start executing the code inside this case.

When this happens switch also looks for any `break` statements inside that case. If it finds any `break` statement it immediately stops execution of the case inside which it is. It also stops execution of the whole switch statement. Otherwise, it will continue to other cases, including the default case until there is no code left.

```JavaScript
// Example 1: using the 'break' statement
// Create switch statement that stops
// when any case matches the expression
switch (expression) {
  case value:
    // Do something if 'value' matches the 'expression'
    break // Stop the execution of switch statement

  case value:
    // Do something if 'value' matches the 'expression'
    break // Stop the execution of switch statement

  default:
    // Do something if no case matches the 'expression'
}


// Example 2: omitting the 'break' statement
// Create switch statement that doesn't stop
// when some case matches the expression
switch (expression) {
  case value:
    // Do something if 'value' matches the 'expression'
    // and then continue to other cases

  case value:
    // Do something if 'value' matches the 'expression'
    // and then continue to default case

  default:
    // Do something if no case matches the 'expression'
}
```

### Omitting break statement

The `break` statement is not required. This means two things. One, JavaScript will not throw an error if you forget it. Two, you can omit it when you want in order to get the result you want. For example, you can omit it in one case block if you want the statement to continue executing and add it to another to stop the execution.

The result will be following. The switch statement will execute the code inside the first case that matches. Then, it will continue to other cases and executes as well. Remember that these subsequent cases don't have to match the expression! Switch will execute these subsequent cases no matter what their values are.

The only way to stop execution of a switch is to put the `break` statement in one of the subsequent cases. Otherwise, it will execute all subsequent cases until it reaches the end of itself.

```JavaScript
// Create switch statement that executes multiple cases
switch (3) {
  case 1:
    console.log('Value is 1.')
    break // Stop the execution of switch statement
    // Note: this break will not be applied
    // because the value is 1 and expression is 3

  case 2:
    console.log('Value is 2.')

  case 3:
    // Value is 3 so this case will be exceed
    console.log('Value is 3.')
    // break is missing so switch will continue
    // and execute any subsequent cases
    // The match between expression
    // and value of these cases doesn't matter anymore

  case 4:
    // Previous case was executed
    // and there was no break to stop the statement
    // This statement will be executed
    // even if the value doesn't match the expression
    console.log('Value is 4.')

  case 5:
    // There was no break to stop the statement
    // in previous statement so this statement
    // will also be executed
    // The value again doesn't matter
    console.log('Value is 5.')
    break // Stop the execution of switch statement

  case 6:
    // Case above contains break statement
    // so this case will not be executed
    console.log('Value is 6.')

  default:
    break
}

// Output
// 'Value is 3.'
// 'Value is 4.'
// 'Value is 5.'
```

## When to use switch statement

When is it better to use switch statement and when `if...else`? The general answer is that it depends. It mostly depends on what you like and prefer. When you compare the performance of switch and `if...else` the difference will not be significant. It could be few milliseconds, something be barely noticeable.

The main reason for using switch over `if...else` statement in some situations is usually improving code clarity and readability. Let's first talk about when to use `if...else` statement and then when switch. The `if...else` statement will probably be better if you want to do one or two match tests.

It will be also better to use `if...else` if you only want to test for truthiness, if something is either `true` or `false`. The last situation where you should use `if...else` is when you want to test different expressions for each case. If some expression is `true` or `false`, else if some other expression is `true` or `false` and so on.

This is easier to do with `if...else` statement because it is better suited to handle different expressions. Using `if...else` in this situation will probably lead to cleaner and more readable code. That was about when to use `if...else`. When to use switch are the opposite situations we just talked about.

First, use switch if the expressions you want to test is based only one integer, string or some variable value. Second, use it when you need to test multiple values, multiple case blocks. Switch tends to perform better than large `if...else`. Larger switch is often also more readable than large `if...else`.

Third and last, use switch when some cases may use the same code. Switch makes grouping case blocks easy. With `if...else` you can "group" various conditions using [binary logical operators]. This can work for a while, but it can quickly turn your code into unreadable mess.

## Conclusion: JavaScript Switch Statement

JavaScript switch statement might look quirky. It might require a some time to learn. However, it is worth it. Switch can help you make your code more readable and cleaner. I hope this tutorial helped you learn what JavaScript switch statement is, how it works and how to use it, and also when.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[binary logical operators]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators#Binary_logical_operators

<!--
### Meta:
-
-->

<!--
### Keywords:
- javascript switch statement
- switch statement
-->

<!--
### Resources:
- https://love2dev.com/blog/javascript-switch-statement/
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/switch
- https://javascript.info/switch
- https://javascript.info/ifelse
-->
