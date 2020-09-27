# Optional Chaining in JavaScript and How It Works

Optional Chaining is one of the newest features in JavaScript. This feature may seem insignificant. However, it can save you a lot of time, code and also a lot of headaches. In this tutorial, you will learn what this feature is about, how it works and how to use it to write better JavaScript code.

<!--more-->
<!--
Table of Contents:
-->

## Defying the problem

Have you ever worked with [objects]? Then, you know how easy it is to run into following problem. Let's say you have an object. This object has some properties and maybe also some methods. Next, let's say that you want to work with some of these properties or methods.

Getting this done is very simple. You can [access any property] using either dot or square bracket notation. The same applies to methods. What happens is if you try to access some property, or method, that doesn't exist in that object? When you try to access property that doesn't exist you will get `undefined`.

```JavaScript
// Create an object
let myObj = {
  name: 'Joe Saladino',
  email: 'joe@saladino.io'
}

// Try to access non-existing property "location"
console.log(myObj.location)
// Output:
// undefined
```

What if you try to access some property that is nested deeper? Imagine you have some object. This object contains some properties. The value of one of these properties is supposed to be also an object. This object should contain some additional properties. What if this nested object doesn't exist?

What happens if you try to access some property in that non-existing nested object? You will not get `undefined`. What will you get instead is a `TypeError`. JavaScript will complain that it can't read property of an object that is not defined.

```JavaScript
// Create an object
let myObj = {
  name: 'Joe Saladino',
  email: 'joe@saladino.io'
}

// Try to access non-existing property "location"
console.log(myObj.location)
// Output:
// undefined

// Try to access non-existing property "city"
// in non-existing object "location"
console.log(myObj.location.city)
// Output:
// TypeError: Cannot read property 'city' of undefined
```

## Solving the problem the old way

Solving this problem this "old" way would mean using the logical [AND] (`&&`) operator. Let's try to solve the problem with the non-existing property `city` in a non-existing object `location` using the `&&` operator.

```JavaScript
// Create an object
let myObj = {
  name: 'Joe Saladino',
  email: 'joe@saladino.io'
}

// Try to access non-existing property "city"
// in non-existing object "location"
// using the && operator
console.log(myObj && myObj.location && myObj.location.city)
// Output:
// undefined
```

## A quick introduction to optional chaining

As you can see, solving the problem with the non-existing property in a non-existing object with `&&` operator is easy. The downside of this solution is that it requires more code. How much code will you have to write depends on how deep you need to get.

```JavaScript
// Create an object
let myObj = {
  name: 'Joe Saladino',
  email: 'joe@saladino.io'
}

// Going down the rabbit hole
console.log(myObj && myObj.location && myObj.location.city && myObj.location.city.address && myObj.location.city.address.houseNumber)
// Output:
// undefined
```

## How optional chaining works

Thanks to optional chaining, all that code is no longer necessary. The way how optional chaining works is simple. Let's say you use it to access some property. If any part before the property you want to access is either `undefined` or `null` it will stop the evaluation and return `undefined`.

Let me put it this way. With optional chaining, JavaScript will always first test any property, that precedes the one you want to access, if it exists. If it does exist JavaScript will move to the next property until it reaches the one you want to access. If it doesn't exists ti will return `undefined`.

## The syntax

The syntax of optional chaining is very simple. All you have to do is use `?` operator. The way to use this operator is to put it between the object and the dot that precedes the property that may not exists. For example, `myObj.myProp1?.myProp2` will ensure the `myProp1` exists before trying to access `myProp2`.

## Solving the problem with optional chaining

Let's demonstrate how optional chaining works by using it to solve the problem non-existing property `city` in a non-existing object `location`. In this example, you were trying to access non-existing property `city`. This property was supposed to exist in non-existing property/object `location`.

What you have to do is to ensure the `location` property/object actually exists, before you try to access any property inside it. To do this, you will put the `?` operator right after the `location` property and before the `.city`. So, `myObj.location?.city`. This will correctly return `undefined`, not `TypeError`.

```JavaScript
// Create an object
let myObj = {
  name: 'Joe Saladino',
  email: 'joe@saladino.io'
}

// Try to access non-existing property "city"
// in non-existing object "location"
// using optional chaining
console.log(myObj.location?.city)
// Output:
// undefined
```

## Going down the rabbit hole

When you need to go deeper, the process is the same. All you have to do is to put the `?` operator right after the object property that may not exist and right before the dot and property you want to access. You can repeat this for any number of properties you want or need.

```JavaScript
// Create an object
let myObj = {
  name: 'Joe Saladino',
  email: 'joe@saladino.io'
}

// Try to access "houseNumber" property
// that is supposed to be in "address"
// that is supposed to be in "city"
// that is supposed to be in "location"
console.log(myObj.location?.city?.address?.houseNumber)
// Output:
// undefined
```

## Optional chaining and methods

Just like with properties, you can use the optional chaining operator also with methods. The process is the same as with properties. You put the `?` operator right after the object property that may not exist, and right before the dot and method you want to call.

If the property doesn't exist, you will get `undefined`. If it does exists JavaScript will try to access the method. If the method exists, it will be invoked. Otherwise, you will again get `undefined`.

```JavaScript
// Create an object
let myObj = {
  name: 'Jack Trout',
  email: 'jack@trou.ai'
}

// Try to call "sayHi()" method directly
console.log(myObj.methods.sayHi())
// Output:
// TypeError: Cannot read property 'sayHi' of undefined


// Use the "?" operator:
// Try to call "sayHi()" method
// that is supposed to exist on "methods" property
// that is supposed to exist on "myObj" object
console.log(myObj.methods?.sayHi())
// Output:
// undefined
```

There is another thing you can do. You can use the optional chaining operator to check if the method itself exist before you call it. In this case, you have to put the `?` operator before the parentheses used to invoke the method. Then, you have to add another dot and only then the parentheses.

```JavaScript
// Create an object
let myObj = {
  name: 'Victoria Wales',
  email: 'joe@saladino.io'
}

// Try to call "sayHi()" method directly
console.log(myObj.sayHi())
// Output:
// TypeError: myObj.sayHi is not a function


// Use the "?" operator:
// Check if "sayHi()" method exists before you call it
// that is supposed to exist on "methods" property
// that is supposed to exist on "myObj" object
console.log(myObj.sayHi?.())
// Output:
// undefined


// Or if the method is nested
console.log(myObj.methods?.sayHi?.())
// Output:
// undefined
```

Using the `?` operator for calling a method if the thing you want to call is not a method will not work. For example, let's say that `sayHi` is not a method but a property. If you try to call it, with `?` operator, JavaScript will still throw `TypeError` saying that `sayHi` is not a function.

So, make sure that the method you want to call is really a method. If it is something else, it will still lead to JavaScript throwing an error.

```JavaScript
// Create an object
let myObj = {
  sayHi: 'Hi'
}

// Try to call property "sayHi"
console.log(myObj.sayHi?.())
// Output:
// TypeError: myObj.sayHi is not a function
```

## Optional chaining and bracket notation

You can also use the `?` operator when you want to access a property using bracket notation. In this case, the `?` operator goes right after the object name. Then comes a dot and after that come the square brackets and property name.

```JavaScript
// Declare new variable and set it to null
const myObj = null

// Try to access "name" property on null value directly
console.log(myObj['name'])
// Output:
// TypeError: Cannot read property 'name' of null


// Use the "?" operator:
// Try to access "name" property on null value
console.log(myObj?.['name'])
// Output:
// undefined
```

## Conclusion: Optional chaining in JavaScript and how it works

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[objects]: https://blog.alexdevero.com/javascript-objects-pt1/
[access any property]: https://blog.alexdevero.com/javascript-objects-pt1/#accessing-properties
[AND]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_AND

<!--
### Meta:
-
-->

<!--
### Keywords:
- Optional chaining in JavaScript
- Optional chaining
-->

<!--
### Resources:
-
-->
