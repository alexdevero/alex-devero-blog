# How to Get Started with JavaScript Classes: A Quick Guide

JavaScript classes are popular feature of JavaScript. This tutorial  will help you learn what you need to know in order to get started with JavaScript classes. You will learn about class constructor, properties and methods. You will also learn what public, static and private class fields are.<!--more-->
<!--
Table of Contents:
-->

## A quick introduction

Before we dive into how to get started with JavaScript classes, let's quickly talk about few things. First, classes were added to JavaScript in ES6 specification (ECMAScript 2015). Second, they are not a new feature per se. Classes basically provide a different way to [create objects] and work with [prototypes] and inheritance.

This is also why many JavaScript developers call classes a syntactic sugar. They are correct. Classes are a syntactic sugar. Under the hood, you are still working with objects, prototypes and so on. The only real difference is in the syntax you are using. Another is that your code will not work in IE. [Babel] will help you fix this.

That being said, there is nothing wrong with using JavaScript classes over other older options. It is mainly a matter of your preference. If you like them, use them. If you don't, don't. Now, let's take a look at what you need to know to get started with JavaScript classes.

## The syntax

The syntax of classes is easy to learn and remember. Every class starts with `class` keyword. Next comes body of the class, a block of code wrapped with curly brackets. There are no parentheses and parameters you know from [functions]. When you declare new class, the convention is to start with a capital letter.

```JavaScript
// Create new class called "MyClass":
class MyClass {
  // Body of the class.
}
```

## Classes, constructor and parameters

When you declare new class there are no parentheses where you could specify parameters. This doesn't mean that classes don't support parameters. They do. They just work with them in a different way. When you want to specify parameters for your class you have to use method called `constructor`.

This `constructor` is a very unique method. You can create it only inside a class and only once. If you don't create this method yourself, JavaScript will automatically use default that is built inside every class. The main job of this method is to execute tasks you have specified when you create a new instance of a class.

Instance is basically a new object based on a specific class, and it inherits all properties and methods defined in that class. Every time you create new instance of a class it will also automatically invoke the `constructor` method. This is useful when you want to do something when you create new class instance.

For example, assigning properties with initial values. Another thing `constructor` allows is specifying parameters. The `constructor` method is a normal method. As such, it can also accept parameters. If you specify some parameter for the `constructor` method these parameters will become parameters of the class itself.

When you create new instance of the class, you can pass in some values as arguments, based on the parameters of the `constructor`. Otherwise, you can omit any parameters and use just the `constructor` to do some initial tasks. If you define your own `constructor`, and replace the default, do at the top of the class.

```JavaScript
// Create new class "MyClass" with constructor,
// but without any parameters.
class MyClass {
  // Create constructor method without any parameters
  constructor() {
    // Code that will be executed
    // when a new class instance is created.
  }
}


// Create new class "MyClass"
// that accepts two parameters: name and age.
class MyClass {
  // Create constructor method
  // and specify "name" and "age" parameters.
  constructor(name, age) {
    // Create properties "name" and "age" on the class
    // and assign them values passed as arguments
    // for "name" and "age" parameters.
    this.name = name
    this.age = age
  }
}
```


[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[]:

<!--
### Meta:
-
-->

<!--
### Keywords:
- getting started with JavaScript Classes
- JavaScript Classes
-->

<!--
### Resources:
-
-->
