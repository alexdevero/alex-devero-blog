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
