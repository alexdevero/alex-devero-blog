# 7 Useful JavaScript ES2020 Features to Learn About
<!--more-->
<!--
Table of Contents:
-->

## String.prototype.trimStart() and String.prototype.trimEnd()

If you've ever worked with strings there is chance you had to deal with unwanted white space. From now on, there will be two ES2020 features that will help you with this issue. These features are .`trimStart()` and `trimEnd()` string methods. These methods do what their names imply.

They both help you trim, or remove, white space from given string. The first one, the `trimStart()` will remove all white space from the start of the string. The second, the `trimEnd()` will remove all white space from the end of the string. If you need to remove white spaces on both sides?

This gives you two options. The first option is using both these ES2019 features together. The second option is to use another string method [trim()]. Both will give you the result you want.

```JavaScript
// String.prototype.trimStart() examples:
// Try string without white space:
'JavaScript'.trimStart()
// Output:
//'JavaScript'

// Try string with white space at the beginning:
' JavaScript'.trimStart()
// Output:
//'JavaScript'

// Try string with white space on both sides
' JavaScript '.trimStart()
// Output:
//'JavaScript '

// Try string with white space at the emd
'JavaScript '.trimStart()
// Output:
//'JavaScript '


// String.prototype.trimEnd() examples:
// Try string without white space:
'JavaScript'.trimEnd()
// Output:
//'JavaScript'

// Try string with white space at the beginning:
' JavaScript'.trimEnd()
// Output:
//' JavaScript'

// Try string with white space on both sides
' JavaScript '.trimEnd()
// Output:
//' JavaScript'

// Try string with white space at the emd
'JavaScript '.trimEnd()
// Output:
//'JavaScript'
```

## Function.prototype.toString()

The `toString()` method for functions has been around for a while. What this method does is it allow you to print the code of a function as you wrote it, or someone else. What is different in ES2019 is how this method handles comments and special characters such as white space.

In the past, `toString()` method removed comments and white space. So, the printed version of the function may not look like the original code. This will no longer happen with the release of ES2019. From now on, the value of returned by `toString()` method will match the original, including comments and special characters.

```JavaScript
// Before ES2019:
function myFunc/* is this really a good name? */() {
  /* Now, what to do? */
}

myFunc.toString()
// Output:
// "function myFunc() {}"


// After ES2019:
function myFunc/* is this really a good name? */() {
  /* Now, what to do? */
}

myFunc.toString()
// Output:
// "function myFunc/* is this really a good name? */() {
//   /* Now, what to do? */
// }"
```

## Array.prototype.flat() and Array.prototype.flatMap()

Arrays are one of the fundamental parts in JavaScript. That said, they can sometimes cause a lot of headaches. This is especially true if you have to deal with multidimensional arrays. Even a seemingly simple task as turning multidimensional array to a one-dimensional can be difficult.

Good news is that there are now two ES2019 features that will make this easier. The first one is `flat()` method. When you use this method on a multidimensional array it will transform it into a one-dimensional. By default, `flat()` will flatten the array only by one level.

If you need more, you can specify the number of levels and pass it as an argument when you call this method. If you are not sure how many levels do you need, you can also use `Infinity`.

```JavaScript
// Create an array:
const myArray = ['JavaScript', ['C', 'C++', ['Assembly', ['Bytecode']]]]

// Flatten the array by one level:
let myFlatArray = myArray.flat(1)

// Log the array:
console.log(myFlatArray)
// Output:
// [ 'JavaScript', 'C', 'C++', [ 'Assembly', [ 'Bytecode' ] ] ]

// Flatten the array by infinite number of levels:
let myInfiniteFlatArray = myArray.flat(Infinity)

// Log the array again:
console.log(myInfiniteFlatArray)
// Output:
// [ 'JavaScript', 'C', 'C++', 'Assembly', 'Bytecode' ]
```

### Array.prototype.flatMap()

Aside to the `flat()` method there is also `flatMap()` method. You can think about this method as an advanced version of `flat()`. The difference is that `flatMap()` method combines `flat()` with [map()] method. Thanks to this, when you flatten an array, you can call a callback function.

This allows you to work with individual elements inside the original array during the process of flattening. This can be handy when you want to make an array flat but also modify the content. Or, if you want to use map to modify content of an array, but you want the result to be a flat array.

```JavaScript
// Create an array:
const myArray = ['One word', 'Two words', 'Three words']

// Split all string in the array to words using map():
// Note: this will create multidimensional array.
const myMappedWordArray = myArray.map(str => str.split(' '))

// Log the value of "myMappedWordArray":
console.log(myMappedWordArray)
// Output:
// [ [ 'One', 'word' ], [ 'Two', 'words' ], [ 'Three', 'words' ] ]


// Example with flatMap():
const myArray = ['One word', 'Two words', 'Three words']

// Split all string in the array to words using map():
// Note: this will create multidimensional array.
const myFlatWordArray = myArray.flatMap(str => str.split(' '))

// Log the value of "myFlatWordArray":
console.log(myFlatWordArray)
// Output:
// [ 'One', 'word', 'Two', 'words', 'Three', 'words' ]
```

## Conclusion: [...] ...

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
-
-->
