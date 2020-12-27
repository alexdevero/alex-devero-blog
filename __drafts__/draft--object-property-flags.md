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
let myObj = {
  name: 'Jack',
  age: 31
}

// Set "name" property to non-writable
Object.defineProperty(myObj, 'name', {
  writable: false
})

// Set "age" property to writable
Object.defineProperty(myObj, 'age', {
  writable: true
})

// Try to change the value of "name" property
myObj.name = 'Tony'

// Try to change the value of "age" property
myObj.age = '44'

// Log the value of "name" property
console.log(myObj.name)
// Output:
// 'Jack'

// Log the value of "age" property
console.log(myObj.age)
// Output:
// '44'
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
