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

## A quick introduction

There are three things can access and retrieve from an object: keys, values and entries. Keys are the property names inside an object. Values are property values associated with property names. Entries are the (key-value) pairs of property names and their values. Let's take a look at how you can access and retrieve each.

## Access object keys with Object.keys() method

When you want to access object keys, the `Object.keys()` method will be the best tool. This method was introduced to JavaScript in ES6. The way this method works is simple. It takes an object whose keys you want to retrieve as argument. The value it returns are keys that exist inside that object.

The value you get, the keys, are in the form of an [array]. You can then use a [forEach()] method or `for` loop to iterate over these values and retrieve them individually. You can also use index. This might be another option if you know the order in which the keys are defined in the object.

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

## Access object values with Object.values() method

An alternative of the previous method that will give you all values is `Object.values()` method. The way to use this method is the same as for the previous. You take some object and pass its name as the argument. The value you get will be also an array. This time, the array will contain all values inside the object you specified.

```JavaScript
// Example no.1: object with values
// Create an object
const mouse = {
  name: 'Jerry',
  color: 'brown',
  age: 2,
  gender: 'male',
}

// Get all values
const objValues = Object.values(mouse)

// Log all values
console.log(objValues)
// Output:
// [ 'name', 'color', 'age', 'gender' ]

// Log all values individually
objValues.forEach(value => console.log(value))
// Output:
// 'Jerry'
// 'brown'
// 2
// 'male'

// Log specific value
console.log(objValues[0])
// Output:
// 'Jerry'


// Example no.2: empty object
const emptyObj = {}

console.log(Object.values(emptyObj))
// Output:
// []
```

## Get all entries with Object.entries() method

When you want to retrieve both, keys and values, the best fit will be `Object.entries()` method. This method, works like her two predecessors. It takes an object as an argument and returns an array. What will be difference in this case is the value you will get. It will be also an array.

However, this array will contain both, keys and values. These keys and values will be grouped together inside additional arrays. There will be one nested array for each group, or pai, of keys and values. The order of data inside these nested arrays will be always the same. The key will come as first and the value as second.

To get all these pairs, or entries, you can again use the `forEach()` method or `for` loop. To get one specific pair, or entry, you can use a specific index. If you want to get a concrete data from specific pair? Add one additional index, `0` for key or `1` for value.

```JavaScript
// Example no.1: object with keys
// Create an object
const dog = {
  name: 'Spike',
  color: 'gray',
  age: 5,
  gender: 'male',
}

// Get all entries
const objEntries = Object.entries(dog)

// Log all entries
console.log(objEntries)
// Output:
// [
//   [ 'name', 'Spike' ],
//   [ 'color', 'gray' ],
//   [ 'age', 5 ],
//   [ 'gender', 'male' ]
// ]

// Log all entries individually
objEntries.forEach(entry => console.log(entry))
// Output:
// [ 'name', 'Spike' ]
// [ 'color', 'gray' ]
// [ 'age', 5 ]
// [ 'gender', 'male' ]

// Log specific entry
console.log(objEntries[2])
// Output:
// [ 'age', 5 ]

// Log only key from a specific entry
console.log(objEntries[2][1])
// Output:
// 5


// Example no.2: empty object
const emptyObj = {}

console.log(Object.entries(emptyObj))
// Output:
// []
```

### Combining Object.entries() with forEach() method

Working with those nested arrays you get from `Object.entries()` can be painful. There is a way to make it more comfortable. What you can do is to combine the `Object.entries()` method either with `forEach()` method. The `forEach()` method allows you to specify function to execute for each item in an array.

This function can take up to three parameters: current value, index of the current value and the source array. If you use the current parameter as it is, you will get current entry, key-value pair, during each iteration. Another thing you can do is to use [destructuring assignment].

This will allow you to directly access object keys or values. You can use the destructuring assignment inside the function of the forEach() method. Or, you can use it when you specify the parameter for current value. In both cases, you will be able to work with keys and values directly.

If you don't want to use destructuring assignment you don't have to. Instead, you can use a combination of the `forEach()` method parameter and array index. This will allow you to access the key (index `0`) and value (index `1`) in each entry as well.

```JavaScript
// Example of Object.entries() and forEach() method
// Create an object
const man = {
  name: 'George',
  color: 'white',
  age: 40,
  gender: 'male',
}

// Get all entries
const myObjEntries = Object.entries(man)

// Use forEach() method to iterate over man object entries
myObjEntries.forEach((entry) => {
  // Use destructuring assignment
  // to get direct access to keys and values
  const [key, value] = entry

  // Log each key, value and entry
  console.log(`
    key: ${key}
    value: ${value}
    entry: { ${key}: ${value} }
  `)
})
// Output:
// '
//   key: name
//   value: George
//   entry: { name: George }
// '
// '
//   key: color
//   value: white
//   entry: { color: white }
// '
// '
//   key: age
//   value: 40
//   entry: { age: 40 }
// '
// '
//   key: gender
//   value: male
//   entry: { gender: male }
// '


// Example no.2: destructuring assignment with parameter
myObjEntries.forEach(([key, value]) => {
  // Log each key, value and entry
  console.log(`
    key: ${key}
    value: ${value}
    entry: { ${key}: ${value} }
  `)
})
// Output:
// '
//   key: name
//   value: George
//   entry: { name: George }
// '
// '
//   key: color
//   value: white
//   entry: { color: white }
// '
// '
//   key: age
//   value: 40
//   entry: { age: 40 }
// '
// '
//   key: gender
//   value: male
//   entry: { gender: male }
// '


// Example no.3: without destructuring
myObjEntries.forEach((entry) => {
  // Log each key, value and entry
  console.log(`
    key: ${entry[0]}
    value: ${entry[1]}
    entry: { ${entry[0]}: ${entry[1]} }
  `)
})
```

### Combining Object.entries() with for...of loop

Another option is to combining the `Object.entries()` with [for...of] loop. The `for...of` loop gives you basically the same options as the `forEach()`. Only the syntax is different. Similarly to `forEach()` method, you can also use destructuring assignment to access keys and values directly.

In this case, you can use destructuring also in two ways. The first is inside the loop on the variable that contains current entry. Or, you can use it directly on the loop variable and destruct that. Without destructuring, you again use a combination of the loop variable and array index.

```JavaScript
// Example of Object.entries() and for...of loop
// Create an object
const woman = {
  name: 'Joan',
  color: 'white',
  age: 30,
  gender: 'female',
}

// Get all entries
const myObjEntries = Object.entries(woman)

// Use for...of loop to iterate over woman object
for (const entry of myObjEntries) {
  // Use destructuring assignment
  // to get direct access to keys and values
  const [key, value] = entry

  // Log each key, value and entry
  console.log(`
    key: ${key}
    value: ${value}
    entry: { ${key}: ${value} }
  `)
}
// Output:
// '
//   key: name
//   value: Joan
//   entry: { name: Joan }
// '
// '
//   key: color
//   value: white
//   entry: { color: white }
// '
// '
//   key: age
//   value: 30
//   entry: { age: 30 }
// '
// '
//   key: gender
//   value: female
//   entry: { gender: female }
// '


// Example no.2: destructuring assignment with loop variable
for (const [key, value] of myObjEntries) {
  // Log each key, value and entry
  console.log(`
    key: ${key}
    value: ${value}
    entry: { ${key}: ${value} }
  `)
}
// Output:
// '
//   key: name
//   value: Joan
//   entry: { name: Joan }
// '
// '
//   key: color
//   value: white
//   entry: { color: white }
// '
// '
//   key: age
//   value: 30
//   entry: { age: 30 }
// '
// '
//   key: gender
//   value: female
//   entry: { gender: female }
// '


// Example no.3: without destructuring
for (const entry of myObjEntries) {
  // Log each key, value and entry
  console.log(`
    key: ${entry[0]}
    value: ${entry[1]}
    entry: { ${entry[0]}: ${entry[1]} }
  `)
}
// Output:
// '
//   key: name
//   value: Joan
//   entry: { name: Joan }
// '
// '
//   key: color
//   value: white
//   entry: { color: white }
// '
// '
//   key: age
//   value: 30
//   entry: { age: 30 }
// '
// '
//   key: gender
//   value: female
//   entry: { gender: female }
// '
```

## Alternative: for...in loop

The methods we just discussed are one way to access object keys or values, or entries. However, there is also another alternative. You can also access object keys and values, or entries, by using [for...in] loop. This alternative might be actually more useful in some cases because than any of the three methods.

The reason is that `for...in` loop can be more flexible. When you use it it allows you to work with both, keys and also values. Those three methods each work with only one type of data. The `Object.entries()` method also works with both. However, it is not very friendly, although the `for...of` or `forEach()` makes it better.

Now, let's consider the `for...in` loop as an alternative. The first thing you need is some object, object you want to iterate over. THe second thing you need is to specify one variable name. This is for the `for...in` loop. When executed, the loop will assign specific object key to this variable on each iteration.

With this quick setup, and the variable, you can quickly access object keys. If you need to access object values you can just combine the object (name of the object variable) and the variable. If you need both, you can use the variable and also combine it with the object (name of the object variable).

```JavaScript
// Example of for...in loop
// Create an object
const cuckoo = {
  name: 'Cuckoo',
  color: 'yellow',
  age: 1,
  gender: 'male',
}

// Iterate over cuckoo object
for (const key in cuckoo) {
  // Log each key
  // then each value
  // and lastly each entry
  console.log(`
    key: ${key}
    value: ${cuckoo[key]}
    entry: ${key}: ${cuckoo[key]}
  `)
}
// Output:
// '
//   key: name
//   value: Cuckoo
//   entry: name: Cuckoo
// '
// '
//   key: color
//   value: yellow
//   entry: color: yellow
// '
// '
//   key: age
//   value: 1
//   entry: age: 1
// '
// '
//   key: gender
//   value: male
//   entry: gender: male
// '
```

## Conclusion: [...] ...

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[array]: https://developer.mozilla.org/en-US/docs/Glossary/array
[forEach()]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach
[destructuring assignment]: https://blog.alexdevero.com/destructuring-assignment-javascript/#destructuring-arrays
[for...of]: https://blog.alexdevero.com/javascript-loops/#for8230of-loop
[for...in]: https://blog.alexdevero.com/javascript-loops/#for8230in-loop

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
