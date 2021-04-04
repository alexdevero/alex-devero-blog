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

## Creating objects with constructor function

Creating constructor functions is one thing. Using them to create new objects is another. Luckily, there is only one way to do this. When you want to create new object using constructor function you use the `new` keyword. This keyword is followed by the constructor name and set of parentheses.

If your constructor accepts any parameters, pass any necessary arguments inside the parentheses. Otherwise, leave them empty. You will usually do this along with assigning new object to a variable. Remember that you can use constructor functions to create as many objects as you want.

```JavaScript
// Create constructor function:
function Person() {}

// Create object with Person constructor:
const personOne = new Person()

// Create another object with Person constructor:
const personTwo = new Person()
```

## Defining properties, methods

Defining properties, and methods, in constructor functions is simple. That said, there is one thing you have to remember. When you want to define property or method you have to use the `this` keyword. Don't use `let`, `const` or `var` to do this. You are not trying to define a variable, but a property.

So, on the left side, start with the `this` keyword and then specify the name of the property. Add dot (`.`) between these two. On the right side, define the value for the property and you are done. If you want to define a method the process is almost the same. You also have to use the `this` keyword, followed by the name of the method.

The only difference is on the right side. Here you have to use the `function` keyword. This will tell JavaScript that you want to define a function. You can also use an [arrow function] instead of a regular function. When you define a constructor method, you can access any property that already exists inside the constructor.

In order to access the property, to reference it correctly, you have to use the `this` keyword. THe `this` in this case is a reference for the constructor function itself. So, `this` is basically like `constructorFunctionItself`.

```JavaScript
// Create constructor function:
function Person() {
  // Define properties "name" and "age":
  this.name = 'Anonymous'
  this.age = 35

  // Define method "getName" that returns a short message:
  this.getName = () => {
    // "this" here refers to the "Person" constructor.
    // "this.name" is like "Person.name".
    return `Hello, my name is ${this.name}.`
  }
}

// Create object with Person constructor:
const personOne = new Person()

// Log the value of "name":
console.log(personOne.name)
// Output:
// 'Anonymous'

// Log the "getName" message:
console.log(personOne.getName())
// Output:
// 'Hello, my name is Anonymous.'

// Create another object with Person constructor:
const personTwo = new Person()

// Log the value of "name":
console.log(personTwo.name)
// Output:
// 'Anonymous'

// Log the "getName" message:
console.log(personTwo.getName())
// Output:
// 'Hello, my name is Anonymous.'
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
