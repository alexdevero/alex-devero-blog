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

One of the most important differences is that, when it comes to maps in JavaScript, you can use any data type to create keys. You can use even objects or functions. Objects will allow you to use ony [strings] or a [symbols]. Another important difference is the order of keys-value pairs.

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

## Adding values to maps

When you want to add values, key-value pairs, to an object there are [two ways] to do that. Well, three, if you count adding values during object initialization. The first is using do notation. The second is using square brackets. The second way, square brackets, works also with maps.

That said, adding values to maps using square brackets is not a good practice. The problem is that when you do this you will lose performance optimizations maps have. The right way to add values to maps is by using `set()` method. This method accepts two parameters. First is for the `key` and second for the `value`.

```JavaScript
// Create new map
const myMap = new Map()

// Create simple function
function sayHi() {
  return 'Hello!'
}

// Add some values (key-value pairs) to "myMap"
myMap.set('name', 'James Reacher')
myMap.set('bio', { age: 35, height: 189, weight: 82 })
myMap.set(sayHi, 'Function as a key?')

// Log the content of "myMap"
console.log(myMap)
// Output:
// Map {
//   'name' => 'James Reacher',
//   'bio' => { age: 35, height: 189, weight: 82 },
//   [Function: sayHi] => 'Function as a key?'
// }
```

When you want to add multiple key-value pairs to a map you can do it only one at the time. One interesting thing is that maps support chaining. So, yes, you have to use `set()` method for every key-value pair you want to add. However, you can chain these methods so you don't have to use the name of the map over and over again.

```JavaScript
// Create new map
const myMap = new Map()

// Add some values using chaining
myMap.set('Language', 'JavaScript')
  .set('Author', 'Brendan Eich')
  .set('First appeared', '1995')

// Log the content of "myMap"
console.log(myMap)
// Output:
// Map {
//   'Language' => 'JavaScript',
//   'Author' => 'Brendan Eich',
//   'First appeared' => '1995'
// }
```

## Removing values from maps

When you want to remove values from maps the process is simple. There is a method you have use called `delete()`. This method accepts one parameter, the key of the key-value pair you want to remove. If the deletion is successful, the `delete()` method will return `true`. If the key doesn't exist, it will return `false`.

One thing to remember about `delete()` method is that it works only with one key at the time. You can't pass in multiple keys. If you try it the `delete()` method will remove only the first key. It will ignore the rest.

```JavaScript
// Create new map
const myMap = new Map()

// Add some values to "myMap"
myMap.set('name', 'Joe')
myMap.set('age', 25)

// Log the content of "myMap"
console.log(myMap)
// Output:
// Map { 'name' => 'Joe', 'age' => 25 }

// Remove "name" from "myMap"
myMap.delete('name')

// Log the content of "myMap" again
console.log(myMap)
// Output:
// Map { 'age' => 25 }


// This will not work
// Create new map
const myMap = new Map()

// Add some values to "myMap"
myMap.set('name', 'Joe')
myMap.set('age', 25)

// Try to remove "name" and "age" at the same time
myMap.delete('name', 'age')

// Log the content of "myMap" again
// Hint: only the "name" will be removed
// because it was the first parameter
console.log(myMap)
// Output:
// Map { 'age' => 25 }
```

## Removing all values from maps

Removing values with `delete()` method is handy when you want to remove just one or few values. If you want to remove all values in a map at once, there is a better and faster way to do it. Aside from overwriting the map, you can do this also with `clear()` method. This method doesn't accepts any parameters.

```JavaScript
// Create new map
const myMap = new Map()

// Add some values to "myMap"
myMap.set('The Lean Startup', 'Eric Ries')
myMap.set('Measure What Matters', 'John Doerr')
myMap.set('The Startup Owner\'s Manual', 'Steve Blank')

// Log the content of "myMap"
console.log(myMap)
// Output:
// Map {
//   'The Lean Startup' => 'Eric Ries',
//   'Measure What Matters' => 'John Doerr',
//   "The Startup Owner's Manual" => 'Steve Blank'
// }

// Remove all values from "myMap"
myMap.clear()

// Log the content of "myMap"
console.log(myMap)
// Output:
// Map {}
```

## Retrieving values from maps

Adding and removing values from maps is straightforward. You can say the same about retrieving them. When you want to retrieve a specific value from a map you can use `get()` method. This methods accepts one parameter, a key that is associated with the value you want to retrieve.

If the key its value you want to retrieve exists, it will return the value. If it doesn't exist it will return `undefined`.

```JavaScript
// Create new map
const myMap = new Map()

// Add some values to "myMap"
myMap.set('front-end', 'React')
myMap.set('back-end', 'Node.js')
myMap.set('database', 'MongoDB')

// Get the value of "back-end" key
myMap.get('back-end')
// Output:
// 'Node.js'

// Try to get the value of non-existent key "cms"
myMap.get('cms')
// Output:
// undefined
```

## Checking if value exists in map

In some sense, the `get()` method can also help you check if some key exists in a map. However, there is a method dedicated for this. This method is called `has()`. Similarly to `get()`, the `has()` method also accepts one parameter, the `key` you are looking for. If the key exists `has()` returns `true`. If not, it returns `false`.

```JavaScript
// Create new map
const myMap = new Map()

// Add some values to "myMap"
myMap.set('language', 'English')

// Check if "myMap" has "language" key
myMap.get('language')
// Output:
// true

// Check if "myMap" has "compiler" key
myMap.get('compiler')
// Output:
// false
```

## Getting the size of the map

In the "Maps vs Objects" we discussed that one of the benefits of maps is that it is easy to find out their size. This is true. Every Map object has its own `size` property. This property is analogous to the [length] property that exists on arrays. Using this `size` property will quickly tell you how many key-value pairs are there in a specific map.

```JavaScript
// Create new map
const myMap = new Map()

// Log the size of "myMap"
console.log(myMap.size)
// Output:
// 0

// Add some values to "myMap"
myMap.set('Tony Stark', 'Iron Man')
  .set('Steve Rogers', 'Captain America')
  .set('Black Widow', 'Natasha Romanoff')
  .set('Bruce Banner', 'Hulk')

// Log the size of "myMap" again
console.log(myMap.size)
// Output:
// 4
```

## Iterating over maps

You know how to add values to maps and how to remove them. You also know how to retrieve values, one by one. Question is, what if you want to retrieve all values from a map? There are four options you can choose from. These options are `keys()`, `values()`, `entries()` and `forEach()` methods.

### Map.keys(), Map.values() and Map.entries()

The first three methods all return `Iterator` object hat contain specific data. The first method, `keys()`, returns an `Iterator` with keys, one key for each pair in the Map. The second method, `values()` `Iterator` with values, also one value for each pair in the Map. The third method `entries()` returns an iterable for all entries.

These entries are returned in the form of a `[key, value]`. When you use these three method you can then iterate over the returned `Iterator` object with `next()` method and its `value` property. Every use of `next()` method, along with `value`, will return the next value in the iterator, next value, key or entry in the map.

```JavaScript
// Create new map
const myMap = new Map()

// Add some values
myMap.set('First name', 'Joshua Doer')
myMap.set('Email', 'joshua@doer.io')
myMap.set('username', 'josh1234')


// Example no.1: Map.keys()
const myKeysIterator = myMap.keys()

// Log the first key
console.log(myKeysIterator.next().value)
// Output:
// 'First name'

// Log the second key
console.log(myKeysIterator.next().value)
// Output:
// 'Email'

// Log the third key
console.log(myKeysIterator.next().value)
// Output:
// 'username'


// Example no.2: Map.values()
const myValuesIterator = myMap.values()

// Log the first value
console.log(myValuesIterator.next().value)
// Output:
// 'Joshua Doer'

// Log the second value
console.log(myValuesIterator.next().value)
// Output:
// 'joshua@doer.io'

// Log the third value
console.log(myValuesIterator.next().value)
// Output:
// 'josh1234'


// Example no.3: Map.entries()
const myEntriesIterator = myMap.entries()

// Log the first entry
console.log(myEntriesIterator.next().value)
// Output:
// [ 'First name', 'Joshua Doer' ]

// Log the second entry
console.log(myEntriesIterator.next().value)
// Output:
// [ 'Email', 'joshua@doer.io' ]

// Log the third entry
console.log(myEntriesIterator.next().value)
// Output:
// [ 'username', 'josh1234' ]
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
[two ways]: https://blog.alexdevero.com/javascript-objects-pt1/#adding-properties
[length]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/length

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
