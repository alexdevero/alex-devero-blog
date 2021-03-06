# TypeScript Interfaces: A Quick Guide to Help You Get Started

TypeScript brings many useful improvements to JavaScript language. One of them is static typing system that can help you write type safe code. Interfaces are part of this typing system. This tutorial will help you understand what TypeScript interfaces are and how to use them.<!--more-->

<!--
Table of Contents:
## JavaScript, objects and black swans
## TypeScript interfaces made simple
## Creating an interface
### Implicit interfaces
## Using interfaces
## Implementing interfaces with classes
## Specifying optional properties
## Specifying read-only properties
## Interfaces for functions
## Extending interfaces
## Creating generic interfaces
## Conclusion: TypeScript interfaces
-->

## JavaScript, objects and black swans

In JavaScript, and elsewhere as well, objects are one of the most popular ways to group related data together and pass them around. The problem is, there is no way in JavaScript to specify how certain object should look like. There is no way to say what properties should object have or what their values should be.

This makes it easy to create code that is prone to errors. For example, to create an object and forget to add some property. Then, when it comes the time to finally use that object, you code will fail and program will crash. Reason? Your program expected specific property that is that is missing.

The problem might not be a missing property. It might be that the type of a value of some property is different from what your program expected. The result is often the same. Code fails and program crashes. One may argue that this is not likely to happen. Well, earthquakes and floods are also not likely to happen.

The thing is, nobody cares about probability when these events, these [black swans], occur. Your users will not care that wrong type or missing property is not likely to happen when the app they are using crashes. If only there was a way to avoid this. Maybe, TypeScript can help you here.

## TypeScript interfaces made simple

The main feature of TypeScript is its powerful type system. This type system allows you to quickly specify [primitive data types] for variables. These simple types are only one part of this type systems. TypeScript also allows you to do this with objects. With the help of TypeScript, you can define shape of any objects.

Shape of an object specifies what properties a given object contains. This also includes their types, what types should values of these properties be. In TypeScript, you can specify this shape via interface. TypeScript interfaces are abstract types. Interfaces tell the compiler two important things.

First, interfaces tell what properties a given object could have or must have. This means that when some property is optional, TypeScript will know that these properties are not required and will not require you to define them. Second, interfaces specify the types of these properties, types of their values.

With this information, TypeScript can warn you when you accidentally define some object property and use a wrong type. TypeScript will know what type is expected to be used for each object property. If you use different type, TypeScript will tell you about the mismatch, where it happened and also how to fix it.

## Creating an interface

When you want to create a new interface, you do it by using the `interface` keyword. This keyword is followed by the name of the interface add curly brackets. These brackets contain the shape of an object, its properties and types. You specify these properties and types as key:value pairs.

This is very similar to creating new [object literal]. However, there are some differences. First, there is no equal sign between the name of the interface and curly brackets. Second, those key:value pairs are separated by semicolons. Below are examples of simple TypeScript interfaces.

```TypeScript
// Create an empty interface:
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

A simple way to avoid this is by defining interfaces by yourself, explicitly. If you create an empty object also create an interface for it. This interface will not specify the current shape of the object, but the shape of it in the future. This will tell TypeScript which properties and types to expect.

## Using interfaces

When you create an interface you also have to tell TypeScript for which object you intend to use it. Doing so is easy. When you assign an object to a variable you can specify its interface by adding colons and the name of the interface between the variable name and equal sign.

```TypeScript
// Create an interface User:
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
// Create an interface User:
interface User {
  password: string;
  email: string;
  role: 'admin' | 'user' | 'guest';
  logUserData: () => string;
}

// Create a function with "user" parameter
// and annotate the "user" parameter with "User" interface.
function getUserEmail(user: User) {
  return user.email
}
```

## Implementing interfaces with classes

TypeScript also allows you to use interface with [JavaScript classes]. With classes, though, the implementation is slightly different. You still specify the interface after the name, class name in this case. However, you don't put colons between the name of the class and the interface.

What you do instead is basically replacing those colons with `implements` keyword. This will tell TypeScript that a given class should use an interface that follows after this keyword.

```TypeScript
// Create interface Person:
interface Person {
  // Define some class properties
  // of type string and number:
  firstName: string;
  lastName: string;
  age: number;
  gender: 'male' | 'female';
  // Define class method that returns a string:
  sayHello: () => string;
}

// Annotate class "Female" with "Person" interface:
class Female implements Person {
  // Define required public properties:
  firstName: string
  lastName: string
  age: number
  gender: 'male' | 'female'

  // Create constructor and assign existing properties:
  constructor(firstName: string, lastName: string, age: number, gender: 'male' | 'female') {
    this.firstName = firstName
    this.lastName = lastName
    this.age = age
    this.gender = gender
  }

  // Define required class method:
  sayHello() {
    return `Hello, my name is ${this.firstName}.`
  }
}
```

## Specifying optional properties

Until now, all examples we were using used only required properties. This will work for many cases. However, it can happen that you may not need some properties in a given object every time. One thing you can do is to create a new interface, without optional properties. Then, you can switch between these interfaces as you need.

This will work, but it will also lead to duplicates and more code to maintain. There is another thing you can do. You can take the original interface and mark the optional properties as optional. You achieve this by placing a question mark (`?`) between the property name and the colons.

```TypeScript
// Create an interface with optional properties:
interface Person {
  firstName: string;
  lastName: string;
  middleName?: string; // <= This property will be optional
}

// This will work:
const bill: Person = {
  firstName: 'Bill',
  lastName: 'Doherty',
  middleName: 'Stevens'
}

// This will also work because "middleName"
// property is not required:
const will: Person = {
  firstName: 'William',
  lastName: 'Connors',
}

// This will not work because "lastName"
// property is required but missing:
const jack: Person = {
  firstName: 'Jack',
  middleName: 'O\'Conor',
}
// TS error: Property 'lastName' is missing in type '{ firstName: string; middleName: string; }' but required in type 'Person'.
```

## Specifying read-only properties

When you create an object you may want to prevent some properties from being changed. You can specify this intent also via TypeScript interfaces. You achieve this by placing the `readonly` keyword before the property name. This will tell TypeScript that the property that follows is a read-only property.

If you use the interface to annotate some object, you will be able to set the value for the read-only property only during initialization. If you try to change the property value later, TypeScript compiler will throw an error.

```TypeScript
// Create interface with read-only property:
interface User {
  username: string;
  password: string;
  readonly email: string; // <= This property will be read-only
}

// Annotate object "userFrank" with "User" interface:
const userFrank: User = {
  username: 'frankie',
  password: '123456782',
  email: 'frankie@frank.com'
}

// Try to change value of "username" property:
userFrank.username = 'frankman'

// Try to change value of "email" property:
userFrank.email = 'frankman@frank.com'
// TS error: Cannot assign to 'email' because it is a read-only property.
```

## Interfaces for functions

Objects, including classes, are not the only things that can use interfaces. You can also use TypeScript interfaces to annotate functions. You can do this by giving the interface a call signature. This means that you will specify only the parameter list and return type of the function.

```TypeScript
// Create interface for multiply function:
interface MultiplyFunc {
  // Specify only parameters and return type:
  (a: number, b: number): number;
}

// Annotate the "multiply" function
// with "MultiplyFunc" interface:
const multiply: MultiplyFunc = (a, b) => {
  return a * b
}

// Note:
// Thanks to MultiplyFunc interface TypeScript
// will know that "a" and "b" in "multiply" function
// are numbers so you don't have to type them explicitly.
```

One thing about interfaces and functions. Name of parameters in an interface doesn't have to match the name of parameters in the actual function. You can use one name for interface parameter and another for the function declaration. TypeScript will connect parameters with their types correctly using their order.

```TypeScript
interface MyFunc {
  // Specify only parameters and return type:
  (a: number, b: string, c: boolean): string;
}

// Annotate the "multiply" function
// with "MultiplyFunc" interface:
const myFunc: MyFunc = (a, b, c) => {
  return `a is ${a}, b is ${b}, c is ${c}`
}
// TypeScript will correctly infer "a" to be number,
// "b" to be string and "c" to be boolean.
```

## Extending interfaces

One useful thing is that interfaces allow extending, just like JavaScript classes. Let's say you have an existing interface. You also have an object, but this object contains more properties than the interface specifies. One thing you can do is to change the interface to fit this object.

The problem is that this will influence all objects using that interface. Another thing is creating new interface, duplicating the old one and adding new properties. This will bloat your code with duplicates. Luckily, there is the third option. You can create new interface and extend it with the original.

This way, the new interface will inherit all properties defined in the original interface. Best part? You will not have to copy a single line of code. You can extend interface by using the `extends` keyword. This keyword allows you to extend one interface with just one interface as well as with multiple.

When you want to extend interface with multiple interfaces you separate them with commas. The `extends` keyword goes between the first interface, the one you are extending, and the second, the one you are extending with.

```TypeScript
// Create "Person" interface:
interface Person {
  name: string;
}

// Create "Male" interface that extends "Person" interface:
interface Male extends Person {
  gender: 'Male';
}
// Basically translates to:
// interface Male {
//   name: string;
//   gender: 'Male';
// }

// Create "Female" interface that also extends "Person" interface:
interface Female extends Person {
  gender: 'Female';
}
// Basically translates to:
// interface Female {
//   name: string;
//   gender: 'Female';
// }

// Create "Boy" interface that extends "Person" and "Male" interfaces:
interface Boy extends Person, Male {
  age: number;
}
// Basically translates to:
// interface Boy {
//   name: string;
//   gender: 'Male';
//   age: number;
// }

// Create "Girl" interface that extends "Person" and "Female" interfaces:
interface Girl extends Person, Female {
  age: number;
}
// Basically translates to:
// interface Girl {
//   name: string;
//   gender: 'Female';
//   age: number;
// }

const stanley: Person = {
  name: 'Stanley'
}

const david: Male = {
  name: 'David',
  gender: 'Male'
}

const sarah: Female = {
  name: 'Sarah',
  gender: 'Female'
}

const andreas: Boy = {
  name: 'Andreas',
  gender: 'Male',
  age: 13
}

const victoria: Girl = {
  name: 'Victoria',
  gender: 'Female',
  age: 6
}
```

## Creating generic interfaces

One more thing. TypeScript also allows to create something called "generic interfaces". These interfaces allow you to specify type of a property based on one or more parameters you provide the interface with when you use it. You can specify these parameters using angle brackets (`<>`) like in the example below.

```TypeScript
// Create interface for UserData:
interface UserData {
  name: string;
  email: string;
}

// Create a generic interface:
interface ApiResponse<T> {
  date: Date;
  code: number;
  payload: T[];
}

// Create function to fetch API
async function fetchAPI() {
  // Use ApiResponse "interface" and pass
  // the "UserData" interface as argument (for T argument):
  const data: ApiResponse<UserData> = await fetch('/some_api_endpoint')

  // The "ApiResponse<UserData>" basically translates to:
  // interface ApiResponse<T> {
  //   date: Date;
  //   code: number;
  //   payload: UserData[];

  //   Or:
  //   payload: [name: string; email: string;]
  // }
}
```

## Conclusion: TypeScript interfaces

TypeScript interfaces provide an easy way to annotate your objects, including classes, and also functions. This can help you write safer and more maintainable code. I hope that this tutorial helped you understand and learn about what interfaces are and how to use them in your code.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->

[black swans]: https://en.wikipedia.org/wiki/Black_Swan_theory
[primitive data types]: https://blog.alexdevero.com/javascript-basics-data-types-pt1/
[object literal]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer
[javascript classes]: https://blog.alexdevero.com/get-started-with-javascript-classes/

<!--
### Meta:
-
-->

<!--
### Keywords:
- TypeScript Interfaces
-->

<!--
### Resources:
-
-->
