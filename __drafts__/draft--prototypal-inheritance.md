# Objects, [[Prototype]] and Prototypal inheritance in JavaScript Explained
<!--more-->
<!--
Table of Contents:
## h2
### h3
### h3
## h2
## Conclusion: [...] ...
-->

## Creating, inheriting and reusability

Knowing how to create objects is useful. It can help you do more things, often in better way. However, creating objects from scratch may not always be the best thing to do. The problem is that this practice can lead to repeated code. What you can do instead is create a base object.

This base object will contain universal properties and methods you may want in other objects. Later, let's say you want to create an object that will use any of these properties or methods. You don't have to write all those properties and methods from scratch. Instead, you can let that new object inherit from the base object.

When you do this, that new object will be able to use any property and method that exists in the base object. This is not everything you can do, yet. You can also add additional properties and methods only to that new object. After this, the base object will still be the same.

That new object, however, will not only be able to use anything from the base object. It will also be able to use anything new you've just added. This degree of reusability can help you make your code much shorter, clearer and cleaner. This is how prototypal inheritance can help you.

## The [[Prototype]] property

The fundamental part of prototypal inheritance is the `[[Prototype]]` property. This is a special hidden property that exists on every object in JavaScript. The value of this property is always either `null` or name of another object. When the value of `[[Prototype]]` is `null` it means that the object doesn't inherit from any other object.

When the value is a name of another object it means that the object's prototype references another object. Put simply, that object inherits from another object, whose name is specified in `[[Prototype]]`. When this happens, the inheriting object can use any property and method from the object it inherits from.

## Own and inherited properties and methods



## __proto__ setter/getter

If the property exists, JavaScript will return its value. If the method exists, JavaScript will call it. This, in esence, is what prototypal inheritance is about. You can access "stuff" in one object even though you are working with a different object, if that different object inherits from the first object.
## Prototype and reading/writing

## The value of "this"

## Looping over object properties and methods

## Conclusion: Objects, __proto__ and prototypal inheritance in JavaScript explained

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
- https://javascript.info/prototype-inheritance
- https://blog.alexdevero.com/javascript-objects-pt2/#looping-over-javascript-objects
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain
-->
