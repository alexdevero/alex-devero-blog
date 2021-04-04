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
  this.getName = function() {
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

### Defining properties and methods outside the constructor

Defining properties and methods only inside the constructor function when you define it is one option. Another option is defining them outside it, after the constructor is created. In this case, you will use a property called [prototype]. This is a special property every function in JavaScript has.

This `prototype` property is an object that contains all properties and methods defined on a constructor function. It also contains `constructor` property. This property points to the constructor you are working with in the moment. Using this property allows you to add properties and methods to constructor, change or remove them.

```JavaScript
// Create constructor function:
function Person() {
  // Define properties "name" and "age":
  this.name = 'Anonymous'
  this.age = 35
}

// Create object with Person constructor:
const personOne = new Person()

// Create another object with Person constructor:
const personTwo = new Person()

// Add properties to Person constructor using prototype:
Person.prototype.gender = 'female'
Person.prototype.height = 1.7

// Log the value of "gender" on "personOne" object:
console.log(personOne.gender)
// Output:
// 'female'

// Log the value of "height" on "personTwo" object:
console.log(personTwo.height)
// Output:
// 1.7

// Add method "getName" to Person constructor using prototype:
Person.prototype.getName = function() {
  // "this" here will correctly refer to the Person constructor.
  // So, "this.name" will again basically become "Person.name".
  return `Hello, my name is ${this.name}.`
}

// Log the message:
console.log(personTwo.getName())
// Output:
// 'Hello, my name is Anonymous.'
```

*Note about `prototype`: As you can see on the example above, there is one thing to remember. When you add property or method to a constructor via prototype, you also add it to all objects already created with that constructor.*

### Defining properties and methods for constructor objects

Sometimes you may want to add a property or method, but only to one object, not all. In this case, `prototype` is not an option since that would add the property or method everywhere. What you can do instead is to add the property or method directly to specific object. For example, using the dot notation.

After this, only the object at hand will have that new property or method. Other objects created with the same constructor will not. This is the way you would use to add a property or method to a regular object. Every object created with a constructor is an object. So, this works here as well.

```JavaScript
// Create constructor function:
function Person() {
  // Define properties "name" and "age":
  this.name = 'Anonymous'
}

// Create object with Person constructor:
const personOne = new Person()

// Create another object with Person constructor:
const personTwo = new Person()

// Add property "gender" only to "personOne" object:
personOne.gender = 'female'

// Add property "height" only to "personTwo" object:
personTwo.height = 1.7

// Log the value of "gender" on "personOne" object:
console.log(personOne.gender)
// Output:
// 'female'

// Log the value of "height" on "personOne" object:
console.log(personOne.height)
// Output:
// undefined // <= this is correct, height exists only on personTwo

// Log the value of "gender" on "personTwo" object:
console.log(personTwo.gender)
// Output:
// undefined // <= this is correct, gender exists only on personOne

// Log the value of "height" on "personTwo" object:
console.log(personTwo.height)
// Output:
// 1.7

// Add "getGender()" method only to "personOne" object:
personOne.getGender = function() {
  return `I am a ${this.gender}.`
}

// Add "getHeight()" method only to "personTwo" object:
personTwo.getHeight = function() {
  return `I am ${this.height}m tall.`
}

// Call the "getGender()" method on "personOne" object:
console.log(personOne.getGender())
// Output:
// 'I am a female.'

// Call the "getHeight()" method on "personOne" object:
console.log(personOne.getHeight())
// Output:
// TypeError: personOne.getHeight is not a function

// Call the "getGender()" method on "personTwo" object:
console.log(personTwo.getGender())
// Output:
// TypeError: personTwo.getGender is not a function

// Call the "getHeight()" method on "personTwo" object:
console.log(personTwo.getHeight())
// Output:
// 'I am 1.7m tall.'
```

## Constructor functions and parameters

The option to create blueprint for objects is nice. So far, you've seen examples of constructors where all data were static and couldn't be changed. This doesn't mean that this is the only way. In the beginning, when we talked about the syntax, I briefly mentioned parameters.

This is how you can make constructor functions more dynamic. Just like you can define parameters for regular functions you can define them also for constructors. In case of constructors, you specify arguments when you create objects with the `new` keyword. You pass these arguments in the parentheses that follow the construct name.

When you define some parameters for a constructor, you can then use it anywhere inside the constructor. Take the `Person` constructor you've been working throughout this tutorial. It usually contained two properties: `name` and `age`. Having these two properties the same for all objects doesn't make sense.

Instead of having both properties defined with static values, you can add two parameters for the constructor. One parameter for each property. Then, inside the constructor, you can use these parameters to assign those properties with provided values. This will allow you to create objects with different values for `name` and `age` properties.

```JavaScript
// Create constructor function
// that accepts two parameters, "name" and "age":
function Person(name, age) {
  // Define properties and assign them
  // with values provided for "name" and "age":
  this.name = name
  this.age = age
}

// Create object with Person constructor:
const personOne = new Person('Stan', 33)

// Create another object with Person constructor:
const personTwo = new Person('July', 29)

// Log the value of "name" on "personOne" object:
console.log(personOne.name)
// Output:
// 'Stan'

// Log the value of "age" on "personOne" object:
console.log(personOne.age)
// Output:
// 33

// Log the value of "name" on "personTwo" object:
console.log(personTwo.name)
// Output:
// 'July'

// Log the value of "age" on "personTwo" object:
console.log(personTwo.age)
// Output:
// 29
```

## A word about constructor functions and this

The `this` keyword is very important when you work with constructor functions. You use it when you want to define new properties and methods. You also use `this` keyword when you want to access some property and call some method. However, it doesn't matter how often you have to use `this` keyword.

Understanding what `this` is, what it refers to, at the time can still be sometimes a difficult question to answer. Here is the simple answer. The value of `this` can be one of two things. First, when you are in a function constructor, the value will be the constructor.

Second, when you create new object with the constructor the value of `this` will become the new object. This will apply to every instance, every new object you create. The value of `this` will always be that specific object.

```JavaScript
// Create constructor function:
function Person(name, age) {
  // "this" here refers to the constructor function.
  // this.name => Person.name
  this.name = name
  this.age = age
}

const objJoe = new Person('Joe', 19)

// For "objJoe" object the value of "this"
// will be the "objJoe" object itself.
// So, "this.name" in constructor will become "objJoe.name".
console.log(objJoe.name)
// Output:
// 'Joe'

const objTim = new Person('Tim', 23)

// For "objTim" object the value of "this"
// will be the "objTim" object itself.
// So, "this.name" in constructor will become "objTim.name".
console.log(objJoe.name)
// Output:
// 'Tim'
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
