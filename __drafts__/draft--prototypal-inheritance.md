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

## The [[Prototype]] property and prototypal inheritance

This is one of the things in JavaScript that can seem weird. Let's say you want to access some property in an object. If that property exists JavaScript will return it. In case of a method, it will call that method. What if the property you want to access, or method you want to call, doesn't exists on that object?

In that case, JavaScript will do something interesting. It will take a look at the value of `[[Prototype]]` property. If the value is not `null`, it will find the object this property refers to. When it finds it, it will take a look if that object contains the property you want to access, or method you want to call.

If the property exists, JavaScript will return its value. If the method exists, JavaScript will call it. This, in esence, is what prototypal inheritance is about. You can access "stuff" in one object even though you are working with a different object, if that different object inherits from the first object.

## The __proto__, Object.setPrototypeOf() and Object.getPrototypeOf()

The `[[Prototype]]` property is hidden. However, there are ways that allow you to change its value. The one often used way to change prototype of an object is by using `__proto__`. One thing you should remember. The `[[Prototype]]` property and `__proto__` are not the same thing.

The `__proto__` is only a setter and getter for `[[Prototype]]` property. It allows you to work `[[Prototype]]` property. Another ways to set `[[Prototype]]` is by using `Object.setPrototypeOf()` method. This is a more modern setter. More modern getter is `Object.getPrototypeOf()` method.

It is mostly due to overall support by browsers why `__proto__` is more preferred than `Object.setPrototypeOf()`and `Object.getPrototypeOf()`. That said, using `__proto__` is deprecated, and not recommended. What you should use instead is either `Object.setPrototypeOf()` or `Object.getPrototypeOf()`.

## Changing the prototype

You know about the `__proto__`, `Object.setPrototypeOf()` and `Object.getPrototypeOf()`. Now, let's take a look at how you can use them to change the prototype of an object. We will take a look at how to do this with both options, the  `Object.setPrototypeOf()` as well as the `__proto__`.

### The __proto__

Fist, the `__proto__`. When you want to change prototype with `__proto__` you will assign a value. First, you need an object that should inherit from another object. You will access `__proto__` of this object. After that, you will choose an object you want the inheriting object to inherit from.

The value of `__proto__` will be a reference to that object you want to inherit from. You will use the name of that object as the value you assign to `__proto__`. That's it. Do this and you will successfully create prototypal inheritance between two objects.

```JavaScript
// Create base object
const myBaseObj = {
  isAlive: true,
  canSpeak: true,
  sayHi() {
    return 'Hello!'
  }
}

// Create new object that will inherit from "myBaseObj"
// Add a couple of its own properties
const myNewObj = {
  canWalk: true,
  canRun: true
}

// Let "myNewObj" inherit from "myBaseObj"
// by setting "myNewObj" prototype to "myBaseObj"
myNewObj.__proto__ = myBaseObj

// Now "myNewObj" basically becomes
// const myNewObj = {
//   isAlive: true,
//   canSpeak: true,
//   sayHi() {
//     return 'Hello!'
//   },
//   canWalk: true,
//   canRun: true
// }

// Access inherited "isAlive" property on "myNewObj"
console.log('isAlive: ', myNewObj.isAlive)
// Output:
// 'isAlive: ' true

// Access inherited "canSpeak" property on "myNewObj"
console.log('canSpeak: ', myNewObj.canSpeak)
// Output:
// 'canSpeak: ' true

// Access own "canWalk" property on "myNewObj"
console.log('canWalk: ', myNewObj.canWalk)
// Output:
// 'canWalk: ' true

// Call inherited "sayHi" method on "myNewObj"
console.log(myNewObj.sayHi())
// Output:
// 'Hello!'

// Create another object that will also inherit from "myBaseObj"
const myAnotherObj = {
  canSleep: true
}

// Let "myAnotherObj" also inherit from "myBaseObj"
myAnotherObj.__proto__ = myBaseObj

// Now "myAnotherObj" basically becomes
// const myAnotherObj = {
//   isAlive: true,
//   canSpeak: true,
//   sayHi() {
//     return 'Hello!'
//   },
//   canSleep: true
// }

// Access inherited "isAlive" property on "myAnotherObj"
console.log('isAlive: ', myAnotherObj.isAlive)
// Output:
// 'isAlive: ' true

// Access inherited "canSpeak" property on "myAnotherObj"
console.log('canSpeak: ', myAnotherObj.canSpeak)
// Output:
// 'canSpeak: ' true

// Access own "canSleep" property on "myAnotherObj"
console.log('canSleep: ', myAnotherObj.canSleep)
// Output:
// 'canSleep: ' true


// Alternative:
// Create base object
const myBaseObj = {
  isAlive: true,
  canSpeak: true,
  sayHi() {
    return 'Hello!'
  }
}

// Create new object that will inherit from "myBaseObj"
const myNewObj = {
  canWalk: true,
  canRun: true,
  __proto__: myBaseObj // set __proto__ inside an object
}
```

When you want to use some object as a prototype, use it's name as it is, as an object. Don't try to use it, assign it in case of `__proto__`, as a string. That will not work.

### The Object.setPrototypeOf()

The `Object.setPrototypeOf()` is the second option to set or change prototype of an object. When you call it, the `Object.setPrototypeOf()` method accepts two arguments. The first argument is the object that should be inheriting. The second argument is the object you want to inherit from.

```JavaScript
// Create base object
const myBaseObj = {
  species: 'bird',
  isAlive: true
}

// Create new object that will inherit from "myBaseObj"
const myNewObj = {
  canFly: false,
  likesIce: true
}

// Let "myNewObj" inherit from "myBaseObj"
// by setting "myNewObj" prototype to "myBaseObj"
Object.setPrototypeOf(myNewObj, myBaseObj)

// Access inherited "species" property on "myNewObj"
console.log(myNewObj.species)
// Output:
'bird'

// Access inherited "isAlive" property on "myNewObj"
console.log(myNewObj.isAlive)
// Output:
true

// Access inherited "canFly" property on "myNewObj"
console.log(myNewObj.canFly)
// Output:
false

// Access inherited "likesIce" property on "myNewObj"
console.log(myNewObj.likesIce)
// Output:
true
```

### The Object.getPrototypeOf()

You know how to use `__proto__` and `Object.setPrototypeOf()` method to set a prototype of an object. When you want to get current prototype of an object you can use the `Object.getPrototypeOf()`. This method accept on parameter, the object whose prototype you want to get.

Before you use this method there are some things you should know. First, it returns the prototype of given object. However, if you try to print it, or log it, it will not tell you the name of the prototype object. Instead, it will tell you what properties and methods given object inherited.

A better way to use this method is by using it to compare two objects. If the first object has the same prototype as the second, if it inherits from it, the result of this comparison will be `true`. Otherwise, `false`. This way, you can check if one object inherits from another because objects are not [created equal].

```JavaScript
// Create base object
const myBaseObj = {
  canEat: true,
  canSwim: true
}

// Create new object that will inherit from "myBaseObj"
const myNewObj = {
  canWalk: true
}

// Let "myNewObj" inherit from "myBaseObj"
// by setting "myNewObj" prototype to "myBaseObj"
Object.setPrototypeOf(myNewObj, myBaseObj)

// Test if "myNewObj" and "myBaseObj" has the same prototype
console.log(Object.getPrototypeOf(myNewObj) === myBaseObj)
// Output:
// true

// Log inherited properties of "myNewObj"
console.log(Object.getPrototypeOf(myNewObj))
// Output:
// { canEat: true, canSwim: true }
```

## Prototypal inheritance and the value of "this"

When you use `this` in an object it refers to the object itself, the object in which you used it. What happens if you use `this` in an object and you then inherit from that object? Which object will `this` refer to? The answer is, the object you are currently working with, the object before the dot (`myObj.someMethod()`).

If you work with the base object, `this` will refer to that base object. If you work with an object that inherits from the base object, `this` will refer to that inheriting object. So, don't worry if your base object uses `this` in some method. It will work correctly also in case of objects inheriting from that base object.

```JavaScript
// Create base object
const personOne = {
  name: 'Tom',
  sayHi() {
    return `Hello I am ${this.name}.`
  }
}

// Create another person that will inherit from "personOne"
const personTwo = {}

// Let "personTwo" inherit from "personOne"
Object.setPrototypeOf(personTwo, personOne)

// Change the "name" of "personTwo" to "Jack"
personTwo.name = 'Jack'

// Call the "sayHi()" method on "personTwo"
console.log(personTwo.sayHi())
// Output:
// 'Hello I am Jack.'

// Create third person that will also inherit from "personOne"
const personThree = {}

// Let "personThree" also inherit from "personOne"
Object.setPrototypeOf(personThree, personOne)

// Change the "name" of "personThree" to "Victoria"
personThree.name = 'Victoria'

// Call the "sayHi()" method on "personThree"
console.log(personThree.sayHi())
// Output:
// 'Hello I am Victoria.'

// Call the "sayHi()" method on "personOne" (the base object)
console.log(personOne.sayHi())
// Output:
// 'Hello I am Tom.'
```

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
// Access inherited "isAlive" property on "myNewObj"
console.log('isAlive: ', myNewObj.isAlive)
// Output:
'isAlive: ' true

// Access inherited "canSpeak" property on "myNewObj"
console.log('canSpeak: ', myNewObj.canSpeak)
// Output:
'canSpeak: ' true
