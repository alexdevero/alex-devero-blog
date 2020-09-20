# Private Class Fields and Methods in JavaScript

JavaScript private class fields and methods are new features for JavaScript classes. In this tutorial, you will learn all you need to know about this feature. You will learn about what private methods and class fields are and how they work. You will also learn how to use them in your projects.<!--more-->
<!--
Table of Contents:
## Introduction
## Keeping it private
## The syntax
## Private class fields
## Accessing private class fields with methods
## Updating private class fields with methods
## Setters and getters and private class fields
## Private static class fields
## Private class fields and subclasses
## Private methods
## Private static methods
## Conclusion: Private class fields and methods in JavaScript
-->

## Introduction

When you want to add some data to [JavaScript class] you can do so through class properties. These properties are by default always public. This also means that they are publicly accessible and modifiable. The same also applies to class methods. They are also public by default.

This might often be okay. However, sometimes, you may want to keep some properties or methods private. You may want to make them inaccessible from the outside of the class they are defined in. This is where private methods and class fields can be handy.

## Keeping it private

The idea of keeping some things private is simple and straightforward. When you want to keep something private, be it a property or method, it should be accessible only from one place. This place is the class in which you defined that property or method.

If you try to access private class field or method from elsewhere JavaScript should not allow it. This includes outside the class in which the class field or method is defined. Also any instance of that class. However, it is possible to access private class field from a method inside the same class.

## The syntax

The syntax for private  class fields and methods is the same. It is also very simple, and quite controversial. When you want to declare some class field or method as private you have to prefix it with `#` (the hashtag symbol). Now, let's take a look more closely at private methods and class fields and how to work with them.

## Private class fields

Declaring private class field is simple. All you have to do is to prefix he name of the class field with `#`. This will tell JavaScript that you want this class field to be private. When you want to access that private class field, remember that you have to include the `#`.

```JavaScript
// Create new class
class MyClass {
  // Declare private class field
  #myPrivateField = 'I am private.'
}
```

## Accessing private class fields with methods

When you want to access some class property you have two options. First, you can create new instance of that class and access the property on that instance. Second, you can declare that property as a [static property]. In that case, you don't have to instantiate the class to access the property.

Private class fields are designed to be inaccessible from the outside. There is a way to overcome this. You can create new method and return the private class field from that method. You can define this method either as public method or [static].

Just like with static properties, you can call static methods without instantiating the class. If you declare the method as public, you will have to instantiate the class. After that, you will be able to call that method on your new instance and get the value of private field.

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

The same rules apply when you want to modify private class field. You can do that through a method. This method will be available for you to call from the outside. It will also be able to access the private class field and modify it in the way you want.

```JavaScript
// Create new class
class MyClass {
  // Declare private class field
  #myPrivateField

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

As we discussed, private class fields are inaccessible from the outside. For this reason, [getter and setter] accessors are useless. When you try to access, or modify, private class field from the outside JavaScript will throw an error. It doesn't matter if there is a setter and/or getter or not.

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

Accessing private class field with static method is a bit more complicated. Public class fields and methods are accessible only through class instances. They are not accessible through the classes themselves. As a result, creating a static method to access private class field will not work.

If you try this JavaScript will throw `TypeError`. One way to make this work is by declaring the private field as static as well. Now, you will be able to access the, now static, private class field through static method without instantiating the class.

When you want to declare class field as static, you have to start with the `static` keyword. This keyword is then followed by the class field name. In case of private class field, the name is prefixed by the `#` symbol.

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
  // NOTE: this will never work
  MyClass.#myPrivateField
  // Output:
  // SyntaxError: Private name #myPrivateField is not defined
} catch(error) {
  // Log any error
  console.log(error)
}
```

## Private class fields and subclasses

As we discussed, both private class field and method are accessible only from the inside of the class in which they are defined. This also means that they will be inaccessible for any subclasses. This applies to both, public as well as static private class field.

```JavaScript
// Create new class
class MyClass {
  // Declare private class field as static
  static #myPrivateField = 'I am private.'

  // Define static method that returns the private field
  static myMethod() {
    // Return the value of #myPrivateField
    return this.#myPrivateField
  }
}

// Create new subclass of MyClass
class MySubClass extends MyClass {}

try {
  // Try to call myMethod() on MySubClass
  MySubClass.myMethod()
  // Output:
  // TypeError: Private static access of wrong provenance

  // Try to access the private field directly on MySubClass
  // NOTE: this will never work
  MySubClass.#myPrivateField
  // Output:
  // SyntaxError: Private name #myPrivateField is not defined
} catch(error) {
  // Log any error
  console.log(error)
}


try {
  // Try to call myMethod() on MyClass
  MyClass.myMethod()
  // Output:
  // 'I am private.'

  // Try to access the private field directly on MyClass
  // NOTE: this will never work
  MyClass.#myPrivateField
  // Output:
  // SyntaxError: Private name #myPrivateField is not defined
} catch(error) {
  // Log any error
  console.log(error)
}
```

## Private methods

Along with private class fields you can also create private methods. Private methods work by the same rules as the class fields. These methods are accessible only from the inside of the class in which they are defined. This is the only place where you can use them.

When you want to call private method from the outside you can use the same thing as with private class fields. You can create new public method and inside this public method you can then call the private method.

The syntax for private methods is the same as for private class fields. The name of the method has to always start with the `#` symbol.

```JavaScript
class MyClass {
  // Declare private class field
  #myPrivateField = 'I am private.'

  // Define private method that returns the private field
  #myPrivateMethod() {
    // Return the value of #myPrivateField
    return this.#myPrivateField
  }

  // Define public method that returns the private method
  myPublicMethod() {
    return this.#myPrivateMethod()
  }
}

// Create new instance of MyClass
const myInstance = new MyClass()

try {
  // Try to call myMethod() on myInstance
  myInstance.myPublicMethod()
  // Output:
  // 'I am private.'

  // Try to access the private field directly on myInstance
  // NOTE: this will never work
  MyClass.#myPrivateMethod()
  // Output:
  // SyntaxError: Private name #myPrivateMethod is not defined
} catch(error) {
  // Log any error
  console.log(error)
}
```

## Private static methods

Just like private static class fields you can also create private static methods. The advantage of these methods is that you can call them without having to instantiate the class. When it comes to private static methods, the syntax is almost the same as for public methods.

The only difference is that now you have to start with the `static` keyword. What follows is the same. There is the method name prefixed by the `#` symbol and the function body.

```JavaScript
// Alternative with static method
class MyClass {
  // Declare static private class field
  static #myPrivateField = 'I am private.'

  // Define static private method that returns the private field
  static #myPrivateMethod() {
    // Return the value of #myPrivateField
    return this.#myPrivateField
  }

  // Define static public method that calls the private method
  static myPublicMethod() {
    return this.#myPrivateMethod()
  }
}

try {
  // Try to call myMethod() on MyClass
  MyClass.myPublicMethod()
  // Output:
  // 'I am private.'

  // Try to access the private field directly on MyClass
  // NOTE: this will never work
  MyClass.#myPrivateMethod()
  // Output:
  // SyntaxError: Private name #myPrivateMethod is not defined
} catch(error) {
  // Log any error
  console.log(error)
}
```

## Conclusion: Private class fields and methods in JavaScript

Private class fields and methods can be handy when you want to keep some data private. I hope this tutorial explained what private methods and class fields are and how they work. I also hope it helped you understand how to use both in your projects.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[JavaScript class]: https://blog.alexdevero.com/javascript-classes-pt1/
[static property]: https://blog.alexdevero.com/static-methods-properties-javascript-classes/#static-properties
[static]: https://blog.alexdevero.com/static-methods-properties-javascript-classes/#static-methods
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
-
-->
