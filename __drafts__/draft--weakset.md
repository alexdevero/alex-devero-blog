# What WeakSet in JavaScript Is and How It Works

WeakSet is one of the newer objects in JavaScript, or a collection. This collection can seem a bit esoteric. Many JavaScript developers don't know much about it, or at all. In this tutorial, you will learn what WeakSet in JavaScript is, how it works and also how you can use it.<!--more-->
<!--
Table of Contents:
-->

## A quick introduction

WeakSets are very similar to [Sets]. If you are not familiar with Sets, don't worry. You don't have to have prior knowledge of Sets. Back to WeakSets and Sets. They are both collections. You can use these collections to store values. One thing that may help you understand this are [arrays].

Arrays, just like WeakSets and Sets, are also collections. They also allow you to store various values, from numbers and string to booleans and objects, even Sets. This is very the similarity ens and the differences start to appear. One difference is that, unlike arrays, Sets can contain only unique values.

With weakSets this difference goes even further. WeakSets can only contain objects. If you try to add anything else than an object JavaScript will throw an error. These objects must be also unique. If you try to add some object twice, the second will not be added.

Another important thing about WeakSets is the "weak" part of the name. The "weak" part means that all objects you store inside a WeakSet are held weakly. So, if you remove all other references to object stored in a WeakSet that object will be, [garbage collected].

That object will be released from the memory. However, this doesn't mean the object will be released immediately. It will be only "marked" for garbage collection. Only when that happens it will be released. There is another important difference between Sets and WeakSets, and also arrays. WeakSets are not iterable.

You can add items or remove any existing. You can also check if WeakSet contains specific item. However, you can't iterate over it with some loop. There is also no `size` property that would tell you how many items are in a particular WeakSet. Now, let's take a look at how you can create new WeakSets.

## Creating new WeakSet

Whe you want to create new WeakSets you have to use `WeakSet()` constructor. This will create new WeakSet you can then use to store values. There are two ways in which you can use the `WeakSet()` constructor. First, you can use it to create an empty WeakSet and add to it values later.

Then, there is another thing you can do. You can pass an iterable with values as a parameter to the constructor at the moment you use it to create new WeakSet. When you hear the word "iterable" imagine some collection of values. In this case, the iterable is an array. So, pass in an array with objects.

```JavaScript
// Creating new WeakSets no.1: Empty
const myWeakSet = new WeakSet()

// Creating new WeakSets no.2: Passing some objects
const myWeakSet = new WeakSet([myObj1, myObj1])
```

## WeakSet methods

We already talked a little bit about what WeakSets allow you to do. You can add items to WeakSets and you can remove them. You can also check if some WeakSet contains specific item. There are specific methods for each of these tasks. Let's take a look at them.

### Adding new items to WeakSets

When you want to add items to WeakSets you can do two things. First, you can pass those items into the `WeakSet()` constructor when you create new WeakSet. Second, you can add items alter with the help of `add()` method. This method accepts one parameter, the object you want to store.

This is something you should remember. It actually accepts only one object, not more. If you try to pass in multiple objects only the first will be added to the WeakSet. The rest will be ignored. So, if you want to add multiple objects, use multiple `add()` methods for each.

```JavaScript
// Adding items no.1: via constructor
// Create some objects
let myObj1 = { name: 'Toby' }

let myObj2 = { name: 'Christine' }

// Create new WeakSet
const myWeakSet = new WeakSet([myObj1, myObj2])


// Adding items no.1: with add() method
// Create some objects
let myObj1 = { name: 'Rafael' }

let myObj2 = { name: 'Victoria' }

// Create new WeakSet
const myWeakSet = new WeakSet()

// Add objects
myWeakSet.add(myObj1)
myWeakSet.add(myObj2)


// This will not work:
// Create some objects
let myObj1 = { name: 'Jack' }

let myObj2 = { name: 'Julie' }

// Create new WeakSet
const myWeakSet = new WeakSet()

// Add objects
// The "myObj2" will not be added to the set
myWeakSet.add(myObj1, myObj2)
```

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Sets]: https://blog.alexdevero.com/sets-in-javascript/
[arrays]: https://developer.mozilla.org/en-US/docs/Glossary/array
[garbage collected]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Memory_Management#Garbage_collection

<!--
### Meta:
-
-->

<!--
### Keywords:
- WeakSet in JavaScript
- WeakSet
-->

<!--
### Resources:
-
-->
