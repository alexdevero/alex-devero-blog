# Getting Started With JavaScript Constructor Functions

JavaScript offers multiple ways to create objects. These ways include object literals, `Object()`, classes and constructor functions. This tutorial will show you the third option. You will learn about what constructor function are, how they work, and how to use them to create objects.<!--more-->
<!--
Table of Contents:
-->

## Objects, blueprints, constructors

In JavaScript, there are multiple ways you can use to create objects. The easiest tools you can use are [object literals], `new Object()` or `Object.create()`. However, what if you want something more different? What if you create an object you can than use as a blueprint, or a recipe, for creating other, similar, objects?

Imagine you want to create a couple of objects all having the same properties, maybe also methods. You can definitely do this object literal. However, it will require copying a lot of code. Or, it will require unnecessary cloning of objects, which can be sometimes quite unpredictable.

Another option is to create something called "constructor". This constructor can have a number of various properties and methods and you can use it to create new objects. Each object you create with this constructor will also have all properties and methods defined in the constructor. This can save you a lot of time and code.

One way to create this constructor is by using [JavaScript classes] introduced in ES6. Another option is to use something called "constructor functions". Let's take a look at what this constructor function are, how they work, and how to use them to create objects.

## The basics of constructor functions

The syntax of constructor functions is simple and straightforward. This is especially true if you know JavaScript functions. Syntax of these two is almost identical. Every constructor function starts with the `function` keyword. What follows is the name of the name of the constructor function.

The name of constructor function should start with a capital letter. This is not required, but it is a popular convention and good practice. However, if you use lowercase letter it will work. Next are parentheses with parameters. Even if you don't want to specify any parameters, you still have to include the parentheses anyway.

The last is the function body that follows after the parentheses with parameters. This body is the place where you specify properties and methods for the constructor. When you use this constructor to create new objects they will all have these properties and methods.

```JavaScript
// Syntax of a constructor function:
// - function keyword
// - name of the constructor function
// - parameters for constructor function
// - body of the constructor function
function MyConstructorFunc(param) {
  // Function constructor body.
}
```


## Conclusion: Getting started with JavaScript constructor functions

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
