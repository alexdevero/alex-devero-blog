# Nullish Coalescing Operator Explained

Nullish coalescing operator is one of those features that look simple, but can be difficult to understand. This tutorial will help you learn about. It will explain what nullish coalescing operator is, you how it works and how to use it. It will also show you some gotchas and how to deal with them.

<!--more-->
<!--
Table of Contents:
-->

## The problem with logical operators

For a long time JavaScript supported only three logical operators. These operators are the [OR] (`||`), [AND] (`&&`) and [NOT] (`!`). These operators are very useful as they allow you to dynamically execute different tasks, based on current conditions. The problem is that these operators have their gotchas.

### Logical operators and truthy and falsy values

These logical operators work well with [boolean] values, in conditional statements for example. When you use these operators with different data types, JavaScript will sometimes convert those data types to booleans. This is possible because every data type in JavaScript is also either [truthy] or [falsy].

This is usually not a problem if you work with truthy values or `null` and `undefined`. The OR operator, and also AND, work very well with both, `null` and `undefined`. Problems may arise if you work with falsy values such as `0` or `""` (empty string). In that case, JavaScript will convert those values to `false`.

When these values are converted to `false` logical operators has no other option than to return the default values. This is something you may neither expect nor desire. Let's illustrate this on one simple example. Let's say you want to access some object property only if it has some value. If it doesn't have any value you want to use some default. You can do this with the logical OR operator.

What happens if that property has value, but that value is falsy? Just to remind you, falsy values in JavaScript are `false`, `0`, `-0`, `0n`, `""` (empty string), `null`, `undefined` and `NaN`. Any other value than these is truthy. When you use OR operator to check if the value exists, it will convert that value to boolean. If the value is falsy the result will be `false`.

What if the value exists, but it 0 or ""? In that case, JavaScript convert that value to `false` and OR operator will return your default value. It doesn't matter there is value actually some value. The only thing that matters for OR operator is that the value is falsy.

```JavaScript
const user = {
  name: 'Justin Lambert',
  age: 0, // 0 is a falsy value
  jobTitle: '', // Empty string is a falsy value
  hobbies: null // Null is also a falsy value
}

// Log the value of name property
// this will work as you expect
console.log(user.name || 'Anonymous')
// Output:
// 'Justin Lambert'

// Log the value of age property
// this not will work as you expect
console.log(user.age || 29)
// Output:
// 29

// Log the value of jobTitle property
// this not will work as you expect
console.log(user.jobTitle || 'Unemployed')
// Output:
// 'Unemployed'

// Log the value of property hobbies
// this will work as you expect
console.log(user.hobbies || 'No hobbies.')
// Output:
// 'No hobbies.'

// Log the value of non-existing property height
// this will work as you expect
console.log(user.height || 'Height is unknown.')
// Output:
// 'Height is unknown.'
```

### Fixing logical operators gotchas

When logical operator encounters falsy value it will return the right operand. This is the value you on the right side you provided as the default. This is what happened on the example above when you tried to access the `age` and `jobTitle` properties. Both values were falsy and logical operator returned the default value.

There is a way to fix this. You fix this problem by changing the condition. The downside is that it introduces more complexity. Anyway, here it is. You will not say some value OR some default value. Instead, you will first check if a property is neither `null` nor `undefined`, by using AND operator.

If the property is neither `null` nor `undefined` it means the property exists. It doesn't matter if the value is truthy or falsy. At this moment, there is no conversion to truthy or falsy value because the condition doesn't operate with the value itself. It only looks if the property itself exists.

If the property exists, you will try to access it and return its value. Otherwise, you will return the default. You can do this either with [if...else statement] or [ternary operator]. This solution will work well with both, existing and non-existing values.

```JavaScript
const user = {
  name: 'Justin Lambert',
  age: 0, // 0 is a falsy value
  jobTitle: '', // Empty string is a falsy value
  hobbies: null // Null is also a falsy value
}

// Log the value of name property
// this will work as you expect
console.log((user.name !== null && user.name !== undefined) ? user.name : 'Anonymous')
// Output:
// 'Justin Lambert'

// Log the value of age property
// this will finally work as you expect
console.log((user.age !== null && user.age !== undefined) ? user.age : 29)
// Output:
// 0

// Log the value of jobTitle property
// this will finally work as you expect
console.log((user.jobTitle !== null && user.jobTitle !== undefined) ? user.jobTitle : 'Unemployed')
// Output:
// ''

// Log the value of property hobbies
// this will work as you expect
console.log((user.hobbies !== null && user.hobbies !== undefined) ? user.hobbies : 'No hobbies.')
// Output:
// 'No hobbies.'

// Log the value of non-existing property height
// this will also work as you expect
console.log(user.height !== null && user.height !== undefined ? user.height : 'Height is unknown.')
// Output:
// 'Height is unknown.'


// Notes:
// first check if property is neither null nor undefined:
// user.name !== null && user.name !== undefined
// according to this condition return either property or default
// obj.someProp : 'Some default value'
```

## Nullish coalescing operator to the rescue

So, there is a way to fix gotchas of falsy values and logical operators. The downside is that can make your code less readable and also less clean. A better solution is the newly added nullish coalescing operator. One could say that this operator is a shortcut for the ternary operator with `null` nor `undefined` check you just saw.

This is actually true. The nullish coalescing operator is a new operator in JavaScript that does similar thing as that ternary operator. It first check if the operand on the left side is either `null` or `undefined`. If it is one of these it will return the operand on the right side, the default value. Otherwise, it will return the operand on the left side.

The syntax of nullish coalescing operator is simple. There is one operand on the left side. This is what you want to return if it is not null or undefined. Then, there is the nullish coalescing operator (`??`). After that is the operand on the right side. This is what will be returned if what you check is `null` nor `undefined`.

Let's go back to the "user" example and use nullish coalescent operator to log either existing properties or default values. We can basically remove the whole ternary operator. After that, we just have to replace the colons with `??`. As you can see on the example below, code will become much shorter and more readable.

```JavaScript
// Nullish coalescing operator
// leftOperand - something you want to return
// if it is neither null nor undefined
// rightOperand - something you want to return
// if leftOperand is null or undefined
// ?? - symbol of nullish coalescing operator
// Syntax: leftOperand ?? rightOperand

const user = {
  name: 'Justin Lambert',
  age: 0, // 0 is a falsy value
  jobTitle: '', // Empty string is a falsy value
  hobbies: null // Null is also a falsy value
}

// Log the value of name property
console.log(user.name ?? 'Anonymous')
// Output:
// 'Justin Lambert'

// Log the value of age property
console.log(user.age ?? 29)
// Output:
// 0

// Log the value of jobTitle property
console.log(user.jobTitle ?? 'Unemployed')
// Output:
// ''

// Log the value of property hobbies
console.log(user.hobbies ?? 'No hobbies.')
// Output:
// 'No hobbies.'

// Log the value of non-existing property height
console.log(user.height ?? 'Height is unknown.')
// Output:
// 'Height is unknown.'
```

## Combining nullish coalescing operator with logical operators

One thing to remember is that you can't use nullish coalescing operator with logical operators, directly. When you try it, JavaScript will throw a syntax error. A way to fix this problem is to wrap the logical operator and its operands with parenthesis. Then, you add the nullish coalescing operator and its operand.

```JavaScript
// This will not work
null || undefined ?? 'You should see me.'
// Output:
// SyntaxError: Unexpected token '??'

null || false ?? 'You should see me.'
// Output:
// SyntaxError: Unexpected token '??'

true || false ?? 'You should see me.'
// Output:
// SyntaxError: Unexpected token '??'


// This will work
(null || undefined) ?? 'You should see me.'
// Output:
// 'You should see me.'

(null || false) ?? 'You should not see me.'
// Output:
// false

(true || false) ?? 'You still should not see me.'
// Output:
// true
```

## Nullish coalescing operator and operator precedence

In JavaScript, there is something called operator precedence. This specifies how, if you combine multiple operators, JavaScript will parse these operators. Every operator when it is added in the language specification is also assign some number that determines this precedence.

The number for the highest precedence is currently 21. The lowest is 1. Operators with higher precedence are evaluated before operators with lower precedence. You can see the precedence for existing operators in [this table]. What this means for nullish coalescing operator?

The nullish coalescing operator has precedence of 5. Logical operator OR has precedence of 6, AND 7. This means two things. First, it puts it in the bottom of the precedence table. Second, if you use nullish coalescing operator in more complex expression nullish coalescing operator will likely be evaluated as last.

This can result to very different outcomes than you may want. If you want to increase precedence of nullish coalescing operator you can wrap it in parentheses. Parentheses, or grouping operator, have precedence of 21. This is the highest number in the precedence table. It should provide sufficient boost.

```JavaScript
// Declare variables for calculating reward for work
const hoursWorked = null;
const hourlyRate = null;

// Without parentheses
// The * has higher precedence than nullish coalescing operator
hoursWorked ?? 1 * hourlyRate ?? 25
// Output:
// 0
// because hoursWorked * hourlyRate = 0 (null * null = 0)

// With parentheses
// Parentheses boost precedence of nullish coalescing operator
(hoursWorked ?? 1) * (hourlyRate ?? 25)
// Output:
// 25
```

## Conclusion: [...] ...

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[OR]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_OR
[AND]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_AND
[NOT]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_NOT
[boolean]: https://blog.alexdevero.com/javascript-basics-data-types-pt2/#boolean-logical-type
[truthy]: https://developer.mozilla.org/en-US/docs/Glossary/truthy
[falsy]: https://developer.mozilla.org/en-US/docs/Glossary/falsy
[if...else statement]: https://blog.alexdevero.com/javascript-if-else-statement
[ternary operator]: https://blog.alexdevero.com/javascript-if-else-statement/#ternary-operator
[this table]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence#Table

<!--
### Meta:
-
-->

<!--
### Keywords:
- nullish coalescing operator
- nullish coalescing
-->

<!--
### Resources:
-
-->
