# JavaScript Classes - A Friendly Introduction Pt.1
JavaScript classes are one of the hottest features introduced in ECMAScript 2015. It is also one of the features that are discussed the most. Learn all you need to know about JavaScript classes, and how they work, so you can start using them with rock-solid confidence.
<!--more-->
<!--
Table of Contents:
## Creating objects the old way, with function constructors
## Creating objects the new way, with JavaScript classes
## Constructor
## Class properties and methods
## Class inheritance (extends)
## Inheritance and child classes, or subclasses
## Overriding class constructor
## Overriding class properties and methods
## Extending class methods with superclasses and subclasses
## Extending class methods with subclasses and subclasses
## Epilogue: JavaScript Classes - A Friendly Introduction Pt.1

JavaScript Classes - A Friendly Introduction [Part 2].
-->

## Creating objects the old way, with function constructors

First things first. How could you as a developer create objects before the introduction of JavaScript classes? You could do so, and still can, with the help of function constructors. Then, when you wanted to add some properties or methods to the object you could do that in two ways. First, you could do it right away inside the constructor using `this`.

The second option? You could also add properties or methods to the object outside the constructor. In that case you would use `prototype` object. When you want to create new instance of the object, you defined it as new variable and use `new` keyword followed by the name of the object, and parenthesis. For example, `let myInstance = new MyObj()`.

Let's take a look at one simple example. As first, let's create new object `Person`, with four properties, `name`, `age`, `height`, `weight`, and one method, using function constructor (Step 1). Next, let's use that object and create two instances, `joe` and `samantha`, both with some data for default properties (Step 2).

Now, let's say that you want `joe` to have a gender (Step 3). As you can see, trying to log the `gender` property on `samantha` will not work (Step 4). Only `joe` has this property. If you want all instances of `Person` to have the `gender` property by default, you can add it, as I mentioned, in the beginning using `this` inside the constructor or later outside it using `prototype` object.

As you can see, logging gender property on `samantha` will now work (Step 5). Lastly, you can also add additional method to `Person` object. Again, using `prototype` object. For example, a method that will return the value of `age` property. As with `gender` property, all instances will also automatically inherit this method (Step 6).

```
///
// Step 1:
// Use function constructor to create Person object
function Person(name, age, height, weight) {
  // Add default object properties using 'this'
  // 'this' refers to the Person object
  this.name = name
  this.age = age
  this.height = height
  this.weight = weight

  // Add method to get the name property
  this.getName = function () {
    // Use 'this' keyword to refer to the 'name' property
    // of Person object.
    return this.name
  }
}


///
// Step 2:
// Create two instances of Person object, joe and samantha
let joe = new Person('Joe', 32, 180, 75)
let samantha = new Person('Samantha', 27, 176, 57)

// Log names of joe and samantha
console.log(joe.getName())
// Outputs: 'Joe'
console.log(samantha.getName())
// Outputs: 'Samantha'


///
// Step 3:
// Add gender property only to the joe instance and log it
joe.gender = 'male'
console.log(joe.gender)
// Outputs: male


///
// Step 4:
// Try to log gender of samantha instance
console.log(samantha.gender)
// Outputs: undefined
// Reason: 'gender' property exists only on joe instance


///
// Step 5:
// Use object prototype to add gender property to Person
Person.prototype.gender = '¯\_(ツ)_/¯'

// Try to log gender of samantha instance again
console.log(samantha.gender)
// Outputs: '¯_(ツ)_/¯'
// Reason: adding 'gender' to Person prototype automatically added it to all instances


///
// Step 6:
// Use object prototype to add method to get age property to the Person object prototype
Person.prototype.getAge = function () {
  // 'this' refers to the Person object
  return this.age
}

// Log age of joe and samantha
console.log(joe.getAge()) // 32
console.log(samantha.getAge()) // 27
```

## Creating objects the new way, with JavaScript classes

If you already heard about JavaScript classes you may also hear developers saying that JavaScript classes are just syntactic sugar. They are right. Although JavaScript classes may look like something completely new, under the hood are still function constructors. There is just a bit of ... Sugar on top.

Let's now rewrite the previous example into a JavaScript class. As you can see, the only difference is in the "Step 1". Here, we defined `person` as a class. The properties we want to pass as arguments when we create new instance are now defined using class `constructor`. Also, notice the lack of `this` when we define the `getName()` method.

What about the rest of the code? As you can see, and test, everything else is basically the same and works just like before. This applies also to the way you create new instances. You still use variables along with `new` keyword and the name of the object, well, now class.

```
///
// Step 1:
// Use JavaScript class to create Person object
class Person {
  constructor(name, age, height, weight) {
    // Add default object properties
    this.name = name
    this.age = age
    this.height = height
    this.weight = weight
  }

  // Add method to get name property
  getName() {
    return this.name
  }
}


///
// Step 2:
// Create two instances of Person object, joe and samantha
let joe = new Person('Joe', 32, 180, 75)
let samantha = new Person('Samantha', 27, 176, 57)

// Log names of joe and samantha
console.log(joe.getName())
// Outputs: 'Joe'
console.log(samantha.getName())
// Outputs: 'Samantha'


///
// Step 3:
// Add gender property only to the joe instance and log it
joe.gender = 'male'
console.log(joe.gender)
// Outputs: male


///
// Step 4:
// Try to log gender of samantha instance
console.log(samantha.gender)
// Outputs: undefined
// Reason: 'gender' property exists only on joe instance


///
// Step 5:
// Use object prototype to add gender property to Person
Person.prototype.gender = '¯\_(ツ)_/¯'

// Try to log gender of samantha instance again
console.log(samantha.gender)
// Outputs: '¯_(ツ)_/¯'
// Reason: adding 'gender' to Person prototype automatically added it to all instances


///
// Step 6:
// Use object prototype to add method to get age property to the Person object prototype
Person.prototype.getAge = function () {
  // 'this' refers to the Person object
  return this.age
}

// Log age of joe and samantha
console.log(joe.getAge()) // 32
console.log(samantha.getAge()) // 27
```

## Constructor

One of the things JavaScript classes have in common is the `constructor` method. This is a special method in the class. It is method that creates and initializes an object created with the class. This means that any time you create new instance of the class, JavaScript will automatically call the `constructor` method.

Few things you should know about JavaScript classes and `constructor` method. One, every class can have only one `constructor`. The use of `constructor` is simple. The typical use is to create default properties of the class. You can then pass these properties when you create new instances of the class. Or, you can declare them with some default values, or both.

Two, `constructor` method is optional. You can define classes with `constructor` (Example 1) or without it (Example 2). Three, if you include `constructor` in the class, you have to define it on the top of the class, as first. Otherwise, JavaScript will throw an error.

```
///
// Example 1: Class with constructor
class MyClass {
  // Use constructor to add class properties
  constructor(message = 'Hello world!') {
    this.message = message
  }

  // Add class method
  printMessage() {
    return this.message
  }
}

// Create instance of 'MyClass' class
const instanceOfMyClass = new MyClass()

// Print the message
console.log(instanceOfMyClass.printMessage())
// Outputs: 'Hello world!'


///
// Example 2: Class without constructor
class MyClass {
  // Add class method
  printMessage() {
    return 'Hello world!'
  }
}

// Create instance of 'MyClass' class
const instanceOfMyClass = new MyClass()

// Print the message
console.log(instanceOfMyClass.printMessage())
// Outputs: 'Hello world!'
```

## Class properties and methods

Attributes and behaviors in JavaScript classes are called class properties and class methods. You already saw examples of both on the previous examples. Few things to remember. One, when you want to add property to class, you do it in the `constructor` method. Two, when you want to add method, you do it inside the class, but outside the  `constructor`.

Three, when you want to reference any property, or method, inside the class you have to use `this` keyword. Here, you can think about `this` as a short alternative for "on this class". So, you could basically say  `this.property` as "property on this class", so to speak. Let's create `NewClass` class with two properties, `classPropOne`, `classPropTwo`, and two methods, `someClassMethod` and `anotherClassMethod`.

```
// Create new class called MyClass
class NewClass {
  // Add two class properties, 'classPropOne', 'classPropTwo'
  constructor(classPropOne, classPropTwo) {
    this.classPropOne = classPropOne
    this.classPropTwo = classPropTwo
  }

  // Add class method called 'someClassMethod'
  someClassMethod() {
    return this.classPropOne
  }

  // Add class method called 'anotherClassMethod'
  anotherClassMethod() {
    return this.classPropTwo
  }
}
```

Working with JavaScript classes and their properties and methods is very easy. You could see this in the example in the very beginning of this article, but it is worth mentioning again. You can also add new properties and methods to JavaScript classes later, without making changes directly to the class definition.

You can do this using the `prototype` object. This works with both, class properties as well as methods. The syntax is simple. First is the name of the class. Next comes the `prototype` keyword followed by the name of method or property, with dots between class name `prototype` and method or property name. After that comes the assignment.

```
// Add new method called 'newClassMethod' to 'NewClass' class
NewClass.prototype.newClassMethod = function() {
  return this.classPropOne + ' & ' + this.classPropTwo
}

// Create instance of NewClass called 'foo'
let foo = new NewClass('foo', 'bar')

// Test that new works
console.log(foo.newClassMethod())
// Outputs: 'foo & bar'
```

## Class inheritance (extends)

That was the basic stuff about JavaScript classes. Now let's talk about inheritance, or extending classes. Extending classes basically means that you create one class, child class or subclass, based on another class, parent class or superclass. The child class, or subclass, inherits properties and methods from the parent class, or superclass.

The main benefit of this is that you can add functionality without changing the original class. This is especially important when you don't want to change instances of that class. If you add functionality to the class using the `prototype` any change you make in the class will automatically propagate to all its instances.

Imagine you have a class called `Vehicle`. This class has some properties, such as `name`, `condition` and `speed`. Now, let's say that you want to use this class to create a plane, car and a boat. All these vehicles can have properties specific to them, such as number of wheels, number of engines, number of propellers, etc.

One, a very bad, option is to add all these properties to the `Vehicle` class. The problem is that this would clutter all instances of `Vehicle` class with properties, or methods, they would never use. Another, and much better, option is to use inheritance. Meaning, you will create subclasses for `plane`, `car` and `ship` using `Vehicle` as a superclass.

This will allow you to add specific properties only to classes, or subclasses, that will use them. What's more, since all these new classes will be subclasses of `Vehicle` superclass, they all will be able to share some properties and methods, those inherited from `Vehicle`.

The way to create subclasses of a superclass, or to extend classes, is simple. You declare the class as usually, but add `extends` and name of the superclass between the name of the class and curly braces. For example, `class MySubclass extends SuperClass {}`. Then, you can add properties and methods as you would with a normal class.

```
// Create superclass Vehicle
class Vehicle {
  constructor(name, condition, speed) {
    this.name = name
    this.condition = condition
    this.speed = speed
  }
}


// Create Car subclass
class Car extends Vehicle {
  constructor(name, condition, speed, numOfWheels) {
    // Call super() with all parameters required for Vehicle class
    super(name, condition, speed)

    this.numOfWheels = numOfWheels
  }

  // Add method to print all properties
  printInfo() {
    return `Name: ${this.name}, Condition: ${this.condition}, Max. speed: ${this.speed}, Number of Wheels: ${this.numOfWheels}`
  }
}


// Create Plane subclass
class Plane extends Vehicle {
  constructor(name, condition, speed, numOfEngines) {
    // Call super() with all parameters required for Vehicle class
    super(name, condition, speed)

    this.numOfEngines = numOfEngines
  }

  // Add method to print all properties
  printInfo() {
    return `Name: ${this.name}, Condition: ${this.condition}, Max. speed: ${this.speed}, Number of Engines: ${this.numOfEngines}`
  }
}


// Create Ship subclass
class Ship extends Vehicle {
  constructor(name, condition, speed, numOfPropellers) {
    // Call super() with all parameters required for Vehicle class
    super(name, condition, speed)

    this.numOfPropellers = numOfPropellers
  }

  // Add method to print all properties
  printInfo() {
    return `Name: ${this.name}, Condition: ${this.condition}, Max. speed: ${this.speed}, Number of Propellers: ${this.numOfPropellers}`
  }
}


// Create instance of Car class
const tesla = new Car('Tesla', 'new', 280, 2)
console.log(tesla.printInfo())
// Outputs: 'Name: Tesla, Condition: new, Max. speed: 280, Number of Wheels: 2'


// Create instance of Ship class
const catamaran = new Ship('Catamaran', 'new', 140, 2)
console.log(catamaran.printInfo())
// Outputs: 'Name: Catamaran, Condition: new, Max. speed: 140, Number of Propellers: 2'


// Create instance of Plane class
const cesna = new Plane('Cesna', 'new', 234, 2)
console.log(cesna.printInfo())
// Outputs: 'Name: Cesna, Condition: new, Max. speed: 234, Number of Engines: 2'
```

### Inheritance and child classes, or subclasses

One thing you should know about inheritance. It is not limited to superclasses. You can also let one subclass inherit from another subclass, that can also inherit from yet another subclass that can inherit from a superclass. Taken to the extreme, you can create a chain of hundreds of subclasses inheriting one from the other with single superclass on top.

```
// Create superclass Animal
class Animal {
  // Some code
}

// Create subclass Mammal that inherits from superclass Animal
class Mammal extends Animal {
  // Some code
}

// Create subclass Cat that inherits from subclass Mammal
class Cat extends Mammal {
  // Some code
}

// Create subclass Kitten that inherits from subclass Cat
class Kitten extends Cat {
  // Some code
}

// Create subclass Tomcat that inherits from subclass Kitten
class Tomcat extends Kitten {
  // Some code
}
```

### Overriding class constructor

As you could see in the example above, all subclasses had their own `constructor` method. This means that they were overriding the superclass `constructor`. When this happens, when a subclass overrides the `constructor` of the superclass, you have to call the `super()` method, with all initial `constructor` parameters.

Calling `super()` inside the `constructor` calls the `constructor` of the superclass, in this case the `Vehicle`. This then allows subclasses to use the properties defined in the superclass `constructor`. One important thing to remember is that you have to call the `super()` method has to be called at the top of `constructor`.

You have to call it before you add any properties. If you forget it, `this`, and its reference to the class, will not exist and JavaScript will throw an error. And, what if the subclass doesn't have its own constructor, it is not overriding the superclass `constructor`? Then, you don't have to worry about anything, the `constructor` or `super()`.

```
// Create superclass MyClass
class MyClass {
  constructor(name) {
    this.name = name
  }
}


// Create subclass of MyClass superclass
// that doesn't override the constructor of the superclass
class MySubClass extends MyClass {
  getName() {
    return this.name
  }
}

// Create instance of MySubClass
let instanceOfMySubClass = new MySubClass('Johny')

// Test that subclass can access the 'name' property
console.log(instanceOfMySubClass.getName())
// Outputs: 'Johny'


// Create subclass of MyClass superclass
// that overrides the constructor of the superclass
class AnotherSubClass extends MyClass {
  constructor(name, mood) {
    // Call super() with all initial parameters - the 'name'
    // Allows to use 'this' and gives access to 'name' property
    super(name)

    // Add new property
    this.mood = mood
  }
}

// Create instance of AnotherSubClass
let instanceOfAnotherSubClass = new AnotherSubClass('Tom', 'happy')
// Log Tom's mood
console.log(instanceOfAnotherSubClass.mood)
// Outputs: 'happy'
```

### Overriding class properties and methods

Now you know how to override `constructor` of a superclass. Overriding properties and methods of a superclass is just as easy. When you want to override class property in a subclass you add the `constructor`, call the `super()` with all initial parameters, pick the property you want to change and simply change it, its value.

When you want to override class method, the process is even easier. All you have to do is use the same method name in the subclass and change what it does, the code inside.

```
// Create superclass Entity
class Entity {
  // Create class constructor
  constructor() {
    // Add class property
    this.isHuman = null
  }

  // Add class method
  identifyYourself() {
    return 'I am neither a human nor a robot.'
  }
}


// Create subclass of Entity superclass
// This subclass overrides both, class property and method.
class Man extends Entity {
  // Add subclass' own constructor
  constructor() {
    // Call super() - allows to use 'this'
    // and gives access to 'isHuman' property
    super()

    // Override class property
    this.isHuman = true
  }

  // Override the 'identifyYourself()' method
  identifyYourself() {
    return 'I am a human.'
  }
}

// Create instance of Man subclass
let jake = new Man()
console.log(jake.isHuman)
// Outputs: true
console.log(jake.identifyYourself())
// Outputs: 'I am a human.'


// Create subclass of Entity superclass
// This subclass overrides only class property.
class Woman extends Entity {
  // Add subclass' own constructor
  constructor() {
    // Call super() - allows to use 'this'
    // and gives access to 'isHuman' property
    super()

    // Override class property
    this.isHuman = true
  }
}

// Create instance of Robot subclass
let melissa = new Woman()
console.log(melissa.isHuman)
// Outputs: true


// Create subclass of Entity superclass
// This subclass overrides only class method.
class Robot extends Entity {
  // Override the 'identifyYourself()' method
  identifyYourself() {
    return 'I am a robot.'
  }
}

// Create instance of Robot subclass
let android = new Robot()
console.log(android.identifyYourself())
// Outputs: 'I am a robot.'
```

### Extending class methods with superclasses and subclasses

Okay, but what if you don't want to completely replace the superclass method? What if you want to build on top of it, extend it or tweak it? This is where you can use the `super` again. Previously, you used `super()` as a method, to call the superclass' `constructor` (inside the constructor only). However, you can use `super` also as a keyword.

When you use `super` as a keyword, along with the name of the method, you call the original version of the method that exists inside the superclass. In other words, you can use call the original method using `super` keyword and then add any additional code. As a result, the subclass will not replace the method, but build on top of it, extend it.

```
// Create superclass Human
class Human {
  // Add class method
  sayHi() {
    console.log('I am a human.')
  }
}


// Create subclass of Human superclass
class Man extends Human {
  // Extend the 'sayHi()' method
  sayHi() {
    // Call the superclass' 'sayHi()' method
    super.sayHi()

    console.log('I am also a man.')
  }
}

// Create instance of Man subclass
let timothy = new Man()
timothy.sayHi()
// Outputs:
// 'I am a human.' (result of calling super.sayHi() in Man)
// 'I am also a man.'
```

### Extending class methods with subclasses and subclasses

As you know, one subclass can inherit from another subclass. What if you use `super` keyword to call some method in a subclass, that inherits from another subclass? It will call the method as it exists in the subclass your current subclass is extending, or one level higher.

In other words, let's say that `foo` extends `bar`, and `bar` extends `bazz`, and `bazz` extends `fuzz`. Then, calling `super.someMethod()` in `foo` will call that `someMethod()` in `bar`, because `foo` extends `bar`. If you call the `super.someMethod()` in `bar` will call that `someMethod()` in `bazz`, because `bar` extends `bazz`.

What if you call some method using the `super` in every subclass it the chain? As you can guess, the result will be nice chain reaction.

```
// Create superclass Human
class Human {
  // Add class method
  sayHi() {
    console.log('I am a human.')
  }
}


// Create subclass of Human superclass
class Man extends Human {
  // Extend the 'sayHi()' method
  sayHi() {
    // Call the superclass' 'sayHi()' method
    super.sayHi()

    console.log('I am also a man.')
  }
}

// Create subclass of Man subclass
class Boy extends Man {
  // Extend the 'sayHi()' method
  sayHi() {
    // Call the superclass' 'sayHi()' method
    super.sayHi()

    console.log('I am also a boy.')
  }
}

// Create subclass of Boy subclass
class Baby extends Boy {
  // Extend the 'sayHi()' method
  sayHi() {
    // Call the superclass' 'sayHi()' method
    super.sayHi()

    console.log('And I am also a baby.')
  }
}

// Create instance of Robot subclass
let timothy = new Baby()
timothy.sayHi()
// Outputs:
// 'I am a human.'
// 'I am also a man.' (result of calling super.sayHi() in Man)
// 'And I am also a boy.' (result of calling super.sayHi() in Boy)
// 'And I am also a baby.'
```

## Epilogue: JavaScript Classes - A Friendly Introduction Pt.1

Congratulations! Let's do a quick recap. In the beginning, you've learned about the difference between the old way to create objects, using function constructors, and the new way, using JavaScript classes. Then, you've learned about the basics, parts of JavaScript classes and related concepts that are important to know.

These parts and concepts include constructor, class properties and methods, inheritance, superclasses and subclasses and also how to override constructor and class properties and methods. These were the basics. In the next part, you will learn about advanced topics such as static properties and methods, class fields, mixins and more.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
<!-- [Part 2]: -->

<!--
### Meta:
-
-->

<!--
#### Resources:
- https://javascript.info
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes
- https://alligator.io/js/objects-prototypes-classes/
- https://alligator.io/js/class-composition/
- https://medium.com/tech-tajawal/javascript-classes-under-the-hood-6b26d2667677
-->
