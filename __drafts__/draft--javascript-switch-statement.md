# JavaScript Switch Statement - All You Need to Know

Switch statement is one of the oldest features of JavaScript. Yet, it is not used as often as `if...else`. This is unfortunate. Switch statement can sometimes do a better job and make your code more readable. This tutorial will teach you what JavaScript switch statement is, how to use it and when.
<!--more-->
<!--
Table of Contents:
## h2
### h3
### h3
## h2
## Conclusion: [...] ...
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

## Case blocks

JavaScript switch statement works in a similar way to `if....else` statement. In case of `if....else`, there is some condition and you "test" if that condition is either `true` or `false`. Then, you can execute code specific for each boolean value, or one of them. Switch statement uses different syntax, but the result is same.

What switch does is it operates with two parts. The first one is the expression you want to check. The second part is a case block. This, the case block, is also the third thing you need to make switch statement work. Every case block you add to a switch statement should have some value.

A bit how it works. When you execute a switch statement, it will do two things. First, it will take the expression you passed in parenthesis, that follow after the `switch` keyword. Second, it will compare this expression with values you specified for each statement. Now, let's talk about the case blocks.

A case block consists of two parts. First, there is the `case` keyword. This keyword defines a case block. This keyword is then followed by some value, colons and code you want to execute if switch expression matches the value a case. This can be a little bit confusing.

Case blocks don't use curly braces. There are only colons at the end of the line. Then, on the next line is the code you want to execute if the case is used. That is, if the switch expression matches the value you specified after the `case` keyword.

When you want to add a new case block you add it to the body of switch statement, inside the curly braces. When it comes to case blocks, there is no limit to how many of them you can use. You can add as many case blocks in a switch statement as you want.

```JavaScript
// Switch statement with one case block
switch (expression) {
  case value:
    // Do something if 'value' matches the 'expression'
    break // stop execution of switch
}

// Switch statement with multiple case blocks
switch (expression) {
  case value:
    // Do something if 'value' matches the 'expression'
    break // stop execution of switch
  case differentValue:
    // Do something if 'differentValue' matches the 'expression'
    break // stop execution of switch
}

// Example with calendar
// Create some expression to check
const today = 'Monday'

// Create a switch statement
// and pass value of 'today' variable as an argument
switch (today) {
  case 'Monday':
    // If value of today is 'Monday' do following
    console.log('It\'s Monday.')
    break // stop execution of switch

  case 'Tuesday':
    // If value of today is 'Tuesday' do following
    console.log('It\'s Tuesday.')
    break // stop execution of switch

  case 'Wednesday':
    // If value of today is 'Wednesday' do following
    console.log('It\'s Wednesday.')
    break // stop execution of switch

  case 'Thursday':
    // If value of today is 'Thursday' do following
    console.log('It\'s Thursday.')
    break // stop execution of switch

  case 'Friday':
    // If value of today is 'Friday' do following
    console.log('It\'s Friday.')
    break // stop execution of switch

  case 'Saturday':
    // If value of today is 'Saturday' do following
    console.log('It\'s Saturday.')
    break // stop execution of switch

  case 'Sunday':
    // If value of today is 'Sunday' do following
    console.log('It\'s Sunday.')
    break // stop execution of switch
}

// Note 1:
// Empty lines between case blocks
// are just for improving readability of the code.

// Note 2:
// You could also pass the string
// to switch statement directly: switch ('Monday') { ... }
```

### Default case

We discussed that every case block should have some value. There is one exception to this rule. The only exception here is a default case. This default case doesn't need any value. This also means one thing. If any preceding case either fails or doesn't stop the execution of the switch statement the default will be executed.

The purpose of default case is to serve as a backup. It should be executed when, for whatever reason, neither of cases in a switch statement match the expression passed to switch as an argument. One thing to remember. The default case will be also applied if any other case matches the expression, but it didn't stop the execution of switch statement.

So, make sure you know what you are trying to achieve. Do you want to use the default case only when no other case matches the expression passed to switch as an argument? Or, do you want to use it regardless? If you want the first to happen, then make sure to stop the switch statement right after it executes the code you want it to execute (more about this in "Break statement" section).

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
    break // Stop the switch statement
}
```

## Break statement

## Conclusion: [...] ...

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[]:

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
