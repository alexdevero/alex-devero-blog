# Getting Started with JavaScript Proxy Object

JavaScript Proxy Object is one of the lesser known and a bit esoteric JavaScript features introduced in ES2015. In this tutorial, you will learn about what a Proxy object is, how it works and how to create it. You will also learn about the six most useful JavaScript Proxy handlers, or traps, and how to use them.
<!--more-->
<!--
Table of Contents:
## Introduction
## How to create JavaScript Proxy
## How JavaScript Proxy works
## JavaScript Proxy handlers, or traps
### The get() trap
### The set() trap
### The ownKeys() trap
### The getOwnPropertyDescriptor() trap
### The deleteProperty() trap
### The has() trap
## Conclusion: Getting Started with JavaScript Proxy Object
-->

## Introduction

When you work with [JavaScript objects] there is always some default behavior. When you try get a value from an object JavaScript will return it, if it exists. If it doesn't exist, JavaScript will throw an error. When you try to set or change a value, or add new prop, JavaScript will do that.

Well, this will work unless the object is [frozen]. Note: you can also [seal] an object to forbid adding or removing properties, but allow changing existing values. What JavaScript Proxy does is it allows you to change this default behavior. You can define your own behavior and use JavaScript Proxy to override the default.

What happens when you try to execute some operation on the object you changed? It will be the behavior you defined what will be executed, not the default. This is, in short, what JavaScript Proxy does. It allows you to hijack or override the default behavior of JavaScript objects.

## How to create JavaScript Proxy

The syntax of JavaScript Proxy is simple. It is also easy to create new Proxy. The Proxy object takes two parameters. The first one is `target`. This is the object whose behavior you want to change. This is important. Creating new JavaScript Proxy and applying it to some object will change only that one object, nothing else.

This also means one thing. If you want to apply some Proxy to multiple objects, you have to apply that Proxy to all those objects. To the second parameter. This parameter is `handler`. The `handler` parameter is an object. Inside this object are methods to control the behaviors of the object specified as the `target`.

The methods inside the `handler` object are called traps. So, the next time your hear about JavaScript Proxy and traps, think about methods that control behavior of target object. Last thing. JavaScript Proxy is an object. So, to create new you have to use the `new` keyword. What you get is `new Proxy(target, handler)`.

```JavaScript
// JavaScript Proxy syntax
// target – is an object to wrap.
// handler – is an object with methods (traps) to control
// the behaviors of the target
const myProxy = new Proxy(target, handler)


// Using Proxy on an object
// Create an object
const myObj = {
  name: 'Tony',
  gender: 'male'
}

// Create new Proxy and apply it to myObj object
// Set myObj variable as the "target" parameter
// and empty object as the "handler" parameter
const myProxy = new Proxy(myObj, {})
```

## How JavaScript Proxy works

You know how to create a Proxy. The next thing you need to know is how it works, at least in general. JavaScript Proxy is wrapper. It wraps the object you specified as the `target` parameter. This means two things. First, as you already know, it means that Proxy will be applied to the object you pass as the `target` parameter.

The second thing is that you will usually want to assign new Proxy to a [variable]. JavaScript Proxy wraps the `target` object, but it doesn't change it. It only connects to that object, to its reference. Any change in behavior you make is always kept inside the Proxy, not the object you want to change.

If you use a Proxy on some object, from now on, you have to work with that Proxy. Only then, will the new behavior apply. When you interact with the Proxy it will automatically connect with the object and execute that task you want, while applying the behavior you specified.

If you try to interact with the original object itself no change you made via the Proxy will be applied. This is a good thing and it is also a bad thing. It is a bad thing because you have to remember to interact with the Proxy to get the behavior you want, not the original object.

It is a good thing because you can switch to the original object any time you want, and easily. All you have to do is to reference the original object instead of the Proxy. When you want to work with the Proxy again, you just have to reference it.

Let's take a look at one example of how you can switch between original object and JavaScript Proxy (You will learn about the `get()` trap in the next section).

```JavaScript
// Create an object
const myObj = {
  name: 'Tony',
  gender: 'male'
}

// Create new Proxy and apply it to myObj object
const myProxy = new Proxy(myObj, {
  // Create get method "trap"
  // This will alter getting properties inside myObj
  get(target, prop) {
    // Check if property exists in target object
    if (prop in target) {
      // If it does exist, return the property value
      return target[prop]
    } else {
      // Otherwise, show some friendly message
      return 'Sorry, such property doesn\'t exist.'
    }
  }
})

// Example no.1: Working with proxy
// Try to access existing "name" property
console.log(myProxy.name)
// Output:
// 'Tony'

// Try to access non-existing "name" property
console.log(myProxy.age)
// Output:
// 'Sorry, such property doesn\'t exist.'


// Example no.2: Switching to the original object
// Try to access existing "name" property
console.log(myObj.name)
// Output:
// 'Tony'

// Try to access nonexisting "age" property
console.log(myObj.age)
// Output:
// undefined
```

## JavaScript Proxy handlers, or traps

JavaScript Proxy allows you to control behavior of `target` object. You can do this by creating handler methods, or traps. There [many default traps] you can use to override specific behavior of JavaScript object. To make things simple, let's focus on few of these traps that might be the most useful.

### The get() trap

The first trap is `get()`. You've seen this trap in the example in "How JavaScript Proxy works" section. This trap allows changing the default behavior that is triggered when you try to access a object property. In the previous example, we used this trap to change the error message you get when you try to access nonexisting property.

There are other ways to use this trap. You can use it to restrict access to certain properties. Or, you can use it to return only parts of the values. For example, when you ask for a credit card number you can return only last 4 numbers while keeping the rest hidden. Or, if you ask for a password you can return only asterisks.

Creating `get()` method, or trap, is easy. You create it as any other object method, either as `get() {}` or `get: function() {}`, or an [arrow function] equivalent `get: () => {}`. Remember to always use the `get` keyword. This method takes two parameters: `target` and `prop` (or property).

The `target` is automatically set the `target` of the Proxy, the target object. The `prop` parameter is always automatically set to the property you want to access. If you want to access property `name` on some object, the "name" will become the value of `prop` parameter.

Thanks to this, having the access to the `prop` parameter, you can target any object property you want and change access behavior only for that property. This way, you can also forbid the access.

```JavaScript
// Create an object
const user = {
  name: 'Jackie',
  creditCardNum: '4510 6459 8301 6543',
  password: 'justSomeStringsAndNumbers1359tru',
  secret: 'This should remain private.'
}

// Create a Proxy and apply it to "user" object
const userProxy = new Proxy(user, {
  // Create get() trap to change the default behavior
  // for accessing object properties
  get(target, prop) {
    // Check if property exists in target object
    if (prop in target) {
      // If it does exist, return the property value
      if (prop === 'secret') {
        return 'You are not allowed to access this property.'
      } else if (prop === 'creditCardNum') {
        // If accessed property is "creditCardNum"
        // return only last four numbers
        return `---- ---- ---- ${target[prop].substring(target[prop].length -4)}`
      } else if (prop === 'password') {
        // If accessed property is "password"
        // return masked string
        return '*'.repeat(target[prop].length)
      } else {
        // Otherwise, return the whole value
        return target[prop]
      }
    } else {
      // Otherwise, show some friendly message
      return 'Sorry, such property doesn\'t exist.'
    }
  }
})

// Try to access "name" in "userProxy" object
// Note: remember to work with the Proxy, not the original object
console.log(userProxy.name)
// Output:
// 'Jackie'

// Try to access "creditCardNum" in "userProxy" object
console.log(userProxy.creditCardNum)
// Output:
// '---- ---- ---- 6543'

// Try to access "password" in "userProxy" object
console.log(userProxy.password)
// Output:
// '********************************'

// Try to access "secret" in "userProxy" object
console.log(userProxy.secret)
// Output:
// 'You are not allowed to access this property.'


// If you try to work with the original object:
console.log(user.name)
// Output:
// 'Jackie'

console.log(user.creditCardNum)
// Output:
// '4510 6459 8301 6543'

console.log(user.password)
// Output:
// 'justSomeStringsAndNumbers1359tru'

console.log(user.secret)
// Output:
// 'This should remain private.'
```

Last thing. Make sure the `get()` trap always returns something, with `return` statement. If it doesn't when you try to access some property you will get `undefined`.

```JavaScript
// Create an object
const user = {
  name: 'Jackie',
  creditCardNum: '4510 6459 8301 6543',
  password: 'justSomeStringsAndNumbers1359tru'
}

// Create a Proxy and apply it to "user" object
const userProxy = new Proxy(user, {
  // Create get() trap to change the default behavior
  // for accessing object properties
  get(target, prop) {
    // Check if property exists in target object
    if (prop in target) {
      // If it does exist, return the property value
      if (prop === 'creditCardNum') {
        // If accessed property is "creditCardNum"
        // return only last four numbers
        return `---- ---- ---- ${target[prop].substring(target[prop].length -4)}`
      }
    }
    // Forget to return something if accessed property
    // is not "creditCardNum"
  }
})

console.log(userProxy.name)
// Output:
// undefined

console.log(userProxy.creditCardNum)
// Output:
// '---- ---- ---- 6543'
```

The `get()` trap also accepts optional third parameter. This parameter is a `receiver`. This optional parameter is useful when the target object property is a getter. In this case, the `receiver` is the object that will be used as `this` when it is called. This object is usually the JavaScript Proxy object itself.

*Note: the first example above is for illustration purpose only. Don't store your passwords, or credit card numbers, anywhere in your code where someone else an find them.*

### The set() trap

Another trap you can create is `set()`. This trap allows you to change the default behavior of changing a value of existing property. The `set()` trap takes three parameters. First is `target`. This is again automatically set the `target` of the Proxy, the target object.

The second parametry is `prop`, or the property name. The third is `value`, the new value you want to set, or write. Similarly to `get()`, the `set()` trap also accepts the `receiver` as an optional parameter. However, since its usage is very specific you may not need to use it, or not that often.

You create the `set()` trap just like the `get()`. As an object method, using either `set() {}`, `set: function() {}` or an arrow function `set: () => {}`. The `set()` trap has access to both, property you want to change and the value you want to assign to it. This makes `set()` a good candidate for a value validation.

For example, let's say you have an object. This object contains some property and the value of this property should be always a string. With `set()`, you can create a test for value type and allow the value change to happen only if the type of the new value is a string. Otherwise, you can reject that change.

```JavaScript
// Create an object
const user = {
  name: 'Toby',
  age: 29
}

// Create a Proxy for "user" object
const userProxy = new Proxy(user, {
  set(target, prop, value) {
    if (prop in target) {
      if (prop === 'name') {
        // Check if the value is a string
        if (typeof value === 'string') {
          // If the value is a string
          // allow to change the property
          target[prop] = value

          // Return true if setting
          // new value was successful
          return true
        } else {
          // If the value is not a string
          // you can throw an error to notify the user
          throw new TypeError('The value of "name" must be a string.')
        }
      } else if (prop === 'age') {
        // Check if the value is a number
        if (Number.isInteger(value)) {
          // If the value is a number
          // allow to change the property
          target[prop] = value

          // Always return true if setting
          // new value was successful
          return true
        } else {
          // If the value is not a number
          // you can throw an error to notify the user
          throw new TypeError('The value of "age" must be a number.')
        }
      }
    }
  }
})

// Try to change the value of "name" to another string
userProxy.name = 'Jacob'
console.log(userProxy.name)
// Output:
// 'Jacob'

// Try to change the value of "name" to a boolean
userProxy.name = false
console.log(userProxy.name)
// Output:
// TypeError: The value of "name" must be a string.

// Try to change the value of "age" to another number
userProxy.age = 33
console.log(userProxy.age)
// Output:
// 33

// Try to change the value of "age" to a string
userProxy.age = 'twenty'
console.log(userProxy.age)
// Output:
// TypeError: The value of "age" must be a number.
```

When you work with `set()` trap, and the change is accepted, you should always return `true`. This is will indicate that the change was successful. If the change wasn't successful, if it was rejected, you can throw appropriate [error]. In this case, you should also use [try...catch] to safely catch that error.

### The ownKeys() trap

Have you ever used `Object.keys()`, `Object.getOwnPropertyNames()` or `Object.getOwnPropertySymbols()`? These methods basically "ask" the object for a list of properties it contains. You can change what these methods get from the object, and return to you, by using the `ownKeys()` trap.

The `ownKeys()` trap takes a single parameter, the `target`. This is the `target` of the Proxy itself, the object you want to change. Since the returned result is expected to be a list, or an array, this is also what the `ownKeys()` trap should return. Each element inside this array can be either a string or symbol.

One example of how you can use the `ownKeys()` trap is to filter which object properties you want to show and which to hide. Inside the `ownKeys()` trap, you can use `Object.keys(target)` method to get all keys of the target object. Then, you can use `filter()` method to filter the array of keys based on a specific condition.

From now on, when someone use the `Object.keys()` or `Object.getOwnPropertyNames()` methods it will always show only the properties that pass your filter.

```JavaScript
// Create an object
const user = {
  _dateOfRegistration: '2017-03-12T10:12:45.910Z',
  _password: 'justSomeNumbersAndStrings8785fals',
  _userType: 'user',
  name: 'Toby',
  email: 'toby@tobyuser.com',
  age: 29
}

// Create a Proxy for "user" object
const userProxy = new Proxy(user, {
  // Create ownKeys() trap
  ownKeys(target) {
    // Return only keys that don't start with '_'
    return Object.keys(target).filter(key => !key.startsWith('_'))
  }
})

// Use Object.keys()
// to get all properties of user object
console.log(Object.keys(userProxy))
// Output:
// [ 'name', 'email', 'age' ]


// Use Object.getOwnPropertyNames()
// to get all properties of user object
console.log(Object.getOwnPropertyNames(userProxy))
// Output:
// [ 'name', 'email', 'age' ]
```

There is another interesting thing you can do with `ownKeys()`. You can also return a different list of keys than those inside the target object. There is one catch. This, returning a completely different list of keys, will work from the get-go only with `Object.getOwnPropertyNames()` method (fix for this in the next section).

```JavaScript
// Create an object
const user = {
  _dateOfRegistration: '2017-03-12T10:12:45.910Z',
  _password: 'justSomeNumbersAndStrings8785fals',
  _userType: 'user',
  name: 'Toby',
  email: 'toby@tobyuser.com',
  age: 29
}

// Create a Proxy for "user" object
const userProxy = new Proxy(user, {
  // Create ownKeys() trap
  ownKeys(target) {
    // Return a list of nonexisting keys
    return ['favorite book', 'favorite author', 'currently reading']
  }
})

// Use Object.getOwnPropertyNames()
// to get all properties of user object
console.log(Object.getOwnPropertyNames(userProxy))
// Output:
// [ 'favorite book', 'favorite author', 'currently reading' ]


// Use Object.keys()
// to get all properties of user object
// NOTE: this will not work, yet
console.log(Object.keys(userProxy))
// Output:
// []
```

### The getOwnPropertyDescriptor() trap

The "problem" with `Object.keys()` is that works only with enumerable object properties. Every object has `GetOwnProperty()` method. This method is used for each property to check if specific property is enumerable or not, if it has `enumerable` flag. If it is not enumerable it will not show up when you use `Object.keys()`.

Let's say that you want to return a list of nonexisting properties. in this case, the object will call the `GetOwnProperty()` method for each imagery property on that list. Unfortunately, since these properties actually doesn't exist in the target object there is no record saying they are enumerable.

If there is no record saying that all those imagery properties in the returned list are enumerable they will not show up if you use the `Object.keys()` method. These properties will only show up when you use `(Object.getOwnPropertyNames()`. That said, there is a way to make this work.

You have to use another Proxy trap called `getOwnPropertyDescriptor()`. This trap allows you to manually set property flags and descriptors. One of these flags is also the `enumerable`. When you use this trap, and set the `enumerable` to `true`, your imagery properties will show up when you use `Object.keys()`.

The `getOwnPropertyDescriptor()` trap takes two parameters: `target` and `prop`. The `target` is the target object for the Proxy. The `prop` is for each property its descriptors you want to get. The value this trap returns is an object with flags you want to apply to object properties in the target object.

Let's get to our example with list of imagery properties. What we need is to create the `getOwnPropertyDescriptor()` trap. We also need this trap to return two flags, `enumerable` and `configurable`, both set to `true`.

Theoretically, we need only first, but ignoring the second will cause `TypeError`. With this, our imagery list of properties will work even with `Object.keys()` method.

```JavaScript
// Create an object
const user = {
  _dateOfRegistration: '2017-03-12T10:12:45.910Z',
  _password: 'justSomeNumbersAndStrings8785fals',
  _userType: 'user',
  name: 'Toby',
  email: 'toby@tobyuser.com',
  age: 29
}

// Create a Proxy for "user" object
const userProxy = new Proxy(user, {
  // Create ownKeys() trap
  ownKeys(target) {
    // Return a list of nonexisting keys
    return ['favorite book', 'favorite author', 'currently reading']
  },
  // Create getOwnPropertyDescriptor() trap
  // This trap will be automatically used for every property
  getOwnPropertyDescriptor(target, prop) {
    // Set enumerable and configurable flags to true
    return {
      enumerable: true,
      configurable: true
    }
  }
})

// Use Object.getOwnPropertyNames()
// to get all properties of user object
console.log(Object.getOwnPropertyNames(userProxy))
// Output:
// [ 'favorite book', 'favorite author', 'currently reading' ]


// Use Object.keys()
// to get all properties of user object
// NOTE: this will finally work!
console.log(Object.keys(userProxy))
// Output:
// [ 'favorite book', 'favorite author', 'currently reading' ]
```

### The deleteProperty() trap

You know how to change accessing and setting individual properties and getting all of them. Another thing you can change is which properties can be deleted and which can't. This can be useful in situations where you want to protect specific object properties from being deleted.

To do this you have to use the `deleteProperty()` trap. This trap takes two parameters: `target`, and `prop`. As usually, the `target` is the target object for the Proxy. The `prop` is for the property you want to delete. When you you want to allow to delete some property, you can allow do that by using `delete` statement.

Successful deletion should always return `true` to indicate the operation was indeed successful. What if you don't want some property to be deleted? You can either return `false` or you can throw some custom `Error`.

```JavaScript
// Create an object
const user = {
  username: 'jack',
  email: 'jack@fowley.com'
}

// Create a Proxy for "user" object
const userProxy = new Proxy(user, {
  // Create deleteProperty() trap
  deleteProperty(target, prop) {
    // Check if property exists
    if (prop in target) {
      // Check if property is not a "username"
      if (prop !== 'username') {
        // Delete the property
        delete target[prop]

        // Always return true if setting
        // new value was successful
        return true
      } else {
        // Reject the deletion and throw an error
        throw new Error('Property "username" can\'t be deleted.')
      }
    } else {
      // Throw an error about nonexisting property
      throw new Error(`Property "${prop}" does not exist.`)
    }
  }
})

// Try to delete "email" property
delete userProxy.email
// Output:

// Try to delete "username" property
delete userProxy.username
// Output:
// Error: Property "username" can't be deleted.

// Try to delete "age" property
delete userProxy.age
// Output:
// Error: Property "age" does not exist.

// Log the content of "userProxy" object
console.log(userProxy)
// Output:
// { username: 'jack' }
```

### The has() trap

The `has()` trap works in a similar way to the `ownKeys()`. It also allows you to filter which properties should be visible and which not. The difference between `has()` and `ownKeys()` is that the `has()` trap works with `in` operator. This operator is useful when you want to check if some property exists in an object.

The `has()` trap allows you to change the boolean value `in` operator returns for a specific property, or all. This trap takes two parameters: `target` and `prop`. The target is as always the target of the JavaScript Proxy object. The `prop` is for the property its existence you want to check for.

When you want to show some existing property as nonexistent, when you use `in` operator, you can simply return `false` for that property. Otherwise, you return `key in target`.

```JavaScript
// Create an object
const user = {
  username: 'anonymous',
  _secret: 'Some secret that should remain hidden.'
}

// Create a Proxy for "user" object
const userProxy = new Proxy(user, {
  has(target, prop) {
    // Check if property is "_secret"
    if (prop === '_secret') {
      // If so, return false to disallow detecting
      // this property with "in" operator
      return false
    } else {
      // Otherwise, allow the property to be detected
      // by "in" operator
      return prop in target
    }
  }
})

// Test if "username" property exists in "userProxy" object
console.log('username' in userProxy)
// Output:
// true

// Test if "_secret" property exists in "userProxy" object
console.log('_secret' in userProxy)
// Output:
// false
```

## Conclusion: [...] ...

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[JavaScript objects]: https://blog.alexdevero.com/javascript-objects-pt1/
[frozen]: https://blog.alexdevero.com/javascript-objects-pt2/#freezing-javascript-objects
[seal]: https://blog.alexdevero.com/javascript-objects-pt2/#partially-freezing-javascript-objects
[variable]: https://blog.alexdevero.com/javascript-variables-introduction/
[arrow function]: https://blog.alexdevero.com/javascript-arrow-functions/
[getter]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/get
[error]: https://blog.alexdevero.com/error-handling-javascript/
[try...catch]: https://blog.alexdevero.com/error-handling-javascript/#error-handling-and-try8230catch-statement
[many default traps]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy/Proxy

<!--
### Meta:
-
-->

<!--
### Keywords:
- Javascript Proxy Object
- Javascript Proxy
- Proxy
-->

<!--
### Resources:
- https://flaviocopes.com/javascript-proxy-objects/
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy
- https://javascript.info/proxy
- https://www.javascripttutorial.net/es6/javascript-proxy/
- https://blog.campvanilla.com/advanced-guide-javascript-proxy-objects-introduction-301c0fce9432
- https://hackernoon.com/introducing-javascript-es6-proxies-1327419ab413
- https://blog.bitsrc.io/a-practical-guide-to-es6-proxy-229079c3c2f0
- https://towardsdatascience.com/why-to-use-javascript-proxy-5cdc69d943e3
-->
