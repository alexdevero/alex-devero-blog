# Garbage Collection in JavaScript Made Simple

Garbage collection is nothing new under the sun. Yet, there are many JavaScript developers who don't know much about it. If you are one of them, don't worry. This tutorial will help you understand the basic of garbage collection in JavaScript. You will learn what it is and how it works.<!--more-->
<!--
Table of Contents:
## A quick introduction
## Memory management and memory life cycle
## Memory release, or garage collection
## Garbage collection and how it works
### Reference and reachability
### Multiple references
### Interlinked objects or circular reference
### Mark-and-sweep algorithm
## Manual garbage collection
## Conclusion: Garbage collection in JavaScript made simple
-->

## A quick introduction

Chances are that you've already heard about this thing called "Garbage collection". If not, here is short version. JavaScript is a unique language. Unlike other languages, JavaScript is able to automatically allocate memory when it is needed. It can also release that memory when it is not needed anymore.

When you create new object, you don't have to use special method to allocate memory for that object. When you no longer need that object, you don't have to use another special method to release that memory. JavaScript will do this for you. It will automatically check if there is a need for memory allocation or memory release.

If there is such a need, JavaScript will do the work necessary to fulfill that need. It will do all this without you even knowing about it. This a good and also a bad thing. It is good because you don't have to worry about this too much. It is a bad thing because it can make you think you don't have to worry about this at all.

The problem is that JavaScript can help you with this memory management only to some degree. It also can't help you if you start throwing obstacles in the way. Before we get to garbage collection, let's quickly talk about memory and memory management.

## Memory management and memory life cycle

One thing programming languages share is something called memory life cycle. This life cycle describes the way memory is managed. It is composed of three steps. The first step is about allocating the memory you need. This happens when you declare new variables and assign the values, call a function that creates values, etc.

All these new values need some space in memory. JavaScript allocates this space, and makes it available, for you. The second step is about using that allocated memory for tasks such as read and writing data. For example, when you want to read value of some variable, or object property, or when you want to change that value or property.

The third and final step is about releasing that allocated memory. You want to free up the allocated memory when it is no longer needed. For example, when you no loner need that variable why keeping it forever? You want JavaScript to get rid of that variable, so it doesn't take up space in memory.

This third step is critical. Without it, your program would continue to consume more and more memory until no more was available. Then, it would crash. It is also this final step that is the most difficult to do correctly. Whether is it for you as a developer in low-level language or the language itself.

## Memory release, or garage collection

As you know, JavaScript takes care of memory management for you. It automatically handles all those three steps of memory life cycle. That is all nice, but what about the garbage collection? Where that comes into play? The quick answer is, in the third step. The whole third step, releasing allocated memory, is about garbage collection.

## Garbage collection and how it works

As we discussed, the third step is the most difficult step of the whole memory life cycle. How does the garbage collection know what memory should be released? There are few tools and tricks garbage collection uses to figure this out. Let's take a look at each of these tools and tricks.

### Reference and reachability

The main concept garbage collection relies on is the concept of references and reachability. It distinguishes between values that are reachable and values that are not. Values that are reachable are local variables and parameters in a current function. If there are nested functions in the chain, reachable values are also parameters and variables of these nested functions.

Lastly, reachable values are also all global variables, variables defined in [global scope]. All these reachable values are called "roots". However, this is not necessarily the end. If there are some other values, values that are reachable from a root by a reference or chain of references, then these values also become reachable.

JavaScript has a special process called garbage collector. This process runs on the background. What it does is it monitors all existing objects. When some object becomes unreachable this garbage collector will remove it. Let's take a look at simple code example.

First, let's declare new global variable called "toRead" and assign it an object as a value. This value will be root because it is in the global scope and there is and the variable "toRead" works as a reference to the object it holds, the value of that variable.

As long as this reference exists the object it holds, the variable value, will not be removed by garbage collector. It will stay in the memory because it is still reachable.

```JavaScript
// Create object in a global scope, a root value
let toRead = { bookName: 'The Art of Computer Programming' }
// JavaScript allocates memory for object { bookName: 'The Art of Computer Programming' },
// the "toRead" becomes reference for this object
// this existing reference prevents { bookName: 'The Art of Computer Programming' } object
// from being removed by garbage collector
```

Let's say you no longer need that object. A simple way you can tell JavaScript it is redundant is by removing all references to it. At this moment, there is only one existing reference, the "toRead" variable. If you remove this reference garbage collector will detect the object it referred to is no longer needed and it will remove it.

```JavaScript
// Remove reference to { bookName: 'The Art of Computer Programming' } object
let toRead = null
// Garbage collector can now detect
// that the { bookName: 'The Art of Computer Programming' } object
// is no longer needed, no longer reachable, and it can remove it,
// release it from the memory
```

### Multiple references

Another scenario is when you have an object and there are multiple references to that object. For example, you declare new global variable and assign it an object. After that, you declare another variable and assign it the first object by referencing the first variable.

As long as at least one of these references exists, this object will not be removed. The space in memory it occupies will not be released. In order for this to happen, you will have to remove both existing references, or more.

```JavaScript
// Create object in a global scope, a root value
let toRead = { bookName: 'The Art of Computer Programming' }
// This is the first reference to { bookName: 'The Art of Computer Programming' } object

// Create another reference for { bookName: 'The Art of Computer Programming' } object
let alreadyRead = toRead
```

The result of this will be still one object with occupying some space allocated in memory. However, there will be two existing references to this object.

```JavaScript
// Remove the first reference to { bookName: 'The Art of Computer Programming' } object
let toRead = null
// The { bookName: 'The Art of Computer Programming' } object
// is still reachable through the second reference
// and garbage collector can't remove it, release it from memory

// Remove the second reference to { bookName: 'The Art of Computer Programming' } object
let alreadyRead = null

// All references to the { bookName: 'The Art of Computer Programming' } object
// are gone and this object is now available
// for the garbage collector to be removed
```

### Interlinked objects or circular reference

Where this concept of reachability and references falls short are interlinked objects. This is also called [circular reference]. This situation happens one two objects reference each other. In that case, garbage collector can't remove any of them because each has at least one reference.

```JavaScript
// Create function that creates circular reference
function createCircularReference(obj1, obj2) {
  // Interlink both objects passed as arguments
  obj1.second = obj2
  obj2.first = obj1

  // Return new object based on the interlinked object
  return {
    winner: obj1,
    loser: obj2
  }
}

// Declare new variable and assign it the result
// of calling the createCircularReference() function
let race = createCircularReference({ name: 'Jack' }, { name: 'Spencer' })
// The value of "race" variable will be the third object
// created by interlinking the two objects
// passed to createCircularReference() function.
// These three objects are now all reachable
// because they reference each other
// and the "race" is a global variable, root
```

### Mark-and-sweep algorithm

The last trick garbage collection uses is mark-and-sweep algorithm. This algorithm is run periodically and performs a set of steps. First, it takes all existing roots and marks them. It basically saves to its memory. Next, it visits all the references reaching out from these roots. It marks these references as well.

After that, it again visits the marked objects and marks their references. This process of visiting and marking goes on and one until every reachable reference is visited. When this situation happens, the garbage collector knows which objects are marked and which are not.

Those objects that are not marked are considered unreachable, and safe to be removed. However, this doesn't mean these objects will be removed immediately. There can be some gap before an object is selected for garbage collection and when it is actually removed.

## Manual garbage collection

Aside to these tools and tricks there are also other optimizations to make your code run smoother, better and faster. These optimizations include generational collection, incremental collection, and idle-time collection. What is not included, what is not even possible, is some kind of a manual garbage collection.

This is the great thing on garbage collection. It happens automatically on the background. You don't have to do anything. It is also the bad thing because it works only automatically. You can neither trigger or force it nor can you top it or prevent it. Garbage collection will happen, you never know when, but it will.

## Conclusion: Garbage collection in JavaScript made simple

Garbage collection one thing JavaScript developers work with every day. It is my hope that this tutorial helped you understand what Garbage collection in JavaScript is and how it works. If you want to learn more about garbage collection in JavaScript, take a look at this [article].

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[global scope]:https://blog.alexdevero.com/javascript-scope-explained/#global-scope
[circular reference]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Memory_Management
[article]: https://jayconrod.com/posts/55/a-tour-of-v8-garbage-collection

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
- https://javascript.info/garbage-collection
-->
