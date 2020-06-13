# ES6, ES7, ES8 & Writing Modern JavaScript Pt4 - Includes, Pads, Loops & Maps

ES6 made JavaScript better and more mature programming language. It brought many features that made developers' lives easier. This part will help you understand ES6 features such as `includes()`, `padStart()`, `padEnd()`, new loops and also `map()` and ... Map. Explore the world of ES6 and learn how to write Modern JavaScript!

<!--
Table of Contents:
## Array.includes()
## String.padStart() and String.padEnd()
## for...of and for...in loops
## map()
## Map
## Epilogue: ES6, ES7, ES8 & Writing Modern JavaScript Pt4
-->

ES6, ES7, ES8 & Writing Modern JavaScript [Part 1] (Scope, let, const, var).

ES6, ES7, ES8 & Writing Modern JavaScript [Part 2] (Template literals, Destructuring & Default Params).

ES6, ES7, ES8 & Writing Modern JavaScript [Part 3] (Spread, Rest, Sets & Object Literal).


## Array.includes()

If you work often with arrays, you may find this ES6 feature useful. This method called `includes()` provides a fast way to find if an array contains specific item, or value. You don't have to use loops or any other iterators and bloat your work with unnecessary code. Instead, you can use `includes()`, specify the value or item you are looking for and let JavaScript do the rest.

What's more, you can also specify at which index should `includes()` start to look for that value or item. In that case, `includes()` method will not start from the beginning of the array, which is the default. Instead, it will start from the index you specified and ignore all values or items that exist in the array before this index.

As I mentioned, `includes()` method takes the beginning of the array as the default place to start from. This means that the index is optional parameter and you can omit it if you don't use it. The only required parameter is the value or item you are looking for. If the value exists, `includes()` will return `true`. Otherwise, it will return `false`.

```
///
// Includes() example No.1:
const includesExample = ['Ruby', 'JavaScript', 'Python', 'C++', 'Swift', 'Brainfuck']

console.log(includesExample.includes('JavaScript'))
// Outputs: true

console.log(includesExample.includes('C'))
// Outputs: false


///
// Includes() example No.2: Using index parameter
const includesExample = ['Ruby', 'JavaScript', 'Python', 'C++', 'Swift', 'Brainfuck']

console.log(includesExample.includes('Python', 1))
// Outputs: true

console.log(includesExample.includes('Python', 3))
// Outputs: false (Python is on the 2nd index)
```

## String.padStart() and String.padEnd()

The two lesser known string methods introduced in ES6 are `padStart()` and `padEnd()`. However, just because these two are not as known as other ES6 features doesn't mean they may not be useful sometimes. They can. These two methods can help you achieve one specific task in faster and easier way, also using less code.

They way `padStart()` and `padEnd()` work is that they add specific characters to existing string. The `padStart()` adds new characters at the beginning of the string while the `padEnd()` at the end. You specify the amount of characters these methods should add through a  parameter called `targetLength`.

There is one thing you need to remember about this parameter. It is not the length in the terms of the number of characters you want to add. It is the whole length of string you want to change. So, let's say you have a string with eight characters and want to expand this string it with four additional characters using either `padStart()` or `padEnd()`.

In this case, the value you would pass as `targetLength` would be 12 (eight plus additional four characters). And, as I mentioned, the `padStart()` would add the new characters at the beginning, the `padEnd()` would add them at the end. What if you accidentally specify length that is smaller than the length of the original string? Nothing will happen.

JavaScript will return the original string without any change. And, what if you specify only `targetLength` and not what character you want to use? JavaScript will use empty space (` `) as default character.

```
///
// padStart() example No.1:
const padStartExample = 'string'

// Make the original string 18 characters long (add 12 '*' characters)
console.log(padStartExample.padStart(18, '*'))
// Outputs: '************string'


//
// padStart() example No.2: Shorter than the original
const padStartExample = 'string'

// Specify length smaller than the length of the original string
console.log(padStartExample.padStart(4, '*'))
// Outputs: 'string'


//
// padStart() example No.3: No character specified
const padStartExample = 'string'

// Omit the character parameter
console.log(padStartExample.padStart(10))
// Outputs: '    string'


///
// padEnd() example No.1:
const padEndExample = 'string'

// Make the original string 14 characters long (add 4 '*' characters)
console.log(padEndExample.padEnd(12, '*'))
// Outputs: 'string******'


///
// padEnd() example No.2: Shorter than the original
const padEndExample = 'string'

// Specify length smaller than the length of the original string
console.log(padEndExample.padEnd(4, '*'))
// Outputs: 'string'


///
// padEnd() example No.3: No character specified
const padEndExample = 'string'

// Omit the character parameter
console.log(padEndExample.padEnd(13))
// Outputs: 'string       '
```

## for...of and for...in loops

Loops are nothing new in JavaScript. There were loops you could use even before ES6, such as `for`, `while` and `do while`. However, some people were convinced that these were not enough. As a result, ES6 introduced two new loops, `for...of` and `for...in`. Both these loops for all iterable JavaScript objects.

This means, you can use them for objects such as strings, arrays, [Sets] and Maps. There are two differences between `for...of` and `for...in` you need to remember. First, the `for...of` iterates over values that are inside the object. The `for...in` iterates over the [enumerable properties] of an object. Second, `for...in` can also iterate over [object literal].

```
///
// for...in example No.1: Array and enumerable properties
const forInExample = ['bazz', true, 21]

for (let prop in forInExample) {
  // Output all enumerable properties of the array
  console.log(prop)
}

// Outputs:
// '0'
// '1'
// '2'


///
// for...in example No.2: Array and values
const forInExample = ['bazz', true, 21]

for (let prop in forInExample) {
  // Output all enumerable properties of the array
  console.log(forInExample[prop])
}

// Outputs:
// 'bazz'
// 'true'
// '21'


///
// for...in example No.3: Object literal and enumerable properties
const forInExample = {foo: 'bazz', lang: 'JavaScript', x: 13, age: 21}

for (let prop in forInExample) {
  // Output all properties inside the object literal
  console.log(prop)
}

// Outputs:
// 'foo'
// 'lang'
// 'x'
// 'age'


///
// for...in example No.4: Object literal and enumerable properties with values
const forInExample = {foo: 'bazz', lang: 'JavaScript', x: 13, age: 21}

for (let prop in forInExample) {
  // Output all properties as well as their values
  console.log(`Property ${prop} has value of ${forInExample[prop]}.`)
}

// Outputs:
// 'Property foo has value of bazz.'
// 'Property lang has value of JavaScript.'
// 'Property x has value of 13.'
// 'Property age has value of 21.'


///
// for...in example No.5: String
const forInExample = 'JavaScript'

for (let character in forInExample) {
  // Output all characters of the string
  console.log(character)
}

// Outputs:
// '0'
// '1'
// '2'
// '3'
// '4'
// '5'
// '6'
// '7'
// '8'
// '9'


///
// for...in example No.5: String and square bracket notation
const forInExample = 'JavaScript'

for (let character in forInExample) {
  // Output all characters of the string
  console.log(forInExample[character])
}

// Outputs:
// 'J'
// 'a'
// 'v'
// 'a'
// 'S'
// 'c'
// 'r'
// 'i'
// 'p'
// 't'
```

Now, let's use the same set of examples using `for...of`. Well, almost. As I mentioned, `for...of` can't be used with object literal. So, we will have to skip that one. Notice the differences between the example above and below. Especially notice the result of using square bracket notation (`array[prop]`), and the last example with strings. As you can see the `for...in` will return values while `for...of` will return `undefined`.

```
///
// for...of example No.1: Array and values
const forOfExample = ['bazz', true, 21]

for (let prop of forOfExample) {
  // Output all value stored inside the array
  console.log(prop)
}

// Outputs:
// 'bazz'
// 'true'
// '21'


///
// for...of example No.2: Array, values and square bracket notation
const forOfExample = ['bazz', true, 21]

for (let prop of forOfExample) {
  // Output all enumerable properties of the array
  console.log(forOfExample[prop])
}

// Outputs:
// undefined
// undefined
// undefined


///
// for...of example No.3: String
const forOfExample = 'JavaScript'

for (let character of forOfExample) {
  // Output all characters of the string
  console.log(character)
}

// Outputs:
// 'J'
// 'a'
// 'v'
// 'a'
// 'S'
// 'c'
// 'r'
// 'i'
// 'p'
// 't'


///
// for...of example No.4: String and square bracket notation
const forOfExample = 'JavaScript'

for (let character of forOfExample) {
  // Output all characters of the string
  console.log(character)
}

// Outputs:
// undefined
// undefined
// undefined
// undefined
// undefined
// undefined
// undefined
// undefined
// undefined
// undefined
```

_Side note: It might not be a good idea to use `for...in` loop with arrays. The reason is that when `for...in` iterates over an array it may do so in an inconsistent order. Meaning, if you use `for...in` multiple times, you may get the items inside an array in different order. So, if the order of items is important, using either `for...of` or `forEach` will be a better thing to do._

## map()

One feature introduce by ES6, that is very often used by JavaScript developers, is `map()`. This method provides a very simple and quick way to iterate over an array and do something with its content. You specify what you want to do with the content via callback function that you pass into the `map()` method.

The callback method accepts three arguments. These arguments are: 1) the value of current array item, 2) the index of current array item and 3) the whole array over which the map is iterating. Sounds too simple, right? Well, it is simple. That's also probably why `map()` method became so popular.

I mentioned that `map()` is one of the favorite tools of many JavaScript developers. This is especially true for JavaScript developers working with frameworks such as React. In React, `map()` methods are often used for iterating over some data and creating components such as lists (code example no.3).

```
///
// map() example no.1: Array with strings
const mapExample = ['foo', 'bar', 'bazz', 'buzzy']

mapExample.map((arrayItem, index, array) => {
  console.log(`${arrayItem} is on index ${index} in array [${array}].`)
})

// Outputs:
'foo is on index 0 in array [foo,bar,bazz,buzzy].'
'bar is on index 1 in array [foo,bar,bazz,buzzy].'
'bazz is on index 2 in array [foo,bar,bazz,buzzy].'
'buzzy is on index 3 in array [foo,bar,bazz,buzzy].'


///
// map() example no.2: Some simple math
const mapExample = [1, 2, 3, 5, 8, 13, 21]

mapExample.map((arrayItem, index, array) => {
  // Output numbers inside the array as squared
  console.log(Math.pow(arrayItem, 2))
})

// Outputs:
// 1
// 4
// 9
// 25
// 64
// 169
// 441


///
// map() example no.3: React
import React from 'react'
import ReactDOM from 'react-dom'

// Array with some user data
const mapExample = [
  {
    name: 'Joe',
    age: 23,
    id: 1
  },
  {
    name: 'Amanda',
    age: 22,
    id: 2
  },
  {
    name: 'Daryl',
    age: 36,
    id: 3
  }
]

// Create main App component
const App = () => {
  return (
    <ul>
      {/* Use map() to iterate over mapExample and generate list of users */}
      {mapExample.map((arrayItem) => {
        return <li key={arrayItem.id}>{arrayItem.name} ({arrayItem.age})</li>
      })}
    </ul>
  )
}

// Render the App component in DOM
ReactDOM.render(<App />, document.getElementById('root'))
```

## Map

Aside to the `map()` method, ES6 also introduced a Map as an object. Maps can be used to store data in the form of key-value pairs. Similar to arrays, Maps are iterable. However, this is where the similarity ends. Map doesn't have `length` property. When you want to know the amount of items inside the Map, you have to use `size` property. This is similar to [sets].

Another thing that distinguishes Maps from arrays is that Map doesn't have `map()` method. Small paradox. When you want to iterate over Map, you need to use either `for...of`, `for...in` or `forEach` loops. Taking into account what you now know about `for...in`, the safe options are either `for...of` or `forEach`.

When you want to create new Map you have to use the `Map()` constructor. This is another similarity Maps share with sets. And, just like with sets, you can initialize the Map either with values (key-value pairs) or empty, and add values later using `set()` method.

When you create Map with values, remember to wrap them with square brackets (`[]`). Lastly, you can also create a new Map by merging two existing Maps. To do this you can use the [spread operator].

```
///
// Map example no.1: Initializing Map empty and adding values later
const mapExample = new Map()

mapExample.set(0, 'John')
mapExample.set(1, 'Dick')
mapExample.set(2, 'Timothy')

for (let [key, value] of mapExample) {
  console.log(key + ': ' + value)
}

// Outputs:
'0: John'
'1: Dick'
'2: Timothy'


///
// Map example no.2: Initializing Map with values
const mapExample = new Map([[1, 'Sticky'], [2, 'Flocky'], [3, 'Flecky']])

for (let [key, value] of mapExample) {
  console.log(key + ': ' + value)
}

// Outputs:
'0: Sticky'
'1: Flocky'
'2: Flecky'


///
// Map example no.3: Map and forEach loop
const mapExample = new Map([[1, 'Foo'], [2, 'Bar'], [3, 'Bazz']])

mapExample.forEach((value, key) => {
  console.log(key + ': ' + value)
})

// Outputs:
'0: Foo'
'1: Bar'
'2: Bazz'


///
// Map example no.4: Merging Maps with spread operator
// Remember to use different keys!
const mapExampleOne = new Map([[1, 'Foo']])
const mapExampleTwo = new Map([[2, 'Bazz']])

// Merge mapExampleOne and mapExampleTwo into new Map
const mapExampleThree = new Map([...mapExampleOne, ...mapExampleTwo])

mapExampleThree.forEach((value, key) => {
  console.log(key + ': ' + value)
})

// Outputs:
'1: Foo'
'2: Bazz'
```

## Epilogue: ES6, ES7, ES8 & Writing Modern JavaScript Pt4

Congratulations! You've just finished the fourth part of this series. In this part, you've learned about `includes()`, `padStart()`, `padEnd()`, new loops, `map()` and Map. Good job! As you explore the depths of ES6 and modern JavaScript, you get better and better. That being said, you are not at the end, yet. There is still a lot you can learn about ES6.

There is still space for improving your knowledge of JavaScript. So, what's next? In the next part, you will learn about features such as arrow functions, export and import statements, promises, async/await and also about classes. Until then, write some code and practice what you've learned so far.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Part 1]: https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt1/
[Part 2]: https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt2/
[Part 3]: https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt3/
[enumerable properties]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Enumerability_and_ownership_of_properties
[Sets]: https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt3/#sets
[sets]: https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt3/#sets
[spread operator]: https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt3/#spread-operator
[object literal]: https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt3/#object-literal

<!--
### Meta:
-
-->

<!--
#### Resources:
- https://webapplog.com/es6/
- https://zellwk.com/blog/es6/
- https://markpollmann.com/ES6/
- https://www.lifewire.com/best-javascript-es6-features-4579821
- https://github.com/lukehoban/es6features
-->
