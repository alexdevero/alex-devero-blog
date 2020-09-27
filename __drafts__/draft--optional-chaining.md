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

// Going down the rabbit hole
console.log(myObj && myObj.location && myObj.location.city && myObj.location.city.address && myObj.location.city.address. houseNumber)
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
