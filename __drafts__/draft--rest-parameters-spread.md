# How JavaScript Spread Operator and Rest Parameters Work

Rest Parameters and Spread Operator are two quite popular features introduced in ES6. Thi tutorial will help you understand them. You will learn what rest parameters and spread operator are and how they work. You will also learn how to use them in the right way.

<!--more-->
<!--
Table of Contents:
-->

## Spread Operator

The spread operator is a feature that allows you to access content of an iterable object. Iterable object is an object, or data structure, that allows to access its content with [for...of] loop. The most popular example of an iterable is an array. Another example of an iterable can be objects literals or [strings].

When you wanted to access all content an some iterable before spread operator you had to use some kind of a loop, such as the mentioned `for...of` loop, or method, such as [forEach()]. Another option were indexes. Spread Operator allows you to do this much faster and with much less code. About the syntax.

The syntax of spread operator is simple and easy to remember. It consists of three dots (`...`). These three dots are followed by the iterable (`...someIterable`), whose content you want to access.

```JavaScript
// Create array
const myArray = ['Venus', 'Ares', 'Mars']

// Use spread operator to access content of "myArray" variable
// Syntax: ...someIterable
console.log(...myArray)
// Output:
// 'Venus' 'Ares' 'Mars'
```

### Spread operator and objects

When you want to use spread operator with objects the syntax is the same. You will use those three dots, but now followed by the name of the object whose content you want to access. The result you will get will be the content, only without the surrounding curly braces.

```JavaScript
// Create object
const myObj = {
  firstName: 'Sam',
  lastName: 'Dodge'
}

// Use spread operator to access content of "myObj" variable
// Note: the {} around ...myObj are to avoid TypeError
// console.log(...myObj) would not work
console.log({ ...myObj })
// Output:
// { firstName: 'Sam', lastName: 'Dodge' }
```

## Duplicating iterables with spread operator

The spread operator allows to quickly access content of an iterable. This can be useful when you want to copy iterable objects. You may not know this, but copying objects can be tricky. When you try to copy some [primitive], like a number or a string, you will create a real copy, or clone. This is called [deep copy].

### Deep and shallow copies

This is not true for objects, including iterables. When you try to copy an object, such as array, you will not create a real copy. What will happen instead is that JavaScript will create new reference for that object. You can think about this as creating new alias or name.

When you copy an object, you only create new alias for it. As a result, you have two names for that thing, that object. However, there is still only one object, not two. This also means that if you do something with the object using the second alias (reference), those changes will also have effect on the first alias.

Remember, there is still only one objects, but two references (aliases) to access it. This type of copy is called [shallow copy] and this type of copying is called [copying by reference].

```JavaScript
// Create an array
const myArray = ['Spread', 'Rest', 'JavaScript']

// Create shallow copy of "myArray" variable
const myShallowCopy = myArray

// Log the content of "myArray"
console.log(myArray)
// Output:
// [ 'Spread', 'Rest', 'JavaScript' ]

// Log the content of "myShallowCopy"
console.log(myShallowCopy)
// Output:
// [ 'Spread', 'Rest', 'JavaScript' ]

// Remove the last item from the original array ("myArray")
myArray.pop()

// Log the content of "myArray" again
// The last item is gone as it should
console.log(myArray)
// Output:
// [ 'Spread', 'Rest' ]

// Log the content of "myShallowCopy" again
// The change of "myArray" will also appear in "myShallowCopy"
// The last item is also gone
console.log(myShallowCopy)
// Output:
// [ 'Spread', 'Rest' ]
```

### Deep copies with spread operator

This is how copying in JavaScript works automatically. The good news is that spread operator allows you to overcome this issue with shallow copies. It allows you to quickly create deep copies of iterables. So, no more worries about changes happening in unexpected places.

Creating a real, deep, copy of some iterable with spread operator is simple. First, create a variable and assign it some iterable, some array. This will be the iterable you will copy. Second, create new variable. To assign this new variable a copy of the first you will use the spread operator followed by the name of first variable, wrapped with square brackets.

The spread operator will access the content and basically strip away the square brackets of the original array. So, in order to re-create the array, you will wrap the content in new pair of square brackets. That's it. You have a new deep copy of the first iterable, in this case the original array.

If you decide to change the original array, or the copy, that change will have effect only for that specific array.

```JavaScript
// Create the original array
const myArray = ['Spread', 'Rest', 'JavaScript']

// Use spread operator to create deep copy of "myArray""
const myDeepCopy = [...myArray]

// Log the content of "myArray"
console.log(myArray)
// Output:
// [ 'Spread', 'Rest', 'JavaScript' ]

// Log the content of "myDeepCopy"
console.log(myDeepCopy)
// Output:
// [ 'Spread', 'Rest', 'JavaScript' ]

// Remove the last item from the original array "myArray"
myArray.pop()

// Log the content of "myArray" again
// The last item is gone as it should
console.log(myArray)
// Output:
// [ 'Spread', 'Rest' ]

// Log the content of "myDeepCopy" again
// The "myDeepCopy" is not affected by change made to "myArray"
// The last item is still there as it should
console.log(myDeepCopy)
// Output:
// [ 'Spread', 'Rest', 'JavaScript' ]
```

### Deep copies of objects with spread operator

Just like you can create deep copies of arrays you can also create deep copies of objects. The syntax is almost the same. You have to use those three dots followed by the name of the object you want to copy. You will assign this into a new variable. Just make sure to wrap this whole thing in curly brackets, not square.

```JavaScript
// Create the original array
const myObj = {
  title: 'Guards! Guards!',
  author: 'Terry Pratchett',
}

// Use spread operator to create deep copy of "myObj""
const myDeepCopy = { ...myObj }

// Log the content of "myObj"
console.log(myObj)
// Output:
// { title: 'Guards! Guards!', author: 'Terry Pratchett' }

// Log the content of "myDeepCopy"
console.log(myDeepCopy)
// Output:
// { title: 'Guards! Guards!', author: 'Terry Pratchett' }

// Add new property the original object "myObj"
myObj.format = 'Hardcover'

// Log the content of "myObj" again
// New property is there
console.log(myObj)
// Output:
// {
//   title: 'Guards! Guards!',
//   author: 'Terry Pratchett',
//   format: 'Hardcover'
// }

// Log the content of "myDeepCopy" again
// The "myDeepCopy" still contains only two properties
console.log(myDeepCopy)
// Output:
// { title: 'Guards! Guards!', author: 'Terry Pratchett' }
```

## Merging with spread operator

Another thing you can do with spread operator is merging two or more iterables. Previously, when you wanted to merge two or more arrays for example you would have to use some method such as `concat()`. Spread operator allows you to do this just as fast, if not faster, with easier syntax.

The process is similar to copying existing array. You create new array. Next, you use the spread operator along with the names of first array you want to merge. This array will be followed by comma and another spread followed by name of the second array. Finally, you will also wrap this inside a pair square brackets.

The result you will get will be all items from the arrays you wanted to merge inside a single array.

```JavaScript
// Create first array
const arrayOne = [1, 2, 3]

// Create second array
const arrayTwo = ['four', 'five', 'six']

// Merge first and second array using spread operator
// Syntax: [...arrayOne, ...arrayTwo, ...arrayThree, etc.]
const arrayMerged = [...arrayOne, ...arrayTwo]

// Log the content of "arrayMerged"
console.log(arrayMerged)
// Output:
// [ 1, 2, 3, 'four', 'five', 'six' ]
```

## Rest Parameters

## Conclusion: [...] ...

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[for...of]: https://blog.alexdevero.com/javascript-loops/#for8230of-loop
[strings]: https://blog.alexdevero.com/javascript-basics-data-types-pt1/#strings
[forEach()]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach
[primitive]: https://blog.alexdevero.com/javascript-basics-data-types-pt1/
[deep copy]: https://blog.alexdevero.com/shallow-deep-copy-in-javascript/#deep-copy
[shallow copy]: https://blog.alexdevero.com/shallow-deep-copy-in-javascript/#shallow-copy
[copying by reference]: https://blog.alexdevero.com/shallow-deep-copy-in-javascript/#by-value-and-by-reference

<!--
### Meta:
-
-->

<!--
### Keywords:
- spread operator
- rest parameters
-->

<!--
### Resources:
- https://javascript.info/rest-parameters-spread
-->
