# JavaScript Objects - A Friendly Introduction Pt.1
JavaScript objects can be difficult concept to grasp, especially for beginners. This tutorial will help you understand them. You will learn about properties, keys and values and how to work with them. After that, you will learn about five ways you can use to create new objects.<!--more-->
<!-- 10-02-20--javascript-objects-friendly-introduction-p1 -->
<!--
Table of Contents:
## The basics of JavaScript objects
## Accessing properties
## Property values
## Adding properties
### Non-existing properties
## Creating objects
### Creating objects with new Object()
### Creating objects with Object.create()
### Creating objects with object literal
### Creating objects with constructor
### Creating objects with ES6 classes
## Conclusion: JavaScript Objects - A Friendly Introduction
-->

## The basics of JavaScript objects

In JavaScript, objects are a data type that is composed of properties. These properties are composed of keys and values. These keys and values are represented in the form of `key: value` pairs. This is why these pairs are called "key/value" pairs. If you have a hard time wrapping your head around properties think about them as variables.

In some sense, object properties are very similar to variables. The difference is that properties are attached to objects. Other than that, properties work pretty much the same as variables. When it comes to properties, there are many things you can do with them. You can create and add new properties.

You can also change the value of those properties, not the properties themselves. Well, unless you create new property, assign it the same value another property has and then delete the "another" property. Lastly, you can also delete properties, using `delete` keyword followed by object's and property's names (using either dot notation or square brackets): `delete obj.someProp` or `delete obj['someProp']`.

Note about changing and deleting properties. This is doable only if the property at hand is not a "read-only" property. Or, if the object you are working with is not [frozen]. Otherwise, you can't change it, either the property or the object, or both. Lastly, of course, you can also access object properties.

```js
// Create new object
const obj = new Object()

// Add property 'name' (using dot notation)
// assign it a value of 'Lisy'
obj.name = 'Lisy'

// Same as
obj['name'] = 'Lisy'

// Log the value of 'name' property
console.log(obj.name)
// 'Lisy'

// obj now looks like:
// {
//   name: 'Lisy'
// }


// Change the value of property 'name' (using dot notation)
// Note: this is like re-assigning a variable
obj.name = 'Wiki'

// Same as
obj['name'] = 'Wiki'

// Log the value of 'name' property
console.log(obj.name)
// 'Wiki'

// obj now looks like:
// {
//   name: 'Wiki'
// }


// Log the content of 'obj'
console.log(obj)
// { name: 'Wiki' }

// Delete the 'name' property (using dot notation)
delete obj.name

// Same as
delete obj['name']

// Log the content of 'obj'
console.log(obj)
// {}

// obj now looks like:
// {}
```

## Accessing properties

One way to access property is by using dot notation. You start with the object name, next is a dot and then the property name: `objName.someProperty`. Another way to access properties inside objects are using square brackets. In this case, the object name is followed by square brackets.

These square brackets contain the name of the property. When you use square brackets, remember to wrap the property name with quotes, either single or double: `objName['someProperty']`. There is not a big difference between dot notation and square bracket. You can choose the one you like more. Well, almost.

There might be cases where you will have to use brackets. For example, when property is composed of multiple words separated by spaces. When this happens, you can't use dot notation. You can't try to access the property, that contains space, using dot notation. Doing something like `obj.some property` will simply not work.

In this case, the only solution is using square brackets, along with quotes: `obj.['some property']`. This alternative will work. So, either use camelCase, SnakeCase, or any case that doesn't contains spaces. Then, you can use only dot notation (`objName.someProperty`). Otherwise, remember to use square brackets when property name contains spaces.

```js
// Accessing properties example no.1: dot notation
myObj.someProperty

// Example:
const myObj = {
  name: 'Andrei'
}

// Access 'name' property
myObj.name
// 'Andrei'


// Accessing properties example no.2: square brackets
myObj['someProperty']

// Example:
const myObj = {
  language: 'English'
}

// Access 'language' property
myObj['language']
// 'English'


// Calling object methods
myObj.someMethod()

// Example:
const myObj = {
  greeting: function() {
    return 'Hello.'
  }
}

// Call 'greeting' method
myObj.greeting()
// 'Hello.'

// or
myObj['someMethod']()

// Call 'greeting' method
myObj['greeting']()
// 'Hello.'
```

## Property values

When it comes to property values, there are four things you can use. The first thing you can use as a value of a property is any primitive JavaScript [data type]. This includes strings, numbers, booleans, etc. The second thing you can use for values is a data collection, an [array] for example. The third thing are objects.

Yes, JavaScript objects can contain key/value pairs where the `value` is another object. The fourth and last thing you can use as a value of a property are [functions]. Since we are talking about functions and objects, there is one thing you need to know. Functions inside objects, or [classes], are called "methods".

Chances that you may have already heard about methods in JavaScript. Well, here is the "secret". Method is just another name for a function. When we talk about methods, we talk about functions used in a specific context. This is the only difference between functions and methods. Methods are functions used inside JavaScript objects and classes. Functions? Well, these are the functions you use everywhere else.

## Adding properties

You know what properties are and what you can use as a value of a property. When you want to create new object property, there are three ways to do it. First, you can add properties to objects by assigning the property a value, using a dot-notation: `objName.someProperty = 'Some value'`.

The second way is similar to the first. This time, instead of using dot, you will use square brackets: `objName['someProperty'] = 'Some value'`. You may have noticed that these two ways of creating properties in objects are very similar to accessing properties in objects. You are correct.

The syntax is almost the same. The difference is that when you access a property, or a variable, you don't do assignment. When you want to add a property you also assign it a value. What about the third way to add properties to objects? You can add properties at the time you create them, using object initializer or literal notation or object literal.

```js
// Creating properties no.1: using dot notation
// Create new object
const myObjectOne = new Object()

// Add new property
myObjectOne.myNewProp = 'This is new property'

// Log the content of myObjectOne
console.log(myObjectOne)
// { myNewProp: 'This is new property' }


// Creating properties no.2: using square brackets
const myObjectTwo = new Object()

// add new property
myObjectTwo['anotherNewProp'] = 'This is another new property'

// Log the content of myObjectTwo
console.log(myObjectTwo)
// { anotherNewProp: 'This is another new property' }


// Creating properties no.3: adding property when creating an object
// Create object using object literal (object initializer or literal notation)
const myObjectThree = {
  someProperty: 'Property added with object literal.'
}

// Log the content of myObjectThree
console.log(myObjectThree)
// { someProperty: 'Property added with object literal.' }


// Adding methods
const myObjectOne = new Object()

// Add property 'name'
myObjectOne.name = 'Thus Spoke Zarathustra'

// Add method 'printBookName'
myObjectOne.printBookName = function() {
  return this.name
}

// Call 'printBookName' method
myObjectOne.printBookName()
// 'Thus Spoke Zarathustra'


// You can also use square brackets to add methods
myObjectOne['printBookName'] = function() {
  return this.name
}

// And to call methods
myObjectOne['printBookName']()
// 'Thus Spoke Zarathustra'
```

### Non-existing properties

This might not be important to remember. Still, it is still good to know it. When you try to access some property that doesn't exist in the object, JavaScript will return `undefined`. This also gives you a simple way to check if property exists in an object or not, by checking for undefined: `myObject.someNonExistingProp === undefined`. If this condition is `true`, the property doesn't exist.

## Creating objects

In JavaScript, there are five ways to create objects. Some of these ways looks similar some look differently. Some are simple and short and others are more complex. Let's take a look at each of them.

### Creating objects with new Object()

First, you can create objects using `new Object()`. Here, you declare new variable for your object and assign it `new Object()` as a value: `let myObj = new Object()`. When you want to add, change, delete or access properties in this object you use the variable name to reference that object.

```js
// Create new object with new Object()
const myBookObj = new Object()

// Add new properties
myBookObj.title = 'Critique of Practical Reason'
myBookObj.author = 'Immanuel Kant'
myBookObj.published = '1788'
myBookObj.numOfPages = 188

// Add new method
myBookObj.printTheBookInfo = function() {
  return `The "${this.title}" written by ${this.author} was published in ${this.published} and has ${this.numOfPages} pages.`
}

// Log the content of myBookObj
console.log(myBookObj)
// {
//   title: 'Critique of Practical Reason',
//   author: 'Immanuel Kant',
//   published: '1788',
//   numOfPages: 188
// }

// Log the title of the myBookObj object
console.log(myBookObj.title)
// 'Critique of Practical Reason'

// Call printTheBookInfo method
myBookObj.printTheBookInfo()
// 'The "Critique of Practical Reason" written by Immanuel Kant was published in 1788 and has 188 pages.'
```

### Creating objects with Object.create()

The second way is about using `Object.create()` method. Similarly to the first way, you again declare new variable for your object. Now, you assign it `Object.create(prototype, objectProperties)`. The first argument is used to specify the object which should be the prototype of this newly created object.

This is useful if you want the new object to inherit properties from existing object. If so, you pass the name of that object, the variable that references that object, as the first argument. If you don't want the object to inherit any existing object, you can pass `Object.prototype` as the first argument instead.

The second parameter, the `objectProperties`, specifies the properties you want to add to the object. If you want to create object with specific properties you pass them as an object, wrapped with curly brackets, as the second argument. Otherwise, you can pass empty object, empty curly brackets (`{}`).

So, to create new empty object the syntax will be: `let myObj = Object.create(Object.prototype, {})`. When you use the `Object.create()` method you can also use descriptors, or attributes, such as `configurable`, `enumerable`, `writable` and `value`. The `value` specifies the value of the property.

The `enumerable` specifies if the property shows up when you try to log or enumerate the properties of the object. The `configurable` specifies if the type of the property can be changed. It also specifies if the property can be deleted.

The last one, the `writable`, specifies if the property can be changed, with re-assignment (`obj.someProp = 'new value'`). Remember to use these descriptors or attributes in the form of an object. Also, remember that you specify them for each property individually.

```js
// Create new object with Object.create() method
const myBookObj = Object.create(Object.prototype, {
  title: {
    value: 'Critique of Practical Reason',
    configurable: true,
    writable: true,
    enumerable: true
  },
  author: {
    value: 'Immanuel Kant',
    configurable: true,
    writable: true,
    enumerable: true
  },
  published: {
    value: '1788',
    configurable: true,
    writable: true,
    enumerable: true
  },
  numOfPages: {
    value: 188,
    configurable: true,
    writable: true,
    enumerable: true
  },
  printTheBookInfo: {
    value: function() {
      return `The "${this.title}" written by ${this.author} was published in ${this.published} and has ${this.numOfPages} pages.`
    },
    configurable: true,
    writable: true,
    enumerable: true
  }
})

// Log the content of myBookObj
// Note: any property with 'enumerable' attribute
// set to 'false' is not visible for console.log()
console.log(myBookObj)
// {
//   title: 'Critique of Practical Reason',
//   author: 'Immanuel Kant',
//   published: '1788',
//   numOfPages: 188
// }

// Log the author of the myBookObj object
console.log(myBookObj.author)
// 'Immanuel Kant'

// Call printTheBookInfo method
myBookObj.printTheBookInfo()
// 'The "Critique of Practical Reason" written by Immanuel Kant was published in 1788 and has 188 pages.'
```

### Creating objects with object literal

The third way is using object literal, also known as `object initializer`. This is, by far, the simplest way to create objects in JavaScript. You, again, start with declaring a variable. Next steps depend on what do you want to do next. You can either assign that variable an empty object (empty curly brackets, `{}`).

Another thing you can do is adding some properties right away. This is one thing I like on object literal. You don't have to create an empty object and add properties in next step. You can do both, at the same time, create object with properties. When you want to add some properties you add them inside the curly brackets: `let myObj = { prop: 'value'}`.

True, you can do this, adding properties and creating new objects at the same time, also with the `Object.create()` method. However, the syntax of object literal is much easier and amount of code much smaller. One downside is that you can't use `configurable`, `enumerable`, `writable` and `value` attributes. Hmm, do you really need them?

```js
// Create new object with object literal
const myBookObj = {
  title: 'Critique of Practical Reason',
  author: 'Immanuel Kant',
  published: '1788',
  numOfPages: 188,
  printTheBookInfo: function() {
    return `The "${this.title}" written by ${this.author} was published in ${this.published} and has ${this.numOfPages} pages.`
  }
}

// Log the content of myBookObj
console.log(myBookObj)
// {
//   title: 'Critique of Practical Reason',
//   author: 'Immanuel Kant',
//   published: '1788',
//   numOfPages: 188
// }

// Log the publishing date of the myBookObj object
console.log(myBookObj.published)
// '1788'

// Call printTheBookInfo method
myBookObj.printTheBookInfo()
// 'The "Critique of Practical Reason" written by Immanuel Kant was published in 1788 and has 188 pages.'
```

### Creating objects with constructor

The fourth way is using constructor. The "constructor" name may sound more complicated than it actually is. Don't let it scare you. Constructor is just a fancy name for a function. These [constructor functions] allows you to create something like a blueprint,  with specific properties.

You can then use these constructors later to create instances, or copies of the original objects. This is done with the help of `new` keyword followed by the name of the constructor (original object). This will cause all instances automatically inherit the properties of the original constructor.

When you want to create new constructor, you start with the `function` keyword. Next is the name of the constructor, or object. Next are parenthesis with any, optional, parameters followed by curly braces. When you want to add properties, you use `this` keyword followed by property name, using dot notation: `this.name = 'Tony'`.

All properties goes inside the function constructor. Meaning, between the curly braces that follows after the name of the constructor. Similarly to object literal and `Object.create()` method, you don't have to create empty constructor first so you can add properties later. You can add properties right away, when you create the constructor. Remember, in the end, you are working with a [function].

```js
// Create new object with constructor
// Create Book constructor that accepts 4 parameters:
// title, author, publishing date and number of pages
function Book(title, author, published, numOfPages) {
  this.title = title;
  this.author = author;
  this.published = published;
  this.numOfPages = numOfPages;
  this.printTheBookInfo = function() {
    return `The "${this.title}" written by ${this.author} was published in ${this.published} and has ${this.numOfPages} pages.`
  }
}

// Create new instance of Book constructor/object
// Pass all required information about the
// title, author, published and numOfPages as arguments
const myBookInstance = new Book('Critique of Practical Reason', 'Immanuel Kant', '1788', 188)

// Log the content of myBookInstance
console.log(myBookInstance)
// Book {
//   title: 'Critique of Practical Reason',
//   author: 'Immanuel Kant',
//   published: '1788',
//   numOfPages: 188
// }

// Log the number of pages of the myBookObj object
console.log(myBookObj.numOfPages)
// 188

// Call printTheBookInfo method
myBookInstance.printTheBookInfo()
// 'The "Critique of Practical Reason" written by Immanuel Kant was published in 1788 and has 188 pages.'

// Create another instance of Book constructor/object
const mySecondBookInstance = new Book('Essays and Aphorisms', 'Arthur Schopenhauer', '1973', 240)

// Log the title of the mySecondBookInstance instance
console.log(mySecondBookInstance.title)
// 'Essays and Aphorisms'
```

Quick side note: It is a good practice to always start the name of constructor functions with a capital letter. The same also applies to classes. The capital letter will not have any effect on how your code works. It may just help you make it more readable.

### Creating objects with ES6 classes

The fifth way to create JavaScript objects is by using ECMAScript 6 classes. From ECMAScript 6 and up, JavaScript supports the concept of "classes" like many other programming languages. When you want to create new object/class, using class, you use `class` keyword followed by the object/class name, followed by curly braces.

If you want to add any properties to the object, or class, you add them inside the curly braces. Remember that there are no parenthesis and parameters that would follow after the class name. When you want to add properties, you do so in `constructor` method, with the help of `this` keyword.

It is also the `constructor` where you can add any parameters the class will accept. This is also done with the help of `this` keyword. One thing, any parameters must be also specified as parameters for the `constructor` method. This doesn't apply to class methods. If you want to add any, you add it inside the class, but outside the `constructor`.

```js
// Create new object with ES6 classes
class Book {
  // Specify the parameters Book class accepts
  constructor(title, author, published, numOfPages) {
    this.title = title
    this.author = author
    this.published = published
    this.numOfPages = numOfPages
  }

  // Add class method printTheBookInfo
  printTheBookInfo() {
    return `The "${this.title}" written by ${this.author} was published in ${this.published} and has ${this.numOfPages} pages.`
  }
}

// Create instance of Book class
const myNewBookClassInstance = new Book('Critique of Practical Reason', 'Immanuel Kant', '1788', 188)

// Log the title of the myNewBookClassInstance instance
console.log(myNewBookClassInstance.title)
// 'Critique of Practical Reason'

// Call printTheBookInfo method
myNewBookClassInstance.printTheBookInfo()
// 'The "Critique of Practical Reason" written by Immanuel Kant was published in 1788 and has 188 pages.'

// Create another instance of Book class
const mySecondBookClassInstance = new Book('Essays and Aphorisms', 'Arthur Schopenhauer', '1973', 240)

// Log the title of the mySecondBookClassInstance instance
console.log(mySecondBookClassInstance.title)
// 'Essays and Aphorisms'
```

## Conclusion: JavaScript Objects - A Friendly Introduction

You are at the end of the first part of this mini series focused on JavaScript objects. Today, you've learned about the basics. You've learned about properties, keys and values and how to work with them. After that, you've learned about five ways you can use to create new objects, namely `new Object()`, `Object.create()` object literal constructor and ES6 classes.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[frozen]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze
[data type]: https://blog.alexdevero.com/javascript-basics-data-types-pt1/
[array]: https://blog.alexdevero.com/javascript-101-9-arrays-pt1/
[functions]: https://blog.alexdevero.com/javascript-functions-pt1/
[classes]: https://blog.alexdevero.com/javascript-classes-pt1/
[Constructor functions]: https://blog.alexdevero.com/javascript-functions-pt2/#function-constructor
[function]: https://blog.alexdevero.com/javascript-functions-pt1/

<!--
### Meta:
-
-->

<!--
#### Resources:
-
-->
