# Blog post title [...]
<!--more-->
<!--
Table of Contents:
-->

## From regular functions to generator functions

Regular [functions] has been around since the beginning of JavaScript. Functions are one of the fundamental building blocks of this programming language. This is not true if we talk about generator functions. These special functions have been introduced to JavaScript quite recently.

Functions have been working very well. Aside to regular functions, there are now also arrow functions. So far, arrow functions proved to be beneficial in some cases. They are often also preferred by JavaScript developers over the regular. One may ask, why to add something new?

Both regular and arrow functions are great when you want to encapsulate a piece of code to make it re-usable. They are also allow you to return a single value or nothing. A single can be also an array or an object that contains multiple values. Nonetheless, there is still one thing you want to return.

This is where generator functions are different. Unlike regular functions, generators are capable of returning multiple values. That said, they don't return all of them at the same time. Instead, they returned one after another, only when you want it. Until then, generator will wait while remembering the last value.

## The syntax

One nice thing about generator functions is that they have a friendly syntax. There is a lot to learn, especially if you already know something about regular [functions]. At this monument, there are two ways to create a generator function. The first one is with the help of [GeneratorFunction constructor].

This approach is not very common and you will see it very rarely. The second, and more common approach, is by using function [declaration]. Yes, you can also create generators with function expression. In both cases, the `function` keyword is followed by asterisk (`*`).

This symbol is what tells JavaScript that you want to create a generator function, not a regular function. Except this small change, the rest of the syntax is the same as for function. There is the function name, parentheses for parameters, and function body with code to execute.

```JavaScript
// Create generator function:
function* myGenerator() {
  // Function body with code to execute.
}
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
