# JavaScript Classes and Static Methods and Properties

JavaScript classes are one of the most discussed features of ES6. Two interesting features of classes are static methods and properties. In this tutorial, you will learn what static methods and properties are and how they work. You will also learn how to use these methods and properties in your projects.

<!--more-->
<!--
Table of Contents:
-->

## Introduction

Let's start with the basics. Every static method and property has to start with the `static` keyword. This tells JavaScript that the method or property that follows after this keyword should be defined as static. Now, the more interesting question. How are static methods and properties different from public methods and properties?

The main difference between static and public methods and properties is two-fold. First, you can call static methods, and access static properties, without having to [instantiate class] in which they are defined. Second, you can't call these methods, and access these properties, on instances of the class in which they are defined.

JavaScript developers usually use static methods and properties something like utility functions and utility properties. For example, you can use static method to create a method that will help you compare two instances of the class. One thing you can do with static properties is keeping count of how many instances some class has.

*Note: All methods defined in a class are by default defined as public. This means that they will be accessible for all instances. Which also means that you can call them on all instances. However, you can't call them on the class in which they are defined unless you instantiate it.*

## Static methods

As you now know, creating static methods is quick. When you want to create one, you can do it in two ways. First, you can create new class and define a new method inside it. When you do this make sure to prepend the method with the `static` keyword. This will define the method as static.

```JavaScript
// Create new class
class MyClass {
  // Create static method
  static myStaticMethod() {
    console.log('Call from myStaticMethod.')
  }
}

MyClass.myStaticMethod()
// Output:
// 'Call from myStaticMethod.'
```

There is also another thing you can do. You can create new class. Then, outside the class, you can add new method to this class using dot notation. In this case, you don't have to use the `static` keyword. The method will become static automatically.

```JavaScript
// Create new class
class MyClass {}

// Add new static method to "MyClass"
MyClass.myStaticMethod = function() {
  console.log('Call from myStaticMethod.')
}

MyClass.myStaticMethod()
// Output:
// 'Call from myStaticMethod.'
```

## Static properties

## Static properties and properties and class inheritance

## Conclusion: JavaScript Classes and Static Methods and Properties

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[instantiate class]: https://blog.alexdevero.com/javascript-classes-pt1/#inheritance-and-child-classes-or-subclasses

<!--
### Meta:
-
-->

<!--
### Keywords:
- Static methods
- properties
-->

<!--
### Resources:
-
-->
