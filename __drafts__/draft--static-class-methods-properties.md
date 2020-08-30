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

  // Create public method
  myPublicMethod() {
    console.log('Call from myPublicMethod.')
  }
}

// Try to call static method "myStaticMethod" on "MyClass"
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

// Try to call static method "myStaticMethod" on "MyClass"
MyClass.myStaticMethod()
// Output:
// 'Call from myStaticMethod.'
```

### Static methods and class instances

When it comes to static methods, remember one thing. These methods can be called only on the class in which they are defined. If you create a an instance of that class, and try to call some static method on that instance, JavaScript will return TypeError. The same will happen if you try to call public method on a class without instantiating it first.

```JavaScript
// Create class
class MyClass {
  // Add new static method to "MyClass"
  static myStaticMethod() {
    console.log('Call from myStaticMethod.')
  }

  // Create public method
  myPublicMethod() {
    console.log('Call from myPublicMethod.')
  }
}

// Try to call static method "myStaticMethod" on "MyClass"
MyClass.myStaticMethod()
// Output:
// 'Call from myStaticMethod.'

// Try to call public method "myPublicMethod" on "MyClass"
MyClass.myPublicMethod()
// Output:
// TypeError: MyClass.myPublicMethod is not a function

// Create instance of "MyClass"
const myClassInstance = new MyClass()

// Try to call static method "myStaticMethod" on "myClassInstance"
myClassInstance.myStaticMethod()
// Output:
// TypeError: myClassInstance.myStaticMethod is not a function

// Try to call public method "myPublicMethod" on "myClassInstance"
myClassInstance.myPublicMethod()
// Output:
// 'Call from myPublicMethod.'
```

### Static methods and this

When you define static method inside a class value of `this` will always be the class itself. Since static methods are inaccessible from instances, you don't have to worry that `this` could change from time to time.

```JavaScript
// Create class
class MyClass {
  static myStaticMethod () {
    console.log(this)
    console.log(this === MyClass)
  }
}

// Try to call static method "myStaticMethod" on "MyClass"
MyClass.myStaticMethod()
// Output:
// [Function: MyClass]
// true
```

## Static properties

Just as you can have static methods you can also have static properties. Static properties work in similar way as static methods. You can define them in two ways. Fist, directly within a class. In this case, you have to prepend the property with `static` keyword. You can also define the property outside the class with dot notation.

```JavaScript
// Create class
class MyClass {
  // Define static property
  static myStaticProperty = 'Hello'
}

// Or, define static property outside the class
MyClass.myStaticPropertyTwo = 'World'

// Try to access static property "myStaticProperty" on "MyClass"
console.log(MyClass.myStaticProperty)
// Output:
// 'Hello'

// Try to access static property "myStaticPropertyTwo" on "MyClass"
console.log(MyClass.myStaticPropertyTwo)
// Output:
// 'World'
```

### Static properties and class instances

Static properties can be accessed only inside the class in which they are defined. They are invisible to instances of that class. If you try to access static property from class instance, JavaScript will return `undefined`.

```JavaScript
// Create class
class MyClass {
  // Create static property
  static myStaticProperty = 'Hello'
}

// Try to access static property "myStaticProperty" on "MyClass"
console.log(MyClass.myStaticProperty)
// Output:
// 'Hello'

// Create instance of "MyClass"
const myClassInstance = new MyClass()

// Try to access static property "myStaticProperty" on "myClassInstance"
console.log(myClassInstance.myStaticProperty)
// Output:
// undefined
```

### Accessing static properties from methods

As we discussed, static properties are not accessible from class instances. JavaScript will also not allow to call public method on a class without instantiating it first. This means that you can't use public method to access static property neither a class, nor in its instance.

This leaves us with two ways in which you can access static properties in classes. The first one via static method. This makes sense. You need a method you can call directly on a class, not its instance. Only static method meets this condition. So, one way to access static property is by using static method.

```JavaScript
// Create class
class MyClass {
  // Create static property
  static myStaticPropertyOne = 'Hello'

  // Create static method
  static updateStaticProp() {
    // Update "myStaticPropertyOne"
    this.myStaticPropertyOne = 'Bye'
  }

  // Create public method
  myPublicMethod() {
    // Try to update "myStaticPropertyOne"
    this.myStaticPropertyOne = 'Come again?'
  }
}

// Log the value of "myStaticPropertyOne"
console.log(MyClass.myStaticPropertyOne)
// Output:
// 'Hello'

// Call static method "updateStaticProp" to change "myStaticPropertyOne"
MyClass.updateStaticProp()

// Log the value of "myStaticPropertyOne" again
console.log(MyClass.myStaticPropertyOne)
// Output:
// 'Bye'

// Create instance of "MyClass"
const myClassInstance = new MyClass()

// Call "myPublicMethod" on "myClassInstance" to change "myStaticPropertyOne"
// This will NOT work
myClassInstance.myPublicMethod()

// Log the value of "myStaticPropertyOne" again
console.log(MyClass.myStaticPropertyOne)
// Output:
// 'Bye'

// Log the value of "myStaticPropertyOne" again
console.log(MyClass.myStaticPropertyOne)
// Output:
// 'Bye'
```

The second option is using class [constructor method]. Constructor is a special method that is called every time you create an instance of a class. Unlike public methods, this special method can also access static properties. If you want to make some automatic updates to static properties, `constructor` might be a good choice.

On thing about using `constructor` to access static properties. When you use it, you have to access the static property using the name of the class, not `this`. The reason is that `this` in constructor refers to the current instance, not the class itself. So, using `this` would be like `instance.property`, not `class.property`.

```JavaScript
// Create class
class MyClass {
  // Create another static property
  static myStaticPropertyOne = 0

  // Create constructor method
  constructor() {
    // Update "myStaticPropertyOne" when new instance
    // of "MyClass" class is created
    // Notice we are using the name of the class, "MyClass",
    // not "this" to access the "myStaticPropertyOne"
    MyClass.myStaticPropertyOne += 1

    // NOTE:
    // This will NOT work
    // this here refers to specific instance of "MyClass"
    // not "MyClass" class itself
    // this.myStaticPropertyOne += 1
  }
}

// Log the value of "myStaticPropertyOne"
console.log(MyClass.myStaticPropertyOne)
// Output:
// 0

// Create instance of "MyClass"
const myClassInstanceOne = new MyClass()

// Log the value of "myStaticPropertyOne"
console.log(MyClass.myStaticPropertyOne)
// Output:
// 1

// Create another instance of "MyClass"
const myClassInstanceTwo = new MyClass()

// Log the value of "myStaticPropertyOne"
console.log(MyClass.myStaticPropertyOne)
// Output:
// 2
```

Aside to this, remember that you can always access static property directly. You can do this by using the name of the class and the name of the property, and dot notation.

```JavaScript
class MyClass {
  // Create another static property
  static myStaticProperty = 'Hello'
}

// Access the "myStaticProperty"
console.log(MyClass.myStaticProperty)
// Output:
// 'Hello'
```

## Static properties and methods and class inheritance

Static properties and methods are not visible for class instances and they can't access them. This is not true for subclasses, or child classes. Let's say you have a class with some static properties or methods. Next, let's say decide to subclass this class. You decide to use this class to [extend] other classes.

If you do this, all those subclasses will also inherit all static properties and methods of the superclass, or parent class. This means that you will be able to access those static properties and methods also on those subclasses. However, static properties and methods will still be inaccessible for instance of these subclasses.

```JavaScript
class MyClass {
  // Create another static property
  static myStaticProperty = 'Hello'
}


// Create subclass of "MyClass"
class MyClassSubclassOne extends MyClass {}

// Try to access the "myStaticProperty" on "MyClassSubclassOne"
console.log(MyClassSubclassOne.myStaticProperty)
// Output:
// 'Hello'


// Create another subclass of "MyClass"
class MyClassSubclassTwo extends MyClass {}

// Try to access the "myStaticProperty" also on "MyClassSubclassTwo"
console.log(MyClassSubclassOne.myStaticProperty)
// Output:
// 'Hello'


// Create instance of "MyClassSubclassOne"
const MyClassSubclassOneInstance = new MyClassSubclassTwo()

// Try to access the "myStaticProperty" on "MyClassSubclassOneInstance"
console.log(MyClassSubclassOneInstance.myStaticProperty)
// Output:
// undefined


// Create instance of "MyClassSubclassTwo"
const myClassSubclassTwoInstance = new MyClassSubclassTwo()

// Try to access the "myStaticProperty" on "myClassSubclassTwoInstance"
console.log(myClassSubclassTwoInstance.myStaticProperty)
// Output:
// undefined
```

### Static properties and methods and class inheritance explained

The reason this works is due to [prototypal inheritance], the [[[Prototype]] property] to be more specific. When you create new class it has its own `[[Prototype]]`. For example, when you create new class "MyClass" the prototype of this class will be "MyClass". What happens when use this class to extend other classes, to create subclasses?

When you use this class to extend other classes the prototypes of those new classes will refer to the superclass prototype. In case of "MyClass" class, their prototype will refer to "MyClass". When you try to access some property or method in a subclass, JavaScript will first look for that property or method in that subclass.

If it finds the property or method on the subclass it will access it. If not, it will look at what is the subclass prototype. Then, it will look at that prototype, the superclass, or parent class, you used to extend that subclass. If it finds the property or method there on the superclass it will access it there.

```JavaScript
class MyClass {
  // Create another static property
  static myStaticProperty = 'Hello'
}


// Create subclass of "MyClass"
class MyClassSubclassOne extends MyClass {}

// Check if prototype of "MyClassSubclassOne" is "MyClass"
console.log(MyClassSubclassOne.__proto__ === MyClass)
// Output:
// true

// Log the prototype of "MyClassSubclassOne"
console.log(MyClassSubclassOne.__proto__)
// Output:
// [Function: MyClass] { myStaticProperty: 'Hello' }


// Create another subclass of "MyClass"
class MyClassSubclassTwo extends MyClass {}

// Check if prototype of "MyClassSubclassTwo" is "MyClass"
console.log(MyClassSubclassTwo.__proto__ === MyClass)
// Output:
// true

// Log the prototype of "MyClassSubclassOne"
console.log(MyClassSubclassTwo.__proto__)
// Output:
// [Function: MyClass] { myStaticProperty: 'Hello' }
```

## Conclusion: JavaScript classes and static methods and properties

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[instantiate class]: https://blog.alexdevero.com/javascript-classes-pt1/#inheritance-and-child-classes-or-subclasses
[constructor method]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/constructor
[extend]: https://blog.alexdevero.com/javascript-classes-pt1/#class-inheritance-extends
[prototypal inheritance]: https://blog.alexdevero.com/prototype-prototypal-inheritance/
[[[Prototype]] property]: https://blog.alexdevero.com/prototype-prototypal-inheritance/#the-prototype-property

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
