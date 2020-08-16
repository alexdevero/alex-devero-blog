# Introduction to Sets in JavaScript

Sets are a new object type introduced in ES6 (ES2015). Although they are lesser known, they can be very useful and powerful. This tutorial will help you learn all you need to know about them. You will learn about what sets in JavaScript are, how they work and how to use them.

<!--more-->
<!--
Table of Contents:
## Introduction to Sets
## Creating sets in JavaScript
## Adding values to Sets
## Removing values from Sets
## Removing all values from Sets
## Checking for existing values in Sets
## Finding out how big a set is
## Sets, keys and values
### Looping over values with for...of loop
## Getting all entries in a set
## Conclusion: Introduction to sets in JavaScript
-->

## Introduction to Sets

Sets are a new object type that was introduced to JavaScript with ES6 (ES2015). What sets allow you to do is to create collections of values. These values can be anything, from [numbers] and [strings] to [arrays] and [objects]. This doesn't sound like something exciting. You can do the same thing with arrays.

The thing about sets, and where they differ from arrays, is that they can contain only unique values. When you try to add multiple same values into a set it will accept only the first. Any subsequent same value will be ignored. This also applies to values such as [null] and undefined. Each will be added only once.

This is one of the reasons why JavaScript developers sometimes choose sets over arrays. When you want to create a collection of some values, and you need all values to be unique, sets are the easiest option.

## Creating sets in JavaScript

When you want to create sets in JavaScript you do it always with the set constructor `set()`, preceded by the `new` keyword. This will create new Set object.

```JavaScript
// Create new empty set
const mySet = new Set()
```

## Adding values to Sets

When you are creating new set, there are two things you can do. First, you can create new empty Set object and add values to it later. You can add values to a set using `add()` method. This method accepts either one value or an iterable. Iterable means an array of values.

So, you can either pass in values one by one, or you can pass in an array with values. Both will work. Remember that set accepts all [primitive data types] as well as objects.

```JavaScript
// Example no.1: Adding a single value
// Create new empty set
const mySet = new Set()

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
const mySet = new Set()

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
const mySetOne = new Set(['Blackout!'])

// Log the value of "mySetOne"
console.log(mySetOne)
// Output:
// Set { 'Blackout!' }


// Create new set and add a single value
const mySetThree = new Set([{ galaxy: 'Milky way' }])

// Log the value of "mySetOne"
console.log(mySetThree)
// Output:
// Set { { galaxy: 'Milky way' } }


// Create new set and add a single value
const mySetFour = new Set([['Andromeda', 'Mayall\'s Object', 'Malin 1']])

// Log the value of "mySetOne"
console.log(mySetFour)
// Output:
// Set Set { [ 'Andromeda', "Mayall's Object", 'Malin 1' ] }


// Create new set and add multiple values
const mySetTwo = new Set(['Entropy', 'atoms', ['gravity', 'space']])

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
const mySet = new Set(['Pegasus', 'Hydra', 'Virgo'])

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

## Removing all values from Sets

Sometimes, you may want to remove all values from set. This can be done using `clear()` method. This method doesn't accept any arguments.

```JavaScript
// Create new set
const mySet = new Set()

// Add some values
mySet.add('Centaurus')
mySet.add('Sculptor')
mySet.add('Circinus')

// Log the value of "mySet"
console.log(mySet)
// Output:
// Set { 'Centaurus', 'Sculptor', 'Circinus' }

// Remove all values
mySet.clear()

// Log the value of "mySet" again
console.log(mySet)
// Output:
// Set {}
```

## Checking for existing values in Sets

The `has()` method is probably the simplest way to test if set contains a specific value. This method accepts a single parameter, value you want to search for. If the value exists, `has()` will return `true`. Otherwise, it will return `false`.

```JavaScript
// Create new set with some values
const mySet = new Set(['Jack', 'Andrew', 'Victoria', 'Emma'])

// Check if "mySet" contains "Andrew"
mySet.has('Andrew')
// Output:
// true

// Check if "mySet" contains "Leopold"
mySet.has('Leopold')
// Output:
// false
```

## Finding out how big a set is

When you want to know how many items are in an array, you can use its `length` property. Sets don't have exactly this property. However, they have an alternative. This alternative is `size` property. It works just like `length` property, returns the number all values that exist in a specific set.

```JavaScript
// Create new set
const mySet = new Set()

// Log the size of "mySet"
console.log(mySet.size)
// Output:
// 0

// Add some values
mySet.add('Earth')
mySet.add('Mars')
mySet.add('Jupiter')

// Log the size of "mySet" again
console.log(mySet.size)
// Output:
// 3
```

## Sets, keys and values

If you want to find out what values a set contains, there are two methods you can use. Well, it is one method and one alias for the same method. The method is `values()` and the alias is `keys()`. Using any of these methods will create an [iterator] object. This iterator contains all values in the order in which you added them to the set.

When you have this iterator you can iterate over all values one by one. If you are not familiar with iterators and generators. When you work with iterator object, you can go to the next value by calling the `next()` method. You call this method on the iterator object you created.

```JavaScript
// Create new set
const mySet = new Set()

// Add some values
mySet.add('Loki')
mySet.add('Thor')
mySet.add('Freyr')

// Create an iterator object that contains all values
const mySetValues = mySet.values()

// Alternative:
// const mySetValues = mySet.keys()

// Log the value of "mySetValues"
console.log(mySetValues)
// Output:
// [Set Iterator] { 'Loki', 'Thor', 'Freyr' }

// Log the first value
console.log(mySetValues.next().value)
// 'Loki'

// Log the second value
console.log(mySetValues.next().value)
// 'Thor'

// Log the third value
console.log(mySetValues.next().value)
// 'Freyr'

// Log the fourth value
// There are only three values in the set
// that's why the "value" is now "undefined"
console.log(mySetValues.next().value)
// Output:
// undefined
```

### Looping over values with for...of loop

If you don't want use the `next()` method to get the values, you can use [for...of loop] instead. The `for...of` loop will help you to loop over the iterator object and get all values one by one automatically.

```JavaScript
// Create new set
const mySet = new Set()

// Add some values
mySet.add('Loki')
mySet.add('Thor')
mySet.add('Freyr')

// Create an iterator object that contains all values
const mySetValues = mySet.values()

// Loop over the "mySetValues" iterator object
// and log all values one by one
for (const val of mySetValues) {
  console.log(val)
}

// Output:
// 'Loki'
// 'Thor'
// 'Freyr'
```

## Getting all entries in a set

Aside to the `values()` and `keys()` methods, you can also access all values inside a set with `entries()` method. Similarly to `values()` and `keys()`, this method also creates an iterator object containing all entries. You can then iterate over this object using either `next()` method or `for...of` loop.

```JavaScript
// Create new set
const mySet = new Set()

// Add some values
mySet.add('MSFT')
mySet.add('AAPL')
mySet.add('BABA')
mySet.add('ADBE')
mySet.add('DELL')

// Create an iterator object that contains all entries (values)
const mySetEntries = mySet.entries()

// Loop over the "mySetValues" iterator object
// and log all values one by one
for (const entry of mySetEntries) {
  console.log(entry)
}

// Output:
// [ 'MSFT', 'MSFT' ]
// [ 'AAPL', 'AAPL' ]
// [ 'BABA', 'BABA' ]
// [ 'ADBE', 'ADBE' ]
// [ 'DELL', 'DELL' ]


// Or using next() method
// Log the first value
console.log(mySetEntries.next().value)
// Output:
// [ 'MSFT', 'MSFT' ]

// Log the second value
console.log(mySetEntries.next().value)
// Output:
// [ 'AAPL', 'AAPL' ]

// Log the third value
console.log(mySetEntries.next().value)
// Output:
// [ 'BABA', 'BABA' ]

// Log the fourth value
console.log(mySetEntries.next().value)
// Output:
// [ 'ADBE', 'ADBE' ]
```

When you use the `entries()` method the format for each entry will be `[ key, value ]`. What may surprise you is that the `key` and `value` in this entry array will be the same. You could see this on the example above. Don't worry about this. This is how the `entries()` method was implemented in JavaScript.

## Iterating over sets with forEach()

The `for...in` loop is not the only way to iterate over a set. You can also use `forEach()` method. This might be even easier and faster than using `for...in` loop.

```JavaScript
// Create new set
const mySet = new Set(['JavaScript', 'Python', 'Ruby', 'Perl'])

// Use forEach() to iterate over "mySet"
// and log all existing values
mySet.forEach(val => {
  console.log(val)
})
// Output:
// 'JavaScript'
// 'Python'
// 'Ruby'
// 'Perl'
```

## Conclusion: Introduction to sets in JavaScript

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
[iterator]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Iterators_and_Generators
[for...of loop]: https://blog.alexdevero.com/javascript-loops/#for8230of-loop

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
