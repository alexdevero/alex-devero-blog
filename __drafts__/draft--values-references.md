# Blog post title [...]
<!--more-->
<!--
Table of Contents:
-->

## A short introduction

In JavaScript, there are the two categories of data types you can work with. First category are primitive data types. At this moment, there exist [seven primitive types]. These primitive data types are number, string, boolean, `null`, `undefined`, BigInt and Symbol. The BigInt and Symbol are newer data types.

Symbol was introduced in [ES6] specification. The BigInt was introduced later, in [ES2020] specification. When something is not one of these primitive data types it is technically an object. This applies to actual objects as well as arrays and even functions. From the view of JavaScript, these are all objects.

This distinction between primitive data types and objects is important because JavaScript handles each differently.


## Primitive data types

Let's start with the first category, primitive data types. Values that contain these primitive data types are called static data. As static data, JavaScript stores them on the [stack]. One important thing about these primitive values is that their size is fixed. JavaScript knows how much memory these data types need.

Let's say you assign some variable a primitive data type as a value. From now on, this variable will contain that value. If you manipulate with that variable, you manipulate directly with the value you assigned to it. A simple way to test this, and the consequences, is assigning the variable to another variable.

When you assign one variable to another, and the value of first is primitive data type, JavaScript will copy that value. When you do this you are copying the values "by value". So, now, if you change the value of the first variable, the second will remain the same. This is because even though you created one variable from another they both have their own, separate, values.

So, if you change the value of one variable it will not change the second. The second variable is a separate entity. Let's go back to the stack. When you assign the first variable, JavaScript will store its value on the stack. When you assign the variable to another variable its value will be also added on the stack.

At this moment, the stack will now contain two values, one for each variable. It doesn't matter that both values are the same. Nor does it matter that you created the second variable from the first. For JavaScript, these are two separate entities. These two variables have no relationship with each other.

This is also why you can safely work with each of these variables as you want. Why you can change one variable without changing the other.

```JavaScript
// Create a variable and assign it
// a primitive value:
let x = 'Hello'

// Assign "x" to another variable:
let y = x

// Change the value of "x":
x = 'Bye'

// Log the value of "x":
console.log(x)
// Output:
// 'Bye'

// Log the value of "x":
console.log(y)
// Output:
// 'Hello'
```


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
-
-->

<!--
### Resources:
-
-->
