# JavaScript Property Getters and Setters (Accessor Properties)

Property getters and setters allow you to change the default behavior when accessing or modifying object properties. This tutorial teach you all you need to know about them. You will learn what JavaScript property getters and setters are, how they work and how to use them.
<!--more-->
<!--
Table of Contents:
## h2
### h3
### h3
## h2
## Conclusion: [...] ...
-->

## Properties and property getters and setters

In JavaScript, there are two types of properties. The first type is data properties. These are the properties you usually use when you work with [objects]. The second type is called "accessor properties". These are a bit different. Put simply, accessor properties are methods.

These methods are executed every time you work with a property. When you access, or get, a value or when you set or change a value. What about property getters and setters? These two represent this group of properties, the accessor properties. To be more specific, getter is that function that is executed when you access some value.

Setter, on the other hand, is that function that is executed when you set or change a value. Interesting thing is that these methods are executed automatically. Well, this assumes there is some existing getter or setter. You don't have to call them explicitly. You don't have to call them at all.

All that is needed is someone trying to access and set a value of some property. If there is a getter or setter for that specific property it will be executed. Now, let's take a look at each.

## Property getters

Property getters, or methods, are used to access properties of objects. When you want to get value of some property, and this property has a getter method, that method will be executed. The getter method looks like a regular object method. The difference is the `get` keyword.

This `get` keyword is what tells JavaScript that you don't want to create regular object method, but a getter method. The way to use this keyword is to put it as first, before the name of the getter method. What follows is the name of the getter, parentheses and function body.

```JavaScript
// Create an object
let myObj = {
  // Example of a getter method
  // this getter will be executed
  // when you use myObj.myGetter
  get myGetter() {
    // Return something
    return ''
  }
}

// Accessing getter method
// NOTE: when you use getter method
// don't use parentheses at the end
myObj.myGetter


// Example:
// Create an object
let dog = {
  name: 'Jack',

  // Create getter method
  // this getter will be executed
  // when you use dog.getName
  get getName() {
    // this here refers to the "dog" object
    return `My dog's name is: ${this.name}`
  }
}

console.log(dog.getName)
// Output:
// "My dog's name is: Jack"
```

One thing to remember. Property getter should always return something, some value. If it doesn't return anything, you will get `undefined` when you try to use the getter. So, if you do add getter method, make sure it also contains `return` statement and returns something.

```JavaScript
// Create an object
let dog = {
  name: 'Jack',

  get getName() {}
}

console.log(dog.getName)
// Output:
// undefined
```

## h2

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
- JavaScript property getters and setters
- property getters and setters
- getters and setters
-->

<!--
### Resources:
-
-->
