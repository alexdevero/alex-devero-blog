# JavaScript Objects - A Friendly Introduction Pt.2
JavaScript objects can be difficult to learn, especially for beginners. In this tutorial you will learn how to loop through JavaScript objects with `for...in` loop, `Object.keys()`, `Object.values()`, `Object.entries()` and `Object.getOwnPropertyNames()`. You will also learn how to freeze objects and about some gotchas.<!--more-->
<!--
Table of Contents:
## Looping over JavaScript objects
### For...in loop
### Object.keys(), Object.values() and Object.entries()
### Object.getOwnPropertyNames()
## Freezing JavaScript objects
### Partially freezing JavaScript objects
### Not-so frozen objects
### Arrays, freezing and object methods
## JavaScript objects are not created equal
## Conclusion: JavaScript Objects - A Friendly Introduction
-->

JavaScript Objects - A Friendly Introduction [Part 1].

## Looping over JavaScript objects

In [previous part], you've learned about the basics of JavaScript objects. What if you want to know what keys and properties specific object contains? In JavaScript, there are multiple built-in ways to find this out. The most popular are `for...in` loop, `Object.keys()`, `Object.values()`, `Object.entries()` and `Object.getOwnPropertyNames()`.

### For...in loop

The first one, `for...in` loop, loops over all the properties of given object and returns `keys`. When you use bracket notation, `obj[key]`, the `for...in` loop will retrieve the value of current key. The syntax of `for...in` loop is very easy. In a fact, it is even easier than syntax of `for` loop.

When you use `for...in` loop you have to specify two things. The first one is a variable. On each iteration, this variables holds current key name, or current property. When you log this variable you will see what key, or property, is currently accessible in the loop. For this variable, you choose any name you want.

What you need to remember is to use the same variable in the loop, when you want to get current key, or property, or its value. The second thing you have to specify is the object you want to loop over. Lastly, you need to put the `in` keyword between the variable and object you want to loop over, i.e. `for (let someKey in someObject) {}`.

```js
// For...in loop example
// Create simple object
const specterObj = {
  id: 's5903',
  name: 'Specter',
  active: true
}

// Use for...in loop to iterate over specterObj
for (let objKey in specterObj) {
  // Log current key, temporarily stored in objKey variable
  console.log(`Current key is: ${objKey}.`)

  // Log the value of current key, using bracket notation
  console.log(`Current value is: ${specterObj[objKey]}.`)
}
// 'Current key is: id.'
// 'Current value is: s5903.'
// 'Current key is: name.'
// 'Current value is: Specter.'
// 'Current key is: active.'
// 'Current value is: true.'
```

Side note: Don't confuse `for...in` loop with `for...of` loop. These two loops look very similar. There is a variable for current property and something to loop through. Aside to that, there two differences. First, there is `of` keyword, instead of `in`. The second difference is in that "something" to loop through.

The `for...in` loop was designed to be used to loop through properties of JavaScript objects. The `for...of` loop, on the other hand, was designed to be used to loop through [iterable objects]. What are iterable objects? In JavaScript, iterable objects are strings, arrays, array-like objects, maps and sets.

JavaScript Objects are not iterable objects. Due to that you can't use `for...of` loop on JavaScript objects. If you try it, you will get a type error saying that object is not iterable. So, remember, when it comes to JavaScript objects use `for...in` loop. In case of strings, arrays, array-like objects, maps and sets use `for...of` loop.

```js
// This will not work: for...of loop with objects
// Create simple object
const exampleObj = {
  firstName: 'Jack',
  lastName: 'Ryan'
}

// Try to use for...of loop to loop through exampleObj
for (let objKey of exampleObj) {
  // Log current key, temporarily stored in objKey variable
  console.log(`Current key is: ${objKey}.`)
}
// TypeError: exampleObj is not iterable


// This will work: for...of loop with iterable object (array)
const exampleArray = ['string', 'number', 'boolean', 56, true]

// Use for...of loop to loop through exampleArray
for (let curItem of exampleArray) {
  // Log current item
  console.log(curItem)
}
// 'string'
// 'number'
// 'boolean'
// 56
// true


// This will work: for...of loop with iterable object (string)
const word = 'Doom'

// Use for...of loop to loop through word
for (let curChar of word) {
  // Log current item
  console.log(curChar)
}
// 'D'
// 'o'
// 'o'
// 'm'
```

### Object.keys(), Object.values() and Object.entries()

The second, third and forth way to loop through objects are `Object.keys()`, `Object.values()` and `Object.entries()`. Using all these three ways, these three `Object` methods, is very simple. First, you need is to decide what type of information do you want to get because all these methods return something different.

The `Object.keys()` returns array of keys that exist in a particular object. The `Object.values()` returns array of values. The last one, `Object.entries()`, returns array of key/value pairs in the form of arrays, `[key, value]`. So, do you want the keys (properties), property values or everything?

Then, when you know what type of data you want to get, the only thing you have to do is to use the object, you want to loop through, as an argument. Meaning, you pass that objects, or reference to it, between the parenthesis that follow each `Object` method, i.e. `Object.keys(myObj)`.

```js
// Create a simple object
const userBilly = {
  name: 'Billy',
  age: 24,
  occupation: 'programmer',
  isEmployed: true
}


// Use Object.keys() to loop through userBilly
// and get all keys, or object properties,
// that exist inside the userBilly
Object.keys(userBilly)
// [ 'name', 'age', 'occupation', 'isEmployed' ]


// Use Object.values() to loop through userBilly
// and get all values that exist inside the userBilly
Object.values(userBilly)
// [ 'Billy', 24, 'programmer', true ]


// Use Object.entries() to loop through userBilly
// and get all key/value pairs
// in the form of arrays, [key, value]
Object.entries(userBilly)
// [
//   [ 'name', 'Billy' ],
//   [ 'age', 24 ],
//   [ 'occupation', 'programmer' ],
//   [ 'isEmployed', true ]
// ]
```

### Object.getOwnPropertyNames()

The last way to loop through JavaScript objects is by using `Object` built-in method `getOwnPropertyNames()`. This method works in a similar way to `Object.keys()`. It also returns an array of all properties that exist on given object. Just like with `Object.keys()` you again pass the object to loop through as an argument.

```js
// Create a simple object
const userTereza = {
  name: 'Tereza',
  nationality: 'Russian',
  isHappy: true
}

// Use Object.getOwnPropertyNames() to loop through userTereza
// and get all keys, or object properties,
// that exist inside the userTereza
Object.getOwnPropertyNames(userTereza)
// [ 'name', 'nationality', 'isHappy' ]
```

The `Object.getOwnPropertyNames()` method returns array of keys, or properties. However, that doesn't mean you can't use it to get the values of those key, or properties. You can. You can use the `Object.getOwnPropertyNames()` method to get an array of keys. Then, you can use loop to iterate over this array.

Inside the loop, you can take each key, find it inside the object you are looping through, and use it to get the value of that key, using bracket notation. Since, `Object.getOwnPropertyNames()` method works similarly to `Object.keys()`, you can use the same approach also with `Object.keys()`.

```js
// Create a simple object
const whatYouDoBook = {
  title: 'What You Do Is Who You Are',
  author: 'Ben Horowitz',
  releaseDate: '29/10/2019'
}

// Use Object.getOwnPropertyNames() to loop through whatYouDoBook
// and get all keys, or object properties,
// that exist inside the whatYouDoBook
// Then, use forEach loop, and bracket notation,
// To get value for each key in whatYouDoBook
Object.getOwnPropertyNames(whatYouDoBook).forEach(bookKey => {
  console.log(`Key: "${bookKey}"; value: "${whatYouDoBook[bookKey]}".`)
})
// 'Key: "title"; value: "What You Do Is Who You Are".'
// 'Key: "author"; value: "Ben Horowitz".'
// 'Key: "releaseDate"; value: "29/10/2019".'


// Alternatively, use Object.keys()
Object.keys(whatYouDoBook).forEach(bookKey => {
  console.log(`Key: ${bookKey}; value: ${whatYouDoBook[bookKey]}`)
})
// 'Key: title; value: What You Do Is Who You Are'
// 'Key: author; value: Ben Horowitz'
// 'Key: releaseDate; value: 29/10/2019'
```

## Freezing JavaScript objects

From time to time, you may want to make some object immutable. Put simply, you want to prevent some object from being changed. This means that nobody can add new properties or remove or change existing properties. When you want to do this, the most straightforward way is by using JavaScript built-in method `Object.freeze()`.

When you use this method, you pass the object you want to freeze as an argument. When you do that, you don't have to assign `Object.freeze()` to any variable. The `Object.freeze()` method will freeze the object you passed. So, create an object, next pass it to `Object.freeze()` method and the original object will be frozen.

```js
// Example no.1: Using unfrozen object
// Create a simple object
const artistAlphonse = {
  firstName: 'Alphonse',
  lastName: 'Mucha',
  nationality: 'Czech',
  occupation: 'artist',
  movement: ['art nouveau']
}

// Try to change some properties of artistAlphonse obj
artistAlphonse.firstName = 'Alfie'
artistAlphonse.occupation = ['painter', 'illustrator', 'graphic artist']

// Try to remove property in artistAlphonse obj
delete artistAlphonse.movement

// Log the writer object
console.log(artistAlphonse)
// {
//   firstName: 'Alfie',
//   lastName: 'Mucha',
//   nationality: 'Czech',
//   occupation: [ 'painter', 'illustrator', 'graphic artist' ]
// }


// Example no.2: freezing object with Object.freeze()
// Create a simple object
const artistPablo = {
  firstName: 'Pablo',
  lastName: 'Picasso',
  nationality: 'Spanish',
  occupation: 'artist',
  movement: ['cubism', 'surrealism']
}

// Freeze artistPablo object
Object.freeze(artistPablo)

// Try to change some properties of artistPablo obj
artistPablo.firstName = 'Salvador'
// TypeError: Cannot assign to read only property 'firstName' of object '#<Object>'

artistPablo.lastName = 'Dali'
// TypeError: Cannot assign to read only property 'lastName' of object '#<Object>'

artistPablo.movement = ['cubism', 'dada', 'surrealism']
// TypeError: Cannot assign to read only property 'movement' of object '#<Object>'
```

Before you start playing with `Object.freeze()`, there is one thing you need to know. There is no "unfreeze()" method in JavaScript. So, if you freeze an object there is no way to undo that. So, make sure you really want to make that object immutable, or unchangeable, before you freeze it.

### Partially freezing JavaScript objects

Another option is freezing you JavaScript objects only partially. Meaning, nobody can add new properties or remove existing properties. However, it is still possible to change existing properties. The process is almost the same as with freezing the object completely, but now instead of `Object.freeze()` you use `Object.seal()`.

As we discussed above, the difference between `Object.freeze()` and `Object.seal()` is that the later will allow you to change the values of properties inside an object. Other than that, they work, and are used, in the same way.

```js
// Partially freezing object example with Object.seal()
// Create a simple object
const writer = {
  firstName: 'Leo',
  lastName: 'Tolstoy',
  nationality: 'Russian',
  occupation: 'writer',
  movement: ['realism']
}

// Seal writer object
Object.seal(writer)

// Try to change some properties of writer object
writer.firstName = 'Isaac'
writer.lastName = 'Asimov'
writer.movement = ['golden age of science fiction']


// Try to delete existing property
delete writer.firstName
// TypeError: Cannot delete property 'firstName' of #<Object>


// Try to add new property
writer.genre = 'science fiction'
// TypeError: Cannot add property genre, object is not extensible


// Log the writer object
console.log(writer)
// {
//   firstName: 'Isaac',
//   lastName: 'Asimov',
//   nationality: 'Russian',
//   occupation: 'writer',
//   movement: [ 'golden age of science fiction' ]
// }
```

### Not-so frozen objects

Do you remember that thing about immutable JavaScript objects and inability to change them? Well, that is only partially true. Yes, it is not possible to add properties, remove them or change them if the object is frozen. However, this rule apply only to the object you are freezing. It does not apply to other objects inside it.

Imagine you have an object. This object has several properties. There are some properties that have [primitive data types] as values, types such as strings or numbers. Then, there are properties whose values are objects. For example, other JavaScript objects and arrays. Here is the interesting part, these, "inner", objects are actually not frozen.

Yes, even though, the object itself is really frozen, any objects inside it are not. You can do whatever you want with these "inner" objects. You can add new properties. You can remove properties and you can also change their values.

```js
// Create a simple object
const foundation = {
  title: 'Foundation',
  author: 'Isaac Asimov',
  numOfPages: 255,
  publicationDate: 1951,
  // array of genres is the first "inner" object we can change
  genres: ['science fiction', 'political drama'],
  // object of sequels is the first "inner" object we can change
  sequels: {
    one: 'Foundation and Empire',
    two: 'Second Foundation',
    three: 'Foundation\'s Edge',
    four: 'Foundation and Earth',
  }
}

// Freeze foundation object
Object.freeze(foundation)

// Try to change the value of property 'one' in sequels object
foundation.sequels.one = 'Prelude to Foundation'
// 'Prelude to Foundation'

// Try to change the value of property 'two' in sequels object
foundation.sequels.two = 'Forward the Foundation'
// 'Forward the Foundation'

// Try to change the first genre
foundation.genres[0] = 'novel'
// 'novel'

// Try to remove the second genre
foundation.genres.splice(1)
// [ 'political drama' ]

// Try to remove the property 'three' in sequels object
delete foundation.sequels.three
// true

// Try to remove the property 'four' in sequels object
delete foundation.sequels.four
// true

// Log the foundation object
console.log(foundation)
// {
//   title: 'Foundation',
//   author: 'Isaac Asimov',
//   numOfPages: 255,
//   publicationDate: 1951,
//   genres: [ 'novel' ],
//   sequels: {
//     one: 'Prelude to Foundation',
//     two: 'Forward the Foundation'
//   }
// }
```

So, is it possible to really freeze an object. Freezing an object in the terms that all objects inside it will be frozen as well? Yes, it is. What you have to do is freezing the parent objects and then freezing each of these "inner" objects individually. Then, neither the parent nor the "inner" objects will be mutable.

```js
const foundation = {
  title: 'Foundation',
  author: 'Isaac Asimov',
  numOfPages: 255,
  publicationDate: 1951,
  // array of genres is the first "inner" object we can change
  genres: ['science fiction', 'political drama'],
  // object of sequels is the first "inner" object we can change
  sequels: {
    one: 'Foundation and Empire',
    two: 'Second Foundation',
    three: 'Foundation\'s Edge',
    four: 'Foundation and Earth',
  }
}

// Freeze foundation object
Object.freeze(foundation)

// Freeze genres array inside foundation object
Object.freeze(foundation.genres)

// Freeze sequels object inside foundation object
Object.freeze(foundation.sequels)

// Try to change the value of property 'one' in sequels object
foundation.sequels.one = 'Prelude to Foundation'
// TypeError: Cannot assign to read only property 'one' of object '#<Object>'

// Try to change the value of property 'two' in sequels object
foundation.sequels.two = 'Forward the Foundation'
// TypeError: Cannot assign to read only property 'two' of object '#<Object>'

// Try to change the first genre
foundation.genres[0] = 'novel'
// TypeError: Cannot assign to read only property '0' of object '[object Array]'

// Try to remove the second genre
foundation.genres.splice(1)
// TypeError: Cannot delete property '1' of [object Array]

// Try to remove the property 'three' in sequels object
delete foundation.sequels.three
// TypeError: Cannot delete property 'three' of #<Object>

// Try to remove the property 'four' in sequels object
delete foundation.sequels.four
// TypeError: Cannot delete property 'four' of #<Object>

// Log the foundation object
console.log(foundation)
// {
//   title: 'Foundation',
//   author: 'Isaac Asimov',
//   numOfPages: 255,
//   publicationDate: 1951,
//   genres: [ 'science fiction', 'political drama' ],
//   sequels: {
//     one: 'Foundation and Empire',
//     two: 'Second Foundation',
//     three: "Foundation's Edge",
//     four: 'Foundation and Earth'
//   }
// }
```

### Arrays, freezing and object methods

In the example above, we used the `Object.freeze()` method to freeze an array, and it actually worked. In JavaScript, arrays are objects, list-like objects. Thanks to this, you can use many of the built-in `Object` methods also on arrays. For example, you can use the `Object.keys`, `Object.values` and `Object.entries` methods.

We used these methods earlier to loop through JavaScript objects. You can use these methods also with arrays. And, as you saw, you can also use `Object.freeze()` to freeze an array. Doing so will freeze an array so you can't change the items inside it. However, there is a catch.

You will not be able to change the items inside it individually, using indices. However, you will still be able to change the items inside the array by re-assigning it. You will also be able to remove items inside the array using methods such as `.pop()` and `shift()`.

```js
// Example no.1: using Object methods with arrays
// Create a simple array
let exampleArrayOne = [1, 2, 3, 4]


// Use Object.keys() with an array
Object.keys(exampleArrayOne)
// [ '0', '1', '2', '3' ]


// Use Object.values() with an array
Object.values(exampleArrayOne)
// [ 1, 2, 3, 4 ]


// Use Object.entries() with an array
Object.entries(exampleArrayOne)
// [ [ '0', 1 ], [ '1', 2 ], [ '2', 3 ], [ '3', 4 ] ]


// Example no.1: freezing an array
let exampleArrayTwo = [5, 6, 7]
Object.freeze(exampleArrayTwo)

// Try to change frozen exampleArray array
exampleArrayTwo[0] = 5
// TypeError: Cannot assign to read only property '0' of object '[object Array]'

exampleArrayTwo[1] = 3
// TypeError: Cannot assign to read only property '0' of object '[object Array]'

// Try to re-assign the array: This will work
exampleArrayTwo = ['five', 'six', 'seven']

// Log the exampleArrayTwo array
console.log(exampleArrayTwo)
// [ 'five', 'six', 'seven' ]

// Try remove items using pop() method
exampleArrayTwo.pop()

// Try remove items using shift() method
exampleArrayTwo.shift()

// Log the exampleArrayTwo array again
console.log(exampleArrayTwo)
// [ 'six' ]
```

## JavaScript objects are not created equal

Let's finish this by taking a look at one interesting thing. When it comes to JavaScript objects, two objects with the same content are never considered the same. It doesn't matter if both objects contain the same properties, and values. When you compare these objects, using abstract or strict equal, JavaScript will always return `false`.

As always, there a way to make two JavaScript objects equal. First, you have to create one object and assign it to a variable. Then, you have to copy that object by reference, i.e. create another variable while referencing the variable storing the first object. When you try to compare these objects JavaScript will consider them to be the same.

The result of both, abstract and strict equal, will be `true`. Remind yourself about this the next time you will want to compare objects by their content.

```js
// Comparing objects example no.1: using two objects
// This will not work:
// Create two objects with the same content
const objOne = { name: 'Joe' }
const objTwo = { name: 'Joe' }

// Compare objOne and objTwo
objOne == objTwo
// false

objOne === objTwo
// false


// Comparing objects example no.2: copying object by reference
// This will work:
// Create one object and copy it by reference
const objOne = { language: 'JavaScript' }
const objTwo = objOne

// Compare objOne and objTwo
objOne == objTwo
// true

objOne === objTwo
// true
```

The same also applies to arrays. When you create two arrays, with identical content, and try to compare them, they will not be the same. Whether you use abstract or strict equal, the result will be false. The only way to make this work, to make two or more arrays the same, is by using the same way you used previously with JavaScript objects.

You have to create one array and then copy that array it by reference. Then, when you try to copy these new arrays they will be the same. Again, remind yourself about this when you will want to compare arrays based on their content. That test will not be as bulletproof as you thought it will.

```js
// Comparing arrays example no.1: using two arrays
// Create two arrays with the same content
const arrOne = [1, 2, 3]
const arrTwo = [1, 2, 3]

// Compare arrOne and arrTwo
arrOne == arrOne
// false
arrOne === arrOne
// false


// Comparing arrays example no.2: copying one array by reference
// Create one array
const arrOne = [1, 2, 3]
// Copy the first array by reference
const arrTwo = arrOne

// Compare arrOne and arrTwo
arrOne == arrOne
// true
arrOne === arrOne
// true
```

## Conclusion: JavaScript Objects - A Friendly Introduction

Congratulations! You've just finished the second part of this mini series focused on JavaScript objects. I hope you've enjoyed it and learned something new. Before I let you go, let's do a quick recap. Today, you've learned how to loop through JavaScript objects with `for...in` loop, `Object.keys()`, `Object.values()`, `Object.entries()` and `Object.getOwnPropertyNames()`.

Next, you've also learned how to freeze objects, either completely or partially, and are some gotchas you have to pay attention to. Lastly, you've also learned about the fact that JavaScript objects are not created equal, and how to overcome this by copying objects by reference.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Part 1]: https://blog.alexdevero.com/javascript-objects-pt1/
[previous part]: https://blog.alexdevero.com/javascript-objects-pt1/
[iterable objects]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#The_iterable_protocol
[primitive data types]: https://blog.alexdevero.com/javascript-basics-data-types-pt1/

<!--
### Meta:
-
-->

<!--
#### Resources:
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects
- https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Basics
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer
- https://www.digitalocean.com/community/tutorials/understanding-objects-in-javascript
- https://codeburst.io/various-ways-to-create-javascript-object-9563c6887a47
- https://javascript.info/object-methods
- https://stackoverflow.com/questions/1184123/is-it-possible-to-add-dynamically-named-properties-to-javascript-object
- https://stackoverflow.com/questions/208016/how-to-list-the-properties-of-a-javascript-object
- https://www.dofactory.com/tutorial/javascript-objects
- https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object-oriented_JS
- https://medium.com/javascript-in-plain-english/javascript-objects-property-accessors-1458f456e6d
-->
