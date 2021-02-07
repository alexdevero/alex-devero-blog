# A Quick Guide to Get Started with JavaScript Classes

JavaScript classes are popular feature of JavaScript. This tutorial  will help you learn what you should know so you can get started with JavaScript classes. You will learn about class constructor, properties and methods. You will also learn what public, static and private class fields are.<!--more-->
<!--
Table of Contents:
## A quick introduction
## The syntax
## Classes, constructor and parameters
## this and classes
## Class properties and methods
### Class methods
### Public class fields and methods
### Static class fields and methods
### Private class fields and methods
## Classes and instances
## Conclusion: How to get started with JavaScript classes
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

This `constructor` is a unique method. You can create it only inside a class and only once. If you don't create this method yourself, JavaScript will automatically use default that is built inside every class. The main job of this method is to execute tasks you have specified when you create a new instance of a class.

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

Other ways to create class properties are class fields. The names class fields and class properties are almost the same. Difference is that properties are defined inside `constructor` method while class fields are defined outside it, inside the class body. Other than that, class properties and class fields are basically interchangeable.

At this moment, there are three types of class fields: public, static and private. We will talk about each in the next section. But first, let's quickly talk about class methods.

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

### Public class fields and methods

Class properties and public class field are very similar. The main difference is that you define class properties in the `constructor` method. With class fields, you don't need the `constructor`, because they are defined outside it. This is also means that if you don't need the `constructor` for something else, you can omit it.

However, if you want to define class parameters or do some stuff during class instantiation, you will still have to use `constructor`. Another important difference is that public fields don't use the `this` keyword. When you define new public field, you start with the name of the field (property), not the `this` and dot.

One thing about public class fields and access. Fields you define as public will be always accessible from the inside as well as the outside of the class, and its instances. This means that you will be able to access and modify them as you want. The same applies to public methods. They will be all accessible and modifiable.

Last thing. Any class field and method you define are public by default. You can change this by defining the field or method either as static or private. This means using corresponding keyword. Otherwise, JavaScript will automatically assume that the field or method should be public and make them that way.

```JavaScript
// Create new class:
class Car {
  // Define class fields for "numOfWheels" and "fuel":
  numOfWheels = 4
  fuelType = 'electric'

  // Define public method:
  startEngine() {
    return 'Engine is running.'
  }
}

// Create instance of Car class:
const tesla = new Car()

// Log the value of public class field "fuelType":
console.log(tesla.fuelType)
// Output:
// 'electric'

// Call the "startEngine" method:
console.log(tesla.startEngine())
// Output:
// 'Engine is running.'
```

### Static class fields and methods

The second type of class fields and methods are static. When you want to define a static class field or method you add the keyword `static` before the field or method name. The main difference between static class fields and public class fields is that you can't access static class fields on instances of the class.

You can access static class fields only on the class itself. The same applies to static methods. You can't call them on instances of the class. You can call them only on the class itself. Static fields and methods are often used for utility purposes. For example, doing cleanups, updates or having an evidence of existing class instances.

When you work with static class fields remember that methods that can work with them are only static methods. You can't access static class fields with neither public nor private methods, only static.

```JavaScript
class Car {
  // Declare static property to keep track
  // of how many instances of Car has been created.
  static numOfCopies = 0

  constructor() {
    // When new instance of Car is created
    // update the number of Car instances:
    Car.numOfCopies++
  }

  // Create static method to access
  // static field "numOfCopies".
  static getNumOfCopies() {
    // Return the value of "numOfCopies" field:
    return Car.numOfCopies
  }
}

// Log number of instances of MyClass
console.log(Car.getNumOfCopies())
// Output:
// 0

// Create instance of Car:
const porsche = new Car()

// Log number of instances of Car again:
console.log(Car.getNumOfCopies())
// Output:
// 1
```

### Private class fields and methods

Private class fields and methods are the last type of fields and methods you can use. Private class fields and methods are basically the opposite of public fields and methods. When you define some field or method as private you can work with it only inside the class. From the outside, they will be invisible.

This can be useful when you want to keep some data private. When you want some data to be inaccessible from the outside and also from any class instance. The syntax for private fields and methods is simple. In order to define private field or method start the name with `#` (hashtag symbol).

When you want to access private field, or call private method, you also have to use the hashtag symbol. One interesting thing is that public method can access private fields and methods. So, if you want, you can create private field or method. Then, you can create a public method to access the private field or call the private method. Both things will work.

```JavaScript
class App {
  // Declare private field "version":
  #version = '1.0'

  // Create private method "getVersion":
  #getVersion() {
    return this.#version
  }

  // Create public method "getVersionPublic" to access
  // private field "version":
  getVersionPublic() {
    // Return the value of "numOfCopies" field:
    return this.#version
  }

  // Create another public method "callGetVersion"
  // that calls the private method "getVersion":
  callGetVersion() {
    return this.#getVersion()
  }
}

// Create instance of Car:
const myApp = new App()

// Log number of instances of Car again:
console.log(myApp.getVersionPublic())
// Output:
// '1.0'

console.log(myApp.callGetVersion())
// Output:
// '1.0'
```

## Classes and instances

We already talked about instances of classes a couple of times. It is time to talk about them more. As I mentioned, instances are like new objects you create based on existing classes. The reason for creating new instances is that they automatically inherit properties and methods you defined in the class they are based on.

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

## Conclusion: A quick guide to get started with JavaScript classes

JavaScript classes are interesting feature that offers a new way of creating objects and working with prototypes and prototypal inheritance. I hope that this short and quick guide helped you understand at least the basics so you can get started with JavaScript classes.

If you found JavaScript classes interesting, and want to learn more, take a look at JavaScript Classes – A Friendly Introduction [part 1] and [part 2]. These two tutorials will give you more in-depth information about JavaScript classes and tell you about what we may have skipped in this short guide.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[create objects]: https://blog.alexdevero.com/create-objects-in-javascript/
[prototypes]: https://blog.alexdevero.com/prototype-prototypal-inheritance/
[Babel]: https://babeljs.io/
[functions]: https://blog.alexdevero.com/javascript-functions-pt1/
[this keyword]: https://blog.alexdevero.com/this-in-javascript-works/
[part 1]: https://blog.alexdevero.com/javascript-classes-pt1/
[part 2]: https://blog.alexdevero.com/javascript-classes-pt2/

<!--
### Meta:
-
-->

<!--
### Keywords:
- get started with JavaScript Classes
- JavaScript Classes
-->

<!--
### Resources:
-
-->
