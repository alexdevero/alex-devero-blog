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
```

## JavaScript Proxy handlers

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
