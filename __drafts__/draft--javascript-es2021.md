# Upcoming Interesting ES2021 JavaScript Features to Learn
<!--more-->
<!--
Table of Contents:
-->


## String.prototype.replaceAll()

Let's start with smaller feature of ES2021, but still nice addition to JavaScript, `replaceAll()` method. At this moment, when you want to replace multiple occurrences of a pattern in a [string] you can you [replace() method]. The problem? If you use a string, this will allow you to replace only the first occurrence of the pattern.

This doesn't mean the `replace()` method is useless if you want to replace all occurrences of a pattern. It can get this job done as well. However, you have to use a [regular expression]. If this is okay with you then no problem. For many developers, regular expressions are not their preferred choice. Far from it.

If you are one these developers, you are going to like the new `replaceAll()` method. This method works in a similar same way as the `replace()` method. The difference is that `replaceAll()` allows you to replace all occurrence of a pattern without having to use regular expression.

The `replaceAll()` method also accepts regular expressions. So, if regex is your thing you can use it as well. You can also use a function as the replacement. If you do, this function will be executed for each match in the string. You can read this proposal in the [official repository].

```JavaScript
// Declare a string:
let str = 'There are those who like cats, there those who like watching cats and there are those who have cats.'

// Replace all occurrences of "cats" with dogs:
str = str.replaceAll('cats', 'dogs')

// Log the new value of "str":
console.log(str)
// Output:
// 'There are those who like dogs, there those who like watching dogs and there are those who have dogs.'


// A simple alternative with replace():
str = str.replace(/cats/g, 'dogs')

// Log the new value of "str":
console.log(str)
// Output:
// 'There are those who like dogs, there those who like watching dogs and there are those have dogs.'
```

## Numeric separators

This is another very small JavaScript ES2021 feature that can make your day at least a bit better. Especially if you work with big numbers. Numeric separators provide you with an easy and simple way to make big numbers more readable and easier to work with. The syntax is just as easy. It is a underscore (`_`).

```JavaScript
// Number without numeric separators:
const num = 3685134689


// Number with numeric separators:
const num = 3_685_134_689
```

Remember that numeric separators are just visual aid. If you use them they will have no effect on the numeric values themselves. For example, if you try to log a number with numeric separators you will get the "raw" and "unedited" version.

```JavaScript
// Use numeric separators with a number:
const num = 3_685_134_689

// Log the value of "num":
console.log(num)
// Output:
// 3685134689
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
- https://codeburst.io/exciting-features-of-javascript-es2021-es12-1de8adf6550b
- https://backbencher.dev/javascript/es2021-new-features
-->
