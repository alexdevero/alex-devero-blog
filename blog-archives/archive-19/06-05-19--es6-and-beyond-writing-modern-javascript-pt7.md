# ES6, ES7, ES8 & Writing Modern JavaScript Pt7 - Async/await & Classes

ES6 classes and async/await are among the most important new features in JavaScript. With ES6 classes, writing object-oriented JavaScript is easier then ever before. The same is true about writing asynchronous JavaScript, thanks to async/await. Learn how to use these two features. Take your JavaScript skills to the next level!<!--more-->
<!--
Table of Contents:
## Async function and await operator
### Enter the hell
### Enter the Promises
### Enter the async/await
### From ES6 to ES8 - The syntax of async/await
### The basics of async/await
### Async/await and errors
## Classes
### The syntax of ES6 classes
### Extending ES6 classes
## Epilogue: ES6, ES7, ES8 & Writing Modern JavaScript Pt7
-->

ES6, ES7, ES8 & Writing Modern JavaScript [Part 1] (Scope, let, const, var).

ES6, ES7, ES8 & Writing Modern JavaScript [Part 2] (Template literals, Destructuring & Default Params).

ES6, ES7, ES8 & Writing Modern JavaScript [Part 3] (Spread, Rest, Sets ).

ES6, ES7, ES8 & Writing Modern JavaScript [Part 4] (Includes, Pads, Loops & Maps).

ES6, ES7, ES8 & Writing Modern JavaScript [Part 5] (WeakMap, WeakSet and Export & Import).

ES6, ES7, ES8 & Writing Modern JavaScript [Part 6] (Arrow Functions & Promises).

## Async function and await operator

If you have a deeper knowledge of JavaScript, especially it asynchronous nature, you are also probably familiar with callbacks. If not, a callback is a function that is executed not immediately, but some time in the future. Callback functions are often required when the results are not immediately available to you.

This is usually not a big problem since you can use the callback function, and wait until you have all data you need. However, what if there is more than just one asynchronous operation? What if you have multiple async operations, one depending on the other? For example, imagine this hypothetical scenario.

### Enter the hell

Let's say that you have an app. This app fetches some data from database. However, before you can use this data, you need to verify it and convert it into different format. When this conversion is completed, the app will display the result(s). The catch is that all these steps are asynchronous, and one depends on the previous one.

Is this scary? What about a scenario where the number of async operations is higher, like three or four times higher. In this situation, callbacks are no longer the best option. You would end up with nesting on so many levels you would need a map or instructions to orient yourself. Put differently, you would end up in a [hell].

```
///
// Callback example:
getData((dataResponse, dataError) => {
  // Verify the data
  verifyData(dataResponse, (verifyResponse, verifyError) => {
    // Convert the data
    convertData((convertResponse, convertError) => {
      // Finally display the data
      displayData(convertResponse, (displayError) => {
        // Handle any exceptions
        console.log(displayError)
      })
    })
  })
})
```

### Enter the Promises

Fortunately, there is the ES6 specification which introduced some handy features to help us deal with similar scenarios. First came [Promises]. Promises work very well. However, they are still not the best and most polished solution. Why? We still have to use callbacks inside every `then()`. Next, we have to use `catch()` for error handling.

Another issue can be working with multiple promises. For example, imagine looping over a number of promises in a sequence to get the data you need, and to get it in the form you need. Easy? Not so much. Fun to do? Definitely not. Case for a headache? Very likely. Better solution?

```
///
// Example of promises:
getData()
  .then(dataResponse => {
    // Verify the data
    return verifyData()
      .then(verifyResponse => {
        // Convert the data
        let convertedData = convertData(verifyResponse)

        return convertedData
      })
      .then(result => {
          // Finally display the data
          displayData(result)
      })
  }).catch(() => {
    // Handle any exceptions
    handleErrors()
  })
```

### Enter the async/await

After ES6 and ES7 came ES8. This specification introduced two features, `async` functions and `await` operator. These two were the solution JavaScript developers were desperately looking for. Asynchronous functions, along with `await`, finally made working with asynchronous code and promises much easier. They marked the end of callback hell.

It is important to mention that async function work on top of promises. They use promises to return the results. Yet, they look more like a normal functions. It is, therefore, better to learn how to work with promises before you start to tinker with `async` functions. So, if you are not good with promises, work on that first.

Another important thing is that `async` function and `await` operator work together. You can use `await` only inside  `async` function. Using it outside will throw an error. And, what is the function, or role of `await` operator? It allows you to pause execution of async function and wait until promise is resolved, either as fulfilled or rejected.

### From ES6 to ES8 - The syntax of async/await

Using async/await is very easy. As I mentioned, you can't use `async` and `await` separately. So, first, you have to use `async` along with a function. This will make the function asynchronous. After that, you can use the `await`, inside that function. There is no limit to how many times you can use `await`. You can use it as many times as you need.

About the syntax. When you declare a standard function, the `async` operator comes at the beginning of the declaration, before the `function` keyword (`async function someFunction() {}`). In the case of [arrow functions], put the `async` operator the equal sign (`=`) and before the parentheses (`const someFunction = async () => {}`).

```
///
// Example of async/await syntax no.1: Standart function
async function someFunction() {
  await ...
}


///
// Example of async/await syntax no.2: Arrow function
const someFunction = async () => {
  await ...
}


///
// Example of async/await syntax no.3: Don't try this
function someFunction() {
  await anotherFunction() // This will throw an error
}
```

That's not all. You can also use `async` functions as methods inside classes or objects. In this scenario, the syntax is similar to a scenario with standard function. The `async` keyword comes before the method name (`async someMethod() {}`). One thing to remember ... Class constructors and getters/setters can't be async.

```
///
// Example of async/await syntax no.4: Object
// As an object's method
const someObj = {
  async anotherFunction() {
    // your code
  }
}


///
// Example of async/await syntax no.5: Class
class SomeClass {
  async anotherFunction() {
    // your code
  }
}
```

Now, let's get back to the hypothetical scenario with app and rendering converted data. Instead of using promises and multiple `then()` methods we can replace this code with `async` function and couple of `await` operators. As you can see on the example below, this will allow us to make the code much cleaner and significantly reduce nesting.

```
///
// Example of async/await no.6:
// Create async function
async function appViewRender() {
  // Use try block
  try {
    // Use await to wait for the data
    const data = await getData()

    // Use await to wait until data is verified
    const verifiedData = await verifyData(data)

    // Use await to wait until data is converted
    const convertedData = await convertData(verifiedData)

    // Finally display the data
    displayData(convertedData)
  } catch(error) {
    // Use catch block to handle any exceptions
    handleErrors()
  }
}
```

### The basics of async/await

As you already know, `async` function always returns a promise. To be more specific, `async` function always returns value via promise and its `resolve()` method. What if there is some problem and the promise is rejected? Then, the `async` function will return a rejected promise. Meaning, `reject()` method with an error will be returned, instead of `resolve()`.

```
///
// Example of async/await no.7: Async function vs regular promise
async function exampleAsyncFunction() {
  return 'Foo'
}

// Async function returns a promise - we can use then()
exampleAsyncFunction.then(console.log)
// Outputs: Foo


///
// The same as using standard function explicitly returning a promise:
function functionWithPromise() {
  return Promise.resolve('Foo')
}

functionWithPromise().then(console.log)
// Outputs: Foo


///
// The same as creating new promise:
const newPromise = () => new Promise((resolve, reject) => {
  resolve('Foo')
  reject('There was a problem with resolving your request.')
})

newPromise().then(console.log)
// Outputs: Foo
```

As you could see on the code example no.6, with `appViewRender()`, we used a couple of `await` operators inside the `async` function. Each of these operators tells the function that the following expression is a promise. And, each of these operators also tells the function to wait until this promise is resolved.

This means that if there is some `await` the function will not proceed to the next expression unless the expression with `await` is resolved. Only when this happens the function will continue evaluating the rest of the code inside the block. What if you use `await` with value that is not a promise?

In that case, it will still end up being a promise. JavaScript will automatically convert it to promise on the fly, using the `resolve()` method. Then, it will be resolved, or rejected, as any other promise.

```
///
// Example of async/await no.8: Await operators, pausing and automatic conversion to promise
async function messageToHall() {
  // Create a time stamp
  console.log(`Stamp one: ${window.performance.now()}`)

  // Create the first part of the message.
  const firstPart = await 'Hello'
  // Automatically converted to promise, to const a = await Promise.resolve('Hello')

  // Pause the function for 2 seconds and then create the second part of the message.
  const secondPart = await new Promise(resolve => setTimeout(
    () => {
      resolve('world')
    }, 2000)
  )

  // Create the third part of the message.
  const thirdPart = await 'Hal!'
  // Automatically converted to promise, to const a = await Promise.resolve('Hal!')

  // Create second time stamp
  console.log(`Stamp two: ${window.performance.now()}`)

  // Return the whole message in correct form
  return `${firstPart} ${secondPart} ${thirdPart}`
}

messageToHall().then(console.log)
// Outputs:
// 'Stamp one: 340.9999999566935'
// 'Stamp two: 2343.899999978021'
// 'Hello world Hal!'
```

As you can see on the time stamps in the code example above, the function was really paused for 2 seconds, by the `setTimeout()` method inside the promise (`const secondPart`). It was only after these 2 seconds the function continued and executed the rest of the code, including the second time stamp.

### Async/await and errors

One great thing on `async` functions is how they handle errors. Thanks to `try ...catch` blocks, error handling is done synchronously. Every promise is resolved, and potential error handled, one by one, without breaking anything. We can demonstrate this on a simple example.

Let's create a function that will return a promise. We will use `Math` to randomly generate either 1 or 0 and use this number to either resolve or reject the promise. Next, let's create `async` function, with [try...catch] statements, that will execute the function with promise, and handle the results.

```
///
// Example of async/await no.9: Async/await and handling errors
// Create function with promise that will be randomly either resolved or rejected
function resolveOrReject() {
  return new Promise((resolve, reject) => {
    // Randomly generate either 1 or 0
    const shouldResolve = Math.round(Math.random() * 1)

    // Resolve or reject the promise based on the value of shouldResolve
    shouldResolve ? resolve('Promise resolved!') : reject('Promise rejected.')
  })
}

// Create async function and use try block to handle case when promise is resolved and catch block when it is rejected
async function myAsyncFunction() {
  try {
    // Execute the resolveOrReject() function
    const result = await resolveOrReject()

    console.log(result)
  } catch(error) {
    // Handle any exceptions
    console.log(error)
  }
}

// Try your luck
myAsyncFunction()
// Outputs: 'Promise rejected.'
myAsyncFunction()
// Outputs: 'Promise resolved!'
myAsyncFunction()
// Outputs: 'Promise resolved!'
myAsyncFunction()
// Outputs: 'Promise rejected.'
myAsyncFunction()
// Outputs: 'Promise rejected.'
myAsyncFunction()
// Outputs: 'Promise resolved!'
```

## Classes

Another big change introduced in ES6 was classes. Before ES6, objects in JavaScript could be created only by using either `new Object()` or function constructor. This is a big difference from other object-oriented programming languages where you would normally use a class. ES6 change it. Now, JavaScript developers can use classes as well.

ES6 classes are similar to another feature introduced in ES6, [arrow functions]. Meaning, it is basically a syntactic sugar. On the background, it is still good old object combined with prototype-based inheritance you know from the past. However, this doesn't mean it is a bad thing, just like in case of arrow functions.

New ES6 classes can make the work of JavaScript developers much easier. The syntax is clearer and cleaner. This is a matter of personal opinion, but I think that classes make it easier for beginners to start with object-oriented JavaScript. Code using ES6 classes seems to me to be more readable than code using objects and prototype-based inheritance.

### The syntax of ES6 classes

The syntax of ES6 classes is simple. You start with `class` keyword followed by the name of the class. Always use uppercase letters for first letter in the name. Then follows the body of the classes wrapped with curly braces (`{}`). Class properties are defined inside `constructor()` method. The `constructor()` method is optional.

If you use `constructor()` it has to come as first, at the top of the class. What follows next are all methods you want the class to have.

```
///
// Classes example no.1: Function constructor vs ES6 class
// Create Person object using function constructor
function Person(name, age, isLiving) {
  this.name = name
  this.age = age
  this.isLiving = isLiving
}

// Add isAlive method to prototype of Person object
Person.prototype.isAlive = function() {
  if (this.isLiving) {
    console.log(`${this.name} is alive.`)
  } else {
    console.log(`${this.name} is dead.`)
  }
}

// Create new instance of Person object
const joe = new Person('Joe', 59, true)

// Check if Joe is alive
joe.isAlive()
// Outputs: 'Joe is alive.'


// Using ES6 class:
// Create Person class
class Person {
  // Define default properties
  constructor(name, age, isLiving) {
    this.name = name
    this.age = age
    this.isLiving = isLiving
  }

  // Create isAlive method to prototype of Person object
  isAlive() {
    if (this.isLiving) {
      console.log(`${this.name} is alive.`)
    } else {
      console.log(`${this.name} is dead.`)
    }
  }
}

// Create new instance of Person class
const anthony = new Person('Anthony', 59, true)

// Check if Anthony is alive
anthony.isAlive()
// Outputs: 'Anthony is alive.'
```

### Extending ES6 classes

Just like classes in other object-oriented programming languages, ES6 classes can also be extended. When you want to create new class by extending existing, you again use the `class` keyword followed by the name of the class. However, the body of the class is preceded by `extends` keyword that is followed by the name of the class you want to extend. Then comes the body, wrapped in curly braces.

When you create class by extending another you must remember to use `super()` method in the `constructor()`. The `super()` method must come as first, right at the top of `constructor()`. Also, if the original class has any properties, and you want the new class to inherit these properties, you must pass them as arguments to both, `constructor()` as well as `super()`.

```
///
// Classes example no.2: Extending classes
// Create Human class
class Human {
  // Define default properties
  constructor(name, age) {
    this.name = name
    this.age = age
  }

  sayHi() {
    console.log(`Hi, I am ${this.name}.`)
  }
}

// Create Woman class by extending Human
class Woman extends Human {
  // Define default properties
  // Pass the name and age properties to constructor() and super() because we want the Woman class to inherit these properties
  constructor(name, age) {
    // Let Woman class inherit name and age properties from human
    super(name, age)

    this.gender = 'female'
  }

  tellYourGender() {
    console.log(`I am a ${this.gender}.`)
  }
}

// Create new instance of Woman class
const jackie = new Woman('Jackie', 26, true)

// Let Jackie introduce herself
jackie.sayHi()
// Outputs: 'Hi, I am Jackie.'

jackie.tellYourGender()
// Outputs: 'I am a female.'


// Create Man class by extending Human
class Man extends Human {
  // Define default properties
  // Pass the name and age properties to constructor() and super() because we want the Man class to inherit these properties
  constructor(name, age) {
    // Let Man class inherit name and age properties from human
    super(name, age)

    this.gender = 'male'
  }

  tellYourGender() {
    console.log(`I am a ${this.gender}.`)
  }
}

// Create new instance of Man class
const johny = new Man('Johny', 31, true)

// Let Johny introduce herself
johny.sayHi()
// Outputs: 'Hi, I am Johny.'

johny.tellYourGender()
// Outputs: 'I am a male.'
```

## Epilogue: ES6, ES7, ES8 & Writing Modern JavaScript Pt7

Congratulations! You've just finished another part of ES6, ES7, ES8 & Writing Modern JavaScript series. Today, you've learned about another two new features, the async/await and classes. Now you know how to use ES6 class to write object-oriented JavaScript. You also know how to make your code asynchronous with async/await, and avoid the callback hell.

Now, take a break and let everything you've learned today settle down. Allow your brain to process everything. After that, once you feel fresh, go through what you have learned today again. Play with the examples. Try them, modify them and then create your own. Remember that practice is the key to really understand anything. So, go and write some code.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Part 1]: https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt1/
[Part 2]: https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt2/
[Part 3]: https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt3/
[Part 4]: https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt4/
[Part 5]: https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt5/
[Part 6]: https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt6/#promise
[hell]: http://callbackhell.com
[Promises]: https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt6/#promise
[arrow functions]: https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt6/#arrow-functions
[try...catch]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch

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
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol
-->
