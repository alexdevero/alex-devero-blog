# Blog post title [...]
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


// Assigning sealed object to new variable:
const myObj = {
  name: 'Joe Doe',
  age: 37
}

// Seal the "myObj" object and assign it to new variable:
const myObjSealed = Object.seal(myObj)

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
