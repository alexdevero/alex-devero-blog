# How Destructuring Assignment in JavaScript Works

Destructuring assignment is one of the features introduced in ES6. It is also ne of the most popular feature. In this tutorial, you will learn all you need to know about it. You will learn what destructuring is and how it works. You will also learn how to use it, when to use it and what to avoid.

<!--more-->
<!--
Table of Contents:
-->

## Introduction to destructuring assignment

What is destructuring? Destructuring is a way to extract values from data and assign those values to one or more variables. One thing to remember about destructuring is that it works only with [arrays] and [objects]. You can't use it with [primitive data types]. Now, a bit about how it works.

In general, there are two ways to use deconstructing. First, you can use it to assign a value to a variable when you declare it. Second, you can declare an empty variable and use destructuring later to assign it a value. Both methods will work. When you want to use the later, pay attention to the [type of variable] you use.

The syntax of destructuring assignment is very simple. If you are declaring a variable the variable keyword comes first. So, either `let`, `const` or `var`. Next comes the destructuring assignment, followed by equal sign. The array or object with data you want to extract is on the right-hand side.

Unlike other JavaScript features, destructuring assignment has two types of syntax. Which type you have to use depends on the data you are working with. If you work with an array destructuring you will use square brackets `[]`. If you work with an object, you will use curly brackets `{}`.

This is the general idea of how destructuring assignment works. Now, let's take a look at each type of syntax in detail.

```JavaScript
// Destructuring assignment syntax for an array
// The [] is the destructuring assignment
const [ /* variable name(s) */ ] = []

// Destructuring assignment syntax for an array
// The {} is the destructuring assignment
const { /* property name(s) */ } = {}
```

## Destructuring arrays

When you want to use destructuring with arrays you have to do two things. First, you have to use syntax with square brackets `[]`. Second, inside these square brackets, you specify the variable name(s) you want to use. When you specify the variables names, make sure you write them in the right order.

The way destructuring with arrays works is that values will be assigned to the variables in the order you write them. So, first variable will be assigned item on index 0, second on index 1, third on index 3 and so on. If you want the order to be different, you have to either change the order variable names or the order of items inside the array.

```JavaScript
// Create an array
const myArray = [1, 2, 3, 4, 5]

// Use destructuring to assign first three values from "myArray"
// The "itemOne", "itemTwo", "itemThree" will create
// three new variables "itemOne", "itemTwo", "itemThree"
const [ itemOne, itemTwo, itemThree ] = myArray

// ^ is the same as:
// const itemOne = myArray[0]
// const itemTwo = myArray[1]
// const itemThree = myArray[2]

console.log(itemOne)
// Output:
1

console.log(itemTwo)
// Output:
2

console.log(itemThree)
// Output:
3


// Using different order
const [ itemThree, itemOne, itemTwo ] = myArray

console.log(itemOne)
// Output:
1

console.log(itemTwo)
// Output:
2

console.log(itemThree)
// Output:
3
```

As I mentioned, destructuring also works when you want to declare variables and assign the later. In this case, you don't use the variable keyword again when you use destructuring to assign values.

```JavaScript
// Create an array
const myArray = [0, 1, 2]

// Declare empty variables
let myVarOne, myVarTwo, myVarThree

// Assign variables later
[myVarOne, myVarTwo, myVarThree, myVarFour] = myArray

console.log(myVarOne)
// Output:
2

console.log(myVarTwo)
// Output:
3

console.log(myVarThree)
// Output:
1
```

Destructuring allows you to assign value that doesn't exist in the array. For example, you can use it to assign 4 variables even though the array contains only two items. In that case, first two items will be assigned values from the array. The remaining two will end up being assigned `undefined`.

```JavaScript
// Create an array
const myArray = ['Joe', 'Victoria']

// Declare empty variables
let [myVarOne, myVarTwo, myVarThree, myVarFour] = myArray

console.log(myVarOne)
// Output:
'Joe'

console.log(myVarTwo)
// Output:
'Victoria'

console.log(myVarThree)
// Output:
undefined

console.log(myVarFour)
// Output:
undefined
```

### Skipping values in arrays

You can change the order of values being assigned by changing the order of variable names. With arrays, you can also skip values. This allows you to assign only some values from an array and skip those you don't care about. You can do this by leaving the place for variable name in a specific position empty.

```JavaScript
// Create an array
const myArr = ['JavaScript', 'Perl', 'C', 'Java', 'Python']

// Example no.1:
// Assign only values on 0th, 2nd, and 4th index
// Notice the empty spaces in place of 1st and 3rd index
// [firstLang, /* 1st index - leave empty */, thirdLang, /* 3rd index - leave empty */, fifthLang]
const [firstLang, , thirdLang, , fifthLang] = myArr

console.log(firstLang)
// Output:
'JavaScript'

console.log(thirdLang)
// Output:
'C'

console.log(fifthLang)
// Output:
'Python'


// Example no.2:
// Assign only values on 1st and 4th index
const [, firstItem, , fourthItem] = myArr

console.log(firstItem)
// Output:
'Perl'

console.log(fourthItem)
// Output:
'Java'
```

### Arrays, destructuring and rest operator

You know how to use destructuring assignment to assign individual values and also how to skip some. Another thing you can do when you use destructuring with arrays is to use [rest operator]. You can assign individual items to some variables. Then, you can assign any remaining items to another variable.

```JavaScript
// Create an array
const myArr = ['JavaScript', 'C', 'Java', 'Python', 'Perl', 'Ruby']

// Assign th first two languages to two variables
// then use rest operator to assign remaining languages to third variable
const [langOne, langTwo, ...remainingLangs] = myArr

console.log(langOne)
// Output:
'JavaScript'

console.log(langTwo)
// Output:
'C'

console.log(remainingLangs)
// Output:
[ 'Java', 'Python', 'Perl', 'Ruby' ]
```

When you try to use rest operator and there are no remaining values the result will be an empty array.

```JavaScript
// Create an array
const myArr = ['JavaScript', 'Python']

// Assign th first two languages to two variables
// then use rest operator to assign remaining languages to third variable
const [langOne, langTwo, ...remainingLangs] = myArr

console.log(langOne)
// Output:
'JavaScript'

console.log(langTwo)
// Output:
'Python'

console.log(remainingLangs)
// Output:
[]
```

One thing about using rest operator. When you want to use it, make sure to use it as the last. Any variables or empty spots for skipped values must come before it.

```JavaScript
// Don't do
const myArray = [1, 2, 3, 4]

const [...remainingArray, elOne, , elThree] = myArray

// Output:
// SyntaxError: Rest element must be last element

// Do
const myArray = [1, 2, 3, 4]

const [elOne, , elThree, ...remainingArray] = myArray

console.log(elOne)
// Output:
1

console.log(elThree)
// Output:
3

console.log(remainingArray)
// Output:
[4]
```

### Swapping values

Another interesting thing you can do with destructuring is swapping values of variables. Put another way, you can declare two variables and assign them some values. Then, you can use destructuring to swap those values.

Here is how to do this. On the left-hand side of the assignment, you will put the variables (their names) you want to swap. On the right-hand side, you will put the same variables (their names) in the new order you want.

```JavaScript
// Declare and assign two variables
let a = 'I am A.'
let b = 'I am B.'; // Note: semicolon here is necessary to avoid referenceError 'I am B.'[a, b]

// se destructuring to swap values of "a" and "b"
[a, b] = [b, a]

console.log(a)
// Output:
'I am B.'

console.log(b)
// Output:
'I am A.'
```

You can use destructuring also to quickly swap values in an array itself. In this case, you will replace variable names with specific indexes.

```JavaScript
// Create an array
const myArray = ['JavaScript', 'Python', 'Swift'];

// Swap items in "myArray" array
// Put the first item (0th index) on the 2nd index
// Put the second item (1st index) on the the 0th index
// Put the third item (2nd index) on the the 1st index
[myArray[0], myArray[1], myArray[2]] = [myArray[2], myArray[0], myArray[1]]

console.log(myArray)
// Output:
[ 'Swift', 'JavaScript', 'Python' ]
```

### Destructuring nested arrays

Destructuring also works with nested arrays. This allows you to extract data from an array even if the array itself is not on the top-level. One thing to remember. When you want to use destructuring to get some value from nested array, you have to follow the structure of the original array.

This also includes using additional square brackets to wrap the variable you want to assign. This will tell JavaScript you are interested in an item in nested array.

```JavaScript
// Create an array
const myArray = ['JavaScript', ['Python', 'Swift']]

// Use deconstruction to extract the first item
// of the nested array
// empty space - ignore the first item in the array
// use additional square brackets to "enter" the nested array
// use empty space to ignore the first nested item
const [, [, swiftLang]] = myArray

console.log(swiftLang)
// Output:
'Swift'

// More extreme example
const myArray = ['JavaScript', ['Python', 'Ruby', ['Swift', 'C++', ['Assembly', 'C']]]];

// Use deconstruction to extract the first item
// of the nested array nested on the fourth level
// empty space - ignore the first item
// first pair of brackets - enter the first nested array
// two empty spaces - ignore the first two items
// second pair of brackets - enter the second nested array
// two empty spaces - ignore the first two items
// third pair of brackets - enter the third nested array
// access the value on the 0th index
const [, [, , [, , [myLang]]]] = myArray

console.log(myLang)
// Output:
'Assembly'
```

## Destructuring objects

## Skipping values in arrays

## Swapping values



## Conclusion: How destructuring assignment in JavaScript works

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
- https://medium.com/javascript-in-plain-english/everything-you-need-to-know-about-destructuring-in-javascript-5e9fde6e86ff
-->