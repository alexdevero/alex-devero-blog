# Getting Started with JavaScript Proxy Object

JavaScript Proxy Object is one of the lesser known features of JavaScript. It was introduced in ES2015. This tutorial will teach what you need to know about it. You will learn...
<!--more-->
<!--
Table of Contents:
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
      // If it does, return it
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

// Try to access non-existing "name" property
console.log(myObj.age)
// Output:
// undefined
```

## JavaScript Proxy handlers, or traps

JavaScript Proxy allows you to control behavior of `target` object. You can do this by creating handler methods, or traps. There many default traps you can use to override specific behavior of JavaScript object. To make things simple, let's focus on few of these traps that might be the most useful.

### get()



### set()

### ownKeys()

### deleteProperty()

## Conclusion: [...] ...

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[JavaScript objects]: https://blog.alexdevero.com/javascript-objects-pt1/
[frozen]: https://blog.alexdevero.com/javascript-objects-pt2/#freezing-javascript-objects
[seal]: https://blog.alexdevero.com/javascript-objects-pt2/#partially-freezing-javascript-objects
[variable]: https://blog.alexdevero.com/javascript-variables-introduction/

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
