# 7 JavaScript ES2017 Features to Learn

The JavaScript ES2017 specification (ES8) has been around for a while. Many of the features introduced in this spec are very useful. Most of them are also well supported and safe to use. In this tutorial, you will learn about what are the ES2017 features, how they work, and how to use them.<!--more-->
<!--
Table of Contents:
-->

## String padding with padStart() and padEnd()

Two smaller ES2017 features added to strings are `padStart()` and `padEnd()`. These two methods allow you to easily add characters to a string so it reaches a specific length. The `padStart()` adds characters at the beginning of the string. The `padEnd()` adds characters at the end.

Both methods accept two parameters. The first parameter is the length of the string you want to reach. The second parameter is the character you want to add. This character will be added repeatedly as long as is needed to reach the target length. If the string is already at the target length, or beyond it, nothing will happen.

This second parameter, the character to add, is optional. If you specify it, both methods will add it if necessary. If you omit it, both methods will add default character

```JavaScript
// padStart() example:
// Add '-' character at the beginning
// until the string reaches length of 9 characters.
'Hello'.padStart(9, '-')
// Output:
// '----Hello'

// Add 'A' character at the beginning
// until the string reaches length of 3 characters.
// Note: the string is already beyond this length
// so nothing will happen.
'Hello'.padStart(3, 'A')
// Output:
// 'Hello'

// Increase the length of a string to 11,
// but don't specify the character to add.
'Hello'.padStart(15)
// Output:
// '          Hello'


// padEnd() example:
// Add '-' character at the beginning
// until the string reaches length of 9 characters.
'Bye'.padEnd(9, '.')
// Output:
// 'Bye......'

// Add 'A' character at the beginning
// until the string reaches length of 3 characters.
// Note: the string is already beyond this length
// so nothing will happen.
'Bye'.padEnd(1, '?')
// Output:
// 'Bye'


// Increase the length of a string to 11,
// but don't specify the character to add.
'Bye'.padEnd(11)
// Output:
// 'Bye        '
```

## Object.values()

Another nice and useful addition to JavaScript language is `Object.values()` method. This method returns values from all object's own properties. It returns these values in the form of an array. This method accepts one parameter. This parameter is the object whose values you want to get.

One interesting thing is that this method also works with arrays. This means that you can pass an array as an argument, instead of an object. As a result, you will get a new array of values, the items from the original array.

```JavaScript
// Object.values() with objects:
// Create an object:
const joshuaObj = { name: 'Joshua', hobbies: 'programming' }

// Get all values from "joshuaObj":
console.log(Object.values(joshuaObj))
// Output:
// [ 'Joshua', 'programming' ]


// Object.values() with arrays:
// Create an array:
const languagesArr = ['C', 'C++', 'Rust', 'Python', 'JavaScript']

// Get all values from "joshuaObj":
console.log(Object.values(languagesArr))
// Output:
// [ 'C', 'C++', 'Rust', 'Python', 'JavaScript' ]
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
