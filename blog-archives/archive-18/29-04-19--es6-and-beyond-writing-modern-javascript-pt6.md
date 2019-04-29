# ES6, ES7, ES8 & Writing Modern JavaScript Pt6 - Arrow functions & Promises

Arrow functions, sometimes also called fat arrows, and Promises are two frequently highlighted features of ES6. This part of ES6, ES7, ES8 & Writing Modern JavaScript series will help you learn all you need to know about these two features so you can use them with absolute confidence. Make another step towards the mastery of ES6.<!--more-->
<!--
Table of Contents:
## Arrow functions
### Arrow functions vs functions
### Anything new?
## Promise
### Chaining Promises
### Promises and racing
## Epilogue: ES6, ES7, ES8 & Writing Modern JavaScript Pt6
-->

ES6, ES7, ES8 & Writing Modern JavaScript [Part 1] (Scope, let, const, var).

ES6, ES7, ES8 & Writing Modern JavaScript [Part 2] (Template literals, Destructuring & Default Params).

ES6, ES7, ES8 & Writing Modern JavaScript [Part 3] (Spread, Rest, Sets ).

ES6, ES7, ES8 & Writing Modern JavaScript [Part 4] (Includes, Pads, Loops & Maps).

ES6, ES7, ES8 & Writing Modern JavaScript [Part 5] (WeakMap, WeakSet and Export & Import).

## Arrow functions

Arrow functions are one of my favorite ES6 features. Chances are, you will like them as well. This may be more likely to happen especially if you often work with React. If you have some experience with other programming languages such as C#, Java, you will probably recognize some similarities in syntax with features in these languages.

The same is true if you have experience with [CoffeeScript], language that transcompiles your code to JavaScript, similarly to [TypeScript]. A lot of features in ES6 and later were available in CoffeeScript and TypeScript before they were officially introduced as parts of JavaScript. In other words, CoffeeScript and TypeScript are early adopters of many JavaScript features.

Arrow functions are basically a shorthand for good old JavaScript functions. They use fat arrow syntax (`=>`). This makes them very easy to spot in the code. It is also why some JavaScript developers like to call this ES6 feature "fat arrows". Similarly to regular functions arrow function also support both, block as well as concise bodies.

When you use arrow function with concise body it will automatically return the value of the concise. Meaning, no `return` statement is require. If you use a JavaScript linter, `return` statement may actually trigger a warning. This can transform some of your functions or methods into a one-liner.

The lack of explicit `return` statement is not only benefit of using the concise version of arrow function. Another one is that you don't have to surround the expression with curly braces (`{}`). And, if your functions takes only argument, you can also omit the parenthesis (`()`), required in case of normal JavaScript functions.

If you need or want to use block body, you will need to add the `return` at the end of the block. With that, you will also need to wrap the body inside curly braces (`{}`). Another important thing to remember is that when you want to return an object literal, you have to surround it with parenthesis (`({ key: value })`) (code example no.5).

```
///
// Example no.1: Basic syntax - Arrow function and concise body
// ! Concise body has no explicit return.
// Using parenthesis and curly braces
// (parameter) => { automatically returned code }
// (parameterOne, parameterTwo) => { automatically returned code }
const arrowFuncExOne = (name) => { console.log(`Hi ${name}!`) }
const arrowFuncExTwo = () => { console.log('Hi!') }

arrowFuncExOne('Stuart')
// Outputs: 'Hi Stuart!"'
arrowFuncExTwo()
// Outputs: 'Hi!'

// Or without parenthesis and curly braces
// parameter => code
const arrowFuncExThree = name => console.log(`Hi ${name}!`)

arrowFuncExThree('Tony')
// Outputs: 'Hi Tony!'


// !!!
// ! When there is no parameter, parenthesis are required!
// ! This will not work!
// !!!
const arrowFuncExFour = => console.log(`Hi ${name}!`)

arrowFuncExFour('Doris')
// Outputs: SyntaxError: Unexpected token =>


// This will work
const arrowFuncExFour = () => console.log(`Hi!`)

arrowFuncExFour()
// Outputs: 'Hi!'


// !!!
// ! When there is more than 1 parameter, parenthesis are also required!
// ! This will not work!
// !!!
const arrowFuncExFive = foo, bar => console.log(`Hi ${foo}. My name is ${bar}.`)

arrowFuncExFive('John', 'Jack')
// Outputs: SyntaxError: Missing initializer in const declaration


// This will work
const arrowFuncExFive = (foo, bar) => console.log(`Hi ${foo}. My name is ${bar}.`)

arrowFuncExFive('John', 'Jack')
// Outputs: 'Hi John. My name is Jack.'


///
// Example no.2: Basic syntax - Arrow function with block body
const arrowFuncExSix = () => {
  // ! Block body doesn't return anything automatically, you have to return it explicitly.
  return 'Hello from the flat land.'
}

console.log(arrowFuncExSix())
// Outputs: 'Hello from the flat land.'


// Or, with a parameter
const arrowFuncExSeven = (country) => {
  return `Hello from the ${country}.`
}

console.log(arrowFuncExSeven('Czech Republic'))
// Outputs: 'Hello from the Czech Republic.'


///
// Example no.3: Arrow function inside map
const arrayExample = [1, 5, 9]

arrayExample.map((number) => console.log(number))
// Outputs:
// 1
// 5
// 9


///
// Example no.4: Arrow function and destructuring
const arrayWordsExample = ['Speak', 'Talk', 'Say', 'Discuss']

// Use map to log the length of the words inside the arrayWordsExample array
arrayWordsExample.map(({ length }) => console.log(length))
// Outputs:
// 5
// 4
// 3
// 7

// The same as
const arrayWordsExample = ['Speak', 'Talk', 'Say', 'Discuss']

arrayWordsExample.map((word) => console.log(word.length))
// Outputs:
// 5
// 4
// 3
// 7


///
// Example no.5: Arrow function, destructuring and renaming the variable
const arrayWordsExample = ['Speak', 'Talk', 'Say', 'Discuss']

// Change the 'length' variable to 'lengthOfWords' and log that
arrayWordsExample.map(({ length: lengthOfWords }) => console.log(lengthOfWords))
// Outputs:
// 5
// 4
// 3
// 7


///
// Example no.5: Arrow function and returning an object literal
const arrowFuncExEight = () => ({ name: 'Dogue', age: 25 })

console.log(arrowFuncExEight().name)
// Outputs: 'Dogue'

console.log(arrowFuncExEight().age)
// Outputs: 25

// !!!
// ! This will not work!
// !!!
const arrowFuncExEight = () => { name: 'Dogue', age: 25 }

console.log(arrowFuncExEight().name)
// Outputs: SyntaxError: Unexpected token :
```

### Arrow functions vs functions

The first major difference between arrow functions and classic functions is that arrows share the same lexical `this` as their parent, or the enclosing scope (surrounding code). In other words, arrow functions don't have their own `this`. Put differently, arrow functions don't bind `this`. As a result, you no longer need to use the `var self = this` or something similar, as you may have seen in some code examples (code example no.1).

The second major difference is that you can't use arrow functions as constructors, along with `new` operator. This will result in an error. Third, there is no `arguments` object in arrow function. This means that arrow function will use `arguments` object from its parent, or the enclosing scope (code example no.2).

Aside to these two, there are other differences between arrow functions and classic function, that may not influence you as much as those two previous. For example, arrow functions don't have `prototype` property. You also can't use arrow function as a generator because you can't use `yield` keyword inside its body.

```
///
// Example no.1: Arrow function and 'this'
// 1) Example with inner classic function
// Create FuncThisConstructor constructor
function FuncThisConstructorOne() {
  // Create 'name' property on FuncThisConstructor
  this.name = 'Sindre'

  // Create inner function
  function funcThisInner() {
    // Try to change the value 'name' property
    this.name = 'Johny'

    // Log message after renaming
    console.log('Renamed.')
  }

  // Call funcThisInner()
  funcThisInner()

  // Return the current value of FuncThisConstructor's 'name' property
  return this.name
}

// Create instance of FuncThisConstructorOne constructor
const functInstanceOne = new FuncThisConstructorOne()

// Log the return valued by functInstanceOne
// !!!
// ! Notice that 'name' property has its original value 'Sindre', not 'Johny'
// !!!
console.log(functInstanceOne)
// Outputs:
// "Renamed."
// [object Object] {
//  name: "Sindre"
// }


// 2) Example with inner arrow function
// Create classic function
function FuncThisConstructorTwo() {
  // Create 'name' property on FuncThisConstructor
  this.name = 'Jacky'

  // Create inner arrow (!!!) function
  arrowFuncThisInner = () => {
    // Try to change the value 'name' property
    this.name = 'Doris'

    // Log message after renaming
    console.log('Renamed.')
  }

  // Call arrowFuncThisInner()
  arrowFuncThisInner()

  // Return the current value of FuncThisConstructor's
  return this.name
}

// Create instance of FuncThisConstructorTwo constructor
const functInstanceTwo = new FuncThisConstructorTwo()

// Log the return valued by functInstanceTwo
// !!!
// ! Notice that value of 'name' property has changed from 'Jacky' to 'Doris'
// !!!
console.log(functInstanceTwo)
// Outputs:
// "Renamed."
// [object Object] {
//   name: "Doris"
// }


///
// Example no.2: Arrow function and arguments
// Create arrow function and try to return its 'arguments' object
const arrowFuncArgsOne = () => arguments

// Call arrowFuncArgsOne() and try to log argument object
console.log(arrowFuncArgsOne(2))
// Outputs: TypeError:: arguments is not defined

// Create classic function
function funcArgs(n) {
  // Log argument object of funcArgs()
  console.log(arguments)
  // Outputs:
  // [object Arguments] {
  //   0: 3
  // }

  // Return argument object of arrowFuncArgsTwo()
  // Arguments object of arrowFuncArgsTwo() is equal to arguments of funcArgs()
  const arrowFuncArgsTwo = () => arguments

  // Call arrowFuncArgsTwo()
  return arrowFuncArgsTwo()
}

// Call funcArgs()
console.log(funcArgs(3))
// Outputs:
// [object Arguments] {
//   0: 3
// }
// !!!
// !! Notice that the result is the same as the result of calling 'console.log(arguments)' in funcArgs
// !!!


///
// Example no.3: Arrow function and new operator
// 1) Example with classic function
// Create FuncNew() constructor
function FuncNew() {
  this.message = 'Hi'
}

// Create instance of FuncNew() constructor
const funcNewInstance = new FuncNew()

// Log 'message' property in funcNewInstance, inherited from FuncNew() constructor
console.log(funcNewInstance.message)
// Outputs:
// Hi


// 2) Example with arrow function
// Try to create ArrowFuncNew() constructor
const ArrowFuncNew = () => {
  this.message = 'Hi'
}

// Try to create instance of ArrowFuncNew() constructor
const arrowFuncNewInstance = new ArrowFuncNew()

// Try to log 'message' property in arrowFuncNewInstance, inherited from ArrowFuncNew() constructor
console.log(arrowFuncNewInstance.message)
// Outputs:
// TypeError: ArrowFuncNew is not a constructor


///
// Example no.4: Arrow function and prototype
// 1) Example with classic function
// Create FuncProt() constructor
function FuncProt() {}

// Log the prototype of FuncProt() constructor
console.log(FuncProt.prototype)
// Outputs:
// [object Object] { ... }


// 2) Example with arrow function
// Try to create ArrowFuncProt() constructor
const ArrowFuncProt = () => {}

// Try to log the prototype of ArrowFuncProt() constructor
console.log(ArrowFuncProt.prototype)
// Outputs:
// undefined
```

### Anything new?

One question you may ask is, "are arrow necessary?". The answer is "No" . They are basically just a syntactic sugar, they don't bring any new functionality to JavaScript. However, they make a lot of things simpler, your code cleaner and easier to read and maintain. As a result, they make programming in JavaScript much more enjoyable.

Start using arrow functions and you will soon see how your code is getting smaller and cleaner. All that is good, but aren't arrow functions just a syntactic sugar? Yes, but they have many benefits. They can also make you fall in love with JavaScript, and with programming in general. So, who cares? P.S.: Watch out. They are quite addictive.

## Promise

Promises are another ES6 feature you will probably like. Especially if you like writing asynchronous JavaScript. The beauty of Promises is that they allow you to easily manage asynchronous code without the necessity to create multiple levels of callback functions. Or, without stepping inside the callback hell, as one could call it.

Simply speaking, Promise is a proxy that exist in one of three states. These states are "pending", "fulfilled" (or "resolved") and "rejected". When Promise is resolved, it usually returns some value or data. This is done via `resolve()` function. When it is rejected it usually returns the error, some error message or some data explaining the error.

Return an error is done via `reject()` function. Pending Promise means that the Promise is still running. It was not fulfilled, but it was also not rejected. This can happen for multiple reasons. It may not be caused by some error or bug. For example, it can be due to slow network, waiting for some data, doing some additional operation, etc.

When you want to create a new Promise, you use Promise constructor (`new Promise()`). The `resolve()` and `reject()` are then specified in a callback function passed into the Promise. `resolve`
and `reject` are also parameters for this callback function (`new Promise((resolve, reject) => { code })`).

Although using `resolve()` and `reject()` functions in the callback function is not required the Promise should return something. Otherwise, what's point of using it? And, you should also use the `reject()` function because it can make debugging easier. The `reject()` function is also a good way to provide a feedback.

For example, imagine you have an app or website with login. In this case, when user use wrong email or password, Promise can return an error message notifying the user about the mistake he made. Aside to these two, there is also `finally()` function. This returns a new promise which is resolved when the original promise is resolved. `finally()` is called whether the promise is fulfilled or rejected.

When you want to call the Promise, you use its name and `then()` function. This function returns the data that have been resolved by the Promise. When you write the `then()` function, you should also use `catch()` function. This function will return any error that occurs when you call the Promise. It returns what you specified with the `reject()` function.

```
///
// Example no.1: Simple Promise with setTimeout
// Create new Promise that resolves into a message after 3 seconds
const promiseExampleOne = new Promise((resolve, reject) => {
  setTimeout(function() {
    // Data shown if Promise is fulfilled or resolved
    resolve('Promise has been resolved!')

    // Error, or data, shown if Promise is rejected
    reject('Promise has not been resolved.')
  }, 3000)
})

// Call the Promise and log response when it is fulfilled or resolved (then()) and error message if it is rejected (catch())
promiseExampleOne.then((response) => console.log(response)).catch((error) => console.log(error))
// Outputs (after 3 seconds): 'Promise has been resolved!'

// Or, more readable version
promiseExampleOne
  .then((response) => console.log(response))
  .catch((error) => console.log(error))


///
// Example no.2: Function returning a Promise
function someAsyncFunction() {
  return new Promise((resolve, reject) => {
    setTimeout(function() {
      // Data shown if Promise is fulfilled or resolved
      resolve('Promise has been resolved!')

      // Error, or data, shown if Promise is rejected
      reject('Promise has not been resolved.')
    }, 3000)
  })
}

// Call someAsyncFunction() and log the response, or any potential error
someAsyncFunction().then((response) => {
  console.log(response)
}).catch((error) => {
  console.log(error)
})
```

### Chaining Promises

This is not everything this cool ES6 feature can do. You can also chain Promises together. You can do this by using multiple `then()` functions. In this case, the value returned by the first `then()` function will become the value available to the next `then()` function in the chain. You can then return it again for another `then()`.

This option, to create basically infinite chain of Promises, is one the main advantage of this ES6 feature. It is also the way Promises can help you avoid the callback hell. You will no longer need to nest one callback function into another. Instead, you can use Promise and return what you need from one `then()` function to another as long as you need.

```
///
// Example: Chaining Promises
const promiseExample = new Promise((resolve, reject) => {
  // Do some asynchronous task(s)
  resolve(data)

  reject('There was a problem with your request')
})

promiseExample.then(resolvedData => {
  console.log('Server responded with' + resolvedData)

  const updatedData = resolvedData + additionalData

  // Pass the updated result to the next then() function
  // The name of the returned variable doesn't matter
  // In the next then(), you can use any variable name you want
  return updatedData
}).then(foo => {
  // Do something
  console.log(foo)
}).then(bar => {
  console.log(bar)
}).then(bazz => {
  console.log(bazz)
}).catch((error) => {
  console.log(error)
})
```

### Promises and racing

Chaining is not the only thing Promises can do. There is something else you can do in ES6. Imagine you have a number of Promises and you need to wait before all of them are fulfilled. In this case, you can call `all()` function on `Promise` object, passing all Promises as an argument, in the form of an array.

When all Promises are resolved , the `all()` function will return all resolved data in the form of an array. This data, inside the array, are in the same order as you passed the Promises to the `all()` function. As always, you can then use `then()` to get this array of data and do whatever you want or need with it.

Another thing you can do in ES6 is that you can wait only for one Promise that is resolved, instead of all of them. To do this, you use `race()` function. Similarly to `all()`, you will again call this function on `Promise` object, passing array of Promises as an argument. Since `race()` resolves when the first Promise is resolved, it will return a single value, and not an array like `all()`.

```
///
// Example no.1: Promises and all()
const promiseOne = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('I am promiseOne.')
  }, Math.floor(Math.random() * 10))
})

const promiseTwo = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('I am promiseTwo.')
  }, Math.floor(Math.random() * 10))
})

const promiseThree = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('I am promiseThree.')
  }, Math.floor(Math.random() * 10))
})

const promiseFour = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('I am promiseFour.')
  }, Math.floor(Math.random() * 10))
})

// Wait until all Promises are resolved and return the resolved values
Promise.all([promiseOne, promiseTwo, promiseThree, promiseFour]).then(value => {
  // Log all resolved values
  console.log(value)
  // Outputs: ['I am promiseOne', 'I am promiseTwo', 'I am promiseThree', 'I am promiseFour']

  // Log value resolved by promiseOne
  console.log(value[0])
  // Outputs: 'I am promiseOne.'

  // Log value resolved by promiseTwo
  console.log(value[1])
  // Outputs: 'I am promiseTwo.'

  // Log value resolved by promiseThree
  console.log(value[2])
  // Outputs: 'I am promiseThree.'

  // Log value resolved by promiseFour
  console.log(value[3])
  // Outputs: 'I am promiseFour.'
})


///
// Example no.2: Promises and race()
const promiseOne = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('I am promiseOne.')
  }, Math.floor(Math.random() * 10))
})

const promiseTwo = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('I am promiseTwo.')
  }, Math.floor(Math.random() * 10))
})

const promiseThree = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('I am promiseThree.')
  }, Math.floor(Math.random() * 10))
})

// Wait until the first Promises is resolved and return its resolved value
Promise.race([promiseOne, promiseTwo, promiseThree]).then(value => {
  // Log the resolved value from the winning Promise
  console.log(value)
  // Outputs: ¯\_(ツ)_/¯
})
```

## Epilogue: ES6, ES7, ES8 & Writing Modern JavaScript Pt6

Another part of ES6, ES7, ES8 & Writing Modern JavaScript series is behind you. Today you've learned the nuts and bolts of two ES6 features. These two features were arrow functions and Promises. Now, after finishing this part, you know how these two hot ES6 features work and how to use them in your work and projects.

In the next part you will learn about ES6 features such as async function and await operator, classes and generators. Until then, take some time, revisit what you've learned today and practice. Make sure you fully understand everything. Remember, only deliberate practice can help you really master anything. So, write some code.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Part 1]: https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt1/
[Part 2]: https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt2/
[Part 3]: https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt3/
[Part 4]: https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt4/
[Part 5]: https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt5/
[CoffeeScript]: https://coffeescript.org
[TypeScript]: https://www.typescriptlang.org

<!--
#### Meta:
-
-->

<!--
#### Inspiration:
- https://webapplog.com/es6/
- https://zellwk.com/blog/es6/
- https://markpollmann.com/ES6/
- https://www.lifewire.com/best-javascript-es6-features-4579821
- https://github.com/lukehoban/es6features
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol
-->
