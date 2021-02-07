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

## this and classes

When you work with JavaScript classes it is very likely you will see the [this keyword] a lot. Basically all you need to know is this. When you use `this` inside a class it will refer to the class itself. When you create new instance of that class, it will refer to that very instance.

One thing that can help you is using your imagination. When you see `this` inside a class you can imagine replacing that `this` with the name of the class you are currently working with. This is, theoretically speaking, what's happening.

```JavaScript
// Create new class:
class MyClass {
  // Create constructor and define one parameter:
  constructor(name) {
    // This:
    this.name = name
    // Can be translated here to:
    // MyClass.name = name

    // When you create an instance of MyClass
    // it can be translated here to:
    // InstanceOfMyClass.name = name
  }
}
```

## Class properties and methods

Every class can have infinite number of properties, just like any object. In the beginning, there was only one way to define these properties. You could define properties only inside the `constructor` method. Note that it doesn't matter if the `constructor` method accepts any parameter.

Even if the `constructor` method doesn't accept any, defining class properties was still possible only inside it. This changed only to some degree. The `constructor` method is still the only place to define parameters for the class and assign their values to some class properties.

```JavaScript
// Create new class:
class MyClass {
  // Create constructor and define one parameter:
  constructor(name) {
    // Create class property called "name"
    // and assign it a value of "name" parameter
    this.name = name

    // Create additional class properties:
    this isHuman = true
    this.isAlive = true
  }
}
```

Other ways to create class properties are class fields. The names class fields and class properties are almost the same. Difference is that properties are defined inside `constructor` method while class fields are defined outside it, inside the class body.

At this moment, there are three types of class fields: public, static and private. We will talk about each in the next section. First, let's quickly talk about class methods.

### Class methods

When you want to create class method, you define it right inside the class body. Defining a class method is as simple as defining a function. There is one difference. When you create a class method you omit the `function` keyword and start with the method name. And, no need for the `this` keyword when you define the method.

However, you will need `this` if you want to reference some property or method of the class you are working with. When you want to call some class method you create new instance of the class. Then, you call the method on that instance, using dot notation.

```JavaScript
// Create new class with method:
class MyClass {
  // Create class method:
  myMethod() {
    return 'Hello!'
  }
}

// Create instance of "MyClass":
const myClassInstance = new MyClass()

// Call "myMethod" on "myClassInstance" instance:
joe.myMethod()
// Output:
// 'Hello!'


// Create new class with method using this:
class MyClass {
  // Create constructor and define one parameter:
  constructor(name) {
    // Create class property called "name"
    // and assign it a value of "name" parameter
    this.name = name
  }

  // Create class method:
  sayHi() {
    return `Hello, my name is ${this.name}.`
  }
}

// Create instance of "MyClass":
const joe = new MyClass('Joe')

// Call "sayHi" on "joe" instance:
joe.sayHi()
// Output:
// 'Hello, my name is Joe.'
```


## Classes and instances

We already briefly talked about creating instances of classes. As I mentioned, instances are like new objects you create based on existing classes. The reason for creating new instances is that they automatically inherit properties and methods you defined in the class they are based on.

This means that you don't have to write the same code over and over again if you want to use it in multiple objects. What you can do is create one class and put the code you want to re-use there. When you need an object that can do all that stuff you can use that class to create new instance.

This instance will inherit properties and methods you defined in that "parent" class. It will be able to work with these properties and methods. In order to create new instance of class, you declare new variable. On the right side, you use the `new` keyword followed by the name of the class you want to instantiate and parentheses.

If the class accepts any parameters, you pass them inside the parentheses that follow after the name of the class. Otherwise, you leave the parentheses empty. This way, you can create as many instances of a specific class as you want.

Remember that all properties and their values you "hard-code" in the `constructor` of a specific class will be inherited by all instances of that class. Any properties you assign values passed as arguments will be dynamic. They will depend on arguments you use during instantiation.

```JavaScript
// Class without parameters:
class MyClass {
  // Create constructor:
  constructor() {
    // Create class property "isAlive" and assign it true.
    this.isAlive = true
  }
}

// Create instance of "MyClass" class:
const myClassInstance = new MyClass('Jessica')

// log the value of "isAlive" property
// on "myClassInstance" instance:
console.log(myClassInstance.isAlive)
// Output:
// true


// Class with one parameter:
class MyClassTwo {
  // Create constructor and define one parameter:
  constructor(name) {
    // Create class property called "name"
    // and assign it a value of "name" parameter
    // and another boolean property "isAlive".
    this.name = name
    this.isAlive = true
  }
}

// Create instance of "MyClassTwo" class
// and pass in argument for "name" parameter:
const myClassInstanceTwo = new MyClassTwo('Jacob')

// log the value of "name" property
// on "myClassInstanceTwo" instance:
console.log(myClassInstanceTwo.name)
// Output:
// 'Jacob'

// Create another instance of "MyClassTwo" class
const myClassInstanceThree = new MyClassTwo('Tobias')

// log the value of "name" property
// on "myClassInstanceTwo" instance:
console.log(myClassInstanceThree.name)
// Output:
// 'Tobias'
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
