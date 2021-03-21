# How to Freeze an Object in JavaScript with Object.freeze() & Object.seal()
<!--more-->
<!--
Table of Contents:
-->

## Object.seal() method

When you want to freeze an object in JavaScript there are two options you can choose from. The first option is less restrictive than the second. This option is about using the `Object.seal()` method. This methods help you prevent anyone from adding, removing  or re-configuring existing properties of an object.

JavaScript does this by marking all existing properties in an object as non-configurable, by changing the [property flags]. This also means that when you seal an object, you can no longer change these flags. This is what "re-configuring existing properties" means, modifying property flags.

That said, sealing an object still allows you to change properties that exist in an object. This is because sealing doesn't change the writable flag. So, unless you change the value of `writable` flag you can modify existing properties. About the syntax. The syntax of `Object.seal()` is simple.

When you want to seal some specific object you pass that object to the `Object.seal()` method as an argument. This method then returns new sealed object. One thing. When you seal an object with `Object.seal()` you don't have to assign that returned sealed object to another variable.

Doing this will create new object that is sealed and assign it to the new variable. However, it will also seal the original object you passed to the `Object.seal()`. So, as a result, you will now have two sealed objects, one original and one copy.

```JavaScript
// Create new object:
const myObj = {
  name: 'Joe Doe',
  age: 37
}

// Seal the "myObj" object:
Object.seal(myObj)

// Check if object is extensible:
console.log(Object.isExtensible(myObj))
// Output:
// false

// NOTE: This will work.
// Try to change the value of "name" property:
myObj.name = 'Jack Pain'

// NOTE: This will not work.
// Try to add new properties:
myObj.occupation = 'Secret agent'
myObj.undercover = true

// Log the "myObj" object:
console.log(myObj)
// Output:
// {
//   name: 'Jack Pain', // <= Only value of "name" prop has changed.
//   age: 37
// }


// Assigning sealed object to new variable (not necessary):
const myObj = {
  name: 'Joe Doe',
  age: 37
}

// Seal the "myObj" object and assign it to new variable:
const myObjSealed = Object.seal(myObj)

// Check if object is extensible:
console.log(Object.isExtensible(myObjSealed))
// Output:
// false

// Try to change the value of "age" in both objects:
myObj.age = 45
myObjSealed.age = 45

// Try to add new properties to both objects:
myObj.height = '90 kg'
myObjSealed.height = '90 kg'

// Log the "myObj" object:
console.log(myObj)
// Output:
// {
//   name: 'Joe Doe',
//   age: 45
// }

// Log the "myObjSealed" object:
console.log(myObj)
// Output:
// {
//   name: 'Joe Doe',
//   age: 45
// }
```

## Object.freeze() method

The `Object.freeze()` is the second option, the more restrictive. While sealing an object allows you to change existing properties, their values, `Object.freeze()` forbids this. When you freeze an object with `Object.freeze()` it will become ultimately locked. You will not be able to add new properties or remove or modify existing.

In addition to this, the `Object.freeze()` method also prevents anyone from changing the [object prototype]. The syntax, and way to use this method, is similar to the `Object.seal()`. The only difference is the replacement of `seal()` method with `freeze()`, and also the outcome.

Another thing `Object.freeze()` shares with `Object.seal()` is that you also don't have to assign the returned frozen object to a variable. When you use the `Object.freeze()` method it will freeze the original object. If you also assign the returned object to a variable you will just end up with two frozen objects.

```JavaScript
// Create new object:
const myObj = {
  title: 'Functional Programming in JavaScript',
  author: 'Luis Atencio'
}

// Freeze the "myObj" object:
Object.freeze(myObj)

// Check if object is extensible:
console.log(Object.isExtensible(myObj))
// Output:
// false

// NOTE: This will not work.
// Try to change the value of "title" property:
myObj.title = 'Functional Programming in JavaScript: How to improve your JavaScript programs using functional techniques'

// NOTE: This will not work.
// Try to add new properties:
myObj.language = 'English'
myObj.format = 'Paperback'

// Log the "myObj" object:
console.log(myObj)
// Output:
// {
//   title: 'Functional Programming in JavaScript',
//   author: 'Luis Atencio'
// }


// Assigning frozen object to new variable (not necessary):
const myObj = {
  title: 'Functional Programming in JavaScript',
  author: 'Luis Atencio'
}

// Freeze the "myObj" object and assign it to new variable:
const myObjFrozen = Object.freeze(myObj)

// Check if object is extensible:
console.log(Object.isExtensible(myObjFrozen))
// Output:
// false

// Try to change the value of "age" in both objects:
myObj.title = 'Functional Programming in JavaScript: How to improve your JavaScript programs using functional techniques'
myObjFrozen.title = 'Functional Programming in JavaScript: How to improve your JavaScript programs using functional techniques'

// Try to add new properties to both objects:
myObj.format = 'Paperback'
myObjFrozen.format = 'Paperback'

// Log the "myObj" object:
console.log(myObj)
// Output:
// {
//   title: 'Functional Programming in JavaScript',
//   author: 'Luis Atencio'
// }

// Log the "myObjFrozen" object:
console.log(myObjFrozen)
// Output:
// {
//   title: 'Functional Programming in JavaScript',
//   author: 'Luis Atencio'
// }
```

## Object.preventExtensions() method

To seal and freeze an object are not the only options to restrict manipulations with objects. There is additional method you can use, the `Object.preventExtensions()`. What this method does is it prevents anyone from adding new properties to an object. That said, you can still add properties to the object prototype.

The `Object.preventExtensions()` also doesn't prevent you from deleting existing properties. The way to use this method is the same as for the previous two. You pass the object you want to prevent from being extended and pass it as an argument to this method. New inextensible object will be returned.

Similarly to previous two methods, you don't have to assign this returned object to a variable. The `Object.preventExtensions()` method will modify the original object you passed as argument. If you do assign it, you will end up with two inextensible objects instead of one.

```JavaScript
// Create new object:
const myObj = {
  language: 'English',
  ethnicity: 'Anglo-Saxons'
}

// Prevent "myObj" from being extended:
Object.preventExtensions(myObj)

// Check if object is extensible:
console.log(Object.isExtensible(myObj))
// Output:
// false

// Try to change the value of existing properties:
myObj.language = 'Italian'
myObj.ethnicity = 'Italians'

// Try to add new property:
myObj.languageFamily = 'Indo-European'

// Try to remove property:
delete myObj.ethnicity

// Log the "myObj" object:
console.log(myObj)
// Output:
// {
//  language: 'Italian' // <= "ethnicity" has been deleted,
//                      // but no property has been added
// }


// Assigning frozen object to new variable (not necessary):
const myObj = {
  language: 'JavaScript',
  type: 'high-level'
}

// Prevent "myObj" from being extended
// and assign it to new variable:
const myObjInextensible = Object.preventExtensions(myObj)

// Check if object is extensible:
console.log(Object.isExtensible(myObj))
// Output:
// false

// Check if object is extensible:
console.log(Object.isExtensible(myObjInextensible))
// Output:
// false

// Try to add new property:
myObj.author = 'Brendan Eich'
myObjInextensible.author = 'Brendan Eich'

// Try to remove property:
delete myObj.type
delete myObjInextensible.type

// Log the "myObj" object:
console.log(myObj)
// Output:
// { language: 'JavaScript' }

// Log the "myObj" object:
console.log(myObjInextensible)
// Output:
// { language: 'JavaScript' }
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
-
-->

<!--
### Resources:
-
-->
