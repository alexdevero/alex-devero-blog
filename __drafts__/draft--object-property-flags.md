# An Overview of JavaScript Object Property Flags and Descriptors

Objects are often used to store data as properties and values. This is not all. There are also tools to make these properties more flexible and powerful. Among them are Object property flags and descriptors. Learn what Object property flags and descriptors are and how to use them.<!--more-->
<!--
Table of Contents:
## h2
### h3
### h3
## h2
## Conclusion: [...] ...
-->

## Object property flags

[JavaScript object] allow you to store data. These data are stored as properties and values in key-value pairs. This is the usual stuff you are likely to do quite often. What you may not know is that this is not everything you can do. Those object properties offer additional options.

These additional options are very powerful and can change the way you work with properties. These additional options you can use to configure properties are called Object property flags and descriptors. Object property flags are attributes that each property in an object has.

These flags are `writable`, `enumerable` and `configurable`. All these flags have [boolean] value. They can be either true or false. Nothing else. Let's take a look at each of them.

### Writable

The `writable` flag tells if a specific object property can be changed. It this flag is `true` anyone can change that property. If it is `false` the property will become read-only and nobody can change it.

```JavaScript
// Create new object.
let myObj = {
  name: 'Jack',
  age: 31
}

// Set "name" property to non-writable.
Object.defineProperty(myObj, 'name', {
  writable: false
})

// Set "age" property to writable.
Object.defineProperty(myObj, 'age', {
  writable: true
})

// Try to change the value of "name" property.
myObj.name = 'Tony'

// Try to change the value of "age" property.
myObj.age = '44'

// Log the value of "name" property.
console.log(myObj.name)
// Output:
// 'Jack'

// Log the value of "age" property.
console.log(myObj.age)
// Output:
// '44'
```

### Enumerable

The second property flag is `enumerable`. When you want to know what are all properties that exist in an object you can iterate over it. For example, you can use [for...in] loop to get each property, one by one. Or, you can use [Object.keys()] to get all properties. The `enumerable` flag helps you to prevent this from happening.

When you set this flag to `false` for a specific property that property will no longer iterable. It will no longer be listed if you iterate over an object with loop. Setting this flag to `true` will do the opposite. The property will show up when you iterate over the object in a loop.

The `enumerable` flag has one exception. Even if you set it to `false` the [Reflect.ownKeys()] method will still be able to reveal it.

```JavaScript
// Create an object.
let myObj = {
  name: 'Victra',
  age: 28
}

// Set "name" property to non-enumerable.
Object.defineProperty(myObj, 'name', {
  enumerable: false
})

// Set "age" property to enumerable.
Object.defineProperty(myObj, 'age', {
  enumerable: true
})

// Try to get all properties from myObj
// using Object.keys() method.
console.log(Object.keys(myObj))
// Output:
// [ 'age' ]

// Try to get all properties from myObj
// using Reflect.ownKeys() method.
console.log(Reflect.ownKeys(myObj))
// Output:
// [ 'name', 'age' ]
```

### Configurable

The last flag, `configurable` specifies if you can delete concrete property or not. It also says if you can change any of its attributes, any of its property flags. Setting this flag to `false` will make a property prevent anyone from deleting and modifying it. Setting it to `true` will allow both.

```JavaScript
// Create an object.
let myObj = {
  name: 'Peter',
  age: 44
}

// Set "name" property to non-configurable.
Object.defineProperty(myObj, 'name', {
  configurable: false
})

// Set "age" property to configurable.
Object.defineProperty(myObj, 'age', {
  configurable: true
})

// Try to remove property "name" from myObj.
delete myObj.name

// Try to remove property "age" from myObj.
delete myObj.age

// Log the value of myObj.
console.log(myObj)
// Output:
// { name: 'Peter' }
```

## The Object.defineProperty() method

On the examples above, you could see that we worked with `Object.defineProperty()` method. This method allows you do two things. First, it allows you to change any flag of an existing property. You can also use it to change or all flags. This is how we used this method in previous examples.

The second thing it allows is to do is to create a new property. During that, you also can also set any of the three flags we discussed. If you don't want to change any of the flags, you don't have to. You can use this method to create the property and let all flags keep their default values.

When you want to use this method you have to do three things. First, you need to create some object. This object can be empty if you want to use the `Object.defineProperty()` method to create property. If you want to use it to configure existing property that property has to already exist on that object.

When you have this object you pass it as the first argument to the `Object.defineProperty()` method. The second thing you need is the name of a property. This is the property you want to either create or configure. You pass this name as the second argument. The last thing is an object.

You pass this object as the third argument. This object contains the flags you want to configure. If you want to create new property, you may also want to add fourth option `value`. This specifies the value that new property should have. If you omit this, JavaScript will assign the new property with value of `undefined`.

```JavaScript
// Example no.1: creating property
// Create empty object.
let myObj = {}

// Create property "name" on myObj
// First argument is object you want to work with.
// Second argument is the name of the property you want to create.
// Third argument is the object with flags and property value.
Object.defineProperty(myObj, 'name', {
  value: 'Jackie', // Value for new property.
  enumerable: true, // Make sure property is visible.
})

// Log the value of myObj.
console.log(myObj)
// Output:
// { name: 'Jackie' }

// Add additional property with value of undefined.
Object.defineProperty(myObj, 'age', {
  enumerable: true, // Make sure property is visible.
})

// Log the value of myObj.
console.log(myObj)
// Output:
// { name: 'Jackie', age: undefined }


// Example no.1: configuring property
// Create empty object.
let myObj = {
  name: 'Baron'
}

// Create property "name" on "myObj"
// First argument is object you want to work with.
// Second argument is the name of the property you want to create.
// Third argument is the object with flags and property value.
Object.defineProperty(myObj, 'name', {
  enumerable: true, // Make sure property is visible.
  writable: false // Make sure the property is read-only.
})

// Log the value of myObj.
console.log(myObj)
// Output:
// { name: 'Baron' }

myObj.name = 'Alexander'

// Log the value of myObj.
console.log(myObj)
// Output:
// { name: 'Baron' }
```

## Property descriptor

So far, we talked about descriptors a couple of times. However, we didn't talk about what it is. Or, did we? Actually, you just saw it on the previous example with the `Object.defineProperty()` method. Property descriptor is the "formal" name of the third parameter of this method, and the third argument you pass into it.

In other words, property descriptor is that object with Object property flags and value. In some way, you can think of the descriptor as the sum of all flags of a property.

```JavaScript
// Example no.1: configuring property
// Create empty object
let myObj = {}

// Create property "age" on myObj.
Object.defineProperty(myObj, 'age', {
  /* Property descriptor (object) */
  enumerable: true,
  writeable: true,
  value: 19
})
```

## Properties, flags and default values

Creating object properties directly and with the `Object.defineProperty()` method may look the same. However, there is one important difference, a difference worth remembering. When you create properties directly default values for all three flags will be set to `true`.

This is not the case with the `Object.defineProperty()` method. This method sets default values for all three flags to `false`. This is also why you set the `enumerable` flag of `name` property to `true`. Otherwise, you would never see it in console. So, keep this in mind when you decide about how will you create an object property.

```JavaScript
// Example no.1: creating property directly
const myObj = {
  subject: 'Programming'
}

// Log all Object property flags of "subject" property.
console.log(Object.getOwnPropertyDescriptor(myObj, 'subject'))
// Output:
// {
//   value: 'Programming',
//   writable: true,
//   enumerable: true,
//   configurable: true
// }

// Log the value of myObj.
console.log(myObj)
// Output:
// { subject: 'Programming' }


// Example no.2: creating property with Object.defineProperty()
const myObj = {}

Object.defineProperty(myObj, 'subject', {
  // Define only value and let flags keep default values.
  value: 'Programming'
})

// Log all Object property flags of "subject" property.
console.log(Object.getOwnPropertyDescriptor(myObj, 'subject'))
// Output:
// {
//   value: 'Programming',
//   writable: false,
//   enumerable: false,
//   configurable: false
// }

// Log the value of myObj.
// NOTE: "subject" property is non-enumerable - it will not show up.
console.log(myObj)
// Output:
// {}
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
