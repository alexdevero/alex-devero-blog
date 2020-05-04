# How Shallow and Deep Copy in JavaScript Work

In this tutorial, you will learn about what is a deep copy and what is a shallow copy. Next, you will learn about what does "by value" and "by reference" mean. After that, you will also learn about when JavaScript creates shallow copies and when deep, and how to create deep copies of arrays and objects when you need them.<!--more-->
<!--
Table of Contents:
## Two types of copies
### Deep copy
### Shallow copy
## By value and by reference
## JavaScript, data and memory
### JavaScript, data, memory and deep copies
### JavaScript, data, memory and shallow copies
## Defaults for copying data in JavaScript
### Primitive data types
### Objects
### Arrays
## How to create deep copies of Arrays
### Spread operator
### .slice()
### map, filter, reduce
### Array.from()
### JSON.parse() & JSON.stringify()
## How to create deep copies of Objects
### Object.assign()
### Spread operator
### JSON.parse() & JSON.stringify()
## Conclusion: How Shallow and Deep Copy in JavaScript Work
-->

## Two types of copies

Copying data in JavaScript, or other programming languages, looks simple. Well, it might actually be more more complicated than you would think, or like. What you may not know is that not all copies are the same. Some copies are actually not even real copies. This is especially true in programming.

In programming, there are two types of copies. The first is called a "deep" copy. The second is called "shallow" copy. If you are not familiar with one or any of these terms, don't worry. You will learn about both, what are they and how they work. You will also learn how to which one is used in JavaScript by default and how to use the other.

### Deep copy

Let's start with the first type, the "deep" copy. Deep copy is what you probably think about when you think about copying something. It a 1:1 copy of that something, like a clone. When you create a deep copy, you create a perfect copy of the original. You take all properties from the original and copy them into the copy.

The copy and the original have the same properties. However, these properties, or the things that contain these properties, are not connected. This is the most important thing to remember. Since properties, and the original and copy, are not connected, if you change the original that change will not have any effect on that copy.

Any change you make to the original will change only that, the original. It will not change the copy. If this is true, then what you've created is a deep copy.

### Shallow copy

That was about deep copy. Now, let's talk about the second type, the shallow copy. Shallow copy is basically the opposite of deep copy. Yes, every copy is still 1:1 copy of the original. However, in case of shallow copy, properties of the original and the copy are connected. So, when you change the original it will also change the copy.

The same applies to the copy. If you change the copy, those changes will also change the original. Let's say you copy something, with all its properties and other stuff, and you create few copies. All these copies are shallow copies. Then, when you change just one of these copies, it will also change all other copies, and also the original.

## By value and by reference

The idea that, when you change one shallow copy that change will also automatically change all other shallow copies, and also the original, may seem weird. It will start making more sense when you understand what is going under the hood, and the idea of "by value" and copying "by reference".

In programming, there are two ways to pass, or copy stuff. One is by value and the other is by reference. When you pass, or copy something by value, you are creating a copy of it, a deep copy. When you pass or copy something by reference you are creating just an alias to the original, a shallow copy. You are not creating new copy, or new clone.

```text
// By reference
// Box is original
// Shallow copy 1,  Shallow copy 2, Shallow copy 3
// are just aliases to Box

|---------|
|   Box   |
|---------|
  |   |  |-------------connected to the Box-----------|
  |   |---connected to the Box-----|                  |
|--------------------| |--------------------| |--------------------|
|   Shallow copy 1   | |   Shallow copy 2   | |   Shallow copy 3   |
|--------------------| |--------------------| |--------------------|


// By value
// Box is original
// Copy 1,  Copy 2, Copy 3 are real and independent,
// i.e. deep, copies fo the Box

|---------|
|   Box   |
|---------|

|------------| |------------| |------------|
|   Copy 1   | |   Copy 2   | |   Copy 3   |
|------------| |------------| |------------|
```

All copies created by reference, i.e. shallow copies, are just aliases. This means that when you change any of these copies you are not actually changing that copy. You are changing the original itself. Remember, all shallow copies are just aliases, aliases for working with the original. Changing alias means changing the original.

This is why any change you make to any shallow copy automatically changes other copies and the original. You are not making any changes to the copy, but to the original. And, since all copies are just aliases to the original, they have to reflect current shape and form of the original.

Quick recap, "by value" means you create a real copy of the original. Both, the copy and original are completely independent. Change of one will not affect the other. "By Reference" means you create an alias to the original. There is no new copy or clone. There is still only one thing, the original, and a new name, or alias, you can use to call it.

So, when you use the alias, you are just using different name that will still "call" the original. Hence, anything you do with the alias will change the original, and also the other way around, because you are always working only with the original.

## JavaScript, data and memory

All these shallow and deep copies, values, references and aliases might be confusing. What might make it easier for you to grasp these concepts is some basic idea of how memory allocation in JavaScript works. When you create new [variable], JavaScript will allocate a spot in memory for it, for the value of that variable.

What happens when you change the value of that variable? JavaScript will find the correct memory spot, or address, where the value of that variable is stored. Then, it will change that value. Meaning, it will change that specific spot, or address, in memory. The same happens when you use that variable, or when you reference it in your code.

In that case, JavaScript will again find the correct memory spot, or address, where the value of that variable is stored and use it. Lastly, when you create new variable, JavaScript allocates yet another spot in memory and store the new variable, its value, there. So, you have three or more spots in memory that are allocated for something.

```JavaScript
// Create variable - JavaScript allocates new spot in memory for it
let myOriginalVariableOne = 'I am now allocated in memory.'


// Change the value of "myOriginalVariableOne"
// JavaScript finds correct spot in memory
// where the value of "myOriginalVariableOne" is stored and changes it
myOriginalVariableOne = 'I have been changed.'


// Reference "myOriginalVariableOne"
// JavaScript finds correct spot in memory
// where the value of "myOriginalVariableOne" is stored and returns it
console.log(myOriginalVariableOne)
// 'I have been changed.'


// Create another variable - JavaScript allocates another new spot in memory
let myOriginalVariableTwo = 'I am second variable allocated in memory.'


// Reference "myOriginalVariableTwo"
// JavaScript finds correct spot in memory
// where the value of "myOriginalVariableTwo" is stored and returns it
console.log(myOriginalVariableTwo)
// 'I am second variable allocated in memory.'
```

### JavaScript, data, memory and deep copies

Let's say you decide to copy some variable, a deep copy. In this case, JavaScript will allocate new spot in memory and store the value, a copy of the original value, of that new variable there. This process is the same as creating completely new variable.

As a result, you now have two different variables and also two different spots in memory. Both these spots are completely independent. Changing one will not change the other.

```JavaScript
// Deep copies are created by value
// Create variable - JavaScript allocates new spot in memory for it
let myOriginalVariable = 'I am now allocated in memory.'


// Create deep copy of "myOriginalVariable" - JavaScript also allocates new spot in memory for the new deep copy
let myDeepCopy = myOriginalVariable


// Reference "myOriginalVariable"
// JavaScript finds correct spot in memory
// where the value of "myOriginalVariable" is stored and returns it
// Note: JavaScript looks for memory spot for "myOriginalVariable"
console.log(myOriginalVariable)
// Value stored in memory for "myOriginalVariable":
// 'I am now allocated in memory.'


// Reference "myDeepCopy"
// JavaScript finds correct spot in memory
// where the value of "myDeepCopy" is stored and returns it
// Note: JavaScript looks for memory spot for "myDeepCopy",
// not the original, "myOriginalVariable"
console.log(myDeepCopy)
// Value stored in memory for "myDeepCopy":
// 'I am now allocated in memory.'


// Change the value of "myOriginalVariable"
// JavaScript finds correct spot in memory
// where the value of "myOriginalVariable" is stored and changes it
myOriginalVariable = 'Update for the original is coming.'


// Reference "myOriginalVariable" again
// JavaScript finds correct spot in memory
// where the value of "myOriginalVariable" is stored and returns it
// Note: JavaScript looks for memory spot for "myOriginalVariable"
console.log(myOriginalVariable)
// Value stored in memory for "myOriginalVariable":
// 'Update for the original is coming.'


// Reference "myDeepCopy" again
// JavaScript finds correct spot in memory
// where the value of "myDeepCopy" is stored and returns it
// Note: JavaScript looks for memory spot for "myDeepCopy",
// not the original, "myOriginalVariable"
console.log(myDeepCopy)
// Value stored in memory for "myDeepCopy":
// 'I am now allocated in memory.'
```

### JavaScript, data, memory and shallow copies

Let's say you also want to copy some variable. But now, you create a shallow copy. What happens at this moment? Now, JavaScript will not allocate new spot in memory for that copy. Instead, JavaScript will create new alias, that's connected to the spot in memory allocated for the original variable.

The result is that when you reference that copy (a shallow copy) JavaScript will find the memory spot allocated for the original variable and let you do whatever you want with the value stored there. Remember, there is no copy. Both original and copy/alias are connected to the same memory spot, the same value.

```JavaScript
// Shallow copies are created by reference
// Create variable - JavaScript allocates new spot in memory for it
let myOriginalVariable = {
  title: 'The Everything Store',
  author: 'Brad Stone',
  releaseDate: 'October 15, 2013',
  publisher: 'Hachette Audio'
}


// Create copy of "myOriginalVariable" - JavaScript does NOT
// allocate new spot in memory
// instead, it will new alias that is connected
// to the memory spot allocated for "myOriginalVariable"
let myShallowCopy = myOriginalVariable


// Reference "myOriginalVariable"
// JavaScript finds correct spot in memory
// where the value of "myOriginalVariable" is stored and returns it
console.log(myOriginalVariable)
// Value stored in memory for "myOriginalVariable":
// {
//   title: 'The Everything Store',
//   author: 'Brad Stone',
//   releaseDate: 'October 15, 2013',
//   publisher: 'Hachette Audio'
// }


// Reference "myShallowCopy"
// "myShallowCopy" is a shallow copy/alias,
// there is no spot in memory
// so, JavaScript looks for correct spot in memory
// where the value of the original "myOriginalVariable" is stored and returns it
console.log(myShallowCopy)
// Value stored in memory also for "myOriginalVariable":
// {
//   title: 'The Everything Store',
//   author: 'Brad Stone',
//   releaseDate: 'October 15, 2013',
//   publisher: 'Hachette Audio'
// }


// Change the shallow copy
// Since "myShallowCopy" is a shallow copy/alias,
// there is no spot in memory
// so, JavaScript looks for correct spot in memory
// where the value of the original "myOriginalVariable" is stored and changes that value
myShallowCopy.title = 'Creativity, Inc.'
myShallowCopy.author = 'Ed Catmull'
myShallowCopy.releaseDate = 'April 8, 2014',
myShallowCopy.publisher = 'Random House Audio'

// this is basically like
// myOriginalVariable.title = 'Creativity, Inc.'
// myOriginalVariable.author = 'Ed Catmull'
// myOriginalVariable.releaseDate = 'April 8, 2014',
// myOriginalVariable.publisher = 'Random House Audio'


// Reference "myOriginalVariable"
console.log(myOriginalVariable)
// Value stored in memory for "myOriginalVariable":
// {
//   title: 'Creativity, Inc.',
//   author: 'Ed Catmull',
//   releaseDate: 'April 8, 2014',
//   publisher: 'Random House Audio'
// }


// Reference "myShallowCopy"
// Uses the same memory spot as "myOriginalVariable"
console.log(myShallowCopy)
// {
//   title: 'Creativity, Inc.',
//   author: 'Ed Catmull',
//   releaseDate: 'April 8, 2014',
//   publisher: 'Random House Audio'
// }


// Change the original
myOriginalVariable.title = 'Shoe dog'
myOriginalVariable.author = 'Phil Knight'
myOriginalVariable.releaseDate = 'April 26, 2016',
myOriginalVariable.publisher = 'Simon & Schuster Audio'


// Reference "myOriginalVariable"
// Value stored on memory spot for "myOriginalVariable"
console.log(myOriginalVariable)
// {
//   title: 'Shoe dog',
//   author: 'Phil Knight',
//   releaseDate: 'April 26, 2016',
//   publisher: 'Simon & Schuster Audio'
// }


// Reference "myShallowCopy"
// Uses the same memory spot as "myOriginalVariable"
console.log(myShallowCopy)
// {
//   title: 'Shoe dog',
//   author: 'Phil Knight',
//   releaseDate: 'April 26, 2016',
//   publisher: 'Simon & Schuster Audio'
// }
```

## Defaults for copying data in JavaScript

I hope that you have some idea about how by value, by reference, shallow and deep copy work. Now, let's take a look at how JavaScript handles copying, because there is a catch. The catch is that JavaScript uses both, shallow and deep copies.

What determines which one JavaScript uses at the moment is the data type you are working with, either with [primitive data types] or objects and data collections.

### Primitive data types

When it comes to copying primitive data types, i.e. numbers, strings, boolean, etc., JavaScript always creates deep copies. So, when you create new variable whose value is one of these data types, and you copy it, you don't have to worry about anything. Every copy has its own spot in the memory and you can't accidentally change one by changing the other.

```JavaScript
// Primitive data types create deep copies by default

// Create variable containing a string
let myOriginalString = 'Let\'s create new memory spot.'


// Create a copy of myOriginalString (deep copy)
let myStringDeepCopy = myOriginalString


// Log the value of "myStringDeepCopy"
console.log(myStringDeepCopy)
// 'Let\'s create new memory spot.'


// Change the value of "myOriginalString"
myOriginalString = 'This will not change the deep copy.'


// Log the value of "myOriginalString"
console.log(myOriginalString)
// 'This will not change the deep copy.'


// Log the value of "myStringDeepCopy"
console.log(myStringDeepCopy)
// 'Let\'s create new memory spot.'


// Change the value of "myStringDeepCopy"
myStringDeepCopy = 'This will not change the original.'


// Log the value of "myStringDeepCopy"
console.log(myStringDeepCopy)
// 'This will not change the original.'
```

### Objects

In case of objects, the situation is different. In JavaScript, objects are stored just once, at the time you create them. When you copy any of them, no new copy, no deep copy, is created. Instead, JavaScript will create shallow copy that is just an alias for the original. In memory, there is still only one spot, for the original and all copies.

```JavaScript
// Objects create shallow copies by default

// Create an object
const usersOne = {
  tony: 'admin',
  joe: 'user',
  ricky: 'guest'
}


// Create copies of usersOne object (shallow copies)
const usersTwo = usersOne
const usersThree = usersOne


// Log values of usersOne
console.log('usersOne: ', usersOne)
// 'usersOne: ' { tony: 'admin', joe: 'user', ricky: 'guest' }


// Log values of usersTwo
console.log('usersTwo: ', usersTwo)
// 'usersTwo: ' { tony: 'admin', joe: 'user', ricky: 'guest' }


// Log values of usersThree
console.log('usersThree: ', usersThree)
// 'usersTwo: ' { tony: 'admin', joe: 'user', ricky: 'guest' }


// Change the value of ricky property in usersOne (original object)
usersOne.ricky = 'user'


// Log values of usersOne again
// The value of "usersOne" changed
console.log('usersOne: ', usersOne)
// 'usersOne: ' { tony: 'admin', joe: 'user', ricky: 'user' }


// Log values of usersTwo again
// The value of "usersTwo" changed
console.log('usersTwo: ', usersTwo)
// 'usersTwo: ' { tony: 'admin', joe: 'user', ricky: 'user' }


// Log values of usersThree again
// The value of "usersThree" changed
console.log('usersThree: ', usersThree)
// 'usersTwo: ' { tony: 'admin', joe: 'user', ricky: 'user' }


// Add another key/value pair to usersThree (shallow copy)
usersThree.jackie = 'guest'


// Log values of usersOne again
// The value of "usersOne" changed again
console.log('usersOne: ', usersOne)
// 'usersOne: ' { tony: 'admin', joe: 'user', ricky: 'user', jackie: 'guest' }


// Log values of usersTwo again
// The value of "usersTwo" changed again
console.log('usersTwo: ', usersTwo)
// 'usersTwo: ' { tony: 'admin', joe: 'user', ricky: 'user', jackie: 'guest' }


// Log values of usersThree again
// The value of "usersThree" changed again
console.log('usersTwo: ', usersThree)
// 'usersTwo: ' { tony: 'admin', joe: 'user', ricky: 'user', jackie: 'guest' }
```

This is why you have to pay attention when you work with objects. It is easy to do something you may not want since you are always working with the original.

### Arrays

Arrays work in the same way as objects. When you create new array, JavaScript will store it at a specific memory spot. If you create a copy of that array, or multiple copies, every copy will be just an alias for the memory location allocated for the original array. So, if you change any copy, or the original, the change will happen everywhere.

```JavaScript
// Arrays create shallow copies by default

// Create an array
let myOriginalArray = [1, 2, 'three', true]

// Create a copy of myOriginalArray (shallow copy)
let myShallowCopyArray = myOriginalArray


// Log the value of "myShallowCopyArray"
console.log(myShallowCopyArray)
// [ 1, 2, 'three', true ]


// Change the content of "myOriginalArray"
myOriginalArray[2] = 11
myOriginalArray.push(false)


// Log the value of "myOriginalArray" again
// The value of "myOriginalArray" changed
console.log(myOriginalArray)
// [ 1, 2, 11, true, false ]


// Log the value of "myShallowCopyArray" again
// The value of "myShallowCopyArray" also changed
console.log(myShallowCopyArray)
// [ 1, 2, 11, true, false ]


// Change the content of "myShallowCopyArray"
myShallowCopyArray.pop()
myShallowCopyArray.push(13)


// Log the value of "myOriginalArray"
// The value of "myOriginalArray" changed
console.log(myOriginalArray)
// [ 1, 2, 11, true, 13 ]


// Log the value of "myShallowCopyArray"
// The value of "myShallowCopyArray" also changed
console.log(myShallowCopyArray)
// [ 1, 2, 11, true, 13 ]
```

Similarly to objects, pay attention when you work with arrays. Since JavaScript creates shallow copies of arrays it is easy to do something you may not want.

## How to create deep copies of Arrays

One simple way to solve the problem with arrays and shallow copies is to always create new arrays. This will always create a deep copy, not a shallow. The problem is that this approach is also quite tedious, not really efficient and hard to maintain. Fortunately, there are better ways to create deep copies of arrays.

_Note: Spread operator works only if the array doesn't contain any nested objects. If there are any nested objects, those nested objects will be shallow copies. So, if you change the object in the original array you will also change the object inside the copied array. The reason is that values in these objects are still copied by reference.

If you work with arrays that contain nested objects, I suggest you use `JSON.parse()` and `JSON.stringify()`. This will allow you to create deep copies, including nested objects._

### Spread operator

The first option is using [spread operator] introduced in ES6. With spread, you can take one array and "spread" its values into a new one. As a result, you will have two arrays with the same content and both will have their own allocated spot in memory. So, when you change one, the other will stay the same.

```JavaScript
// Create an array
let myOriginalArray = ['Java', 'JavaScript']


// Create deep copy of myOriginalArray using spread
let myDeepCopyArray = [...myOriginalArray]


// Log the value of "myOriginalArray"
console.log(myOriginalArray)
// [ 'Java', 'JavaScript' ]


// Log the value of "myDeepCopyArray"
console.log(myDeepCopyArray)
// [ 'Java', 'JavaScript' ]


// Change the content of "myOriginalArray"
myOriginalArray.push('C', 'C++')


// Log the value of "myOriginalArray"
// The original array, we changed, changed
console.log(myOriginalArray)
// [ 'Java', 'JavaScript', 'C', 'C++' ]


// Log the value of "myDeepCopyArray"
// The deep copy, we did NOT change, did NOT change
console.log(myDeepCopyArray)
// [ 'Java', 'JavaScript' ]


// Change the content of "myDeepCopyArray"
myDeepCopyArray.push('Python', 'Ruby')


// Log the value of "myDeepCopyArray"
// The deep copy, we changed, changed
console.log(myDeepCopyArray)
// [ 'Java', 'JavaScript', 'Python', 'Ruby' ]


// Log the value of "myOriginalArray"
// The original array, we did NOT change, did NOT change
console.log(myOriginalArray)
// [ 'Java', 'JavaScript', 'C', 'C++' ]
```

### .slice()

Another option for creating a deep copy of an array is using `slice()` method. The `slice()` method is usually used to return piece of an array. However, you can also use it to create deep copies of arrays. All you have to do is to omit both parameters, for beginning and end. You can use either empty parenthesis or pass 0, i.e. `.slice(0)`.

```JavaScript
// Create an array
let myOriginalArray = ['Doc', 'Marty']


// Create deep copy of myOriginalArray using .slice()
let myDeepCopyArray = myOriginalArray.slice()

// Creates the same result as using .slice(0):
// let myDeepCopyArray = myOriginalArray.slice(0)


// Log the value of "myOriginalArray"
console.log(myOriginalArray)
// [ 'Doc', 'Marty' ]


// Log the value of "myDeepCopyArray"
console.log(myDeepCopyArray)
// [ 'Doc', 'Marty' ]


// Change the content of "myOriginalArray"
myOriginalArray.push('Einstein')


// Log the value of "myOriginalArray"
// The original array, we changed, changed
console.log(myOriginalArray)
// [ 'Doc', 'Marty', 'Einstein' ]


// Log the value of "myDeepCopyArray"
// The deep copy, we did NOT change, did NOT change
console.log(myDeepCopyArray)
// [ 'Doc', 'Marty' ]
```

### map, filter, reduce

The map, filter and reduce methods also introduced in ES6 will also help you create deep copy of an array. The reason this works is the same as in the case with `slice()`. All these methods return an array. So, when you use them to return an array (unchanged), and assign it to a variable, you will create a deep copy.

```JavaScript
//// Create an array
let myOriginalArray = ['Hard sci-fi', 'Soft sci-fi', 'Space opera']


// Create deep copy of myOriginalArray using .map()
// Map the original array and simply return all elements
let myMapDeepCopyArray = myOriginalArray.map(el => el)


// Create deep copy of myOriginalArray using .filter()
// Iterate over the original array and don't filter anything, just return every element
let myFilterDeepCopyArray = myOriginalArray.filter(el => el)


// Create deep copy of myOriginalArray using .reduce()
// Iterate over the original array and don't reduce it, just return the whole array (4th parameter)
let myReduceDeepCopyArray = myOriginalArray.reduce((accumulator, currentValue, currentIndex, array) => array)


// Log the value of "myOriginalArray"
console.log(myOriginalArray)
// [ 'Hard sci-fi', 'Soft sci-fi', 'Space opera' ]


// Log the value of "myMapDeepCopyArray"
console.log(myMapDeepCopyArray)
// [ 'Hard sci-fi', 'Soft sci-fi', 'Space opera' ]


// Log the value of "myFilterDeepCopyArray"
console.log(myFilterDeepCopyArray)
// [ 'Hard sci-fi', 'Soft sci-fi', 'Space opera' ]


// Log the value of "myReduceDeepCopyArray"
console.log(myReduceDeepCopyArray)
// [ 'Hard sci-fi', 'Soft sci-fi', 'Space opera' ]


// Change the original array
myOriginalArray.pop()
myOriginalArray.push('Social sci-fi')


// Log the value of "myOriginalArray" again
// The value did change, as we wanted
console.log(myOriginalArray)
// [ 'Hard sci-fi', 'Soft sci-fi', 'Social sci-fi' ]


// Log the value of "myMapDeepCopyArray" again
// The value did NOT change
console.log(myMapDeepCopyArray)
// [ 'Hard sci-fi', 'Soft sci-fi', 'Space opera' ]


// Log the value of "myFilterDeepCopyArray" again
// The value did NOT change
console.log(myFilterDeepCopyArray)
// [ 'Hard sci-fi', 'Soft sci-fi', 'Space opera' ]


// Log the value of "myReduceDeepCopyArray" again
// The value did NOT change
console.log(myReduceDeepCopyArray)
// [ 'Hard sci-fi', 'Soft sci-fi', 'Space opera' ]
```

### Array.from()

You can create deep copies of arrays also with `Array.from()`. When you want to create a deep copy of an array this way you assign a variable `Array.from()`, passing the original array to the `.from()` method. The result will be 1:1 deep copy.

```JavaScript
// Create an array
let myOriginalArray = ['Action', 'Simulation']


// Create deep copy of myOriginalArray using .map()
// Map the original array and simply return all elements
let myDeepCopyArray = Array.from(myOriginalArray)


// Log the value of "myOriginalArray"
console.log(myOriginalArray)
// [ 'Action', 'Simulation' ]


// Log the value of "myDeepCopyArray"
console.log(myDeepCopyArray)
// [ 'Action', 'Simulation' ]


// Change the value of "myOriginalArray"
myOriginalArray.push('RTS', 'Logic')


// Log the value of "myOriginalArray"
// The value did change, as we wanted
console.log(myOriginalArray)
// [ 'Action', 'Simulation', 'RTS', 'Logic' ]


// Log the value of "myDeepCopyArray"
// The value did NOT change
console.log(myDeepCopyArray)
//[ 'Action', 'Simulation' ]
```

### JSON.parse() & JSON.stringify()

The last, and probably most universal, option to create a deep copy of an array is by using `JSON.parse()` and `JSON.stringify()`. What the `JSON.stringify()` does is that it transforms something into a string. Then, the `JSON.parse()` transforms it back to the original form, or data type. If you combine this with assigning, the result is new array.

```JavaScript
// Create an array
let myOriginalArray = ['video', 'audio']


// Create deep copy of myOriginalArray using JSON.parse() and JSON.stringify()
let myDeepCopyArray = JSON.parse(JSON.stringify(myOriginalArray))


// Log the value of "myOriginalArray"
console.log(myOriginalArray)
// ['video', 'audio']


// Log the value of "myDeepCopyArray"
console.log(myDeepCopyArray)
// ['video', 'audio']


// Change the "myOriginalArray"
myOriginalArray.push('VR', 'AR')
myOriginalArray.sort()


// Log the value of "myOriginalArray"
// Value has changed as we wanted
console.log(myOriginalArray)
// [ 'AR', 'VR', 'audio', 'video' ]


// Log the value of "myDeepCopyArray"
// Value is still the same, as we wanted
console.log(myDeepCopyArray)
// [ 'video', 'audio' ]
```

## How to create deep copies of Objects

Similarly to arrays, one way to create deep copies of objects is by creating new objects, instead of copying them. Fortunately, there are other options that are easier, faster and less annoying.

_Note: Also similarly to arrays, the problem with spread operator and nested objects persists also in case of objects, not arrays. In case of nested objects, another object-specific option that doesn't work is `Object.assign()`. This too will create shallow copies of nested objects. Fortunately, `JSON.parse()` and `JSON.stringify()` will solve this problem, and allow you to create deep copies._

### Object.assign()

The first option for creating deep copies of objects is `Object.assign()`. The `assign()` method is often used by JavaScript developers to merge objects, by providing objects to merge, i.e. the "target" and "source" objects. However, this method can be also used for copying objects. More importantly, for creating deep copies.

When you want to use this method to copy objects, you have to do two things. First, you have to pass empty object as the "target", the first parameter. Second, you have to pass the original object as the "source". Lastly, since the `assign()` method returns new object, you have to assign it to a variable. This will create a deep copy of an object.

```JavaScript
// Create an object
let myOriginalObj = {
  language: 'English',
  difficulty: 'Easy'
}


// Create deep copy of "myOriginalObj" using Object.assign()
let myDeepCopyObj = Object.assign({}, myOriginalObj)


// Log the value of "myOriginalObj"
console.log(myOriginalObj)
// { language: 'English', difficulty: 'Easy' }


// Log the value of "myDeepCopyObj"
console.log(myDeepCopyObj)
// { language: 'English', difficulty: 'Easy' }


// Change the "myOriginalObj"
myOriginalObj.ethnicity = 'anglo-saxons'


// Log the value of "myOriginalObj"
// Value has changed as we wanted
console.log(myOriginalObj)
// {
//   language: 'English',
//   difficulty: 'Easy',
//   ethnicity: 'anglo-saxons'
// }


// Log the value of "myDeepCopyObj"
// Value is still the same, as we wanted
console.log(myDeepCopyObj)
// { language: 'English', difficulty: 'Easy' }
```

### Spread operator

Similarly to arrays, you can also use spread operator to create deep copies of objects.

```JavaScript
// Create an object
let myOriginalObj = {
  occupation: 'programmer',
  language: 'JavaScript'
}


// Create deep copy of myOriginalObj using Object.assign()
let myDeepCopyObj = { ...myOriginalObj }


// Log the value of "myOriginalObj"
console.log(myOriginalObj)
// { occupation: 'programmer', language: 'JavaScript' }


// Log the value of "myDeepCopyObj"
console.log(myDeepCopyObj)
// { occupation: 'programmer', language: 'JavaScript' }


// Change the "myOriginalObj"
myOriginalObj.language = ['JavaScript', 'TypeScript']


// Log the value of "myOriginalObj"
// Value has changed as we wanted
console.log(myOriginalObj)
// {
//   occupation: 'programmer',
//   language: [ 'JavaScript', 'TypeScript' ]
// }


// Log the value of "myDeepCopyObj"
// Value is still the same, as we wanted
console.log(myDeepCopyObj)
// { occupation: 'programmer', language: 'JavaScript' }
```

### JSON.parse() & JSON.stringify()

Again like with arrays you can also use `JSON.parse()` and `JSON.stringify()` to copy objects. It works in the same way as with arrays. The `JSON.stringify()` transforms an object into a string. Then, the `JSON.parse()` transforms it back to the original form, or an object. If you assign it to something, you get deep copy of the original object.

```JavaScript
// Create an object
let myOriginalObj = {
  class: 'English',
  students: {
    ricky: {
      name: 'Ricky',
      grade: 'A+'
    },
    tommy: {
      name: 'Tommy',
      grade: 'B'
    }
  }
}


// Create deep copy of myOriginalObj using Object.assign()
let myDeepCopyObj = JSON.parse(JSON.stringify(myOriginalObj))


// Log the value of "myOriginalObj"
console.log(myOriginalObj)
// {
//   class: 'English',
//   students: {
//     ricky: { name: 'Ricky', grade: 'A+' },
//     tommy: { name: 'Tommy', grade: 'B' }
//   }
// }


// Log the value of "myDeepCopyObj"
console.log(myDeepCopyObj)
// {
//   class: 'English',
//   students: {
//     ricky: { name: 'Ricky', grade: 'A+' },
//     tommy: { name: 'Tommy', grade: 'B' }
//   }
// }


// Change the "myOriginalObj"
myOriginalObj.students.jimmy = {
  name: 'Jimmy',
  grade: 'B+'
}


// Log the value of "myOriginalObj"
// Value has changed as we wanted
console.log(myOriginalObj)
// {
//   class: 'English',
//   students: {
//     ricky: { name: 'Ricky', grade: 'A+' },
//     tommy: { name: 'Tommy', grade: 'B' },
//     jimmy: { name: 'Jimmy', grade: 'B+' }
//   }
// }


// Log the value of "myDeepCopyObj"
// Value is still the same, as we wanted
console.log(myDeepCopyObj)
// {
//   class: 'English',
//   students: {
//     ricky: { name: 'Ricky', grade: 'A+' },
//     tommy: { name: 'Tommy', grade: 'B' }
//   }
// }
```

## Conclusion: How Shallow and Deep Copy in JavaScript Work

Congratulations. You've just finished this tutorial about shallow and deep copies in JavaScript. I hope you enjoyed this tutorial. In a recap, today you've learned about the two types of copies, shallow and deep copies. You've also learned about what does "by value" and "by reference" mean.

Next, you've learned a bit about how data and memory work in JavaScript. After that, you've learned about the defaults for copying data in JavaScript. When JavaScript creates shallow copies and when deep. Lastly, you've also learned how to create deep copies of arrays and objects when you need.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[variable]: https://blog.alexdevero.com/javascript-variables-introduction/
[primitive data types]: https://blog.alexdevero.com/javascript-basics-data-types-pt1/
[spread operator]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax

<!--
#### Meta:
-
-->

<!--
#### Inspiration:
-
-->
