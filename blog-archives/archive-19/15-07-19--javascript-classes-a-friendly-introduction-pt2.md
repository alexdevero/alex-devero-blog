# JavaScript Classes - A Friendly Introduction Pt.2
JavaScript classes can make your code cleaner and more readable. This article will help you understand concepts such as class fields, getter and setter accessors and mixins. Learn how to work with JavaScript classes like a Pro, improve your programming skills, and become a better JavaScript developer.
<!--more-->
<!--
Table of Contents:
## JavaScript classes and class fields
### Public fields and methods
### Private fields and methods
### Static properties and methods
## Getter and setter accessors
## Mixins
### Combining mixins
### Mixins and overriding properties and methods
### Mixins as class blueprints
## Epilogue: JavaScript Classes - A Friendly Introduction Pt.2
-->

JavaScript Classes - A Friendly Introduction [Part 1].

## JavaScript classes and class fields

The more often you start using JavaScript classes the faster you will get used to the new syntax. That being said, future ECMAScript proposals may make working with JavaScript classes easier. Class fields are one example. Do you remember the class `constructor`? Good news is that it may no longer be required.

The goal of class fields, also called class properties, is to allow JavaScript developers create simpler constructors in JavaScript classes. Put simply, you will no longer have to declare class properties inside `constructor`. Instead, you could declare them directly, outside it and even omit the `constructor` itself.

### Public fields and methods

One thing you need to know, and remember for the future, is that when you do this, all the fields you declared will become "public" fields by default. This means that all those fields will be accessible from the inside as well as the outside of the class. You will be able to examine them and change them as you want. The same applies to methods.

```
// ES6 class - without class fields
class SoccerPlayer {
  // Declare all class properties inside the constructor
  constructor() {
    this.assists = 0
    this.goals = 0
    this.number = null
    this.position = null
    this.team = null
  }

  addAssist() {
    this.assists++
  }

  addGoal() {
    this.goals++
  }

  addToTeam(team) {
    this.team = team
  }

  assignNumber(number) {
    this.number = number
  }

  assignPosition(position) {
    this.position = position
  }
}

// ESNext class - with public class fields
class SoccerPlayer {
  // Declare all properties directly, as public by default
  assists = 0
  goals = 0
  number = null
  position = null
  team = null

  // All these methods created as public by default
  addAssist() {
    this.assists++
  }

  addGoal() {
    this.goals++
  }

  addToTeam(team) {
    this.team = team
  }

  assignNumber(number) {
    this.number = number
  }

  assignPosition(position) {
    this.position = position
  }
}
```

As you can see, class fields can make working with JavaScript classes easier and your code cleaner and more readable. This is especially true if you work with React. Then, class fields can help you reduce your JavaScript code even more.

```
// ES6 class + React - without class fields
import * as React from 'react'

class MyComponent extends React.Component {
  // Declare class state inside the constructor
  constructor(props) {
    super(props)

    this.state = {
      firstName: '',
      lastName: '',
      age: 0
    }

    this.handleInputChange = this.handleInputChange.bind(this)
  }

  handleInputChange(event) {
    this.setState({
      [event.target.name]: [event.target.value]
    })
  }

  render() { ... }
}


// ESNext class + React - with class fields
import * as React from 'react'

class MyComponent extends React.Component {
  // Declare class state directly as public class property
  state = {
    firstName: '',
    lastName: '',
    age: 0
  }

  handleInputChange = (event) => {
    this.setState({
      [event.target.name]: [event.target.value]
    })
  }

  render() { ... }
}
```

The proposal for class fields is currently at [TC39 stage 3]. If everything goes well, it could appear in ES2019, or ES10. However, that doesn't mean you can't use it today. Both, [TypeScript] and [Babel] support class fields. So, if you use one of these you can also start using class fields right away.

### Private fields and methods

As we discussed, all class properties, or fields, are public by default. So, anyone can access them and modify them. This may not be desirable in all situations. Sometimes, you may want to keep some properties to be hidden, or inaccessible, from the outside of the class. This is exactly what private fields can do.

When you declare some class property as private you can access it only inside that class. So, if you want to access and change that property you can create methods inside that class and use them to change those properties. The syntax for creating private fields is simple, just start the property name with `#`. Remember to use the `#` when you want to access the property.

```
// Class with public and private properties
class MyClass {
  // Create public property
  foo = 'This is a public property.'

  // Create private property
  // Remember to start with '#'
  #bar = 'This is a private property.'

  // Add method to access and return public property 'foo'
  getFoo() {
    return this.foo
  }

  // Add method to access and return private property 'bar'
  getBar() {
    // Remember to use full name of the property, including the '#'
    return this.#bar
  }

  // Add method to change private property 'bar'
  changeBar(text) {
    // Remember to use full name of the property, including the '#'
    this.#bar = text
  }
}

// Create instance of MyClass
const classInstanceOne = new MyClass()

// Try to log public property 'foo' with 'getFoo()' method
console.log(classInstanceOne.getFoo())
// Outputs: 'This is a public property.'

// Try to log private property 'bar' with 'getBar()' method
console.log(classInstanceOne.getBar())
// Outputs: 'This is a private property.'

// Try to log public property 'foo' directly
console.log(classInstanceOne.foo)
// Outputs: 'This is a public property.'

// Try to log private property 'bar' directly
console.log(classInstanceOne.#bar)
// Outputs: SyntaxError: Undefined private field undefined: must be declared in an enclosing class

// Use 'changeBar' method to change private property 'bar'
classInstanceOne.changeBar('This is new text.')

// Try to log private property 'bar' with 'getBar()' method again
console.log(classInstanceOne.getBar())
// Outputs: 'This is new text.'
```

Similarly to public methods, you can also create methods that are [private]. The rules are the same as for private properties, or fields. These methods are visible only from the inside of the class. You can't access them or use them from the outside. The syntax is the same as well. Start the name of the method with '#'.

```
// Class with private property and method
class MyClass {
  #bar = 'This is a private property.'

  // Add private method
  #getBar() {
    // Change the value of private property 'bar'
    this.#bar = 'Let\'s update this property.'
  }

  // Add public method to triggers private method 'useGetBar()'
  useGetBar() {
    this.#getBar()
  }
}
```

### Static properties and methods

Public and private properties and methods are not the only you can use in your code. JavaScript classes also support static properties and methods. One difference between public, and private, and static properties and methods is that static properties and methods can be called on a class without creating new instance.

Well, this is actually the only time you can use static properties and methods, calling them on the class. You can't call static properties and methods on instances of classes. The syntax for declaring property or method as static is also simple. All you need to do is to use `static` keyword before the name of the property, or method.

```
// Class with static property and method
class MyClass {
  // Declare static property
  static foo = 'My static property.'

  // Declare static method
  static getFoo() {
    // Return the value of static property 'foo'
    return MyClass.foo
  }
}

// Try to access the 'foo' static property directly on MyClass
console.log(MyClass.foo)
// Outputs: 'My static property.'

// Try to access the 'foo' static property
// using getFoo() static method on MyClass
console.log(MyClass.getFoo())
// Outputs: 'My static property.'


// Create instance of MyClass
const myClassInstance = new MyClass()

// Try to access the 'foo' static property on myClassInstance
console.log(myClassInstance.getFoo())
// Outputs: TypeError: myClassInstance.getFoo is not a function

console.log(myClassInstance.foo)
// Outputs: undefined
```

Since static methods can be called only on classes developers often them to create utility methods for their applications. For example, you can use them to do some cleanup or updates when you create new class instances, or destroy existing. The same applies to static properties. For example, you can use them to keep count of class instances you've created.

```
class MyClass {
  // Declare static property to retain
  // the number of instances of MyClass created
  static count = 0

  constructor() {
    // Update count of MyClass instances
    // during every instantiation
    MyClass.count++;
  }

  // return number of instances of MyClass
  static getCount() {
    return MyClass.count
  }
}

// Log number of instances of MyClass
console.log(MyClass.getCount())
// Outputs: 0


// Create one instance of MyClass
const firstInstanceOfMyClass = new MyClass()

// Log number of instances of MyClass
console.log(MyClass.getCount())
// Outputs: 1


// Create another instance of MyClass
const secondInstanceOfMyClass = new MyClass()

// Log number of instances of MyClass
console.log(MyClass.getCount())
// Outputs: 2
```

You may find static properties very useful if you work with React library. As we discussed in [React Best Practices & Tips], it is a good habit to adopt to, to use `defaultProps` and `prop-types`. Before, it was possible to use static properties in JavaScript classes you had to define `defaultProps` and `prop-types` outside the class component.

After the introduction static properties, this is no longer necessary. You can now define `defaultProps` as well as `prop-types` right inside your components using the `static` keyword. This can help you make your code more readable and cleaner.

```
// Import React and ReactDom
import React from 'react'
import ReactDOM from 'react-dom'

// Import prop-types
import { PropTypes } from 'prop-types'

class MyClassComponent extends React.Component {
  static defaultProps = {
    name: 'Anonymous',
    age: 0
  }

  // Define prop-types for MyClassComponent
  static propTypes = {
    name: PropTypes.string,
    age: PropTypes.number.isRequired
  }

  render() {
    return(
      <div>{this.props.name} ({this.props.age})</div>
    )
  }
}
```

Props are not the only good candidates for using `static` keyword. In a fact, there are some [lifecycle methods] in React that even require the use of `static` keyword. For example, the `getDerivedStateFromProps()` and `getDerivedStateFromError()`.

## Getter and setter accessors

Another relatively new addition to JavaScript classes are getter and setter accessors. These two were introduced in ES5. These names may sound like we are talking about some complex topic. Nothing can be farther from the truth. Getter and setter accessors are actually very simple to understand as well as use.

Put simply, getters and setters are methods that allow you to process data before accessing or setting property values. You use setter methods when you want to set or define property values. For example, you can use setter method to validate some value before your program allow to use it as a property value.

Next, the getters. Getters are methods you use when you want to accessing and/or return a property value. For example, when you want to access some property value you don't have to simply return that value. Instead, you can use a getter method to define a "custom" output, such as a short message that contains that property value.

When you want to create a setter accessor you prefix the method name with `set`. When you want to create a getter accessor the prefix you use will be `get`.

```
class User {
  constructor(username) {
    // This will invoke the setter
    this.username = username
  }

  // Create getter for 'username' property
  get username() {
    console.log(`Your username is ${this._username}.)
  }

  // Create setter for 'username' property
  set username(newUsername) {
    // Check for the newUsername length
    if (newUsername.length === 0) {
      // Show a message if username is too short
      console.log('Name is too short.')
    }

    // Otherwise, accept the newUsername and use it as a value for 'username'
    this._username = newUsername
  }
}

// Create instance of User
const userOne = new User('Stuart')

// Access the username property of userOne
// This will automatically invoke the getter method for 'username' property
userOne.username
// Outputs: 'Your username is Stuart.'

// Try to create instance of User without username
// This will automatically invoke the setter method for 'username' property
const userTwo = new User('') // 'Name is too short.'
```

In the example above, we created a getter and setter for the username property. As you can see, we prepended the username property with `_`. Without this, every time the `get` or `set` method is called it would cause a stack overflow. Meaning, the `get` would be called and that would cause the `get` to be called again and again. This would create an infinite loop.

Two things about getter and setter functions you need to know. First, you don't call them explicitly. All you need to do is just to define them. JavaScript will do the rest of the work for you. The second thing is that setter and getter method must have the same name as the property you want them to process.

This is why, in the example above, we used the "username" as the name for our setter and getter methods. This, along with the `get` and `set` keywords, tells JavaScript what should be done and with which property should it be done. So, make sure the names of setter and getter methods always match the names of properties.

```
class Cat {
  constructor(name, age) {
    // Automatically invokes setters for 'name' and 'age'
    this.name = name
    this.age = age
  }

  // Create getter for 'name' property
  get name() {
    console.log(`My name is ${this._name}.`)
  }

  // Create getter for 'age' property
  get age() {
    console.log(`My age is ${this._age}.`)
  }

  // Create setter for 'name' property
  set name(newName) {
    if (newName.length === 0) {
      console.log('Name must contain at least one character.')
    }

    this._name = newName
  }

  // Create setter for 'age' property
  set age(newAge) {
    if (typeof newAge !== 'number') {
      console.log('Age must be a number.')
    }

    this._age = newAge
  }
}

// Create instance of Cat
const doris = new Cat('Doris', 2)

// Access doris' name
// Automatically invokes getter for 'name' property
doris.name
// Outputs: 'My name is Doris.'

// Access doris' age
// Automatically invokes getter for 'age' property
doris.age
// Outputs: 'My age is 2.'
```

## Mixins

In the [previous part], you've learned about class inheritance and how extending works. The problem is that in JavaScript objects can inherit only from a single object. In the case of JavaScript classes, one class can extend only one other class. This is when you want one class to inherit from another class.

However, what if you want or need one class to inherit from multiple classes? What if you want to do something like `class One extends Two and Three`? Well, there is a bad news and good news. The bad news is that class inheritance doesn't allow this. The good news is that it doesn't matter because there is a solution.

Although JavaScript classes doesn't support use of `extend` with multiple classes they support something else. This something is called mixins. What are mixins? Put simply, mixins allow you to take one classes let it extend, or inherit from, multiple classes. The best part? Mixins are very easy to understand, create and also use.

When you want to create new mixin, you don't have to use any special syntax or keyword. You define mixins simply as a function that accepts the superclass as a parameter and creates a new subclass from it. When you want to use mixin you use it with the `extend` keyword, i.e. `class MyClass extends MyMixin(MySuperclass) {}`. Don't forget to pass the superclass as an argument.

```
// Create mixin
const MyMixin = (superclass) => class extends superclass {
  // Add some method all classes inheriting
  // from this mixin will inherit, and be able to use.
  sayHi() {
    console.log('Hi!')
  }
}

// Create Human superclass
class Human {
  isHuman = true
}

// Use mixin to create class Man and let it inherit from Human
// 1) Class has to extend the MyMixin mixin and
// 2) Pass the superclass as an argument to mixin
class Man extends MyMixin(Human) {
  isMan = true
}

// Create instance of Man class
const jack = new Man()

// Log the value of 'isMan' property
console.log(jack.isMan)
// Outputs: true

// Log the value of 'isHuman' property (inherited from Human)
console.log(jack.isHuman)
// Outputs: true

// Call 'sayHi()' method inherited from 'MyMixin' mixin
jack.sayHi()
// Outputs: 'Hi!'
```

### Combining mixins

As you can see, working with mixins is very easy. And, that is not all you can do with mixins. You can also apply multiple mixins, i.e. let a class inherit from multiple mixins. To do that, you pass one mixin as an argument into another mixin. Then, you pass the superclass as an argument to the very last mixin. The order of mixins doesn't matter.

```
// Create first mixin
const MyMixinOne = (superclass) => class extends superclass {
  sayHi() {
    console.log('Hi!')
  }
}

// Create second mixin
const MyMixinTwo = (superclass) => class extends superclass {
  getSomeZzz() {
    console.log('Zzzzz...')
  }
}

// Create third mixin
const MyMixinThree = (superclass) => class extends superclass {
  getWorkout() {
    console.log('Building some muscles...')
  }
}

// Create class superclass
class Human {
  isHuman = true
}

// Create class Man and let it inherit from all Mixins
// Note 1: the order of mixins really doesn't matter.
// Note 2: Make sure to pass the superclass as an argument to the last, innermost, mixin
class Man extends MyMixinThree(MyMixinTwo(MyMixinOne(Human))) {
  isMan = true
}

// Create instance of Man class
const scott = new Man()

scott.sayHi()
// Outputs: 'Hi!'

scott.getWorkout()
// Outputs: 'Building some muscles...'

scott.getSomeZzz()
// Outputs: 'Zzzzz...'
```

### Mixins and overriding properties and methods

Another good thing about mixins is that everything works as with it does in case of JavaScript classes. Meaning, you can override methods, you can use `super` keyword to access superclass properties and methods and also call `super()` method in subclass `constructor()`.

```
// Create mixin
const MyMixin = (superclass) => class extends superclass {
  // Add public method to print message with gender (defined in superclass)
  printGender() {
    console.log(`My gender is ${this.gender}.`)
  }
}

// Create Human superclass
class Human {
  // Add some public properties
  isHuman = true
  gender = undefined
}

// Create class Man
class Man extends MyMixin(Human) {
  // Override Human's gender property
  gender = 'Male'
}

// Create class Woman
class Woman extends MyMixin(Human) {
  // Override Human's gender property
  gender = 'Female'

  // Override 'printGender()' method
  printGender() {
    // Call the original 'printGender()' method defined in mixin
    super.printGender()

    // Create new message for Woman class
    console.log(`I am a ${this.gender}.`)
  }
}

// Create instance of Man class
const andreas = new Man()

// Print gender of andreas instance
andreas.printGender()
// Outputs: 'My gender is Male.'

// Create instance of Man class
const victorie = new Woman()

// Print gender of victorie instance
victorie.printGender()
// Outputs:
// 'My gender is Female.' (invoked by calling 'super.printGender()')
// 'I am a Female.' (new message)
```

### Mixins as class blueprints

Another way to think about mixins is in the terms of templates for JavaScript classes. This is further supported by the fact that you can add properties and methods to mixins and let your classes inherit all of them. So, you can also use mixins in this way, as a blueprint for your JavaScript classes.

Aside to that, you can also use mixins as a storage of properties and methods you want to share with various classes. Why repeat yourself, or create long chains chains of class inheritance? Put all the properties and methods you want to share to a mixin and let your classes inherit from it.

```
// Create mixin with shared properties and methods
const MyMixin = (superclass) => class extends superclass {
  someSharedProperty = 'Foo'
  anotherSharedProperty = 13

  someShareMethod() {
    // Do something
  }

  anotherShareMethod() {
    // Do something
  }
}

// Create various different superclasses
class MySuperclassOne {}

class MySuperclassTwo {}

class MySuperclassThree {}

// Create various different subclasses, all sharing properties and methods defined in mixin
class MySubclassOne extends MyMixin(MySuperclassOne) {}

class MySubclassTwo extends MyMixin(MySuperclassTwo) {}

class MySubclassThree extends MyMixin(MySuperclassThree) {}
```

## Epilogue: JavaScript Classes - A Friendly Introduction Pt.2

This is it! You've just finished the second, and last, part of this miniseries focused on JavaScript classes. By now, you know all you need to know about JavaScript classes. What now? Review what you've learned. Revisit the examples we worked with, play with them and create your own. Make sure you really understand everything.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Part 1]: https://blog.alexdevero.com/javascript-classes-pt1/
[TC39 stage 3]: https://github.com/tc39/proposal-class-fields
[TypeScript]: https://www.typescriptlang.org
[Babel]: https://babeljs.io
[private]: https://github.com/tc39/proposal-private-methods
[React Best Practices & Tips]: https://blog.alexdevero.com/react-best-practices-pt2/
[lifecycle methods]: https://reactjs.org/docs/react-component.html#commonly-used-lifecycle-methods
[previous part]: https://blog.alexdevero.com/javascript-classes-pt1/#class-inheritance-extends

<!--
#### Meta:
-
-->
