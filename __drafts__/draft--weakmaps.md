# An Easy Introduction to WeakMap in JavaScript

WeakMap is one of the most underrated and least used collections in JavaScript. There are many JavaScript developers who don't even know they exist. This tutorial will help you understand them. You will learn about what WeakMaps are, how they work and how they differ from Maps.

<!--more-->
<!--
Table of Contents:
-->

## A quick introduction to WeakMap

Both, [Maps] and WeakMaps are new data structures, or collections, introduced in [ES6]. Another example of a collection is an [array]. Similarly to an array, both Maps and WeakMaps allow you to store data. In case of these Maps and WeakMaps you store the in the form of key-value pairs.

If you want to access some value stored in a Map, all you have to do is to use the correct `key`. This also works for WeakMaps. When you want you want to access some value stored in a WeakMap, you also have to use correct `key`. Both, Maps and WeakMaps allow you to add new key-value pairs and remove existing.

What if you are not sure if a Map or WeakMap contains specific key? There is a method you can use to quickly check if the key exists. So, this is where Maps and WeakMaps work in the same way. Along with these similarities, there are some important differences between these two you need to know.

### Differences between Maps and WeakMaps

The first difference between Maps and WeakMaps is the type of data you can use. With Maps, you can use any data type you want to create a key for the key-value pair. This also includes objects and functions. This is not true for WeakMaps. WeakMaps allow you to create keys only with objects, not with any other data type.

This is one of the main differences between Maps and WeakMaps. Another important difference is that all keys in a WeakMap are weakly referenced. This means that objects used as key for a WeakMap can still be garbage collected. This will happen when all references to those objects are gone.

When these objects are no longer used by any part of the program [garbage collection] will free them from memory. It is important to note that garbage collection will not free those objects from memory immediately. These objects will be only "marked" to be garbage collected.

Only when the next "cycle" of garbage collected happens, they will actually be freed. JavaScript runs these cycles automatically. So, you don't have to worry about it. The last big difference between Maps and WeakMaps is that WeakMaps are not iterable. You can't iterate over them using a loop or `forEach()` method like you can over Maps.

This also means that you have to know the key you are looking for. Since we are talking about iterability. WeakMaps also don't have any `size` property. So, you don't really know how many pairs are inside one. Lastly, there is no `clear()` method that would allow to remove all data from a WeakMap.

These differences are quite important and put serious constraints on what you can do with WeakMaps. However, don't let this discourage you from learning more about them because WeakMaps can still be useful. We will talk about this soon, but first, let's take a look at how to you can create WeakMaps and what you can do with them.

## How to create WeakMaps

When you want to create a WeakMap, you have to use [WeakMap() constructor]. This constructor will create new WeakMap object. When you have this object you can then do all the stuff you want. You can add new key-value pairs, check, retrieve or remove existing.

```JavaScript
// Create new WeakMap
const myWeakMap = new WeakMap()
```

## WeakMap methods

By default, WeakMap offer a set of methods that make working with them easier. These methods allow you to do (almost) all the things you may want to do. These methods are `set()`, `get()`, `delete()` and `has()`. Let's quickly take a look at each.

### Adding values

When you want to add new key-value pair to WeakMaps the `set()` method is what you need. This method takes two parameters, The first parameter is for the `key` inside the key-value pair. This will be some object. The second parameter is for `value`. This can be a string, number, boolean, etc.

One thing you need to remember about the `set()` method. This method allows you to add only one key-value pair at the time. If you want to add multiple pairs, you have to use this method multiple times, once for each pair.

```JavaScript
// Create new WeakMap
const myWeakMap = new WeakMap()

// Create some objects
const myObj1 = { name: 'Dexter' }
const myObj2 = { name: 'Jordan' }
const myObj3 = {}

// Add three new key-value pairs
myWeakMap.set(myObj1, 'I am not quite sure about this guy.')
myWeakMap.set(myObj2, 'This is a baller.')
myWeakMap.set(myObj3, 'We fired this guy a month ago.')


// You can also chain set() methods
myWeakMap
  .set(myObj1, 'This is first object.')
  .set(myObj2, 'This is second object.')
  .set(myObj3, 'This is third object.')
```

### Retrieving values

The `get()` method is what you are looking for when you want to retrieve values from WeakMaps. This method takes one parameter, the object you used as a key for the value you want to retrieve. If the key exists the `get()` method will return the value associated with it. Otherwise, it will return `undefined`.

```JavaScript
// Create new WeakMap
const myWeakMap = new WeakMap()

// Create some objects
const myObj1 = { language: 'JavaScript' }
const myObj2 = { language: 'Python' }
const myObj3 = { language: 'Rust' }

// Add two new key-value pairs
myWeakMap.set(myObj1, 'Language for every platform, soon even a fridge.')
myWeakMap.set(myObj2, 'I kind of miss those curly braces.')

// Retrieve the value associated with "myObj1"
myWeakMap.get(myObj1)
// Output:
// 'Language for every platform, soon even a fridge.'

// Try to retrieve the value associated with "myObj3"
// that was not added to "myWeakMap"
myWeakMap.get(myObj3)
// Output:
// undefined

// Try to retrieve the value associated with non-existing "myObj3"
myWeakMap.get(myObj4)
// Output:
// ReferenceError: myObj3 is not defined
```

### Removing values

The best, and probably only, way to remove values from WeakMaps is with the `delete()` method. This methods takes one parameter, a key. This is the object you used as the key to store the value associated with it. This metod will return either `true` or `false`. `true` if the pair in the WeakMap object has been removed successfully.

If the pair was not removed it will return `false`. You will also get `false` if the key doesn't exit in the WeakMap. The same will also happen if the thin you are trying to pas as a key is not an object.

```JavaScript
// Create new WeakMap
const myWeakMap = new WeakMap()

// Create some objects
const myObj1 = { language: 'JavaScript' }
const myObj2 = { language: 'Python' }
const myObj3 = {}

// Add two new key-value pairs
myWeakMap.set(myObj1, 'Semicolons or not?')
myWeakMap.set(myObj2, 'White space matters.')

// Remove the value associated with "myObj2"
myWeakMap.delete(myObj2)
// Output:
// true

// Try to remove the value associated with "myObj2" again
myWeakMap.delete(myObj2)
// Output:
// false

// Try to use "myObj3" that is not in myWeakMap
myWeakMap.delete(myObj2)
// Output:
// false
```
## Conclusion: [...] ...

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[array]: https://developer.mozilla.org/en-US/docs/Glossary/array
[Maps]: https://blog.alexdevero.com/maps-in-javascript/
[garbage collection]: https://javascript.info/garbage-collection
[WeakMap() constructor]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakMap/WeakMap

<!--
### Meta:
-
-->

<!--
### Keywords:
- WeakMap in JavaScript
- WeakMap
-->

<!--
### Resources:
-
-->
