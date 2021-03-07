# Blog post title [...]
<!--more-->
<!--
Table of Contents:
-->

## Asynchronous iteration

Asynchronous iteration is one of the lesser discussed ES2018 features. While there is a lot of talk about other ES2018 features such rest and spread, there is almost none about asynchronous iteration. What is this about? With asynchronous iteration we get asynchronous iterables and iterators.

Well, this might not be helpful. One thing this means is that asynchronous iteration allows you to use the [await] keyword with for...of loops. You can use these loops to iterate over iterable objects. Examples of iterable objects include arrays, Maps, Sets, NodeLists, function arguments, TypedArray, etc.

Before ES2018 `for...of` loops worked synchronously. If you tried to iterate over iterable that involved asynchronous operations and await it, it would not work. The loop itself would remain synchronous, basically ignore the `await`, and complete the iteration before asynchronous operation inside it could finish.

```JavaScript
// This would not work pre-ES2018
// because the loop remains synchronous.
// Create an async function:
async function processResponses(someIterable) {
  // Try to iterate over iterable
  for (let item of someIterable) {
    // Process item via asynchronous operation, like promise:
    await processItem(item)
  }
}
```

With asynchronous iteration `for...of` loops also work with asynchronous code. This means that if you want to iterate over iterable and do some asynchronous operation you can. The `for...of` loop will now be asynchronous and let you await for asynchronous operations to complete.

What you have to remember is where to use the `await` keyword. You don't put it inside the loop. Instead, you put it at the beginning of the `for...of` loop, after the `for` keyword. Now, when you use the `next()` method to get the next value of the async iterator, you will get a Promise. If you want to know more, you can find the proposal on [GitHub].

```JavaScript
// Create an async function:
async function processResponses(someIterable) {
  // Iterate over iterable and await the result
  // of an asynchronous operation
  for await (let item of someIterable) {
    processItem(item)
  }
}
```

## Rest/Spread properties

The rest and spread are not really new features. Both were introduced in ES6 as new operators. They quickly rose in popularity and usage. It is safe to say that JavaScript developers loved them. The only problem was that they worked only with arrays and parameters. ES2018 introduced these two features also for objects.

The syntax of both, rest and spread operator is very simple. It is composed of three dots (`...`). These dots are then followed by the object on which you want to use the rest or spread operator. Now, let's quickly discuss how both work.

### The rest operator for objects

The first one, rest operator, allows you to extract all remaining object properties properties of an object onto a new object. Note that these properties must be enumerable. If you already used destructuring for some properties, the rest operator will extract only properties that remained.

```JavaScript
// Rest example:
// Create an object:
const daysObj = {
  one: 'Monday',
  two: 'Tuesday',
  three: 'Wednesday',
  four: 'Thursday',
  five: 'Friday'
}

// Use destructuring to assign
// first two properties to variables.
// Then, use rest to assign rest of properties
// to the third variable.
const { one, two, ...restOfDays } = daysObj
// The rest will extract only "three", "four"
// and "five" because we already extracted
// the "one" and "two" vie destructuring.

// Log the value of "one":
console.log(one)
// Output:
// 'Monday'

// Log the value of "two":
console.log(two)
// Output:
// 'Tuesday'

// Log the value of "restOfDays":
console.log(restOfDays)
// Output:
// { three: 'Wednesday', four: 'Thursday', five: 'Friday' }
```

If you want to use rest operator for objects, remember two things. First, you can use it only once. Exception is if you use it with nested objects. Second, you must use it at the last one. This is why, in the example above, you saw it after destructuring the first two properties, not before.

```JavaScript
// This will not work - rest operator as first:
const { ...all, one, two } = { one: 1, two: 2, three: 3 }

// This will work - rest operator as last:
const { one, two, ...all } = { one: 1, two: 2, three: 3 }


// This will not work - multiple rest operators on the same level:
const { one, ...some, ...end } = { /* some properties */ }

// This will work - multiple rest operators on multiple levels:
const { one, {...secondLevel }, ...firstLevel } = { /* some properties */ }
```

### The spread operator for objects

What spread operator does is it allows you to create new objects by inserting all properties of another object. Spread operator also allows you to insert properties from multiple objects. You can also combine this operator with adding new properties.

```JavaScript
// Spread example:
// Create an object:
const myOriginalObj = { name: 'Joe Doe', age: 33 }

// Use spread operator to create new object:
const myNewObj = { ...myOriginalObj }

// Log the value of "myNewObj":
console.log(myNewObj)
// Output:
// { name: 'Joe Doe', age: 33 }


// Spread operator plus adding properties:
const myOriginalObj = { name: 'Caesar' }

// Use spread operator to create new object
// and add new property "genre":
const myNewObj = { ...myOriginalObj, genre: 'Strategy' }

// Log the value of "myNewObj":
console.log(myNewObj)
// Output:
// {
//   name: 'Caesar',
//   genre: 'Strategy'
// }


// Spread operator and combining two objects:
const myObjOne = { title: 'Eloquent JavaScript' }
const myObjTwo = { author: 'Marijn Haverbeke' }

// Use spread operator to create new object
// by combining "myObjOne" and "myObjTwo":
const myNewObj = { ...myObjOne, ...myObjTwo }

// Log the value of "myNewObj":
console.log(myNewObj)
// Output:
// {
//   title: 'Eloquent JavaScript',
//   author: 'Marijn Haverbeke'
// }
```

One thing about insert properties from multiple objects and adding new properties. In these two scenarios remember that the order matters. Let me explain. Let's say you want use spread operator to create a new object from two existing objects. The first existing object contains property `title` with some value.

The second existing object also contains property `title`, but with different value. Which one `title` wins? The one that comes last. If you use spread operator with the first object and then the second, the second `title` will be the winner. If you use spread operator with the second object as first, the first `title` will be the winner.

```JavaScript
// Spread operator and combining two objects:
const myObjOne = {
  title: 'Eloquent JavaScript',
  author: 'Marijn Haverbeke',
}

const myObjTwo = {
  title: 'You Don\'t Know JS Yet',
  language: 'English'
}

// Use spread operator to create new object
// by combining "myObjOne" and "myObjTwo":
// NOTE: "title" from "myObjTwo" will overwrite "title"
// from "myObjOne" because "myObjTwo" comes as last.
const myNewObj = { ...myObjOne, ...myObjTwo }

// Log the value of "myNewObj":
console.log(myNewObj)
// Output:
// {
//   title: "You Don't Know JS Yet",
//   author: 'Marijn Haverbeke',
//   language: 'English'
// }


// NOTE: Now, "title" from "myObjOne" will overwrite "title"
// from "myObjTwo" because "myObjOne" comes as last.
const myNewObj = { ...myObjTwo, ...myObjOne }

// Log the value of "myNewObj":
console.log(myNewObj)
// Output:
// {
//   title: 'Eloquent JavaScript',
//   language: 'English',
//   author: 'Marijn Haverbeke'
// }
```

## Promise.prototype.finally()

From the beginning, there were two callback functions for promises. One was `then()`, executed when promise is fulfilled. The second was `catch()`, executed either when promise is rejected or when the `then()` throws an exception. One of the ES2018 features is third callback function for promises called `finally()`.

The `finally()` callback will be executed every time the promise is settled. It doesn't matter if the promise is fulfilled or rejected. The general use for this callback is to do something that should always happen. For example, closing modal dialog, closing database connection or some cleanup.

```JavaScript
// finally() example:
// Fetch some API endpoint:
fetch()
  // Convert response to JSON:
  .then(response => response.json())
  // Log the JSON:
  .then(data => console.log(data))
  // Log error:
  .catch(error => console.log(error))
  // Do something at the end:
  .finally(() => console.log('Operation done.'))
```

## Regular Expression improvements

The list of ES2018 features also includes a couple of improvements for regular expression. These improvements include s(dotAll) flag, lookbehind assertion, named capture groups and unicode property escapes.

### s(dotAll)

First, the s(dotAll). Unlike dot (`.`), the s(dotAll) allows to match new line characters and also emojis.

```JavaScript
// s(dotAll) example:
/hello.world/.test('hello\nworld')
// Output:
// false

/hello.world/s.test('hello\nworld')
// Output:
// true
```

### Lookbehind assertions

Before ES2018, JavaScript supported only [lookahead assertion]. Lookahead assertion to match a pattern based on a text that follows it. With ES2018, JavaScript now also supports lookbehind assertion. This assertion allows you to match a pattern based on a text that precedes it. The syntax of lookbehind assertion is `?<=`.

```JavaScript
// Lookbehind assertion example:
/(?<=green) apple/.test('One red apple is on the table.')
// Output:
// false

/(?<=green) apple/.test('One green apple is on the table.')
// Output:
// true
```

There is also a negative lookbehind assertion. This assertion matches a pattern only if the substring is not preceded by the assertion. The syntax of negative lookbehind assertion is `?<!`.

```JavaScript
// Lookbehind assertion example:
/(?<!green) apple/.test('One red apple is on the table.')
// Output:
// true

/(?<!green) apple/.test('One green apple is on the table.')
// Output:
// false
```

### Named capture groups

Another nice feature introduced to regular expression by ES2018 is the ability to assign capturing group to a custom name. The syntax for named capture groups is `?<some_name>`, at the beginning of a capture group.

```JavaScript
const date_pattern = /(?<day>\d{2})\/(?<month>\d{2})\/(?<year>\d{4})/
const result = date_pattern.exec('11/12/2021')

// Log the matches array:
console.log(result)
// Output:
// [
//   '11/12/2021',
//   '11',
//   '12',
//   '2021',
//   index: 0,
//   input: '11/12/2021',
//   groups: [Object: null prototype] { day: '11', month: '12', year: '2021' }
// ]

// Log the group for day:
console.log(result.groups.day)
// Output:
// '11'

// Log the group for month:
console.log(result.groups.month)
// Output:
// '12'

// Log the group for year:
console.log(result.groups.year)
// Output:
// '2021'
```

### Unicode property escapes

Unicode property escapes is the last improvement for regular expressions when it comes to ES2018 features. Every unicode character has a number of properties. For example, White_Space, Uppercase, Lowercase, Alphabetic, ASCII, Emoji, etc. From now, you can access these properties inside regular expressions.

In order to use this, you need two things. First, you have to use the `/u` flag. This flag tells JavaScript that your string is a series of Unicode code points. The second thing is using `\p{}`. The property you want to check goes between the curly brackets. The negation is `\P{}`.

```JavaScript
// Create a string in Russian (Cyrillic script):
const myStrCyr = 'Доброе утро'

// Create a string in English (Latin script):
const myStrLat = 'Good morning'

// Test the "myStrCyr" if it contains Cyrillic script:
/\p{Script=Cyrillic}/u.test(myStrCyr) // true

// Test the "myStrLat" if it contains Cyrillic script:
/\p{Script=Cyrillic}/u.test(myStrLat) // false

// Test the "myStrCyr" if it contains Latin script:
/\p{Script=Latin}/u.test(myStrCyr) // false

// Test the "myStrLat" if it contains Latin script:
/\p{Script=Latin}/u.test(myStrLat) // true
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
