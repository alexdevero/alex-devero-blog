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

### Adding new objects to WeakSets

When you want to add objects to WeakSets you can do two things. First, you can pass those objects into the `WeakSet()` constructor when you create new WeakSet. Second, you can add objects later with the help of `add()` method. This method accepts one parameter, the object you want to store.

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

### Removing objects from WeakSets

Removing objects from WeakSets is simple and straightforward. When you want to remove some object, there is a method you use. This method is `delete()`. This method accepts one parameter, name of the object you want to remove. Similarly to `add()`, it also works with one object at the time.

So, if you want to remove multiple objects you have to use multiple `delete()` methods, one for each object. When you use this method, it will always return a [boolean]. It will return `true` if the object was successfully removed. If the object is not stored in the WeakSet it will return `false`.

```JavaScript
// Create some objects
let myObj1 = {
  language: 'JavaScript'
}

let myObj2 = {
  language: 'TypeScript'
}

let myObj3 = {
  language: 'Python'
}

// Create new WeakSet
// and add first two objects
const myWeakSet = new WeakSet([myObj1, myObj2])

// Remove "myObj1" object
myWeakSet.delete(myObj1)
// true

// Remove "myObj2" object
myWeakSet.delete(myObj2)
// true

// Try to remove "myObj3" object
myWeakSet.delete(myObj3)
// false
// Object "myObj3" is not stored in myWeakSet


// This will not work:
let myObj1 = {
  language: 'JavaScript'
}

let myObj2 = {
  language: 'TypeScript'
}

// Create new WeakSet
const myWeakSet = new WeakSet([myObj1, myObj2])

// Try to remove two objects at the same time
myWeakSet.delete(myObj1, myObj2)
// true
// It will successfully remove "myObj1",
// but ignore "myObj2"
```

### Checking if object exists in a WeakSet

WeakSets are not iterable, and there is no `size` property. This can make it hard to know if specific object does or doesn't exist in a WeakSet. Fortunately, there is a method you can use to find this out. This method is `has()`. Similarly to `delete()` and `add()` it also accepts one parameter.

This parameter is the name of an object you want to check for. When you use this method it also return a boolean, just like `delete()`. It returns either `true` if an object exists in a WeakSet or `false` if it doesn't exist.

```JavaScript
// Create some objects
let myObj1 = {
  language: 'React'
}

let myObj2 = {
  language: 'Vue.js'
}

let myObj3 = {
  language: 'Angular'
}

// Create new WeakSet
// and add first two objects
const myWeakSet = new WeakSet([myObj1, myObj2])

// Check if "myObj1" exists in "myWeakSet"
myWeakSet.has(myObj1)
// Output:
// true

// Check if "myObj2" exists in "myWeakSet"
myWeakSet.has(myObj2)
// Output:
// true

// Check if "myObj3" exists in "myWeakSet"
myWeakSet.has(myObj3)
// Output:
// false
```

## No iteration and size property

As you know, one difference between WeakSets and Sets is that WeakSets are not iterable. Another difference is that WeakSets don't have `size` property. This may not make sense. If you think about it, it actually does make sense. As we discussed, all object inside WeakSets are weakly held.

If any of those objects loses all references it will be "marked" for garbage collection. When this garbage collection happens this object is released from the memory. It is gone. The thing about garbage collection is that it works whenever it wants. You can't predict when it will happens.

Let's say you have an object. You add this object to a WeakSet. What if you, in another part of the code, remove that object? The answer is, it depends. It depends on whether the garbage collection had time to run or not. If it did, the object is released from memory, and it is also gone from the WeakSet.

Let's imagine for a moment you could use `size` or iterate over the WeakSet. If you iterate over it before the garbage collection, you will get one result. If you iterate over after the garbage collection you will get different one. The same with `size`. You would get two different numbers.

This is why it makes sense WeakSets are not iterable and there is no `size`. These two wouldn't be reliable. They would tell you one thing now and something completely different just a second later. It would be like rolling a dice.

### What about has()

I hope you understand why iterable WeakSets and `size` property doesn't make sense. What about the `has()` method? The `has()` is different story. Think about how this method works, or how you use it. When you use it, you pass in the name of the object you want to check for.

This name, the variable name, is a reference. When you pass it in, you don't pass in the object itself. Instead, you pass in that reference. Reference is the memory address of the variable. It is a pointer to the memory location where the variable is stored.

Back to garbage collection. Garbage collection collects objects only when all references to those objects are gone. Otherwise, it leaves them alone. When you use the `has()` method and you pass in a reference to some object it means there is still at least one reference to that object.

This means that this object was not garbage collected. It still exists. So, if you use the `has()` method you will get information that is reliable. This is why `has()` method does make sense while iteration and `size` property don't. The `has()` requires reference, existing object. The iteration and `size` property don't.

## Use case for WeakSets

Because of how they work, WeakSets are not used very often. When you want to store some values, objects or not, an array or a [Map] will be a better choice. One scenario where WeakSets can be useful is tracking existing objects. You could store references to those objects in an array or a Map.

This would prevent the garbage collection from collecting any of those object if all other references to them were gone. These objects would remain in memory and could potentially cause a memory leak. Use WeakSets to store those objects and you no longer have this problem.

One simple example can be a login system. You could keep track of users (objects) that are online by adding them to a WeakSet. When any of those users leaves you remove appropriate object. Later, you can use the `has()` method to check if specific user is still online, appropriate object exists, or not.

```JavaScript
// Create three users that are logged into a system
let user1 = { username: 'joey' }
let user2 = { username: 'jack15' }
let user3 = { username: 'skylar' }

// Create new WeakSet
const loggedUsers = new WeakSet()

// Add "user1" to "loggedUsers"
loggedUsers.add(user1)

// Add "user2" to "loggedUsers"
loggedUsers.add(user2)

// Add "user3" to "loggedUsers"
loggedUsers.add(user3)

// Check if all users are present
// loggedUsers.has(user1)
// // Output:
// // true

// loggedUsers.has(user2)
// // Output:
// // true

// loggedUsers.has(user3)
// // Output:
// // true

// Let "user2" and "user3" log out
user2 = null
user3 = null

// Check if all users are still logged in
loggedUsers.has(user1)
// Output:
// true

loggedUsers.has(user2)
// Output:
// false

loggedUsers.has(user3)
// Output:
// false
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
