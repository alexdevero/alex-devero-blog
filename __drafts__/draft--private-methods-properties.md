# Private Class Fields and Methods in JavaScript

Private class fields are one of the new features for JavaScript classes. In this tutorial, you will learn all you need to know about this feature. You will learn about what private class fields are and how they work. You will also learn how to use them in JavaScript, or TypeScript, projects.

<!--more-->
<!--
Table of Contents:
-->

## Introduction

When you want to add some data to [JavaScript class] you can do so through class properties. These properties are by default always public. This also means that they are publicly accessible and modifiable. The same also applies to class methods. They are also public by default.

This might be okay in many cases. However, sometimes, you may want to keep some properties or methods private. You may want to make them inaccessible from the outside of the class they are defined in. This is where private class fields and private methods can be handy.

## Keeping it private

The idea of keeping some things private is simple and straightforward. When you want to keep something private, be it a property or method, it should be accessible only from one place. This place is the class in which you defined that property or method.

If you try to access private property or method from elsewhere JavaScript should not allow it. This includes outside the class in which the property or method at hand is defined, or some instance of that class. However, it is possible to access private property from a method inside the same class.

## The syntax

The syntax for private class fields and methods is the same. It is also very simple, and quite controversial. When you want to declare some property or method as private you have to prefix it with `#` (the hashtag symbol). Now, let's take a look more closely at private properties and methods and how to work with them.

## Private class fields

Declaring private class field is simple. All you have to do is to prefix he name of the property with `#`. This will tell JavaScript that you want this property to be private. When you want to access that private property, remember that you have to include the `#`.

```JavaScript
// Create new class
class MyClass {
  // Declare private class field
  #myPrivateField = 'I am private.'
}
```

## Accessing private class fields with methods

When you want to access some class property you have two options. First, you can create new instance of that class and access the property on that instance. Second, you can declare that property as [static]. In that case, you don't have to instantiate the class in order to access the property.

That said, remember that private properties are designed to be inaccessible from the outside. One way to overcome this is by creating new method and returning the private property from that method. You can define that method either as a public method or [static method].

Just like with static properties, you can call static methods without instantiating the class first. If you declare the method as public, you will have to instantiate the class. After that, you will be able to call that method on your new instance and get the value of private field.

```JavaScript
// Create new class
class MyClass {
  // Declare private class field
  #myPrivateField = 'I am private.'

  // Define public method
  myMethod() {
    // Return the value of #myPrivateField
    return this.#myPrivateField
  }
}

// Create instance of MyClass
const myInstance = new MyClass()

try {
  // Try to call myMethod() on myInstance
  myInstance.myMethod()
  // Output:
  // 'I am private.'

  // Try to access the private field directly
  myInstance.#myPrivateField
  // Output:
  // SyntaxError: Private name #myPrivateField is not defined
} catch(error) {
  // Log any error
  console.log(error)
}
```

## Updating private class fields with methods

The same rules apply when you want to modify private property. You can do that through a method. This method, when you call it from the outside, will be able to access the private property and modify it in the way you want.

```JavaScript
// Create new class
class MyClass {
  // Declare private class field
  #myPrivateField = 'I am private.'

  // Define public method to return the private field
  returnPrivateField() {
    // Return the value of #myPrivateField
    return this.#myPrivateField
  }

  // Define public method to update the private field
  updatePrivateField(val) {
    // Update the value of #myPrivateField
    this.#myPrivateField = val
  }
}

// Create instance of MyClass
const myInstance = new MyClass()

try {
  // Try to call myMethod() on myInstance
  myInstance.updatePrivateField('Hello')

  // Try to access the private field directly
  myInstance.returnPrivateField()
  // Output:
  // 'Hello'
} catch(error) {
  // Log any error
  console.log(error)
}
```

## Setters and getters and private class fields

Private class fields, or private properties, are inaccessible from the outside. For this reason, [getter and setter] accessors are useless. When you try to access, or modify, private property from the outside JavaScript will throw an error. It doesn't matter if there is a setter and/or getter or not.

```JavaScript
// Create new class
class MyClass {
  // Declare private class field
  #myPrivateField

  // Define setter method for the private field
  set myPrivateField(value) {
    // Return the value of #myPrivateField
    this.#myPrivateField = value
  }

  // Define getter method for the private field
  get myPrivateField() {
    // Return the value of #myPrivateField
    return this.#myPrivateField
  }
}

// Create instance of MyClass
const myInstance = new MyClass()

try {
  // Try to change the value of  call myMethod() on myInstance
  myInstance.#myPrivateField = 'Hi'
  // Output:
  // SyntaxError: Private name #myPrivateField is not defined

  // Try to access the private field directly
  myInstance.#myPrivateField
  // Output:
  // SyntaxError: Private name #myPrivateField is not defined
} catch(error) {
  // Log any error
  console.log(error)
}
```

## Private static class fields

The second option, creating the method to access the private class field as static is a bit more complicated. Public properties and methods are accessible only through class instances, not through classes themselves. Here is the thing. Creating static method to access private property will not work.

If you try this JavaScript will throw `TypeError` about trying to access private field on non-instance. The way to make this work is by declaring the private field as static as well. Now, you will be able to access the, now static, private property through static method without instantiating the class.

```JavaScript
// Alternative with static method
class MyClass {
  // Declare private class field as static
  static #myPrivateField = 'I am private.'

  // Define public method
  static myMethod() {
    // Return the value of #myPrivateField
    return this.#myPrivateField
  }
}

try {
  // Try to call myMethod() on MyClass
  MyClass.myMethod()
  // Output:
  // 'I am private.'

  // Try to access the private field directly
  MyClass.#myPrivateField
  // Output:
  // SyntaxError: Private name #myPrivateField is not defined
} catch(error) {
  // Log any error
  console.log(error)
}
```

## Private class fields and subclasses



## Private methods

## Conclusion: [...] ...

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[JavaScript class]: https://blog.alexdevero.com/javascript-classes-pt1/
[static]: https://blog.alexdevero.com/static-methods-properties-javascript-classes/#static-properties
[static method]: https://blog.alexdevero.com/static-methods-properties-javascript-classes/#static-methods
[getter and setter]: https://blog.alexdevero.com/javascript-classes-pt2/#getter-and-setter-accessors

<!--
### Meta:
-
-->

<!--
### Keywords:
- private class fields
- javascript private methods
- private properties
-->

<!--
### Resources:
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/Private_class_fields
- https://javascript.info/private-protected-properties-methods
- https://www.sitepoint.com/javascript-private-class-fields/
- https://www.valentinog.com/blog/private/
- https://blog.alexdevero.com/static-methods-properties-javascript-classes/
-->
