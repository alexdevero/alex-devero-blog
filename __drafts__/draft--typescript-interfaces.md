# TypeScript Interfaces: A Quick Guide to Help You Start

TypeScript brings many useful improvements to JavaScript language. One of them is static typing system that can help you write type safe code. Interfaces are part of this typing system. This tutorial will help you learn what TypeScript interfaces are, how they work and how to use them.<!--more-->

<!--
Table of Contents:
## h2
### h3
### h3
## h2
## Conclusion: [...] ...
-->

## JavaScript, objects and black swans

In JavaScript, and elsewhere as well, objects are one of the most popular ways to group related data together and pass them around. The problem is, there is no way in JavaScript to specify how certain object should look like. There is no way to say what properties should object have or what their values should be.

This makes it easy to create code that is prone to errors. For example, to create an object and forget to add some property. Then, when it comes the time to finally use that object, you code will fail and program will crash. Reason? Your program expected specific property that is that is missing.

The problem might not be a missing property. It might be that the type of a value of some property is different from what your program expected. The result is often the same. Code fails and program crashes. One may argue that this is not likely to happen. Well, earthquakes and floods are also not likely to happen.

The thing is, nobody cares about probability when these events, these [black swans], occur. Your users will not care that wrong type or missing property is not likely to happen when the app they are using crashes. If only there was a way to avoid this. Maybe, TypeScript can help here.

## TypeScript interfaces made simple

The main feature of TypeScript is its powerful type system. This type system allows you to quickly specify primitive data types for variables. These simple types are only one part of this type systems. TypeScript also allows you to do this with objects. With the help of TypeScript, you can define shape of any objects.

Shape of an object specifies what properties a given object contains. This also includes their types, what types should values of these properties be. In TypeScript, you can specify this shape via interface. TypeScript interfaces are abstract types. Interfaces tell the compiler two important things.

First, interfaces tell what properties a given object could have or must have. This means that when some property is optional, TypeScript will know that these properties are not required and will not require you to define them. Second, interfaces specify the types of these properties, types of their values.

With this information, TypeScript can warn you when you accidentally define some object property and use a wrong type. TypeScript will know what type is expected to be used for each object property. If you use different type, TypeScript will tell you about the mismatch, where it happened and also how to fix it.

## Creating an interface

When you want to create a new interface, you do it by using the `interface` keyword. This keyword is followed by the name of the interface ad curly brackets. These brackets contain the shape of an object, its properties and types. You specify these properties and types as key-value pairs.

This is very similar to creating new [object literal]. However, there are some differences. First, there is no equal sign between the name of the interface and curly brackets. Second, those key-value pairs are separated by semicolons. Below are examples of simple TypeScript interfaces.

```TypeScript
// Create an empty interface
interface EmptyObject {}

// Create interface Cat:
interface Cat {
  name: string;
  age: number;
  hairColor: string;
  weight: number;
  height: number;
}

// Create interface Car:
interface Car {
  model: string;
  manufacturer: string;
  numberOfWheels: number;
  type: string;
}

// Create interface User:
interface User {
  username: string;
  password: string;
  email: string;
  isActive: boolean;
  role: 'admin' | 'user' | 'guest';
}
```

The `Cat` interface defines an object that has five properties: `name`, `age`, `hairColor`, `weight` and `height`. All these properties are required. Values of `name` and `hairColor` must be strings. The rest must be numbers. The `Car` interface defines an object that has four properties: `model`, `manufacturer`, `numberOfWheels` and `type`.

These properties are also all required. Value of `numberOfWheels` must be a number. The rest must be strings. Lastly, the `User` interface defines an object that has again five properties: `username`, `password`, `email`, `isActive` and `role`. Values of the first three must be strings.

The value of `isActive` property must be a boolean, either true or false. The value of `role` is more concrete. It says that the value must be one of these three strings: `'admin'`, `'user'` or `'guest'`. If you use any other string, TypeScript will warn you that the value you use is wrong, even though the type is the same.

### Implicit interfaces

TypeScript interfaces don't have to be created only by you, explicitly. TypeScript will also create interfaces on its own when you define an object. TypeScript will look at the properties of that object and values of these properties. Then, it will infer specific types using type inference.

The result will be implicit interface that matches the object you've just created. This also applies if you create empty object, without any properties. TypeScript will simply create an empty interface. This can later cause troubles when you try to add properties because TypeScript will expect the object to be, and remain, empty.

A simple way to avoid this is by defining interfaces by yourself, explicitly. If create an empty object also create an interface for it. This interface will not specify the current shape of the object, but the shape of it in the future. This will tell TypeScript which properties and types to expect.

## Using interfaces

When you create an interface you also have to tell TypeScript for which object you intend to use it. Doing so is easy. When you assign an object to a variable you can specify its interface by adding colons and the name of the interface between the variable name and equal sign.

```TypeScript
// Create an interface:
interface User {
  password: string;
  email: string;
  role: 'admin' | 'user' | 'guest';
  logUserData: () => string;
}

// Use interface to annotate an object:
const userJoe: User = {
  password: 'some_secret_password123645',
  email: 'joe@user.co',
  role: 'user',
  logUserData: () => `${email}, ${role}`
}
```

This also applies elsewhere. If you want to use an interface for an object used as a function parameter you use the same approach. You specify the parameter, then add colons, and then you specify the interface.

```TypeScript
// Create an interface:
interface User {
  password: string;
  email: string;
  role: 'admin' | 'user' | 'guest';
  logUserData: () => string;
}

// Create a function with "user" parameter
// and annotate the "user" parameter with User interface.
function getUserEmail(user: User) {
  return user.email
}
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
