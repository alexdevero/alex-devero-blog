# What Method Chaining in JavaScript, How it Works and How to Use It

Method chaining is popular method that can help you write more concise and readable code. In this tutorial, you will learn what method chaining in JavaScript is and how it works. You will also learn how to use method chaining to improve the quality and readability of your code.<!--more-->
<!--
Table of Contents:
-->

## A quick introduction to method chaining

Have you ever worked with some library such as jQuery? Then, you've probably seen something like this. There are two or more methods used in cascade, one after another, and on the same line. Nowadays, it is also very common to see this practice in plain JavaScript. You could see this with arrays, strings and promises.

In all these cases, the process is the same. First, you reference the thing you want to work with. Second, you use as many methods as you need. However, instead of using these methods separately, you use them one after another. You basically chain them together. Let's take a look at some examples to demonstrate this.

### Examples of method chaining

Let's say you want to work with a string. There are two ways to get this done. The first one is without method chaining. This requires using each method on the string separately. You also have to reference the string each and every time. The second option is to use method chaining.

In this case, you use all string methods you want one after another. You can do this either on a single line or multiple. That depends on you. And, you also reference the string only once, at the very beginning. The same result, but different amount of code that you have to write.

```JavaScript
// Method chaining with string.
let myStr = ' - Hello-world. '

// Without method chaining:
myStr = myStr.toLowerCase()
myStr = myStr.replace(/-/g, ' ')
myStr = myStr.trim()

// With method chaining:
myStr = myStr.toLowerCase().replace(/-/g, ' ').trim()

// Alternative with method chaining and multiple lines:
myStr = myStr
  .toLowerCase()
  .replace(/-/g, ' ')
  .trim()

// Log the value of "myStr" variable.
console.log(myStr)
// Output:
// 'hello world.'
```

The same applies if you have an array and want to use a couple of array methods to work with it. You can also choose between these two approaches. The longer one not using method chaining and the shorter and more succinct using chaining. Just like with the string, the result will be the same. The amount code will be different.

```JavaScript
// Method chaining with array.
let myArray = [1, 7, 3, null, 8, null, 0, null, '20', 15]

// Without method chaining:
myArray = myArray.filter(el => typeof el === 'number' && isFinite(el))
myArray = myArray.sort((x, y) => x - y)

// With method chaining:
myArray = myArray.filter(el => typeof el === 'number' && isFinite(el)).sort((x, y) => x - y)

// Alternative with method chaining and multiple lines:
myArray = myArray
  .filter(el => typeof el === 'number' && isFinite(el))
  .sort((x, y) => x - y)

// Log the value of "myArray" variable.
console.log(myArray)
// Output:
// [ 0, 1, 3, 7, 8 ]
```

Promises are a very good example because they almost require method chaining in order to work. First, you [create a promise]. Then, you add appropriate [handler functions]. These handler functions are necessary for you to process the value you get when the promise is resolved. Well, unless you use [async function] and [await] keyword.

```JavaScript
// Create a Promise
const myPromise = new Promise((resolve, reject) => {
  // Create a fake delay
  setTimeout(function() {
    // Resolve the promise with a simple message
    resolve('Sorry, no data.')
  }, 1000)
})

// With method chaining:
myPromise.then((data) => console.log(data)).catch(err => console.log(error))

// Alternative with method chaining and multiple lines:
myPromise
  .then((data) => console.log(data))
  .catch(err => console.log(error))
// Output:
// 'Sorry, no data.'
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
