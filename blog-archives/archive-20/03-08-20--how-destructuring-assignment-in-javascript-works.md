# How Destructuring Assignment in JavaScript Works

Destructuring assignment is one of the features introduced in ES6. It is also one of the most popular features. In this tutorial, you will learn all you need to know about it. You will learn what destructuring is and how it works. You will also learn how to use it, when to use it and what to avoid.<!--more-->
<!--
Table of Contents:
## Introduction to destructuring assignment
## Destructuring arrays
### Skipping values in arrays
### Arrays, destructuring and rest operator
### Swapping values
### Destructuring nested arrays
### Arrays, destructuring and default values
## Destructuring objects
### Destructuring and already declared variables
### Changing variable names
### Objects, destructuring and default values
### Computed property names
### Destructuring nested objects
## Conclusion: How destructuring assignment in JavaScript works
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

// Use destructuring to assign first three values from "myArray" to new variables
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

Destructuring allows you to assign value that doesn't exist in the array. For example, you can use it to assign four variables even though the array contains only two items. In that case, first two items will be assigned values from the array. The remaining two will end up being assigned `undefined`.

```JavaScript
// Create an array
const myArray = ['Joe', 'Victoria']

// Use destructuring to declare and assign new variables
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
['Java', 'Python', 'Perl', 'Ruby']
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

Another interesting thing you can do with destructuring is swapping values of variables. Put another way, you can declare two variables and assign them some values. Then, you can use destructuring to swap those values. Here is how to do this.

On the left-hand side of the assignment, you will put the variables (their names) you want to swap. On the right-hand side, you will put the same variables (their names) in the new order you want.

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
['Swift', 'JavaScript', 'Python']
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

### Arrays, destructuring and default values

When you try to extract value that doesn't exist in an array it the value you will get is `undefined`. For example, if you try to extract value of third item from an array that contains only two items. You can avoid this. You can provide default value for every variable you want to assign with destructuring.

If any variable doesn't find a match in the array, item on specific index, the default value will be assigned to it. You can specify default value by adding equal sign and some value after the variable name. This way, you can specify default values for any variable you want.

```JavaScript
// Create an array
const myArray = ['Jack', 'Joe']

// Use destructuring to declare and assign new variables
// Set default value of "myVarThree" to 'Anonymous'
let [myVarOne, myVarTwo, myVarThree = 'Anonymous'] = myArray

console.log(myVarOne)
// Output:
'Jack'

console.log(myVarTwo)
// Output:
'Joe'

console.log(myVarThree)
// Output:
'Anonymous'
```

## Destructuring objects

When it comes to destructuring objects there are some differences. The first difference is that you have to use curly brackets instead of square brackets. The second difference is that the order of variable you want to assign doesn't matter. The reason is that, with object, destructuring works a bit differently.

When you work with objects, JavaScript doesn't care about some order. It doesn't use it. Instead, it uses object properties. This is the third difference. You don't use random variable names to assign values from an object. Instead, you use names of existing properties to get values of those properties.

If you want to extract the value of property "name" you have to use variable "name". This tells JavaScript what property it should look for. So, order no longer matters, but the variable name does.

```JavaScript
// Create an object
const myObj = {
  name: 'Stuart',
  age: 37,
  sex: 'male'
}

// Use destructuring to assign values of "sex" and "name" to new variables
// Notice that the order of variable names doesn't matter
// What matters is that "sex" variable name matches "sex" property in myObj
// and "name" variable name matches "name" property in myObj
// try also to assign value from non-existing property "education"
const { sex, name, education } = myObj

// ^ is alternative to:
// const sex = myObj.sex
// const name = myObj.name

console.log(name)
// Output:
'Stuart'

console.log(sex)
// Output:
'male'

console.log(education)
// Output:
undefined
```

You can also use destructuring to assign values from objects that have not been declared.

```JavaScript
// Use destructuring to assign values from objects that have not been declared.
const { firstName, lastName } = {
  firstName: 'Sam',
  lastName: 'Mendez',
  age: 26
}

console.log(firstName)
// Output:
'Sam'

console.log(lastName)
// Output:
'Mendez'
```

### Destructuring and already declared variables

Arrays allow you to declare empty variables first and use destructuring to assign them values later. You can do the same also with objects. However, there is catch. You have to wrap the whole assignment with parentheses (`()`). Otherwise, JavaScript will think that the `{}` is a block.

```JavaScript
// Create an object
const myObj = {
  name: 'Fat Tony',
  nationality: 'Italian'
}

// Declare empty variable for "name" and "nationality"
let name, nationality

// This will NOT work:
{ name, nationality } = myObj
// SyntaxError: Unexpected token

// This will work (wrapping the whole assignment with ()):
({ name, nationality } = myObj)

console.log(name)
// Output:
'Fat Tony'

console.log(nationality)
// Output:
'Italian'
```

### Changing variable names

JavaScript uses property names to understand what value do you want to extract from an object. Fortunately, there is a way to change the variable name you want the value to be assigned to. What you have to do is to add colons (`:`) and new variable name right after the original variable name. Then, you can use that new name to access that value.

```JavaScript
// Create an object
const myObj = {
  name: 'John Doer',
  education: 'College',
  born: 1973
}

// Use destructuring to extract values of "education" and "born"
// and assign "education" to variable "highestEducation"
// and "born" to "dateOfBirth"
const { education: highestEducation, born: dateOfBirth } = myObj

// ^ is alternative to
// const highestEducation = myObj.education
// const dateOfBirth = myObj.born

console.log(highestEducation)
// Output:
'College'

console.log(dateOfBirth)
// Output:
1973
```

### Objects, destructuring and default values

Just like with arrays, you can also set default values when you use destructuring with objects. The syntax is the same.

```JavaScript
// Create an object
const myObj = {
  name: 'Jack',
  country: 'New Zealand'
}

// Use destructuring to extract values of "name" and "age"
// if "age" doesn't exist, use 0 as a fallback
const { name, age = 0 } = myObj

console.log(name)
// Output:
'Jack'

console.log(age)
// Output:
30


// Without default value:
const myObj = {
  name: 'Jack',
  country: 'New Zealand'
}

const { name, age } = myObj

console.log(name)
// Output:
'Jack'

console.log(age)
// Output:
undefined
```

### Computed property names

When it comes to destructuring and objects, you can also define property which value you want extract using computed property name. For example, you can use value of a variable to specify property you are looking for. When you want to use computed property name you have to wrap it with square brackets.

When you use computed property name you also have to specify a variable name. You do this in the same way as when you want to change variable name. First, you use the computed property in square brackets. After that, you add colons and specify the variable name. Later, you can use the variable name to access the extracted value.

```JavaScript
// Declare variable and assign it a property name
// This variable will be later used to extract the value
// of an object property that matches the value
// assigned to this variable, that is "nationality" property
const myProp = 'nationality'

// Create an object
const myObj = {
  name: 'Samantha',
  nationality: 'German'
}

// Use computed property name to extract value of "nationality" property
// Then, assign the extracted value to new variable "country"
const { [myProp]: country } = myObj

console.log(country)
// Output:
'German'
```

### Destructuring nested objects

Similarly to nested arrays, you can also use destructuring with nested objects. Also like with arrays, if you want to extract data from nested objects you have to follow the structure of the original object.

```JavaScript
// Create nested object
const myObj = {
  name: 'Jackie',
  address: {
    state: 'USA',
    city: 'NY'
  },
  employment: {
    job: 'manager',
    title: 'CTO'
  }
}

// Use destructuring to extract "name", "state" from "address" object and "title" from "employment" object
const { name, address: { state }, employment: { title } } = myObj

console.log(name)
// Output:
'Jackie'

console.log(state)
// Output:
'USA'

console.log(title)
// Output:
'CTO'
```

You can also change variable names when you extract data from nested objects.

```JavaScript
// Create nested object
const myObj = {
  name: 'Jackie',
  address: {
    state: 'USA',
    city: 'NY'
  },
  employment: {
    job: 'manager',
    title: 'CTO'
  }
}

// Use destructuring to extract "state" and "title"
// and rename variable for "state" to "place"
// and variable for "title" to "position"
const { address: { state: place }, employment: { title: position } } = myObj

console.log(place)
// Output:
'USA'

console.log(position)
// Output:
'CTO'
```

## Conclusion: How destructuring assignment in JavaScript works

Destructuring assignment is one of the features hat can help you do more with less code. I hope this tutorial helped you understand what destructuring assignment is, how it works and how to use it. By now, you should know how to use destructuring with arrays and objects, and what are some gotchas and mistakes to avoid.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[primitive data types]: https://blog.alexdevero.com/javascript-basics-data-types-pt1/
[objects]: https://blog.alexdevero.com/javascript-objects-pt1/
[arrays]: https://developer.mozilla.org/en-US/docs/Glossary/array
[type of variable]: https://blog.alexdevero.com/javascript-variables-introduction/
[rest operator]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax

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
