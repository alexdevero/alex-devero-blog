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
// Syntax
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

// Using getter method
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

// Execute the getter method
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

// Execute the getter method "getName"
console.log(dog.getName)
// Output:
// undefined
```

## Property setters

When you set or change value of some property JavaScript will execute existing property setter, or setter method, for that property. The syntax of setter method is almost the same as of getter. One thing that is different is the keyword. When you want to define a setter you have to use `set` keyword, instead of `get`.

This keyword tells JavaScript that the method that follows is a setter method. Another thing that is different is that you will probably want to specify at least one parameter. The setter method is used to set value. Method parameter is a way to pass that value to a setter so it can be used.

Lastly, unlike, the getter method, the setter method doesn't have to return anything. Setter is used to set values and no one probably expects it to return anything. So, omitting `return` statement is perfectly fine.

```JavaScript
// Syntax
// Create an object
let myObj = {
  // Example of a setter method
  // this setter will be executed
  // when you use myObj.mySetter = ...
  get mySetter() {
    // Return something
    return ''
  }
}

// Execute the setter method "mySetter"
// NOTE: when you use setter method
// you use as if you were assigning a value
myObj.mySetter = 'Hello'


// Example:
// Create an object
let user = {
  name: 'Stuart Douglass',
  isAdmin: false,

  // Create setter method
  // this setter will be executed
  // when you use user.setName = ...
  set setName(newName) {
    // Allow only string with more than 0 characters
    if (typeof newName === 'string' && newName.length > 0) {
      this.name = newName
    } else {
      if (typeof newName !== 'string') {
        console.log('Please use only string.')
      } else if (newName.length === 0) {
        console.log('Please use name with more than 0 characters.')
      }
    }
  }
}

// Try to change the value of "name" to an empty string
// This executes the setter method for "name"
user.setName = ''
// 'Please use name with more than 0 characters.'

// Try to change the value of "name" to a number
// This executes the setter method for "name"
user.setName = 55
// 'Please use only string.'

// Check the value of "name" property
// This executes the getter method for "name"
console.log(user.name)
// Output:
// 'Stuart Douglass'

// Try to change the value of "name" to a string
// This executes the setter method for "name"
user.setName = 'Jeremy Guire'

// Check the value of "name" property again
// This executes the getter method for "name"
console.log(user.name)
// Output:
// 'Jeremy Guire'
```

## Creating getters and setters on the go

So far, we've looked only on creating property getters and setters at the time of creating an object. However, there is a way to add property getters and setters also to an object that already exists. You can do this with the help of [Object.defineProperty()] method. This method allows you to add new properties to objects or change existing.

You can use this method also to add or change accessor properties, property getters and setters. Adding getters and setters with this method is similar to adding them when you create an object. When you use the `defineProperty()` you pass in three parameters. The first argument is the object you want to update.

The second parameter is the property you want to add or change. In case of property getters and setters, it is the property for which you want to add getter and/or setter method. For new property, the last parameter is for object with descriptors, such as `enumerable`, `configurable`, `value` and so on.

In case of getters and setters, you replace the object with descriptors with an object containing the getter and setter method. The syntax for both, getter and setter, is in this case almost the same as in previous examples. One difference is missing method name. You specified that as the second parameter, the property name.

```JavaScript
// Create an object
const book = {
  _title: 'Six of Crows',
  _author: 'Leigh Bardugo',
  _pubDate: 'February 6, 2018'
}

// Add getter and setter for title
// Parameter 1: object to update
// Parameter 2: property to add/update
// Parameter 3: object containing getter and setter
Object.defineProperty(book, 'title', {
  get() {
    return this._title
  },
  set(newTitle) {
    if (typeof newTitle === 'string' && newTitle.length > 0) {
      this._title = newTitle
    }
  }
})

// Add getter and setter for title
// Parameter 1: object to update
// Parameter 2: property to add/update
// Parameter 3: object containing getter and setter
Object.defineProperty(book, 'author', {
  get() {
    return this._author
  },
  set(newAuthor) {
    if (typeof newAuthor === 'string' && newAuthor.length > 0) {
      this._author = newAuthor
    }
  }
})

// Add getter and setter for title
// Parameter 1: object to update
// Parameter 2: property to add/update
// Parameter 3: object containing getter and setter
Object.defineProperty(book, 'pubDate', {
  get() {
    return this._pubDate
  },
  set(newPubDate) {
    if (typeof newPubDate === 'string' && newPubDate.length > 0) {
      this._pubDate = newPubDate
    }
  }
})

// Get current book title
// This executes the getter method for "title"
console.log(book.title)
// Output:
// 'Six of Crows'

// Get current book author
// This executes the getter method for "author"
console.log(book.author)
// Output:
// 'Leigh Bardugo'

// Get current book publication date
// This executes the getter method for "pubDate"
console.log(book.pubDate)
// Output:
// 'February 6, 2018'

// Change book data
// This executes the setter method for "title"
book.title = 'Red Rising'
// This executes the setter method for "author"
book.author = 'Pierce Brown'
// This executes the setter method for "pubDate"
book.pubDate = 'January 28, 2014'

// Get new book title
// This executes the getter method for "title" again
console.log(book.title)
// Output:
// 'Red Rising'

// Get new book author
// This executes the getter method for "author" again
console.log(book.author)
// Output:
// 'Pierce Brown'

// Get new book publication date
// This executes the getter method for "pubDate" again
console.log(book.pubDate)
// Output:
// 'January 28, 2014'
```

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
