# Introduction to Sets and WeakSets in JavaScript
<!--more-->
<!--
Table of Contents:
-->

## Introduction to Sets

Sets are a new object type that was introduced to JavaScript with ES6 (ES2015). What sets allow you to do is to create collections of values. These values can be anything, from [numbers] and [strings] to [arrays] and [objects]. This doesn't sound like something exciting. You can do the same thing with arrays.

The thing about sets, and where they differ from arrays, is that they can contain only unique values. When you try to add multiple same values into a set it will accept only the first. Any subsequent same value will be ignored. This also applies to values such as [null] and undefined. Each will be added only once.

This is one of the reasons why JavaScript developers sometimes choose sets over arrays. When you want to create a collection of some values, and you need all values to be unique, sets are the easiest option.

## Creating sets in JavaScript

When you want to create sets in JavaScript you do it always with the set constructor `set()`, preceded by the `new` keyword. This will create new Set object.

```JavaScript
// Create new empty set
let mySet = new Set()
```

## Adding values to Sets

When you are creating new set, there are two things you can do. First, you can create new empty Set object and add values to it later. You can add values to a set using `add()` method. This method accepts either one value or an iterable. Iterable means an array of values.

So, you can either pass in values one by one, or you can pass in an array with values. Both will work. Remember that set accepts all [primitive data types] as well as objects.

```JavaScript
// Example no.1: Adding a single value
// Create new empty set
let mySet = new Set()

// Add single values to "mySet" set
mySet.add('Helo')
mySet.add(314)
mySet.add(false)
mySet.add(null)
mySet.add(undefined)
mySet.add({ name: 'Joe' })

// Log the value of "mySet"
console.log(mySet)
// Output:
// Set { 'Helo', 314, false, null, undefined, { name: 'Joe' } }


// Example no.2: Adding multiple values
// Create new empty set
let mySet = new Set()

// Add multiple values to "mySet" set vie iterable
mySet.add(['Strike', 13, false, null, [5, 6], { language: 'JS & TS' }])

// Log the value of "mySet"
console.log(mySet)
// Output:
// Set { [ 'Strike', 13, false, null, [ 5, 6 ], { language: 'JS & TS' } ] }
```

The second option is to add values right at moment you are creating a set. To do this, you have to pass an iterable with some values as a parameter to set constructor.Remember that it is necessary to pass those values as iterable, that is an array. Otherwise, nothing will be added. This applies to both, single and multiple values.

```JavaScript
// Create new set and add a single value
let mySetOne = new Set(['Blackout!'])

// Log the value of "mySetOne"
console.log(mySetOne)
// Output:
// Set { 'Blackout!' }


// Create new set and add a single value
let mySetThree = new Set([{ galaxy: 'Milky way' }])

// Log the value of "mySetOne"
console.log(mySetThree)
// Output:
// Set { { galaxy: 'Milky way' } }


// Create new set and add a single value
let mySetFour = new Set([['Andromeda', 'Mayall\'s Object', 'Malin 1']])

// Log the value of "mySetOne"
console.log(mySetFour)
// Output:
// Set Set { [ 'Andromeda', "Mayall's Object", 'Malin 1' ] }


// Create new set and add multiple values
let mySetTwo = new Set(['Entropy', 'atoms', ['gravity', 'space']])

// Log the value of "mySetOne"
console.log(mySetTwo)
// Output:
// Set { 'Entropy', 'atoms', [ 'gravity', 'space' ] }
```

Notice that when you add values to set when you create it that array will get [deconstructed]. This means that `new Set(['a', 'b'])` will become `Set {'a', 'b'}`. See? No array wrapping the values. However, if you add an array inside the outer most array it will remain an array, such as in `['Entropy', 'atoms', ['gravity', 'space']]`.

## Removing values from Sets

The easiest way to remove a value from a set is by using `delete()` method. This method works in a similar way as the `add()` method. You pass the value as an argument when you call this method. If deletion is successful, `delete()` will return `true`. If not, it will return `false`.

One potential downside of this method is that it works only with one value at the time. If you try to pass in multiple values in the form of multiple arguments it will work only partially. The `delete()` method will remove only the first value, the first argument, and ignore the rest.

If you try to pass in values in the form of an array. The `delete()` method will ignore all values.

```JavaScript
// Create new set with some values
let mySet = new Set(['Pegasus', 'Hydra', 'Virgo'])

// Log the value of "mySet"
console.log(mySet)
// Output:
// Set { 'Pegasus', 'Hydra', 'Virgo' }

// Remove some values
mySet.delete('Pegasus')

// Log the value of "mySet" again
console.log(mySet)
// Output:
// Set { 'Hydra', 'Virgo' }


// Try to remove multiple values again using array
// Doesn't work at all
mySet.delete(['Hydra', 'Virgo'])

// Log the value of "mySet" again
console.log(mySet)
// Output:
// Set { 'Hydra', 'Virgo' }


// Try to remove multiple values using multiple parameters
// Removes only the first value passed into delete()
mySet.delete('Hydra', 'Virgo')

// Log the value of "mySet" again
console.log(mySet)
// Output:
// Set { 'Virgo' }
```

## Conclusion: Introduction to sets and WeakSets in JavaScript

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[numbers]: https://blog.alexdevero.com/javascript-basics-data-types-pt1/#numbers
[strings]: https://blog.alexdevero.com/javascript-basics-data-types-pt1/#strings
[arrays]: https://developer.mozilla.org/en-US/docs/Glossary/array
[objects]: https://blog.alexdevero.com/javascript-objects-pt1/
[null]: https://blog.alexdevero.com/javascript-basics-data-types-pt2/#null
[undefined]: https://blog.alexdevero.com/javascript-basics-data-types-pt2/#undefined
[primitive data types]: https://blog.alexdevero.com/javascript-basics-data-types-pt1/
[deconstructed]: https://blog.alexdevero.com/destructuring-assignment-javascript/#destructuring-arrays

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
- https://alligator.io/js/sets-introduction/
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakSet
-->
