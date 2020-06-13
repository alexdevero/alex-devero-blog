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

Every JavaScript switch statement must have three things in order to work. The first thing is the `switch` keyword. Every switch statement has to start with this keyword. The second thing is an expression you want to compare with case value. You will learn more about case later.

The expression goes between the parenthesis, that follow after the `switch` keyword. What follows next are curly braces with block of code. This block of code is the body of a switch statement.

```JavaScript
// Switch statement syntax
switch (someExpression) {
  // body with block of code
}
```

## Value and case blocks

JavaScript switch statement works in a similar way to `if....else` statement. In case of `if....else`, there is some condition and you "test" if that condition is either `true` or `false`. Then, you can execute code specific for each boolean value, or one of them. Switch statement uses different syntax, but the result is same.

What switch does is it operates with two parts. The first one is the expression you want to check. The second part is a case block. This, the case block, is also the third thing you need to make switch statement work. Every case block you add to switch statement has to have some value.

A bit how it works. When you execute a switch statement, it will do two things. First, it will take the expression you passed in parenthesis, that follow after the `switch` keyword. Second, it will compare this expression with values you specified for each statement. Now, let's talk about the case blocks.

A case block consists of two parts. First, there is the `case` keyword. This keyword defines a case block. This keyword is then followed by some value, colons and code you want to execute if switch expression matches the value a case. This can be a little bit confusing.

Case blocks don't use curly braces. There are only colons at the end of the line. Then, on the next line is the code you want to execute if the case is used. That is, if the switch expression matches the value you specified after the `case` keyword.

When you want to add a new case block you add it to the body of switch statement, inside the curly braces. When it comes to case blocks, there is no limit to how many of them you can use. You can add as many case blocks in a switch statement as you want.

```JavaScript
// Switch statement with one case block
switch (someExpression) {
  case 'someValue':
    // do something
    break
}

// Switch statement with multiple case blocks
switch (someExpression) {
  case 'someValue':
    // do something
    break
  case 'someOtherValue':
    // do something
    break
}
```

### Default case

The only exception here is a `default` case. This case doesn't need any value. This also means one thing. It will used if any preceding case will either fail or will not stop the execution of the switch statement.

## Labels

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
