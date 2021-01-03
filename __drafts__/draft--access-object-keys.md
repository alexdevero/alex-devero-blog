Object are very good for storing data as key-value pairs. Having those keys and values stored is one thing. Another is to know how to retrieve them so you can work with them. In this article, you will learn four different ways to do this, to access object keys, values and entries JavaScript.
<!--more-->
<!--
Table of Contents:
## h2
### h3
### h3
## h2
## Conclusion: [...] ...
-->


## Object.keys() and accessing all keys

When you want to access only object keys, the `Object.keys()` method will be the best tool. This method was introduced to JavaScript in ES6. The way this method works is simple. It takes an object you are interested in as argument. The value it returns are keys that exist inside that object.

The value you get, the keys, are in the form of an [array]. You can then use a `forEach()` method or `for` loop to iterate over these values and retrieve them individually. You can also use index. This might be another option if you know the order in which the keys are defined in the object.

The `Object.keys()` method will return these in the order you defined them. So, if you want the second or third key, you can use index `1` or `2` to get these keys. In case the object has no keys the array you will get will be also empty.

```JavaScript
// Example no.1: object with keys
// Create an object
const cat = {
  name: 'Tom',
  color: 'gray',
  age: 3,
  gender: 'male',
}

// Get all keys
const objKeys = Object.keys(cat)

// Log all keys
console.log(objKeys)
// Output:
// [ 'name', 'color', 'age', 'gender' ]

// Log all keys individually
objKeys.forEach(key => console.log(key))
// Output:
// 'name'
// 'color'
// 'age'
// 'gender'

// Log specific key
console.log(objKeys[3])
// Output:
// 'gender'


// Example no.2: empty object
const emptyObj = {}

console.log(Object.keys(emptyObj))
// Output:
// []
```

## Object.values() and accessing all values

An alternative of the previous method that will give you all values is `Object.values()` method. The way to use this method is the same as for the previous. You take some object and pass its name as the argument. The value you get will be also an array. This time, the array will contain all values inside the object you specified.

```JavaScript
// Example no.1: object with values
// Create an object
const cat = {
  name: 'Tom',
  color: 'gray',
  age: 3,
  gender: 'male',
}

// Get all values
const objValues = Object.values(cat)

// Log all values
console.log(objValues)
// Output:
// [ 'name', 'color', 'age', 'gender' ]

// Log all values individually
objValues.forEach(value => console.log(value))
// Output:
// 'Tom'
// 'gray'
// 3
// 'male'

// Log specific value
console.log(objValues[3])
// Output:
// 'male'


// Example no.2: empty object
const emptyObj = {}

console.log(Object.values(emptyObj))
// Output:
// []
```

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
