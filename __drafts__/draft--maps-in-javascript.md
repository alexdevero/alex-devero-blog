# Introduction to Maps in JavaScript

Have you ever heard about maps in JavaScript? Maps are a new object type that was introduced in ES2015. In this tutorial, you will learn all you need to know about this feature. You will learn about what maps in JavaScript are, how they work and how to use them.

<!--more-->
<!--
Table of Contents:
## Conclusion: [...] ...
-->

## Quick introduction to maps

As a JavaScript developer you probably know JavaScript [objects]. Objects allow you to store data in the form of a key-value pair. Maps are very similar to JavaScript objects. When you want to store some data in maps, you store those data also in the form of a key-value pair.

Also just like with objects, you can add new keys and delete existing, and retrieve their values from maps. When you compare maps and objects, there are some differences you should know about. Let's take a look at those differences before moving further.

## Maps vs Objects

One of the most important differences is that, when it comes to maps, you can use any data type to create keys. You can use even objects or functions. Objects will allow you to use ony [strings] or a [symbols]. Another important difference is the order of keys-value pairs.

In maps, keys are ordered based on the order you've added them to the map. If you iterate over a map, you will get its keys in the same order in which you've created them. In case of objects, this is true since ES2015 and only for JavaScript engines that support this specification. Before ES2015, keys in objects were not ordered.

Another difference is how easy it is to get the size of a map. Like [set], every map has a `size` property that says how many key-value pairs it contains. With objects, you would have to use `keys()` or `values()` to get an array of keys or values. Then use `length` to get the length of this array to finally get the size of an object.

Another nice thing is that maps, like array, are iterable. You don't have to get the keys or values first in order to iterate over them. You can do it right away. For example, you can use [forEach() method], just like with array. You can also use [for...of loop], just like with objects.

The last difference, that is good to know, is that maps are optimized for adding and removing of key-value pairs. Objects are not. This may not matter if you don't need to manipulate with data often. If you do using maps may help you improve performance of your JavaScript code.

## Creating maps in JavaScript

Maps are similar to objects. One thing that is different between them, among the things we just discussed, is how you create them. When you want to create a new object, there are multiple options to do that. For example, you can use `new Object()`, `Object.create()`, object literal or object constructor.

When you want to create a new map, there is only one option to do it. You can create new maps only by creating new Map object, using `new Map()`.

```JavaScript
// Creating new map
let myMap = new Map()
```

## Conclusion: [...] ...

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[objects]: https://blog.alexdevero.com/javascript-objects-pt1/
[strings]: https://blog.alexdevero.com/javascript-basics-data-types-pt1/#strings
[symbols]: https://blog.alexdevero.com/javascript-basics-data-types-pt2/#symbols
[set]: https://blog.alexdevero.com/sets-in-javascript/
[forEach() method]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map/forEach
[for...of loop]: https://blog.alexdevero.com/javascript-loops/#for8230of-loop

<!--
### Meta:
-
-->

<!--
### Keywords:
- Maps in JavaScript
-->

<!--
### Resources:
- https://www.digitalocean.com/community/tutorials/js-maps-introduction
- https://javascript.info/map-set
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map
-->
