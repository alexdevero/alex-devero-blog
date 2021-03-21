# How to Freeze an Object in JavaScript: Object.freeze(), Object.seal() & Object.preventExtensions()

In JavaScript, it is possible to freeze an object, to make it immutable, and prevent it from being changed. This tutorial will show you how to do it. You will learn how to freeze an object in JavaScript with Object.freeze(), seal it with Object.seal(), prevent extending it and more.<!--more-->
<!--
Table of Contents:
## Object.seal() method
## Object.freeze() method
## Object.preventExtensions() method
## Deeply frozen objects
## Unfreeze?
## Frozen objects and strict mode
## Conclusion: How to freeze an object in JavaScript: Object.freeze(), Object.seal() & Object.preventExtensions()
-->

## Object.seal() method

When you want to freeze an object in JavaScript there are two options you can choose from. The first option is less restrictive than the second. This option is about using the `Object.seal()` method. This method helps you prevent anyone from adding, removing  or re-configuring existing properties of an object.

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

// Check if object is frozen:
console.log(Object.isFrozen(myObj))
// Output:
// false

// NOTE: This will work.
// Try to change the value of "name" property:
myObj.name = 'Jack Pain'

// NOTE: This will not work.
// Try to add new properties:
myObj.occupation = 'Secret agent'
myObj.undercover = true

// NOTE: This will also not work.
// Try to remove "age" property:
delete myObj.age

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

// Check if object is frozen:
console.log(Object.isFrozen(myObjSealed))
// Output:
// false

// Try to change the value of "age" in both objects:
myObj.age = 45
myObjSealed.age = 45

// Try to add new properties to both objects:
myObj.height = '90 kg'
myObjSealed.height = '90 kg'

// Try to remove "age" property:
delete myObj.age
delete myObjSealed.age

// Log the "myObj" object:
console.log(myObj)
// Output:
// {
//   name: 'Joe Doe',
//   age: 45
// }

// Log the "myObjSealed" object:
console.log(myObjSealed)
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

// Check if object is frozen:
console.log(Object.isFrozen(myObj))
// Output:
// true

// NOTE: This will not work.
// Try to change the value of "title" property:
myObj.title = 'Functional Programming in JavaScript: How to improve your JavaScript programs using functional techniques'

// NOTE: This will not work.
// Try to add new properties:
myObj.language = 'English'
myObj.format = 'Paperback'

// NOTE: This will also not work.
// Try to remove "author" property:
delete myObj.author

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

// Check if object is frozen:
console.log(Object.isFrozen(myObjFrozen))
// Output:
// true

// Try to change the value of "age" in both objects:
myObj.title = 'Functional Programming in JavaScript: How to improve your JavaScript programs using functional techniques'
myObjFrozen.title = 'Functional Programming in JavaScript: How to improve your JavaScript programs using functional techniques'

// Try to add new properties to both objects:
myObj.format = 'Paperback'
myObjFrozen.format = 'Paperback'

// Try to remove "author" property:
delete myObj.author
delete myObjFrozen.author

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

// Try to remove "ethnicity" property:
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

## Deeply frozen objects

The `Object.freeze()` method allows you to freeze an object. The `Object.seal()`, and also `Object.preventExtensions()`, allows to freeze an object partially. That said, there is a catch. All these methods perform only a "shallow" freeze. These methods will freeze only the object itself.

This will not be enough if you have an object whose properties are also objects. In this case, these "inner" or "nested" object will not be frozen. Neither of the methods we discussed today will have any effect on these inner object. This, also applies to properties that are arrays.

One way to solve this is by using a [recursion]. You can create a function. This function will take an object and return object frozen with the `Object.freeze()` method. Inside this function, you will iterate over all values of the object and check if any value is an object. If so, you will call the function on that value.

```JavaScript
// Create object for testing:
const myObj = {
  name: 'Joe',
  age: 29,
  profession: {
    title: 'Programmer',
    experience: 'senior'
  }
}

// Create function for deep freezing:
const deepFreeze = obj => {
  // Iterate over all values of provided object:
  Object.values(obj).forEach(value => {
    // Check if each value is an object:
    if (typeof value === 'object' && !Object.isFrozen(value)) {
      // If it is and if it is not frozen
      // call deepFreeze function on it:
      deepFreeze(value)
    }
  })

  // Return provided object as frozen:
  return Object.freeze(obj)
}

// Deep freeze the object:
deepFreeze(myObj)

// Check if the object itself is extensible:
console.log(Object.isExtensible(myObj))
// Output:
// false

// Check if the "inner" object is extensible:
console.log(Object.isExtensible(myObj.profession))
// Output:
// false

// Try to change properties of the object:
myObj.name = 'Jack'

// Try to change properties of the "inner" object:
myObj.profession.title = 'DevOps architect'
myObj.profession.experience = 'junior'

// Log the "myObj" object:
console.log(myObj)
// Output:
// {
//   name: 'Joe',
//   age: 29,
//   profession: { // This "inner" object is remained unchanged.
//     title: 'Programmer',
//     experience: 'senior'
//   }
// }
```

## Unfreeze?

Now the bad news. When you freeze an object in JavaScript, with the `Object.freeze()` method, you can't unfreeze it. Freezing an object is the ultimate solution. There is no way to reverse this. Once some object has been frozen it can't be unfrozen, or modified in any way. This may look too much, but it is the best way to ensure objects will stay as you left them.

## Frozen objects and strict mode

In JavaScript, there are two variants of JavaScript you can work with. One is [sloppy mode]. The other is [strict mode]. Sloppy mode is the normal mode of JavaScript. It is the one you work with by default. One difference between these two is that sloppy mode let you do some things without throwing an exception, showing an error.

One example of this is manipulating with frozen object. When you try to do something with frozen object that is forbidden in sloppy mode nothing will happen. The change you want to make will not happen and no error will appear. It will fail silently. This will not happen if you switch to strict mode.

When you try to manipulate with properties of a frozen object JavaScript will throw an exception. This exception will be some `TypeError`, which specifically will depend on what you are trying to do. If you want JavaScript to throw these exceptions, switch to strict mode by adding the `'use strict'` statement.

```JavaScript
// Use strict mode:
'use strict';

// Create an object:
const myObj = {
  title: 'Functional Programming in JavaScript',
  author: 'Luis Atencio'
}

// Freeze the "myObj" object:
Object.freeze(myObj)

// Try to change the value of "title" property:
myObj.title = 'Functional Programming in JavaScript: How to improve your JavaScript programs using functional techniques'
// Output:
// TypeError: Cannot assign to read only property 'title' of object '#<Object>'

// Try to add new properties:
myObj.language = 'English'
myObj.format = 'Paperback'
// Output:
// TypeError: Cannot add property language, object is not extensible

// Try to remove "author" property:
delete myObj.author
// Output:
// TypeError: Cannot delete property 'author' of #<Object>
```

## Conclusion: How to freeze an object in JavaScript: Object.freeze(), Object.seal() & Object.preventExtensions()

Freezing objects in JavaScript, either completely or partially, is easy. It is also easy to prevent objects only from being extended by adding new properties. With a bit code, you can also ensure frozen objects are deeply frozen. I hope that this tutorial helped you understand how to do all these things.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[property flags]: https://blog.alexdevero.com/javascript-object-property-flags/#properties-flags-and-default-values
[object prototype]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object#object_prototypes
[recursion]: https://blog.alexdevero.com/recursion-in-javascript/
[sloppy mode]: https://developer.mozilla.org/en-US/docs/Glossary/Sloppy_mode
[strict mode]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode

<!--
### Meta:
-
-->

<!--
### Keywords:
- Freeze an Object in JavaScript
- Freeze an Object
-->

<!--
### Resources:
-
-->
