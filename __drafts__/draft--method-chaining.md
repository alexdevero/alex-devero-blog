# What Method Chaining in JavaScript Is, How It Works and How to Use It

Method chaining is popular method that can help you write more concise and readable code. In this tutorial, you will learn what method chaining in JavaScript is and how it works. You will also learn how to use method chaining to improve the quality and readability of your code.<!--more-->
<!--
Table of Contents:
## A quick introduction to method chaining in JavaScript
### Examples of method chaining
## How method chaining in JavaScript works
## How to implement method chaining in JavaScript
## Methods, chaining, this and arrow functions
## Method chaining and classes
## Conclusion: What method chaining in JavaScript is, how it works and how to use it
-->

## A quick introduction to method chaining in JavaScript

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

## How method chaining in JavaScript works

You know how method chaining looks like. The more important question is, how it works. The answer is very simple. It works because of `this`. Yes, we are talking about the notorious [this] keyword. When it comes to `this` there is [a lot] one can learn. To keep this tutorial short, let's not get too deep and keep it simple instead.

Let's say you have an object. If you use `this` inside that object it will refer to that object. If you then create an instance, or copy, of that object, `this` will refer to that instance or copy. When you work with some string or array method you are working with an object.

```JavaScript
const myObj = {
  name: 'Stuart',
  age: 65,
  sayHi() {
    // This here refers to myObj
    return `Hi my name is ${this.name}.`
  },
  logMe() {
    console.log(this)
  }
}

myObj.sayHi()
// Output:
// 'Hi my name is Stuart.'

myObj.logMe()
// Output:
// {
//   name: 'Stuart',
//   age: 65,
//   sayHi: ƒ,
//   logMe: ƒ
// }
```

In case of a string you are working with a primitive [data type]. However, the method you are using, such as `toLowerCase()`, exists on the prototype of a `String` object. Having a new method on some object is not enough to make chaining work. There is one critical ingredient, the `this`.

For chaining to work, a method must return the object it works with. It has to return the `this`. Think about this as a baton. There are some runners on the field in different positions. However, they can't all run at once. Only one can run at the time. When currently running runner completes his part, he has to pass the baton to the next runner.

Only when this happens, when the next runner receives the baton, can he run his part. In our case, each method is a runner. The baton is returned `this`, the object the method is working with. If there is not baton, no `this` returned, next runner can't run and chaining will not work.

## How to implement method chaining in JavaScript

That was about the theory. Now, to practice. So, in order to make chaining work you need three things. First, you need some object. Second, that object needs some methods you can later call. Third, these methods have to return the object itself. They have to return the `this` if you want to make them chainable.

Let's create a simple object as a metaphor for a person. This person will have few properties: `name`, `age` and `state`. The `state` will specify in what state the person currently is. To change this state, there will be few methods: `walk()`, `sleep()`, `eat()`, `drink()`, `work()` and `exercise()`.

Since we want all these method to be chainable they all have to return `this` in the very end. There will be also one utility method. This method will log the current state to console. When you use one of the methods to change person's state, it will also call this method will so you can see the new state in console.

```JavaScript
// Create person object.
const person = {
  name: 'Jack Doer',
  age: 41,
  state: null,
  logState() {
    console.log(this.state)
  },
  drink() {
    // Change person's state.
    this.state = 'Drinking.'

    // Log current person's state.
    this.logState()

    // Return this to make the method chainable.
    return this
  },
  eat() {
    // Change person's state.
    this.state = 'Eating.'

    // Log current person's state.
    this.logState()

    // Return this to make the method chainable.
    return this
  },
  exercise() {
    // Change person's state.
    this.state = 'Exercising.'

    // Log current person's state.
    this.logState()

    // Return this to make the method chainable.
    return this
  },
  sleep() {
    // Change person's state.
    this.state = 'Sleeping.'

    // Log current person's state.
    this.logState()

    // Return this to make the method chainable.
    return this
  },
  walk() {
    // Change person's state.
    this.state = 'Walking.'

    // Log current person's state.
    this.logState()

    // Return this to make the method chainable.
    return this
  },
  work() {
    // Change person's state.
    this.state = 'Working.'

    // Log current person's state.
    this.logState()

    // Return this to make the method chainable.
    return this
  }
}

// Let's have some fun.
person
  .drink() // Output: 'Drinking.'
  .exercise() // Output: 'Exercising.'
  .eat() // Output: 'Eating.'
  .work() // Output: 'Working.'
  .walk() // Output: 'Walking.'
  .sleep() // Output: 'Sleeping.'

// Alternative on a single line:
person.drink().exercise().eat().work().walk().sleep()
// Output:
// 'Drinking.'
// 'Exercising.'
// 'Eating.'
// 'Working.'
// 'Walking.'
// 'Sleeping.'
```

## Methods, chaining, this and arrow functions

The necessity to work with `this` also means one thing. You can't create chainable methods with [arrow functions]. The reason is that, in arrow functions, `this` is not bound to the instance of object. `this` will refer to the global object `window`. If you try to return `this` it will return `window`, not the object itself.

Another issue would be accessing and changing object properties from the inside of the arrow function. Since `this` would be global object `window` you could not use it to reference the object and then its property. You would be trying to reference `window` and its property.

There is a way to bypass this, if you insist on using arrow functions. Instead of using `this` to reference the object you would have to reference the object by its name directly. You would have to replace all occurrences of `this` inside arrow functions with the object name.

```JavaScript
// Create person object.
const person = {
  name: 'Jack Doer',
  age: 41,
  state: null,
  logState() {
    console.log(this.state)
  },
  drink: () => {
    person.state = 'Drinking.'

    person.logState()

    return person
  },
  eat: () => {
    person.state = 'Eating.'

    person.logState()

    return person
  },
  exercise: () => {
    person.state = 'Exercising.'

    person.logState()

    return person
  },
  sleep: () => {
    person.state = 'Sleeping.'

    person.logState()

    return person
  },
  walk: () => {
    person.state = 'Walking.'

    person.logState()

    return person
  },
  work: () => {
    person.state = 'Working.'

    person.logState()

    return person
  }
}

// Let's have some fun.
person
  .drink() // Output: 'Drinking.'
  .exercise() // Output: 'Exercising.'
  .eat() // Output: 'Eating.'
  .work() // Output: 'Working.'
  .walk() // Output: 'Walking.'
  .sleep() // Output: 'Sleeping.'
```

One potential downside of this is that you would also loose all flexibility. If you copy the object, all arrow functions will still be hard-wired to the original object. This will happen if you create the copy with both, [Object.assign()] and [Object.create()].

```JavaScript
// Create original person object.
const person = {
  name: 'Jack Doer',
  age: 41,
  state: null,
  logState() {
    // Log the whole object.
    console.log(this)
  },
  drink: () => {
    person.state = 'Drinking.'

    person.logState()

    return person
  },
  eat: () => {
    person.state = 'Eating.'

    person.logState()

    return person
  }
}

// Let person eat.
person.eat()
// Output:
// {
//   name: 'Jack Doer',
//   age: 41,
//   state: 'Eating.',
//   logState: ƒ,
//   drink: ƒ,
//   eat: ƒ
// }

// Create new object based on person object.
const newPerson = new Object(person)

// Change the "name" and "age" properties.
newPerson.name = 'Jackie Holmes'
newPerson.age = 33

// Let newPerson drink.
// This will print Jack Doer not Jackie Holmes.
newPerson.drink()
// Output:
// {
//   name: 'Jack Doer',
//   age: 41,
//   state: 'Drinking.',
//   logState: ƒ,
//   drink: ƒ,
//   eat: ƒ
// }
```

However, the problem above will not happen if you use [Object()] constructor. If you use the `Object()` constructor, with `new` keyword, you will create that new object as an independent copy. When you use some method on that copy it will have effect only on that copy, not the original.

```JavaScript
// Create original person object.
const person = {
  name: 'Jack Doer',
  age: 41,
  state: null,
  logState() {
    // Log the whole object.
    console.log(this)
  },
  drink: () => {
    person.state = 'Drinking.'

    person.logState()

    return person
  },
  eat: () => {
    person.state = 'Eating.'

    person.logState()

    return person
  }
}

// Let person eat.
person.eat()
// Output:
// {
//   name: 'Jack Doer',
//   age: 41,
//   state: 'Eating.',
//   logState: ƒ,
//   drink: ƒ,
//   eat: ƒ
// }

// Create new object based on person object.
const newPerson = new Object(person)

// Change the "name" and "age" properties.
newPerson.name = 'Jackie Holmes'
newPerson.age = 33

// Let newPerson drink.
newPerson.drink()
// Output:
// {
//   name: 'Jackie Holmes',
//   age: 33,
//   state: 'Drinking.',
//   logState: ƒ,
//   drink: ƒ,
//   eat: ƒ
// }
```

So, if you insist on using arrow functions, and want to copy objects? It will be better to create those copies with `Object()` constructor and `new` keyword. Otherwise, spare yourself the hustle and just use [regular functions].

## Method chaining and classes

Are a fan of [JavaScript classes]? Then, I have some good news for you. You can use method chaining in JavaScript also if you prefer to work with classes. The process is the same as with object, only the syntax is a bit different. The important thing is that every method that should be chainable must return `this`.

```JavaScript
// Create Person class.
class Person {
  constructor(name, age) {
    this.name = name
    this.age = age
    this.state = null
  }

  logState() {
    console.log(this.state)
  }

  drink() {
    this.state = 'Drinking.'

    this.logState()

    return this
  }

  eat() {
    this.state = 'Eating.'

    this.logState()

    return this
  }

  sleep() {
    this.state = 'Sleeping.'

    this.logState()

    return this
  }
}

// Create instance of Person class.
const joe = new Person('Joe', 55)

// Use method chaining.
joe
  .drink() // Output: 'Drinking.'
  .eat() // Output: 'Eating.'
  .sleep() // Output: 'Sleeping.'
```

## Conclusion: What method chaining in JavaScript is, how it works and how to use it

Method chaining is one simple method that can be quite useful. It can help you write code that is shorter and more readable. I hope that this tutorial helped you understand what method chaining in JavaScript is and how it works. Now, it is up to you to use what you've learned about method chaining in your code.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[[create a promise]: https://blog.alexdevero.com/javascript-promises/#creating-a-promise
[handler functions]: https://blog.alexdevero.com/javascript-promises/#handling-javascript-promises-with-handler-functions
[async function]: https://blog.alexdevero.com/javascript-async-await/#async-functions
[await]: https://blog.alexdevero.com/javascript-async-await/#the-await-keyword
[this]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this
[a lot]: https://blog.alexdevero.com/this-in-javascript-works/
[data type]: https://blog.alexdevero.com/javascript-basics-data-types-pt1/
[arrow functions]: https://blog.alexdevero.com/javascript-arrow-functions/
[Object.assign()]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign
[Object.create()]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/create
[Object()]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/Object
[regular functions]: https://blog.alexdevero.com/javascript-functions-pt1/
[JavaScript classes]: https://blog.alexdevero.com/javascript-classes-pt1/

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
