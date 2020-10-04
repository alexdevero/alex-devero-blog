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
