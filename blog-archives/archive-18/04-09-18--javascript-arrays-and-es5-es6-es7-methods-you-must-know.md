# JavaScript Arrays and ES5, ES6 & ES7 Methods You Must Know

How often do you work with JavaScript arrays? There has been a lot of talk about ES5, ES6 and ES7. Yet, it almost seems like there is nothing new about arrays to talk about. That is not true. This article will show you that arrays still have a lot to show. Learn about the 14 new and interesting array methods. Make your work with arrays fresh and fun again.

<!--
Table of Contents:
## A quick preparation
## find()
## filter()
## map()
## reduce()
## forEach()
## some()
## every()
## includes()
## Array.from()
## Array.of()
## findIndex()
## fill()
## values()
## keys()
## Epilogue: JavaScript Arrays
-->

## A quick preparation

Before we start, let's create a few arrays and store them in variables. We can then work with these variables throughout this tutorials. This will help us avoid repetitive code and make our work faster. So, let's create three arrays. The first array will contain numbers, the second words and the last one will contain objects. With that, we can start playing with arrays.

```
// Create array of numbers.
let arrOfNumbers = [53, 14, 85, 66, 67, 108, 99, 10]

// Create array of words.
let arrOfWords = ['mathematics', 'physics', 'philosophy', 'computer science', 'engineering', 'biology', 'nano technology']

// Create array of objects.
let arrOfObjects = [
  {
    name: 'Aristotle',
    living: false
  },
  {
    name: 'Al-Khwarizmi',
    living: false
  },
  {
    name: 'Leonardo da Vinci',
    living: false
  },
  {
    name: 'Sir Isaac Newton',
    living: false
  },
  {
    name: 'Bertrand Russell',
    living: false
  },
  {
    name: 'Herbert Simon',
    living: false
  },
  {
    name: 'John von Neumann',
    living: false
  },
  {
    name: 'Franklin Story Musgrave',
    living: true
  },
  {
    name: 'Hamlet Isakhanli',
    living: true
  }
]
```

## find()

The `find` method lets you iterate through an array and executes specific function you pass as a callback. It executes this function immediately when the first element causes the callback function to return true. After that, the return statement is called and value is returned, the `find` method is interrupted. This means that `find` will find only the first element that matches the condition and causes the callback function to fire.

```
// Find the first even number and store it inside a variable.
let firstEvenNumber = arrOfNumbers.find((number) => number % 2 !== 1)

// Find the first odd number and store it inside a variable.
let firstOddNumber = arrOfNumbers.find((number) => number % 2 === 1)

// Find the first number bigger than 5 and store it inside a variable.
let firstNumberBiggerThanFiftyFive = arrOfNumbers.find((number) => number > 55)

// Find the first number smaller than 1 and store it inside a variable
let firstNumberSmallerThanOne = arrOfNumbers.find((number) => number < 1)

// Find the first living person.
let firstLivingPerson = arrOfObjects.find((person) => person.living)

// Log firstEvenNumber, firstNumberBiggerThanFiftyFive, firstNumberSmallerThanOne variables in console.
console.log(firstEvenNumber) // 14

console.log(firstOddNumber) // 53

console.log(firstNumberBiggerThanFiftyFive) // 85

console.log(firstNumberSmallerThanOne) // returns nothing

// Log first living person from the array object.
console.log(firstLivingPerson) // { living: true, name: 'Franklin Story Musgrave' }
```

## filter()

The `filter` method allows us to iterate through an array and return all items or elements that fit the condition you provided through the callback function.

```
// Create an array with all even numbers from arrOfNumbers.
let evenNumbers = arrOfNumbers.filter((number) => number % 2 !== 1)

// Create an array with all odd numbers from arrOfNumbers.
let oddNumbers = arrOfNumbers.filter((number) => number % 2 === 1)

// Create an array with all living people from arrOfObjects.
let livingPeople = arrOfObjects.filter((person) => person.living)

// Create an array with all dead people from arrOfObjects.
let livingPeople = arrOfObjects.filter((person) => !person.living)

// Log results.
console.log(evenNumbers) // [14, 66, 108, 10]

console.log(oddNumbers) // [53, 85, 67, 99]

console.log(livingPeople) // { living: true, name: "Franklin Story Musgrave" }, { living: true, name: "Hamlet Isakhanli" }

console.log((deadPeople)) // { living: false, name: "Aristotle" }, { living:  false, name: "Al-Khwarizmi" }, { living: false, name: "Leonardo da Vinci" }, { living: false, name: "Sir Isaac Newton" }, { living: false, name: "Bertrand Russell" }, { living: false, name: "Herbert Simon" }, { living: false, name: "John von Neumann" }
```

## map()

the `map` method works in a similar way as `filter`. It also allows us to iterate through an array. However, `map` gives is much more universal than `filter`. When you use `map` you can do whatever you want with the content of array, its items.

```
// Create an array with modulus of 4 for all numbers.
let modulus = arrOfNumbers.map(number => number % 4)

// Log the result.
console.log(modulus) // [1, 2, 1, 2, 3, 0, 3, 2]

// Create an array with all subjects to learn.
let toLearn = arrOfWords.map((word) => `I have to learn: ${word}`)

// Log the result.
console.log(toLearn) // ["I have to learn mathematics", "I have to learn physics", "I have to learn philosophy", "I have to learn computer science", "I have to learn engineering", "I have to learn biology", "I have to learn nano technology"]

// Create an array with reversed version of items in arrOfWords.
let reversedWords = arrOfWords.map((word) => word.split('').reverse().join(''))

// Log the result.
console.log(reversedWords) // ["scitamehtam", "scisyhp", "yhposolihp", "ecneics retupmoc", "gnireenigne", "ygoloib", "ygolonhcet onan"]

```

## reduce()

The `reduce` method works with two parameters, `accumulator` and `currentValue`. Well, it uses four parameters, but two are optional. It then returns a single value based on a reducer function you provided as a callback. About the parameters. The `accumulator` stores the previous value returned by reducer function. The `currentValue` stores the value of item of current iteration.

In other words, imagine that you have an array with five items. And, the reducer is currently passing the fourth item. In this case, the `accumulator` stores a single value of the item one to three. For example addition of these items. The `currentValue` stores the value of the fourth item, executing the reducer function you provided as a callback.

This method can be useful if you have an array, or arrays, and want to do some quick mathematical operations with all its items, such as adding, subtracting, multiplying, dividing, etc.

```
// Create an array with total sum of all numbers in arrOfNumbers.
let sumTotal = arrOfNumbers.reduce((accumulator, currentValue) => accumulator + currentValue)

// Log the result.
console.log(sumTotal) // 502

// Create another array but now subtract all numbers in arrOfNumbers.
let subtract = arrOfNumbers.reduce((accumulator, currentValue) => accumulator - currentValue)

// Log the result.
console.log(subtract) // -396
```

## forEach()

The `forEach` works in a very simple way. It executes a callback you provided for each and every item in the array. `forEach` is one of my favorites. I use it as a replacement for the good old `for` loop, especially with combination with `querySelectorAll`.

```
// Get all buttons on the website.
let buttons = document.querySelectorAll('button')

// Create a simple function for handling clicks.
let handleClick = (e) => {
  e.preventDefault()

  ... do something ...

  console.log(`Button with id ${e.currentTarget.id} has been clicked.`)
}

// Add event listener to all buttons.
buttons.forEach((button) => {
  button.addEventListener('click', handleClick)
})

// Create new empty array.
let randoms = []

// Iterate over arrOfNumbers array, increase every value by adding a random number and push it to new randoms array.
arrOfNumbers.forEach((number) => {
  randoms.push(number + Math.floor(Math.random() * 10))
})

// Log the result.
console.log(randoms) // [56, 23, 93, 74, 67, 109, 101, 17] (well, maybe)
```

## some()

The `some` checks if at least one of the items in the array you provided match a condition you specified in a callback function. What if you use `some` with an empty array? `some` will simply return `false`.

```
// Is any number in arrOfNumbers array even?
console.log(arrOfNumbers.some((number) => number % 2 === 0)) // true

// Does the arrOfWords contains word 'mathematics'?
console.log(arrOfWords.some((word) => word === 'mathematics')) // true

// Is any person in arrOfObjects array still alive?
console.log(arrOfObjects.some((person) => person.living)) // true

// Is any person in arrOfObjects array dead?
console.log(arrOfObjects.some((person) => !person.living)) // true

// Test an empty array.
console.log([].some((item) => item % 2 === 0)) // false
```

## every()

`every` works in somewhat a similar fashion as `some`. The difference is that all items in an array, or arrays, has to pass the condition you set via callback function. When this is true, `every` will also return `true`. What about an empty array? This is interesting. When you use `some` on an empty array it will actually return `true`.

```
// Are all items in arrOfNumbers array numbers?
console.log(arrOfNumbers.every((number) => typeof number === 'number')) // true

// Are all items in arrOfWords array strings?
console.log(arrOfWords.every((subject) => typeof subject === 'string')) // true


// Are all items in arrOfWords array strings?
console.log(arrOfWords.every((subject) => typeof subject === 'string')) // true

// Are all items in arrOfWords array objects?
console.log(arrOfObjects.every((person) => typeof person === 'object')) // true

// Are all persons in arrOfObjects array still alive?
console.log(arrOfObjects.every((person) => person.living)) // false

// Are all persons in arrOfObjects array dead?
console.log(arrOfObjects.every((person) => !person.living)) // false

// Test an empty array.
console.log([].every((item) => item > 0)) // true
```

## includes()

`includes` helps us test if an array, or arrays, contain specific item. As always, it is you who specifies what item are you looking for by specifying the element. One thing to remember, `includes` doesn't work with callback function.

```
// Is one of the numbers in arrOfNumbers array 108?
console.log(arrOfNumbers.includes(108)) // true

// Is one of the subjects in arrOfWords array 'engineering'?
console.log(arrOfWords.includes('engineering')) // true
```

## Array.from()

`from` method allows us to take some iterable object and create a new array from it. One simple example can be a string manipulating with letters and creating a new array from the result. If you think about it, `from` works like a good old `split`, except that `split` is more universal because it allows to specify the condition for splitting.

One interesting thing is that `from` allows us to use arrow functions and, therefore, manipulate with items inside arrays.

```
// Take the fourth item (third index) in arrOfWords and convert it into a new array.
console.log(Array.from(arrOfWords[3]) // ['c', 'o', 'm', 'p', 'u', 't', 'e', 'r', ' ', 's', 'c', 'i', 'e', 'n', 'c', 'e']

// Good old split.
console.log(arrOfWords[3].split('')) // ['c', 'o', 'm', 'p', 'u', 't', 'e', 'r', ' ', 's', 'c', 'i', 'e', 'n', 'c', 'e']

// Take all numbers in arrOfNumbers and double them.
console.log(Array.from(arrOfNumbers, number => number * 2)) // [106, 28, 170, 132, 134, 216, 198, 20]

// Convert all characters of the fourth item (3rd index) in arrOfWords to upper case.
console.log(Array.from(arrOfWords[3], (letter) => letter.toUpperCase())) // ["C", "O", "M", "P", "U", "T", "E", "R", " ", "S", "C", "I", "E", "N", "C", "E"]
```

## Array.of()

The `of` method allows us to create arrays out of the values you specify as arguments when you use it.

```
// Create a new array with '1' as the only item.
console.log(Array.of(1)) // [1]

// Create a new array with '1' as the only item.
console.log(Array.of(1)) // [1]

// Create a new array with 'alpha', 'beta', 'gama', 'delta' as its items.
console.log(Array.of('alpha', 'beta', 'gama', 'delta')) // ['alpha', 'beta', 'gama', 'delta']

// What about undefined or null?
console.log(Array.of(undefined, null)) // [undefined, null]
```

## findIndex()

When you use`findIndex` it will one of two things, depending on the condition you provided via callback function. First, if any item passes your condition it will return its index. Keep in mind that `findIndex` will return only the index of the first item that passes your condition. So, if your array, or arrays, contain duplicates `findIndex` will not return their indexes. And, the second option is that if none of the items passes your condition `findIndex` will return -1.

```
// Find index of the first occurrence of the number 67.
console.log(arrOfNumbers.findIndex((number) => number === 67)) // 4

// Find index of the first occurrence of the number 1024.
console.log(arrOfNumbers.findIndex((number) => number === 1024)) // -1

// Create new array with some duplicit values.
let duplicates = [97, 3, 51, 3, -85, 102, 5, 3]

// Find index of the first occurrence of the number 3.
console.log(duplicates.findIndex((number) => number === 3)) // 1
```

## fill()

`fill` allows us to fill an array with specific values, starting and ending at specific index. You pass the value is the first argument, starting index as the second and ending index as the third. If you omit the starting and ending indexes `fill` will fill the whole array. If you omit just one of the indexes `fill` take the one as starting index and fill the rest of the array.

```
// Replace the second, third and fourth item in arrOfNumbers with 11.
console.log(arrOfNumbers.fill(11, 1, 5)) // [53, 11, 11, 11, 11, 108, 99, 10]

// Omit the starting and ending indexes.
console.log(arrOfNumbers.fill(33)) // [33, 33, 33, 33, 33, 33, 33, 33]

// Omit one of the indexes.
console.log(arrOfNumbers.fill(768, 5)) // [53, 14, 85, 66, 67, 768, 768, 768]
```

## values()

The `values` method is a little bit different from the methods we above. It doesn't return any specific value. Instead, it creates a new `Array Iterator` object. It is this object that contains the values for every index in your array, or arrays. If you want to iterate through this object, you can use the `for...of` statement for example.

If you don't want to get all values at once, but individually you can use `next` method in conjunction with `values`.

```
// Create new Array Iterator object.
let arrIterator = arrOfWords.values()

// Iterate through arrIterator and log every value.
for (let value of arrIterator) {
  console.log(value)
}

// Result:
// 'mathematics'
// 'physics'
// 'philosophy'
// 'computer science'
// 'engineering'
// 'biology'
// 'nano technology'

// Use next() method and value
console.log(arrIterator.next().value) // 'mathematics'
console.log(arrIterator.next().value) // 'physics'
console.log(arrIterator.next().value) // 'philosophy'
```

## keys()

`keys` works almost in the same way as `values`, except that it creates new `Array Iterator` object filled with keys. Let's use the previous example and just replace `arrOfWords.values()` with `arrOfWords.keys()`.

```
// Create new Array Iterator object.
let arrIterator = arrOfWords.keys()

// Iterate through arrIterator and log every key.
for (let key of arrIterator) {
  console.log(key)
}

// Result:
// 0
// 1
// 2
// 3
// 4
// 5
// 6

// Use next() method and value
console.log(arrIterator.next().value) // 0
console.log(arrIterator.next().value) // 1
console.log(arrIterator.next().value) // 2
```

## Epilogue: JavaScript Arrays

Congratulations! You just finished this article about JavaScript ES5, ES6 and ES7 methods you can use with arrays. It is my hope that you enjoyed this article and learned something new. I also hope that this article proved that JavaScript arrays don't belong to the old iron. There are a lot of new things and I am sure more is coming in the future.

What now? You will not become a master of anything just by reading an article. So, take some time to play with arrays and practice the methods we discussed today. And, remember, JavaScript is awesome and arrays are still cool. With that, thank you for your time and have a great day!

[xyz-ihs snippet="thank-you-message"]
