# Memory Life cycle, Heap, Stack and Call Stack in JavaScript

There are topics in JavaScript you as a developer may not know and still get the work done. However, knowing about these topics can help you write better code. Memory heap, stack and call stack are some them. In this tutorial, you will learn about these topics and a bit about how JavaScript works.
<!--more-->
<!--
Table of Contents:
-->

## A quick introduction

JavaScript is a very forgiving programming language. It allows you to do a lot, in many ways. It also does a lot of work for you. Memory management is one of these things. Ask yourself: how many time did you have to think about allocating memory for your variables or functions?

How many times did you have to think about releasing that memory when you no longer needed those variables or functions? Chances are not even once. The same applies to knowing how is heap, stack and call stack work, or what it even is. And yet, you can still work with JavaScript. You can still write code that works every day.

These things are not necessary for you to know. Nor are they required. However, knowing about them and how they work can help you understand how JavaScript works. This, in turn, can help you write better code and become a better JavaScript.

## Memory life cycle

Let's start with the easiest part. What is a memory life cycle, what it is about and how it works in JavaScript? Memory life cycle refers to how a programming language works with memory. Regardless of the language, memory life cycle is almost always the same. It is composed of three steps.

The first step is memory allocation. When you assign a variable or create a function or object some amount of memory has to be allocated for it. The second step is memory use. When you work with data in your code, read or write, you are using memory. Reading from variables or changing values is reading from, and write to, memory.

The third step is memory release. When you no longer use some function or object, that memory is can be released. Once it is released it can be used again. This is the memory life cycle in a nutshell. The nice thing on JavaScript is that it does these three steps for you.

JavaScript allocates memory as you need and want. It makes it easier for you to work with that allocated memory. Lastly, it also does the heaving lifting and cleans up all the mess. It uses [garbage collection] to continuously check memory and release it when it is no longer in use. The result?

As a JavaScript developer, you don't have to worry about allocating memory to your variables or functions. You also don't have to worry about selecting correct memory address before reading from it. And, you don't have to worry about releasing the memory you used somewhere in the past.

## The stack and memory heap

Now you know about the steps of memory life cycle. You know about memory allocation, use and release. One question you may ask is where are those variables, functions and objects actually stored? The answer is: it depends. JavaScript doesn't store all these things at the same place.

What JavaScript does instead is it uses two places. These places are stack and memory heap. Which of these places will be used depends on what you are currently working with.

### The stack

The stack is a place that JavaScript uses to store only static data. This includes primitive [data types] values. For example, numbers, strings, booleans, `undefined` and `null`. These static data also include references. These references point to objects and functions you've created.

These data have one thing in common. The size of these data is fixed and JavaScript knows this size at compile time. This also means that JavaScript knows how much memory it should allocate, and allocates that amount. This type of memory allocation is called "static memory allocation". It happens right before the code is executed.

There is one important thing about static data and memory. There is a limit to how large these primitive values can be. This is also true for the stack itself. That too has limits. How high are these limits depends on specific browser and engine.

```JavaScript
// Declare and assign some variables
// and assign them primitive data types
// All these variables are stored in stack
const firstName = 'Jill'
const lastName = 'Stuart'
const age = 23
const selfEmployed = true
const dateOfMarriage = null

// The stack after declaring
// and assigning those variables:
///           Stack           ///
/////////////////////////////////
///   dateOfMarriage = null   ///
///   selfEmployed = true     ///
///   age = 23                ///
///   lastName = 'Stuart'     ///
///   firstName = 'Jill'      ///
/////////////////////////////////
```

### The memory heap

The second place where JavaScript can store data is memory heap. This storage is more dynamic. When it comes to memory heap, JavaScript doesn't allocate fixed amount of memory. Instead, it allocates memory as needed at the moment. This type of memory allocation is called "dynamic memory allocation".

Which data are stored in memory heap? While the stack is a place where JavaScript stores static data, memory heap is a place where JavaScript stores objects and functions. So, remember, when you create with primitives, you are working with static data. JavaScript stores these static data in the stack.

These data has always fixed allocated memory. When, on the other hand, you create objects or functions JavaScript stores them in memory heap. Allocated memory for these is not fixed. It is allocated dynamically as necessary.

```JavaScript
// Declare a variable and assign it an object
const terryP = {
  firstName: 'Terry',
  lastName: 'Pratchett',
  profession: 'author'
}

function introduceTerry() {
  return `Hi, my name is ${terryP.firstName}.`
}

const series = ['Discworld', 'Johnny Maxwell', 'Long Earth']

const isDone = true

///                  Stack                     ///
//////////////////////////////////////////////////
///   isDone = true                            ///
///   introduceTerry (reference to function)   ///
///   terryP (reference to "terryP" object)    ///
///   series (reference to "series" array)     ///
//////////////////////////////////////////////////


///                    Memory heap                  ///
///////////////////////////////////////////////////////
///  {                                              ///
///    firstName: 'Terry',                          ///
///    lastName: 'Pratchett',                       ///
///    profession: 'author'                         ///
///  }                                              ///
///  function introduceTerry() {                    ///
///    return `Hi, my name is ${terryP.firstName}.` ///
/// }                                               ///
///  ['Discworld', 'Johnny Maxwell', 'Long Earth']  ///
///////////////////////////////////////////////////////

// NOTE:
// the "terryP" in stack points
// to the "terryP" object in memory heap
// the "introduceTerry" in stack points
// to introduceTerry() function in memory heap
// the "series" in stack points
// to the "series" array in memory heap
// arrays are objects in JavaScript
```

## Stack, heap and references

When you create a variable and assign it a primitive value, it will be stored in stack. Something different happens when you try the same but with an object. If you declare a variable and assign it an object, two things will happen. First, JavaScript will allocate memory in stack for that variable.

When it comes to the object itself, JavaScript will store it in the memory heap. That variable that exists in the stack will only point to this object in memory heap. That variable will be a reference to this object. You can think of references as shortcuts, or aliases, for existing things.

These references are not those things themselves. They are only links to those "real" things. You can use those links to access those things they reference (they are linked to) and manipulate with them.

```JavaScript
// Declare variable and assign it an object
// The "cat" variable will be stored in stack
// It will hold the reference to the "cat" object
const cat = {
  name: 'Kitty'
  breed: 'Abyssinian'
}

// The "cat" object itself will be stored in memory heap:
///       Memory heap         ///
/////////////////////////////////
///  {                        ///
///    name: 'Kitty',         ///
///    breed: 'Abyssinian'    ///
///  }                        ///
/////////////////////////////////
```

### Copying objects and primitives

This is also why creating copies of objects is a not actually that simple in JavaScript. Trying to create a copy of an object stored in a variable by referencing it will not create real copy. It will not copy the object itself. It will copy only reference to that object. This is called [shallow copy].

When you then change the original object, the copy will change as well. This is because there is still only one object. However, there are two references (aliases or links) to that one object. When you use one of these references to change the object, the other reference still points to the same object, the one you just changed.

```JavaScript
// Declare a variable and assign it an object
const bookShelf = {
  read: 'Colour Of Magic',
  reading: 'Night Watch',
  toRead: 'Going Postal'
}

// Create a copy of the "bookShelf"
const newBookShelf = bookShelf

// Update the "bookShelf"
bookShelf.reading = 'Mort'
bookShelf.justFinished = 'Night Watch'

// Log the value of "bookShelf"
console.log(bookShelf)
// Output:
// {
//   read: 'Colour Of Magic',
//   reading: 'Mort',
//   toRead: 'Going Postal',
//   justFinished: 'Night Watch'
// }

// Log the value of "newBookShelf"
// Since "newBookShelf" and "bookShelf"
// points to the same object
// the output will be the same
console.log(newBookShelf)
// Output:
// {
//   read: 'Colour Of Magic',
//   reading: 'Mort',
//   toRead: 'Going Postal',
//   justFinished: 'Night Watch'
// }
```

This will not happen when you try to copy primitive value. When you try to copy primitive value, and you change the original, the copy will remain unchanged. The reason: there are no references. You are creating real copies and you are working directly with those copies.

```JavaScript
// Declare a variable with some primitive value
let book = 'Guards! Guards! (Paperback)'

// Create a copy of the "book"
const bookToRead = book

// Update the value of "book"
book = 'Guards! Guards! (Kindle Edition)'

// Log the value of "book"
// This will log the updated value
console.log(book)
// Output:
// 'Guards! Guards! (Kindle Edition)'

// Log the value of "bookToRead"
// This will log the old value because the "bookToRead"
// is a real copy of "book"
console.log(bookToRead)
// Output:
// 'Guards! Guards! (Paperback)'
```

Creating a real copy, [deep copy], is a bit more complicated. One option, less effective one, is writing that object from again scratch. Another option is using [Object.assign()]. Another one is using combination of `JSON.parse()` and `JSON.stringify()`.

```JavaScript
// Declare a variable and assign it an object
const bookShelf = {
  read: 'Colour Of Magic',
  reading: 'Night Watch',
  toRead: 'Going Postal'
}

// Create a copy of the "bookShelf"
const newBookShelf = Object.assign({}, bookShelf)

// Update the "bookShelf"
bookShelf.reading = 'Mort'
bookShelf.justFinished = 'Night Watch'

// Log the value of "bookShelf"
console.log(bookShelf)
// Output:
// {
//   read: 'Colour Of Magic',
//   reading: 'Mort',
//   toRead: 'Going Postal',
//   justFinished: 'Night Watch'
// }

// Log the value of "newBookShelf"
// The output will be different this time
// because // the "newBookShelf" points
// to a different object than the "bookShelf"
console.log(newBookShelf)
// Output:
// {
//   read: 'Colour Of Magic',
//   reading: 'Night Watch',
//   toRead: 'Going Postal'
// }
```

## The call stack

Chances are that you've already heard about something called "call stack". This is not the same as the stack we previously discussed in this tutorial. As you know, stack is a place JavaScript uses to store variables assigned with primitive values. Call stack is something different.

Call stack is a mechanism JavaScript uses to keep track of functions. When you call a function JavaScript will add that function to the call stack. If this function calls another function, JavaScript will add that function to the call stack as well, above the first function.

This process will repeat with any other function that will be called by the previous function. When one function is finished, JavaScript will remove that function from the call stack. There are two important things. The first thing is that every new function in the stack will be added to the top of the call stack.

The second thing is that the call stack is executed from the top to the bottom. The last function added to the stack will be executed as first. The first function added to the stack will be executed as last. This is also called LIFO principle (Last-In-First-Out). Let's illustrate this in code on one simple example.

```JavaScript
function myFuncOne() {
  return 'This is the end.'
}

function myFuncTwo() {
  myFuncOne()

  return 'Knock knock.'
}

// Call stack is still empty here

myFuncTwo()

// Call stack:
// Step 1: myFuncTwo() is invoked
// Step 2: myFuncTwo() added to the call stack
// Step 3: myFuncTwo() calls myFuncOne()
// Step 4: myFuncOne() is added to the call stack
// Step 5: myFuncOne(), is executed
// Step 6: myFuncOne() removed from the stack
// Step 7: JavaScript goes back to myFuncTwo()
// Step 8: any code left inside myFuncTwo() after myFuncOne() call is executed
// Step 9: myFuncTwo() is removed from the stack
// Step 10: call stack is empty
```

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
