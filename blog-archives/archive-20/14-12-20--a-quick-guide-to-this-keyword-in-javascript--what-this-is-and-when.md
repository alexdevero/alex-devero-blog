# A Quick Guide To this Keyword In JavaScript: What this Is And When

Many JavaScript developers try to avoid using the `this` keyword. One reason is that what `this` refers to changes. This guide will help you with it. You will learn what `this` keyword refers to in specific contexts. This will make it easier for you to work with it and help you predict what to expect when you use it.<!--more-->
<!--
Table of Contents:
## Quick introduction
## Strict and sloppy mode
## Global scope
## Functions
### Strict mode
### Immediately Invoked Function Expression (IIFE)
### Function constructors
## Objects and methods
## Classes
## Event listeners
## Arrow functions
### Global and local scope, this and arrow functions
### Arrow IIFEs
### Objects, classes, this and arrow functions
### Event listeners, this and arrow functions
## Conclusion: A quick guide to this keyword in JavaScript
-->

## Quick introduction

The `this` is a special keyword in JavaScript. There is one problem JavaScript developers struggle with when they learn about `this`. It can have different values. It can refer to different things. What determines what `this` refers to is context, the context at which you use it. Let's take a look at these contexts and what to expect from `this` keyword in each of them.

## Strict and sloppy mode

In JavaScript, there are two modes or variants of JavaScript you can work with. The first one is [strict mode]. The second one is [sloppy mode]. By default, you write your JavaScript code in a sloppy mode. This mode is more ... sloppy. It allows you to do things that would be [forbidden] in a strict mode. These things would not work.

JavaScript offers you an option to switch from sloppy mode to strict mode. You can do this by using `'use strict'` statement at the beginning of your code. Any code that follows after this statement will automatically follow the rules and restrictions of strict mode. This also includes the `this` keyword.

## Global scope

When you are in a global scope, the `this` keyword will refer to the global object `window`. This is the case at least if you are in the browser. If you are in a Node.js environment, the `this` will refer to global object called `global`. In a global scope, it doesn't matter if you are in a sloppy mode or a strict mode.

```JavaScript
// Global context example no.1: sloppy mode
console.log(this)
// Output:
// Window {0: Window, 1: Window, window: Window, self: Window, document: document, name: "", location: Location, …}

// In Node.js:
console.log(this)
// Output:
// <ref *1> Object [global] {
//   global: [Circular *1],
//   clearInterval: [Function: clearInterval],
//   clearTimeout: [Function: clearTimeout],
//   setInterval: [Function: setInterval],
//   setTimeout: [Function: setTimeout] {
//     [Symbol(nodejs.util.promisify.custom)]: [Getter]
//   },
//   queueMicrotask: [Function: queueMicrotask],
//   clearImmediate: [Function: clearImmediate],
//   setImmediate: [Function: setImmediate] {
//     [Symbol(nodejs.util.promisify.custom)]: [Getter]
//   }
// }


// Global context example no.2: strict mode
// Switch to strict mode.
'use strict'

console.log(this)
// Output:
// Window {0: Window, 1: Window, window: Window, self: Window, document: document, name: "", location: Location, …}

// In Node.js:
console.log(this)
// Output:
// <ref *1> Object [global] {
//   global: [Circular *1],
//   clearInterval: [Function: clearInterval],
//   clearTimeout: [Function: clearTimeout],
//   setInterval: [Function: setInterval],
//   setTimeout: [Function: setTimeout] {
//     [Symbol(nodejs.util.promisify.custom)]: [Getter]
//   },
//   queueMicrotask: [Function: queueMicrotask],
//   clearImmediate: [Function: clearImmediate],
//   setImmediate: [Function: setImmediate] {
//     [Symbol(nodejs.util.promisify.custom)]: [Getter]
//   }
// }
```

## Functions

When it comes to [functions], the mode at which you are makes a difference for the `this` keyword. When you are in sloppy mode, `this` will refer to the global object `window`. Global object `global` in Node.js. This is true even for functions declared inside another functions, in a local scope.

```JavaScript
// Function example no.1: function in a global scope
// Declare a function.
function foo() {
  // Log the value of this
  console.log(this)
  console.log(this === window)
}

// Invoke foo() function.
foo()
// Output:
// Window {0: Window, 1: Window, window: Window, self: Window, document: document, name: "", location: Location, …}
// true


// Function example no.2: function in a local scope
// Declare a function.
function foo() {
  return function bar() {
    // Log the value of this
    console.log(this)
    console.log(this === window)
  }
}

// Invoke foo() and bar() functions.
foo()()
// Output:
// Window {0: Window, 1: Window, window: Window, self: Window, document: document, name: "", location: Location, …}
// true
```

### Strict mode

This will change if you switch your JavaScript code to strict mode. In a strict mode, the default value of `this` in a function is set to `undefined`.

```JavaScript
// Strict mode example no.1: function in a global scope
// Switch to strict mode.
'use strict'

// Declare a function.
function foo() {
  // Log the value of this
  console.log(this)
  console.log(this === window)
}

// Invoke foo() function.
foo()
// Output:
// undefined
// false


// Strict mode example no.2: function in a local scope
// Switch to strict mode.
'use strict'

// Declare a function.
function foo() {
  return function bar() {
    // Log the value of this
    console.log(this)
    console.log(this === window)
  }
}

// Invoke foo() and bar() functions.
foo()()
// Output:
// undefined
// false
```

### Immediately Invoked Function Expression (IIFE)

The `this` keyword works in IIFEs like in regular functions. In a sloppy mode, `this` will refer to the global object `window`. If you switch to a strict the value of `this` will become `undefined`.

```JavaScript
// IIFE example no.1: sloppy mode
// Declare IIFE.
(function() {
  console.log(this)
  console.log(this === window)
})()
// Output:
// Window {0: Window, 1: Window, window: Window, self: Window, document: document, name: "", location: Location, …}
// true


// IIFE example no.2: strict mode
// Switch to strict mode.
'use strict';

// Declare IIFE.
(function() {
  console.log(this)
  console.log(this === window)
})()
// Output:
// undefined
// false
```

### Function constructors

When you want to create new functions with similar behavior you can use [function constructor]. This allows you to create a blueprint you can then use for your functions. If you use function constructor remember one thing. The `this` keyword inside a constructor will refer to the instance of that constructor, not the constructor itself. This applies to both, sloppy and strict mode.

```JavaScript
// Function constructors example no.1: sloppy mode
// Create function constructor Person.
function Person(name, age) {
  this.name = name
  this.age = age

  this.readPerson = function() {
    console.log(this)
  }
}

// Create joe instance.
const joe = new Person('Joe', 31)

// Create natalie instance.
const natalie = new Person('Natalie', 28)

// Invoke readPerson() method on joe instance.
joe.readPerson()
// Output:
// Person {
//   name: 'Joe',
//   age: 31,
//   readPerson: ƒ (),
//   __proto__: Person { constructor: ƒ Person() }
// }

// Invoke readPerson() method on natalie instance.
natalie.readPerson()
// Output:
// Person {
//   name: 'Natalie',
//   age: 28,
//   readPerson: ƒ (),
//   __proto__: Person { constructor: ƒ Person() }
// }


// Function constructors example no.2: strict mode
// Switch to strict mode.
'use strict'

// Create function constructor Person.
function Person(name, age) {
  this.name = name
  this.age = age

  this.readPerson = function() {
    console.log(this)
  }
}

// Create joe instance.
const joe = new Person('Joe', 31)

// Create natalie instance.
const natalie = new Person('Natalie', 28)

// Invoke readPerson() method on joe instance.
joe.readPerson()
// Output:
// Person {
//   name: 'Joe',
//   age: 31,
//   readPerson: ƒ (),
//   __proto__: Person { constructor: ƒ Person() }
// }

// Invoke readPerson() method on natalie instance.
natalie.readPerson()
// Output:
// Person {
//   name: 'Natalie',
//   age: 28,
//   readPerson: ƒ (),
//   __proto__: Person { constructor: ƒ Person() }
// }
```

## Objects and methods

When you use `this` keyword in an object method, the result can vary. What matters is if the method is a regular function or an arrow function. You will learn about `this` and arrow functions later. For now, let's focus on regular functions.

When you use `this` in an object method, it will refer to the object itself. This is for both, sloppy as well as strict mode.

```JavaScript
// Object example no.1: sloppy mode
const myObj = {
  name: 'Jack',
  age: 30,
  readObj() {
    console.log(this)
  }
}

// Invoke the readObj() method on myObj.
myObj.readObj()
// Output:
// { name: 'Jack', age: 30, readObj: ƒ readObj() }


// Object example no.2: strict mode
// Switch to strict mode.
'use strict'

const myObj = {
  name: 'Jack',
  age: 30,
  readObj() {
    console.log(this)
  }
}

// Invoke the readObj() method on myObj.
myObj.readObj()
// Output:
// { name: 'Jack', age: 30, readObj: ƒ readObj() }
```

## Classes

[JavaScript classes] are a newer addition to JavaScript. They are definitely one of those more discussed features. Some developers like to use them and some not. If you like using them, or want to start using them, you will like what follows. When it comes to classes, the `this` keyword is very consistent and predictable.

It doesn't matter if you are in a sloppy mode or a strict mode. If you use `this` in a class it will refer to the class itself.

```JavaScript
// Classes example no.1: with instantiation in sloppy mode (regular function, no binding)
// Declare a class with public property and method.
class Person {
  constructor(name) {
    this.name = name
  }

  sayHi() {
    console.log(this)
  }
}

// Instantiate the Person class.
const joshua = new Person('Joshua')

// Invoke sayHi() on "joshua" instance.
joshua.sayHi()
// Output:
// Person {name: "Joshua"}


// Classes example no.2: with instantiation in sloppy mode (arrow function)
// Declare a class with public property and method.
class Person {
  constructor(name) {
    this.name = name
  }

  sayHi = () => {
    console.log(this)
  }
}

// Instantiate the Person class.
const joshua = new Person('Joshua')

// Invoke sayHi() on "joshua" instance.
joshua.sayHi()
// Output:
// Person {name: "Joshua", sayHi: ƒ}


// Classes example no.3: with instantiation in strict mode (regular function, no binding)
// Switch to strict mode.
'use strict'

// Declare a class with public property and method.
class Person {
  constructor(name) {
    this.name = name
  }

  sayHi() {
    console.log(this)
  }
}

// Instantiate the Person class.
const joshua = new Person('Joshua')

// Invoke sayHi() on "joshua" instance.
joshua.sayHi()
// Output:
// Person {name: "Joshua"}


// Classes example no.4: with instantiation in strict mode (arrow function)
// Switch to strict mode.
'use strict'

// Declare a class with public property and method.
class Person {
  constructor(name) {
    this.name = name
  }

  sayHi = () => {
    console.log(this)
  }
}

// Instantiate the Person class.
const joshua = new Person('Joshua')

// Invoke sayHi() on "joshua" instance.
joshua.sayHi()
// Output:
// Person {
//   sayHi: ƒ (),
//   name: 'Joshua',
//   __proto__: Person { constructor: ƒ Person() }
// }


// Classes example no.5: without instantiation in sloppy mode (regular function, no binding)
// Declare a class with static property and method.
class Person {
  static name = 'Luke'
  static sayHi() {
    console.log(this)
    console.log(this === Person)
  }
}

// Invoke sayHi() method.
Person.sayHi()
// Output:
// class Person {
//   static name = 'Luke'
//   static sayHi() {
//     console.log(this)
//     console.log(this === Person)
//   }
// }
// true


// Classes example no.6: without instantiation in sloppy mode (arrow function)
// Declare a class with static property and method.
class Person {
  static name = 'Luke'
  static sayHi = () => {
    console.log(this)
    console.log(this === Person)
  }
}

// Invoke sayHi() method.
Person.sayHi()
// Output:
// class Person {
//   static name = 'Luke'
//   static sayHi = () => {
//     console.log(this)
//     console.log(this === Person)
//   }
// }
// true


// Classes example no.7: without instantiation in strict mode (regular function, no binding)
// Switch to strict mode.
'use strict'

// Declare a class with static property and method.
class Person {
  static name = 'Luke'
  static sayHi() {
    console.log(this)
    console.log(this === Person)
  }
}

// Invoke sayHi() method.
Person.sayHi()
// Output:
// class Person {
//   static name = 'Luke'
//   static sayHi() {
//     console.log(this)
//     console.log(this === Person)
//   }
// }
// true


// Classes example no.8: without instantiation in strict mode (arrow function)
// Switch to strict mode.
'use strict'

// Declare a class with static property and method.
class Person {
  static name = 'Luke'
  static sayHi = () => {
    console.log(this)
    console.log(this === Person)
  }
}

// Invoke sayHi() method.
Person.sayHi()
// Output:
// class Person {
//   static name = 'Luke'
//   static sayHi = () => {
//     console.log(this)
//     console.log(this === Person)
//   }
// }
// true
```

## Event listeners

When you use the `this` keyword with event listeners, it will refer to the HTML element to which you attach the event listener. If you attach event listener to a button, `this` will refer to that button element. That button will become value of `this`. If you attach event listener to global `window` object, `this` will refer to the global `window` object.

```JavaScript
// Event listener example no.1: sloppy mode
// Find button in the DOM.
const btn = document.querySelector('.btn')

// Attach event listener to the button.
btn.addEventListener('click', function() {
  console.log(this)
  console.log(this === window)
})

// Output on click on the button:
// <button>Click me</button>
// false


// Arrow function example no.2: strict mode
// Switch to strict mode.
'use strict'

// Find button in the DOM.
const btn = document.querySelector('.btn')

// Attach event listener to the button.
btn.addEventListener('click', function() {
  console.log(this)
  console.log(this === window)
})

// Output on click on the button:
// <button>Click me</button>
// false


// Arrow function example no.3: event listener on window
// Attach event listener to the button.
window.addEventListener('click', function() {
  console.log(this)
  console.log(this === window)
})

// Output on click on the button:
// Window {0: Window, 1: Window, window: Window, self: Window, document: document, name: "", location: Location, …}
// true
```

## Arrow functions

With [arrow functions], `this` keyword works differently than with regular functions. Arrow functions don't have their own `this`. When you use `this` in an arrow function it will inherit its value from its context. Context here is the context at which you defined that arrow function.

### Global and local scope, this and arrow functions

If your arrow function is in a global scope, `this` will refer to the global object `window`. This is true for sloppy and strict mode. It is also true if the arrow function is inside a regular function, in a sloppy mode. If you are in a strict mode, and arrow function is inside a regular function, the value of `this` will be `undefined`.

```JavaScript
// Arrow function example no.1: global function in a sloppy mode
// Declare an arrow function.
const foo = () => {
  // Log the value of this.
  console.log(this)
  console.log(this === window)
}

// Invoke foo() and bar() functions.
foo()
// Output:
// Window {0: Window, 1: Window, window: Window, self: Window, document: document, name: "", location: Location, …}
// true


// Arrow function example no.2: global function in a strict mode
// Switch to strict mode.
'use strict'

// Declare a function.
const foo = () => {
  // Log the value of this.
  console.log(this)
  console.log(this === window)
}

// Invoke foo() and bar() functions.
foo()
// Output:
// Window {0: Window, 1: Window, window: Window, self: Window, document: document, name: "", location: Location, …}
// true


// Arrow function example no.3: local function in a sloppy mode
// Declare a regular function.
function foo() {
  // Return an arrow function.
  return () => {
    // Log the value of this.
    console.log(this)
    console.log(this === window)
  }
}

// Invoke foo() and bar() functions.
foo()()
// Output:
// Window {0: Window, 1: Window, window: Window, self: Window, document: document, name: "", location: Location, …}
// true


// Arrow function example no.4: local function in a strict mode
// Switch to strict mode.
'use strict'

// Declare a regular function.
function foo() {
  // Return an arrow function.
  return () => {
    // Log the value of this.
    console.log(this)
    console.log(this === window)
  }
}

// Invoke foo() and bar() functions
foo()()
// Output:
// undefined
// false
```

### Arrow IIFEs

When you use arrow function to create Immediately Invoked Function Expression (IIFE) `this` will refer to global `window` object. This applies to both, sloppy as well as strict mode.

```JavaScript
// Arrow IIFE example no.1: sloppy mode
// Declare arrow IIFE.
(() => {
  console.log(this)
  console.log(this === window)
})()
// Output:
// Window {0: Window, 1: Window, window: Window, self: Window, document: document, name: "", location: Location, …}
// true


// Arrow IIFE example no.2: strict mode
// Switch to strict mode.
'use strict';

// Declare arrow IIFE.
(() => {
  console.log(this)
  console.log(this === window)
})()
// Output:
// Window {0: Window, 1: Window, window: Window, self: Window, document: document, name: "", location: Location, …}
// true
```

### Objects, classes, this and arrow functions

If you declared your arrow function in an object, `this` will refer to global object `window`. In case of a class, it will refer to the class itself.

```JavaScript
// Arrow function example no.5: object in sloppy mode
// Declare an object.
const obj = {
  name: 'Luke',
  sayHi: () => {
    console.log(this)
    console.log(this === window)
  }
}

obj.sayHi()
// Output:
// Window {0: Window, 1: Window, window: Window, self: Window, document: document, name: "", location: Location, …}
// true


// Arrow function example no.6: object in strict mode
// Switch to strict mode.
'use strict'

// Declare a function
const obj = {
  name: 'Luke',
  sayHi: () => {
    console.log(this)
    console.log(this === window)
  }
}

obj.sayHi()
// Output:
// Window {0: Window, 1: Window, window: Window, self: Window, document: document, name: "", location: Location, …}
// true


// Arrow function example no.7: class in sloppy mode
// Declare a class with static property and method.
class Person {
  static name = 'Luke'
  static sayHi = () => {
    console.log(this)
    console.log(this === Person)
  }
}

Person.sayHi()
// Output:
// Luke()
// true


// Arrow function example no.8: class in strict mode
// Switch to strict mode.
'use strict'

// Declare a class with static property and method.
class Person {
  static name = 'Luke'
  static sayHi = () => {
    console.log(this)
    console.log(this === Person)
  }
}

Person.sayHi()
// Output:
// Luke()
// true
```

### Event listeners, this and arrow functions

If you use arrow function as a callback for event listener, `this` will refer to global object `window`. This will happen in both, sloppy and also strict mode.

```JavaScript
// Arrow function example no.9: event listener in sloppy mode
// Find button in the DOM.
const btn = document.querySelector('.btn')

// Attach event listener to the button.
btn.addEventListener('click', () => {
  console.log(this)
  console.log(this === window)
})

// Output on click on the button:
// Window {0: Window, 1: Window, window: Window, self: Window, document: document, name: "", location: Location, …}
// true


// Arrow function example no.10: event listener in strict mode
// Switch to strict mode.
'use strict'

// Find button in the DOM.
const btn = document.querySelector('.btn')

// Attach event listener to the button.
btn.addEventListener('click', () => {
  console.log(this)
  console.log(this === window)
})

// Output on click on the button:
// Window {0: Window, 1: Window, window: Window, self: Window, document: document, name: "", location: Location, …}
// true


// Arrow function example no.11: event listener on window
// Attach event listener to the button.
window.addEventListener('click', () => {
  console.log(this)
  console.log(this === window)
})

// Output on click on the button:
// Window {0: Window, 1: Window, window: Window, self: Window, document: document, name: "", location: Location, …}
// true
```

## Conclusion: A quick guide to this keyword in JavaScript

The `this` keyword can be sometimes confusing and unpredictable. It is no wonder some JavaScript developers don't like to use it, and even discourage it.  I hope that this tutorial helped you understand what `this` keyword refers to in specific contexts.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[strict mode]: https://developer.mozilla.org/en-US/docs/Glossary/strict_mode
[sloppy mode]: https://developer.mozilla.org/en-US/docs/Glossary/Sloppy_mode
[forbidden]: http://speakingjs.com/es5/ch07.html#strict_mode
[function]: https://blog.alexdevero.com/javascript-functions-pt3/
[arrow functions]: https://blog.alexdevero.com/javascript-arrow-functions/
[JavaScript classes]: https://blog.alexdevero.com/javascript-classes-pt1/
[function constructor]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/Function

<!--
### Meta:
-
-->

<!--
### Keywords:
- this keyword in JavaScript
- this keyword
-->

<!--
### Resources:
-
-->
