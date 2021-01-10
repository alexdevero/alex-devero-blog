# Blog post title [...]
<!--more-->
<!--
Table of Contents:
## h2
### h3
### h3
## h2
## Conclusion: [...] ...
-->


## Object literal

## No.1: Object literal

Using object literals is the first way to create objects in JavaScript. It is probably also the easiest to learn, remember and use. This is probably also why it is the most popular way to create objects in JavaScript. Creating an object this way is simple. You wrap the key-value pairs with curly brackets (`{}`).

Those key-value pairs are pairs of `keys` and `values` you want the object to have. Another name for object `key` that is used very often is "property". Keys, or properties, are on the left side of the pair and values on the right. Between these two are colons (`key: value`).

When you wrap this pair with curly brackets you have an object. If you want to create an empty object you use only the curly brackets. After that, you can assign that new object to some [variable]. Or, you can use it right away as you want.

```JavaScript
// Creating object with object literal.
const myObj = {
  name: 'Tom Jones',// One key-value pair.
  role: 'admin',
  isWorking: false
}

// Log the object to console.
console.log(myObj)
// Output:
// {
//   name: 'Tom Jones',
//   role: 'admin',
//   isWorking: false
// }


// Creating an empty object with object literal.
const myEmptyObj = {}

// Log the object to console.
console.log(myEmptyObj)
// Output:
// {}
```

## No.2: The "new" keyword

The second way you can create an object is by using `new` keyword with `Object()` constructor. When you use this constructor it returns a value, new object. You can assign this object to a variable so you can continue working with it. If you want to add new properties there are two things you can do.

The first one is to create an empty object and assign it to a variable. Then, you can add properties to that object with dot-notation or using square brackets. This allows you to define only one property at the time. So, if you want to create multiple properties you will have to do this a couple of times.

The second option is to pass an object to the Object constructor as an argument. This will also create an object with properties and values you want. However, if you want to pass an object, using the Object constructor is redundant. It is also probably not a good practice and definitely not recommended.

What you can do instead in this case, is use the object literal way. We discussed this in the previous section above.

```JavaScript
// Creating object with object constructor.
const myObj = new Object()

// Add properties.
myObj.username = 'Skylar'
myObj.gender = 'female'
myObj.title = 'Fullstack dev'

// Log the object to console.
console.log(myObj)
// Output:
// {
//   username: 'Skylar',
//   gender: 'female',
//   title: 'Fullstack dev'
// }


// Passing an object - not a good idea
const myObj = new Object({
  username: 'Skylar',
  gender: 'female',
  title: 'Fullstack dev'
})

// Log the object to console.
console.log(myObj)
// Output:
// {
//   username: 'Skylar',
//   gender: 'female',
//   title: 'Fullstack dev'
// }
```


### h3

### h3

## h2

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
