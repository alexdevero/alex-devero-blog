# Blog post title [...]
<!--more-->
<!--
Table of Contents:
## h2
### h3
### h3
## h2
## Conclusion: [...] ...
-->


## Object literal

## No.1: Object literal

Using object literals is the first way to create objects in JavaScript. It is probably also the easiest to learn, remember and use. This is probably also why it is the most popular way to create objects in JavaScript. Creating an object this way is simple. You wrap the key-value pairs with curly brackets (`{}`).

Those key-value pairs are pairs of `keys` and `values` you want the object to have. Another name for object `key` that is used very often is "property". Keys, or properties, are on the left side of the pair and values on the right. Between these two are colons (`key: value`).

When you wrap this pair with curly brackets you have an object. If you want to create an empty object you use only the curly brackets. After that, you can assign that new object to some [variable]. Or, you can use it right away as you want.

```JavaScript
// Creating object with object literal.
const myObj = {
  name: 'Tom Jones',// One key-value pair.
  role: 'admin',
  isWorking: false,
  sayHi: function() {
    return `Hi, my name is ${this.name}.`
  }
}

// Log the object to console.
console.log(myObj)
// Output:
// {
//   name: 'Tom Jones',
//   role: 'admin',
//   sayHi: ƒ sayHi()
// }


// Creating an empty object with object literal.
const myEmptyObj = {}

// Log the object to console.
console.log(myEmptyObj)
// Output:
// {}
```

## No.2: The "new" keyword

The second way you can create an object is by using `new` keyword with [Object() constructor]. When you use this constructor it returns a value, new object. You can assign this object to a variable so you can continue working with it. If you want to add new properties there are two things you can do.

The first one is to create an empty object and assign it to a variable. Then, you can add properties to that object with dot-notation or using square brackets. This allows you to define only one property at the time. So, if you want to create multiple properties you will have to do this a couple of times.

The second option is to pass an object to the `Object()` constructor as an argument. This will also create an object with properties and values you want. However, if you want to pass an object, using the `Object()` constructor is redundant. It is also probably not a good practice and definitely not recommended.

What you can do instead in this case, is use the object literal way. We discussed this in the previous section above.

```JavaScript
// Creating object with object constructor.
const myObj = new Object()

// Add properties.
myObj.username = 'Skylar'
myObj.gender = 'female'
myObj.title = 'Fullstack dev'

// Add a method.
myObj.sayHi = function() {
  return `Hi, I am ${this.username}.`
}

// Log the object to console.
console.log(myObj)
// Output:
// {
//   username: 'Skylar',
//   gender: 'female',
//   title: 'Fullstack dev'
//   sayHi: ƒ ()
// }


// Passing an object - not a good idea
const myObj = new Object({
  username: 'Skylar',
  gender: 'female',
  title: 'Fullstack dev'
})

// Log the object to console.
console.log(myObj)
// Output:
// {
//   username: 'Skylar',
//   gender: 'female',
//   title: 'Fullstack dev'
// }
```

## No.3: Object.create() method

When you want to create new object based on existing `Object.create()` method will be very useful. This method accepts two parameters. The first parameter is for the original object you want to duplicate. This will be the `prototype`. The second parameter is for object with properties and values you want to add to the new object.

When you use this way and add new properties, remember one thing. You specify the values of new properties via `value` in [property descriptor], not directly. You can also specify other flags such as `writable`, `enumerable` and `configurable`. You can do this for every property you want to add.

Similarly to the `Object()` constructor, this method will also return new object as a result. So, assign it to a variable when you use it so you can work with afterwards.

```JavaScript
// Create new object (using object literal).
const human = {
  species: 'human',
  isAlive: true
}

// Create new object "female" with Object.create()
// and use "human" as the prototype
// and add two new properties - "gender" and "pregnant".
const female = Object.create(human, {
  // Add "gender" property.
  gender: {
    value: 'female', // Value of "gender" property.
    writable: true,
    enumerable: true,
    configurable: true
  },
  // Add "pregnant" property.
  pregnant: {
    value: false, // Value of "pregnant" property.
    writable: true,
    enumerable: true,
    configurable: true
  }
})

// Log the "female" object.
console.log(female)
// Output:
// {
//   gender: 'female',
//   pregnant: false,
//   __proto__: {
//     species: 'human',
//     isAlive: true
//   }
// }

// Log the value of "gender" property.
console.log(female.gender)
// Output:
// 'female'

// Log the value of "species" property.
// This property is inherited from "human" object.
console.log(female.species)
// Output:
// 'human'

// Log the value of "isAlive" property.
// This property is inherited from "human" object.
console.log(female.isAlive)
// Output:
// true
```

### A note on __proto__, prototypes and inheritance

Note: The `species` and `isAlive` properties were inherit from the original `human` object. If you log the content `female` object these two properties will not appear inside it directly. They will be inside `__proto__` object. This object refers to the original object `human`.

You can imagine replacing the `__proto__` with `human`. Or, replace it with any other object you used as the prototype. When you work with these two properties JavaScript will look at that prototype object to get the actual value. So, basically, for JavaScript `female.isAlive` will become `human.isAlive`.

This is why these properties are not listed directly inside the new object and why you can still access them. It is also why, if you change the property value in `human` you will get the new value also in `female`. For example, if you set `human.isAlive` to `false`, `female.isAlive` will now be also `false`.

The reason is that in both cases you are working with the same property. You are working with `human.isAlive`. In one situation, you just replace the `human` with `female` as an "alias". You can learn more about prototypes and prototypal inheritance in JavaScript in this [tutorial].

```JavaScript
// Log the value of "isAlive" property.
// This property is inherited from "human" object.
console.log(female.isAlive)
// Output:
// true

// Change the "isAlive" property in "human" object.
human.isAlive = false

// Log the value of "isAlive" property again.
console.log(female.isAlive)
// Output:
// false
```

## No.4: Object.assign() method

The `Object.assign()` method offers another way to create objects in JavaScript. This method is very similar to the `Object.create()`. This method also creates new objects by copying existing ones. Unlike the `Object.create()`, this method allows you to use any number of source objects you want.

With `Object.create()` you can create one object with properties from one object. With `Object.assign()` you can create one object with properties from multiple object. Using this method to create new objects is simple. It takes two parameters. The first parameter is the new object you want to create.

If you want don't want to add any new properties, you pass in an empty object (`{}`). Otherwise, you pass in an object with properties you want to add. The second argument are any objects you want to use as source objects. Your new object will inherit its properties from these source objects.

```JavaScript
// Create some source objects.
const lang = {
  language: 'JavaScript'
}

const job = {
  jobTitle: 'Programmer'
}

const experience = {
  experienceLevel: 'senior'
}


// Create new empty object with Object.assign() method.
// Use "lang", "job" and "experience" objects.
// First argument is an empty object to create.
// Second argument are source objects.
const coderAnonymous = Object.assign({}, lang, job, experience)

// Log the "coderAnonymous" object
console.log(coderAnonymous)
// Output:
// {
//   language: 'JavaScript',
//   jobTitle: 'Programmer',
//   experienceLevel: 'senior'
// }


// Create new object with Object.assign() method.
// Use "lang", "job" and "experience" objects
// as source objects and also add new property "name".
// First argument is an object to create with property "name".
// Second argument are source objects.
const coderJack = Object.assign({
  // Add new property "name".
  name: 'Jack'
}, lang, job, experience) // Specify source objects.

// Log the "coderJack" object
console.log(coderJack)
// Output:
// {
//   name: 'Jack',
//   language: 'JavaScript',
//   jobTitle: 'Programmer',
//   experienceLevel: 'senior'
// }
```

## No.5: Function constructor

The fifth way to create objects in JavaScript is by using [function constructors]. These function constructors look like regular [functions]. However, there are some differences. The first one is that when you use regular function you call it, or invoke it. This is not the case with function constructors.

When you want to use function constructor to create an object you use it similarly to `Object()` constructor. You use it with the `new` keyword. Second difference is that you usually use regular functions to do something, some action, when you invoke them. Function constructors are used to create objects.

Third difference is that function constructors use the [this] keyword, a lot. Regular functions? Well, that depends on your preference and mode. Still, you are less likely to use `this` in a regular function. In constructor, you will use it often. The last difference is that names of function constructors start with capital letter.

Let's take a look at how to create, and use, a function constructor. First comes the `function` keyword. Next is the function constructor name, starting with capital letter. Following this are parameters for the function constructor. These parameters define properties you want every object you create with the constructor to have.

Inside the function body you assign those parameters as new properties of the function constructor. This is where you use the `this` keyword. This will help you reference the function constructor when you create it. It will also help you reference each instance, new object, you create with the constructor.

When you want to use this function constructor you use it like the `Object()` constructor. In this case, you also pass some arguments according to the parameters your function constructor takes. If you want to add some method, you can. Just make sure to use the `this` keyword before the name of the method.

```JavaScript
// Create function constructor called "User".
function User(name, username, email) {
  // Assign parameters as new properties of the function constructor.
  // This allows you to use <objName>.property: userJoe.name
  // and get the value of "name" property of "userJoe" object
  // and not any other instance of User, i.e. other object.
  this.name = name
  this.username = username
  this.email = email
  // Add object method
  this.sayHi = function() {
    return `Hi, my name is ${this.name}.`
  }
}

// Use "User" function constructor to create new objects.
const userJoe = new User('Joe', 'joe123', 'joe@hello.com')
const userCathy = new User('Catherine', 'cathy', 'Catherine@hello.com')

// Log names of new users.
console.log(userJoe.name)
// Output:
// 'Joe'

console.log(userCathy.name)
// Output:
// 'Catherine'

// Log usernames of new users.
console.log(userJoe.username)
// Output:
// 'joe123'

console.log(userCathy.username)
// Output:
// 'cathy'

// Log emails of new users.
console.log(userJoe.email)
// Output:
// 'joe@hello.com'

console.log(userCathy.email)
// Output:
// 'Catherine@hello.com'

// Call the sayHi method for all new users.
console.log(userJoe.sayHi())
// Output:
// 'Hi, my name is Joe.'

console.log(userCathy.sayHi())
// Output:
// 'Hi, my name is Catherine.'
```

## No.6: ES6 classes

This last way to create new object is also the newest. [JavaScript classes] were introduced in ES6 specification. Classes may look like something new. They are not. When you look at them closely, you will see they are actually very similar to function constructors we just talked about. Under the hood, they also work in a similar way.

When you want to create new class, you start with the `class` keyword. Next, you specify the name of the class. After this follows curly brackets and the class body. Here, you can define class properties and class methods the class should have. These properties are defined in a similar way as in function constructors.

You define them all with the `this` keyword in the beginning. However, you don't define them directly in the body, but inside [constructor] method. This is a special method that is invoked every time you create an [instance] of the class. Creating an instance is basically creating new object based on a class.

This is also where you define parameters for the class. These parameters will be used for passing values to properties when you create new instances (copies) of that class. When you want to create new instance of the class, new object based on it, you use the class name with the `new` keyword.

This is the same process you saw in the previous section where we talked about function constructors. If your class accepts any parameters, you can now pass appropriate values as arguments. You defined those parameters in the `constructor` method where you also assigned them as class properties.

Let's use the `User` function constructor and write it as a class. This will help you see how similar classes and function constructors are. If you want to learn more about JavaScript classes, take a look at this tutorial I wrote, [part one] and [part two].

```JavaScript
// Create a new class "User".
class User {
  // Create constructor method
  // and define parameters for "name", "username" and "email".
  constructor(name, username, email) {
    this.name = name
    this.username = username
    this.email = email

    // Also, add one class method.
    this.sayHi = function() {
      return `Hi, my name is ${this.name}.`
    }
  }
}

// Use "User" class to create new instance, new object.
const userJill = new User('Jill', 'jill987', 'jill@hello.com')

// Log the content of userJill instance/object
console.log(userJill)
// Output:
// User {
//   name: 'Jill',
//   username: 'jill987',
//   email: 'jill@hello.com',
//   sayHi: ƒ (),
//   __proto__: User { constructor: ƒ User() }
// }

// Log the value of "name" property of "userJill".
console.log(userJill.name)
// Output:
// 'Jill'

// Log the value of "username" property of "userJill".
console.log(userJill.username)
// Output:
// 'jill987'

// Log the value of "email" property of "userJill".
console.log(userJill.email)
// Output:
// 'jill@hello.com'

// Call the sayHi method.
console.log(userJill.sayHi())
// Output:
// 'Hi, my name is Jill.'
```

## Conclusion: [...] ...

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
-
-->
