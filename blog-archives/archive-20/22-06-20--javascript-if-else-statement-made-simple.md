# JavaScript If Else Statement Made Simple

JavaScript if else statement makes it easy to execute code based on different conditions. This tutorial will help you learn all you need to know about if else statement. You will learn how to use `if`, `else`, `else if` and nested if else. You will also learn about ternary operator and much more.
<!--more-->
<!--
Table of Contents:
## The if statement
### Negating the condition
## The else statement
## The else if
## The if else statement and multiple conditions
### Multiple conditions and else if
### Else if or multiple ifs
## Nested if else statements
### Word of caution
## Omitting the curly brackets
## Ternary operator
### Multiple ternary operators
## Conclusion: JavaScript If Else Statement Made Simple
-->

## The if statement

JavaScript if else statement makes it very easy to execute your code if specific conditions is truthy. Its syntax is just as easy. It is composed of three parts. The first part is `if` keyword. You use this keyword to tell JavaScript that you are about to create an if else statement.

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

// Create an if statement that tests
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

// Create an if statement that tests
// if the value of name variable starts with 'A'
// this is the condition
if (name[0] === 'A') {
  // If the value of name starts with 'A' run the code below
  console.log('The value of name starts with \'A\'.')
}

// Output:
// ... nothing
```

### Negating the condition

There is one thing about if statement, and the condition, worth mentioning. You can quickly make any condition truthy or falsy, by using [logical NOT operator] (`!`). This logical operator will negate any boolean expression. It will transform `true` to `false` and `false` to `true`.

```JavaScript
// Example of if statement: using logical NOT operator
// Create a variable and assign it a number
const num = 10

// Create an if statement that tests
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

// Create an if statement that tests
// if the value of name variable doesn't start with 'A'
// this is the condition
if (name[0] !== 'A') { // or (!(name[0] === 'A'))
  // If the value of name doesn't start with 'A' run the code below
  console.log('The value of name doesn\'t start with \'A\'.')
}

// Output:
// 'The value of name doesn\'t start with \'A\'.'
```

## The else statement

Having the option execute code only when some condition is met is definitely useful. That's not all the if else statement allows you to do. You can also add code that will be executed if the condition evaluates to `false`, if it is falsy. What you need to do is to add `else` keyword and another code block right after the `if` code block.

Doing this allows you to cover both cases, truthy and falsy. If condition is truthy, the `if` code block will be executed. If it is falsy, the `else` code block will be executed.

```JavaScript
// Syntax of if else
if (condition) {
  // This is the "if" code block
  // This block of code will be executed
  // if condition is truthy
} else {
  // This is the "else" code block
  // This block of code will be executed
  // if condition is falsy
}


// Example of if else statement
// Create a variable and assign it a number
const num = 53

// Create an if statement that tests
// if the value of num variable is bigger than 5
// this is the condition
if (num >= 50) {
  // If num is bigger than or equal to 50 run the code below
  console.log('The value of num is bigger than 50.')
} else {
  // If num is smaller than 50 run the code below
  console.log('The value of num is bigger than 50.')
}

// Output:
// 'The value of num is bigger than 50.'
```

One thing about the else statement. This part of if else statement is purely optional. You don't have to use it if you don't want to, or if there is no reason to do so.

## The else if

You know how to use if else statement to execute one snippet of code when condition is truthy. You also know how to execute another when the condition is falsy. There is another thing you can do with if else statement. You can test for one condition and then check the condition, still being in the same if else statement.

This can be done with `else if`. This looks very similar to the `else` we just discussed. There are two differences. First, you have to add `if` keyword after the `else`. Second, you have to add new condition you want to test. Then, similarly to `else`, or `if`, what follows is the code block you want to execute if new condition is truthy.

```JavaScript
// Syntax of else if (or if else if statement)
if (condition) {
  // This is the "if" code block
  // This block of code will be executed
  // if condition is truthy
} else if (newCondition) {
  // This is the "else if" code block
  // This block of code will be executed
  // if the new condition is truthy
}


// Syntax of else if (or if else if statement)
if (condition) {
  // This is the "if" code block
  // This block of code will be executed
  // if condition is truthy
} else if (newCondition) {
  // This is the "else if" code block
  // This block of code will be executed
  // if the new condition is truthy
}
```

Just like with `if` statement you can use `else` statement also with `if else`. The only thing you need to watch for is always using the `else` statement, and its code block at the end.

```JavaScript
if (condition) {
  // This is the "if" code block
  // This block of code will be executed
  // if condition is truthy
} else if (newCondition) {
  // This is the "else if" code block
  // This block of code will be executed
  // if the new condition is truthy
} else {
  // This is the "else" code block
  // This block of code will be executed
  // if neither the first nor the second condition is truthy
}
```

## The if else statement and multiple conditions

The else if is a very powerful tool. It can help you create more controlled code quickly and easily. That being said, there is one thing you have to pay attention to. Let's say you have one if else statement with one `else if`. That means one `if`, one `else if` and maybe `else`.

When JavaScript executes this code, it will test the `else if` condition only if the `if` condition is falsy. If the `if` condition is truthy, JavaScript will execute its code block and then move on to the code that follows after the if else statement. It will not get to the `else if` and that new condition.

In short, JavaScript will not execute multiple blocks of code if preceding conditions are truthy. It will always execute only the code block for the first truthy condition. The rest will be ignored.

```JavaScript
// Create if else if statement
if (condition) {
  // Do something only if "condition" is truthy
} else if (newCondition) {
  // Do something only if "condition" is falsy
  // and "newCondition" is truthy

  // This "else if" block will be ignored
  // if the preceding "if" condition is truthy
} else {
  // Do something only if neither "condition"
  // nor "newCondition" are truthy

  // This "else if" block will be ignored
  // if any of the preceding condition is truthy
}
```

What if you want to test for multiple conditions and execute different snippets of code. You can do two things. First, let's suppose the code is the same. Then, you can use all the conditions as one complex condition for the first `if` block. If you also use [logical OR operator] (`||`) you can make sure that if any of these conditions applies following code block will be executed.

```JavaScript
// If statement with multiple conditions:
// using logical OR operator to test if any condition applies
if (condition || newCondition || anotherCondition) {
  // Do something if either "condition", "newCondition" or "anotherCondition" are truthy
}


// Or,
// If statement with multiple conditions
// using logical AND operator to test if all conditions apply
if (condition && newCondition && anotherCondition) {
  // Do something only if "condition", "newCondition" and "anotherCondition" are all truthy
}
```

### Multiple conditions and else if

Using logical OR operator and multiple conditions also works with `else if` statement. So, you can test for one condition and then use `else if` to test for a set of multiple conditions.

```JavaScript
// Create if else if statement
if (condition) {
  // Do something if "condition" is truthy
} else if (conditionTwo || conditionThree || conditionFour) {
  // Do something if either "conditionTwo", "conditionThree" or "conditionFour" is truthy
} else if (conditionFive && conditionFive) {
  // Do something only if "conditionFive" and "conditionFive" are both truthy
} else {
  // If no condition applies do something else
}
```

### Else if or multiple ifs

Problem might arise if you want to test for different conditions and also execute different code for each. This is something `else if`, or if else statement in general, can't help you with. The only way to do this, if you want to use if else statement, is by using two or more if statements, or if else.

```JavaScript
// Create one if statement to test for one condition
// JavaScript will execute this statement first
if (someCondition) {
  // Do one thing
}

// Then, it will execute this statement as second
if (someOtherCondition) {
  // Do something else
}

// If both apply both code blocks will be executed.
// If one, one code block will be executed. Otherwise, none.
```

## Nested if else statements

You know that you can use multiple conditions in a single `if`, or `else if`. Another thing you can do with if else statements is nesting them. Put simply, you can put one if else statement into another. This can be useful if you want to test for some conditions. Then, you want to narrow it down even more and test for another.

Some JavaScript developers like to use this to make their code more readable. Although, this might be debatable. Let's say you want to test for three conditions and all three must be truthy. One thing you do is to create one `if` statement and use logical AND operator to create a complex condition composed of multiple conditions.

The second option is to use nested if else statement. You can create one `if` statement with one of the three conditions. Next, you can create another `if` statement with second condition and put it inside the first `if` statement. Then, you can repeat this process with the third `if` statement and third condition.

```JavaScript
// Nested if else statements examples
if (condition) {
  if (anotherCondition) {
    if (yetAnotherCondition) {
      // Do something if "condition", "anotherCondition"
      // and "yetAnotherCondition" are all truthy
    }
  }
}


// Single-if alternative
if (condition && anotherCondition && yetAnotherCondition) {
  // Do something if "condition", "anotherCondition"
  // and "yetAnotherCondition" are all truthy
}
```

### Word of caution

As a mentioned, some JavaScript developers use nested if else statements to make code more readable. This may work in theory. In reality, it is very easy to go over the edge. You nest one `if` statement then another and, before you realize it, you have a deep chain of `if` statements that make your code harder to work with instead of easier.

So, don't start converting all `if` statements with complex conditions to multiple nested `if` statements. Instead, try to use line breaks to make that complex condition more readable, while sticking to one `if` statement. In the end, JavaScript doesn't treat white space and line breaks in the same way Python does.

```JavaScript
// Using line breaks to make complex condition more readable
if (
  conditionOne && conditionTwo &&
  conditionThree && conditionFour &&
  conditionFive
) {
  // Do something if all conditions apply
}

// Alternative with logical OR operator
if (
  conditionOne || conditionTwo ||
  conditionThree || conditionFour ||
  conditionFive
) {
  // Do something if all conditions apply
}


// The first example Looks better than this [nightmare]
if (conditionOne) {
  if (conditionTwo) {
    if (conditionThree) {
      if (conditionFour) {
        if (conditionFive) {
          // Do something if all conditions apply
        }
      }
    }
  }
}
```

## Omitting the curly brackets

You know that the `else`, also the `else if`, is optional. Another thing that is sometimes optional are the curly brackets surrounding the code block. Important thing is that "sometimes". Curly brackets are not required if two conditions are true. First, the code you want to execute is a one-liner.

Second, that one-liner you want to execute is on the same line as the `if` keyword and condition. If these two conditions are true you can safely omit the curly braces and that `if` statement will still work and your code will be valid. This is basically how curly brackets work in [arrow functions].

```JavaScript
// If statement without curly brackets
if (condition) // do something

// Is the same as
if (condition) {
  // do something
}
```

## Ternary operator

The syntax of if else statement is short and simple. That said, there is a way to make it even shorter. You can achieve this by using something called "ternary operator", also called "conditional operator". Ternary operator is like a shortcut for if else statement. It also works in the same way.

Similarly to if else statement, ternary operator is also composed of three parts. The first is a condition. The second and third are both expressions. The condition and first expression are separated by question mark (`?`). Second and third expression are separated by colons (`:`), `condition ? expressionOne : expressionTwo`.

If condition evaluates to `true`, the first expression is executed. If it evaluates to `false`, then evaluated is the second expression. As you can see on the example below, ternary operator can be very useful for example when you want to quickly assign a variable based on specific condition.

```JavaScript
// Ternary operator vs if else statement

// Option no.1: if else statement
// Create variable age and set it to 17
// and another variable lifeStage and leave it undefined
let age = 17
let lifeStage

// Using if to assign "lifeStage" variable a value
if (age >= 18) {
  lifeStage = 'You are an adult.'
} else {
  lifeStage = 'You are not an adult.'
}


// Option no.1: ternary operator
// Create variable age and set it to 17
let age = 17

// and another variable lifeStage and use ternary operator
// to assign it a value right away based on specific condition
let lifeStage = age >= 18 ? 'You are an adult.' : 'You are not an adult.'

// Explanation:
// If "age" is more than, or equal to, 18 the value of "lifeStage" will be 'You are an adult.'
// If "age" is less than 18 the value of "lifeStage" will be 'You are an not adult.'
```

Similarly to `if` statement, you can wrap the condition with parentheses. This can help you make your code more readable.

```JavaScript
// Ternary operator with parentheses
let age = 17

// Wrap condition with parentheses
let lifeStage = (age >= 18) ? 'You are an adult.' : 'You are not an adult.'
```

### Multiple ternary operators

Similarly to `if` statement you can also nest ternary operators. The upside is that you can create more complex logic. The downside? It can quickly reduce readability of your code. One way to counter this is by using line breaks. Still, I recommend not overusing ternary operators.

Using multiple ternary operators is easy. First, you have to create one ternary operator. After that, you replace one expression with another ternary operator. For example, `condition ? expressionOne : differentCondition ? expressionThree : expressionFour`.

This way, by replacing expressions in existing ternary operators with new ternary operators, you can use as many ternary operators as you want. Having said that, use this with caution. Otherwise, not even you will be able to read your code.

```JavaScript
// Multiple ternary operators
let age = 7

// use multiple ternary operators to assign lifeStage a value
let lifeStage = (age <= 3) ? 'infancy' :
  (age > 3 && age) <= 6 ? 'early childhood' :
  (age > 6 && age) <= 8 ? 'middle childhood' :
  (age > 8 && age) <= 11 ? 'late childhood' :
  (age > 11 && age) <= 20 ? 'adolescence ' :
  (age > 20 && age) <= 35 ? 'early adulthood' :
  (age > 35 && age) <= 50 ? 'midlife' :
  (age > 50 && age) <= 80 ? 'mature adulthood' :
  (age > 80) ? 'late adulthood' :
```

## Conclusion: JavaScript If Else Statement Made Simple

The if else statement is a great tool that can give you more control over what code should be executed and under what conditions. I hope that this tutorial made it easier for you to understand all you need to know about if else statement so you can start using it in your code.

I also hope it showed you what are some potentially dangerous things to look for and avoid. For example, too deeply nested `if` statements, or ternary operators. Now, take what you've learned today and apply it.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[boolean]: https://blog.alexdevero.com/javascript-basics-data-types-pt2/#boolean-logical-type
[logical NOT operator]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_NOT
[logical OR operator]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_OR
[arrow functions]: https://blog.alexdevero.com/javascript-arrow-functions/

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
