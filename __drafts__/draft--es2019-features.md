# 7 Useful JavaScript ES2020 Features to Learn About
<!--more-->
<!--
Table of Contents:
## String.prototype.trimStart() and String.prototype.trimEnd()
## Function.prototype.toString()
## Array.prototype.flat() and Array.prototype.flatMap()
### Array.prototype.flatMap()
## Object.fromEntries()
## Optional catch binding
## Well-formed JSON.stringify()
## Symbol.prototype.description
### Symbol.prototype.toString() alternative
## Conclusion: 8 useful JavaScript ES2019 you should know
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

## Object.fromEntries()

When you need to convert some object to an array you can do it with a single method, [entries()]. However, until now, there wasn't a method that would just as easily reverted this. This will no longer be an issue thanks to one of the ES2019 features. This feature is `fromEntries()` method.

What this method does is simple. It takes an iterable, such as an array or a [Map], of key-value pairs. Then, it transforms it into an object.

```JavaScript
// Convert an array to object:
// Create an array:
const myArray = [['name', 'Joe'], ['age', 33], ['favoriteLanguage', 'JavaScript']]

// Transform the array to an object:
const myObj = Object.fromEntries(myArray)

// Log the new object:
console.log(myObj)
// Output:
// {
//   name: 'Joe',
//   age: 33,
//   favoriteLanguage: 'JavaScript'
// }


// Convert a Map to object:
// Create a map:
const myMap = new Map(
  [['name', 'Spike'], ['species', 'dog'], ['age', 3]]
)

// Transform the Map to an object:
const myObj = Object.fromEntries(myMap)

// Log the new object:
console.log(myObj)
// Output:
// {
//   name: 'Spike',
//   species: 'dog',
//   age: 3
// }
```

## Optional catch binding

Previously, when you wanted to use `try...catch` you also had to use binding. You had to pass in the exception as a parameter, even if you didn't use it. One change that ES2019 brings is that it makes this optional. If you don't want to use the exception, you can use the catch block without a parameter.

```JavaScript
// Before ES2019:
try {
  // Do something.
} catch (e) {
  // Ignore the required e parameter
  // if you don't want to use it, but keep it.
}

// After ES2019:
try {
  // Do something.
} catch {
  // No need to add any parameter
}
```

## Well-formed JSON.stringify()

In the past, when you used `JSON.stringify()` on something that contained specific characters, you would get ill-formed Unicode string. Code points from U+D800 to U+DFFF would become malformed ("�"). What's worse, there was no way to transform those malformed code points back.

Part of the ES2019 features was also a fix for the `JSON.stringify()` method. From now on, you will be able to stringify those problematic code points. You will be also able to transform them back into their original representations.

## Symbol.prototype.description

Symbols are new data type introduced to in ES2015 (ES6). They are often used to identify object properties. One of the ES2019 features is also a `description` property. This property is a read-only, so you can't change its value. What it does is it returns the description of given Symbol.

Two things to keep in mind. First, description is not required when you create a symbol, but optional. So, it can happen that when you try to access the `description` you might not get anything other than `undefined`. This, `undefined`, is what you will get if you try to access description of a Symbol without a description.

The second things is that `description` is a description of a Symbol. It is not its identifier. This means that you can't use existing description, the value of `description` property, to access existing Symbol. You can use it just to make it easier to identify Symbol you are working with.

Quick note. When you create new Symbol, you can add description by passing some string as an argument to the `Symbol()` object. If you leave this empty, description will be `undefined`.

```JavaScript
// Create new Symbol and add description:
// Note: description is the "My first symbol."
const mySymbol = Symbol('My first symbol.')

// Log the value of "description" property:
console.log(mySymbol.description)
// Output:
// 'My first symbol.'


// Try to read non-existing description:
console.log(Symbol().description)
// Output:
// undefined


// Try to read description defined as empty string:
console.log(Symbol('').description)
// Output:
// ''
```

### Symbol.prototype.toString() alternative

The `toString()` method offers another way to read the description of a Symbol. The downside of this method is that it also includes the "Symbol()" in the string it returns. Another difference is that the `toString()` method will never return an `undefined` of description doesn't exist.

If you have a Symbol without description and use the `toString()` method you will still get the "Symbol()" part. You will also get this if the description is an empty string. This makes it basically impossible to distinguish between non-existing description and empty string used as description. Another reason to use `description`.

```JavaScript
// Create new Symbol with description:
const mySymbol = Symbol('REAMDE.')

// Log the value of "description" property:
console.log(mySymbol.toString())
// Output:
// 'Symbol(REAMDE.)'


// Try to read non-existing description:
console.log(Symbol().toString())
// Output:
// 'Symbol()'


// Try to read description defined as empty string:
console.log(Symbol('').toString())
// Output:
// 'Symbol()'
```


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
