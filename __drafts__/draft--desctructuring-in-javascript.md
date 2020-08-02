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

## Object destructuring

## Destructuring objects

## Default values

## Destructuring and rest operator

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
