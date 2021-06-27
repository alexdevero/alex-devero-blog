# Getting Started With TypeScript Built-in Utility Types Part 1

TypeScript can be difficult to understand for many developers. One area causing troubles are advanced types. Part of this area are utility types built in TypeScript. They can help you create new types from existing. In this article, you will learn how some of these utility types work and how to use them.<!--more-->

<!--
Table of Contents:
## A short introduction to utility types
## About the syntax
## Note on availability
## Partial<Type>
## Required<Type>
## Readonly<Type>
## Record<Keys, Type>
## Pick<Type, Keys>
## Omit<Type, Keys>
## Exclude<Type, ExcludedUnion>
## Extract<Type, Union>
## Conclusion: Getting Started With TypeScript Built-in Utility Types Part 1
-->

## A short introduction to utility types

TypeScript provides a powerful system for working with types. There are the basic types you already know from JavaScript. For example, types such as number, string, boolean, object, symbol, null, undefined. This is not all TypeScript offers. On top of these types are also built-in utility types.

It is sometimes also these utility types that can be the most difficult to understand for developers coming to TypeScript. This is especially true when you see this types for the first time. The good news is that these types are actually not that difficult, if you understand one important thing.

All those built-in utility types are actually simple functions, function you already know from JavaScript. Main difference here is that these functions, these utility types, work only with types. What these functions do is they transform types from one type to another. They take some input.

This input is some type you are starting with. You can also provide multiple types. What comes next is that the function transforms that input and return appropriate output. This output are also some types. The type of transformation that happens depends on the utility type you use.

There are currently around 17 utility types: `Partial<Type>`, `Required<Type>`, `Readonly<Type>`, `Record<Keys,Type>`, `Pick<Type, Keys>`, `Omit<Type, Keys>`, `Exclude<Type, ExcludedUnion>`, `Extract<Type, Union>`, `NonNullable<Type>`, `Parameters<Type>`, `ConstructorParameters<Type>`, `ReturnType<Type>`, `InstanceType<Type>`, `ThisParameterType<Type>`, `OmitThisParameter<Type>`, `ThisType<Type>` and Intrinsic String Manipulation Types. Let's start with the first eight.

## About the syntax

All utility types in TypeScript use similar syntax. This will make it easier for you to learn it and remember it. It will also make it easier if you try to see these types as something like functions. Then, usually helps to understand the syntax faster, sometimes much faster. About the syntax.

Every utility type starts with the name of the type. This name always starts with capital letter. Following the name are left- and right-pointing angle bracket, less than and greater than symbols (`<>`). Between these brackets goes parameters. These parameters are the types you are working with, the input.

When you think about it, using a utility type is like calling a function and passing something as an argument. One difference here is that the function always starts with capital letters. Second difference is that you don't use parentheses after the function name, but those angle brackets.

Some types require one parameter, others require two. Similarly to JavaScript, these parameters are divided by colon (`,`), and passed between the angle brackets. The simple example below illustrates the similarity between plain function and TypeScript utility type.

```TypeScript
// Calling a function in JavaScript
myFunction('some argument')

// Using built-in type in TypeScript
UtilityType<'some type'>
UtilityType<'some type', 'some type'>
```

## Note on availability

The types you will learn about are available in TypeScript from version 4.0. Make sure you use this version. Otherwise, some of the types bellow may not work, or not without some additional packages.

## Partial<Type>

When you create a [type] or an [interface], all types defined inside will be required as default. If you want to mark some as optional, you can use the `?` and place it after the property name. This will make the property optional. If you want all properties to be optional, do you have to add the `?` after all of them?

You can do this, but it will change the interface. It will also have an impact on everything that works with that interface. Another option you can use is `Partial<Type>`. This type accepts one parameter, the type want to make optional. It returns the same type, but in which all previously required properties are now optional.

```TypeScript
// Create an interface:
interface Person {
  name: string;
  age: number;
  jobTitle: string;
  hobbies: string[];
}

// Create object using Person interface:
const jack: Person = {
  name: 'Jack',
  age: 33,
  jobTitle: 'CTO',
  hobbies: ['reading']
}
// This works because 'jack' object contains
// all properties specified in Person interface.

// Create another object using Person interface:
const andrei: Person = {
  name: 'Andrei',
  age: 48,
}
// TS error: Type '{ name: string; age: number; }' is missing the following properties from type 'Person': jobTitle, hobbies.

// Use Partial<Type> along with Person interface
// to make all properties in Person interface optional:
const andrei: Partial<Person> = {
  name: 'Andrei',
  age: 48,
}

// This will also work:
const joe: Partial<Person> = {}

// The interface after Partial:
// interface Person {
//   name?: string;
//   age?: number;
//   jobTitle?: string;
//   hobbies?: string[];
// }
```

## Required<Type>

The `Required<Type>` is the direct opposite of the `Partial<Type>`. If the `Partial<Type>` makes all properties optional, the `Required<Type>` makes them all required, non-optional. The syntax of `Required<Type>` is the same as of `Partial<Type>`. Only difference is the name of the utility type.

```TypeScript
// Create an interface:
interface Cat {
  name: string;
  age: number;
  hairColor: string; // <= Make "owner" property optional
  owner?: string; // <= Make "owner" property optional
}

// This will work:
const suzzy: Cat = {
  name: 'Suzzy',
  age: 2,
  hairColor: 'white',
}

// Use Required<Type> along with Cat interface
// to make all properties in Cat interface required:
const suzzy: Required<Cat> = {
  name: 'Suzzy',
  age: 2,
  hairColor: 'white',
}
// TS error: Property 'owner' is missing in type '{ name: string; age: number; hairColor: string; }' but required in type 'Required<Cat>'.

// Works without errors:
const lucy: Cat = {
  name: 'Lucy',
  age: 1,
  hairColor: 'brown',
}

// Make all properties of Cat required:
const lucy: Required<Cat> = {
  name: 'Lucy',
  age: 1,
}
// TS error: Type '{ name: string; age: number; }' is missing the following properties from type 'Required<Cat>': hairColor, owner
```

## Readonly<Type>

Sometimes you may want to make some data immutable, prevent them from being changed. The `Readonly<Type>` type helps you make this change for the whole type. For example, you can make all properties in an interface readonly. When you use that interface with some object, and try to change some object property, TypeScript will throw an error.

```TypeScript
// Create an interface:
interface Book {
  title: string;
  author: string;
  numOfPages: number;
}

// Create an object that uses the Book interface:
const blitzscaling: Book = {
  title: 'Blitzscaling',
  author: 'Reid Hoffman, Chris Yeh',
  numOfPages: 318
}

// Try to change properties:
blitzscaling.title = 'High Growth Handbook'
blitzscaling.author = 'Elad Gil'
blitzscaling.numOfPages = 353

// Log the value of blitzscaling:
console.log(blitzscaling)
// Output:
// {
//   "title": "High Growth Handbook",
//   "author": "Elad Gil",
//   "numOfPages": 353
// }


// Make all properties of Book readonly
const sevenPowers: Readonly<Book> = {
  title: '7 Powers',
  author: 'Hamilton Helmer',
  numOfPages: 226
}

// Try to change properties:
sevenPowers.title = 'The Innovator\'s Dilemma'
// TS error: Cannot assign to 'title' because it is a read-only property.
```

## Record<Keys, Type>

Let's say you have a set of properties and values for these properties. Based on this data, the `Record<Keys, Type>` allows you to create a records of key-value pairs. The `Record<Keys, Type>` basically creates a new interface by mapping all unit types specified as `Keys` parameter with their value's types specified as `Type` parameter.

```TypeScript
// Example no.1:
// Create type Table with Record:
type Table = Record<'width' | 'height' | 'length', number>

// type Table is basically ('width' | 'height' | 'length' are keys, number is a value):
// interface Table {
//   width: string;
//   height: string;
//   length: string;
// }

// Create new object based on Table type:
const smallTable: Table = {
  width: 50,
  height: 40,
  length: 30
}

// Create new object based on Table type:
const mediumTable: Table = {
  width: 90,
  length: 80
}
// TS error: Property 'height' is missing in type '{ width: number; length: number; }' but required in type 'Table'.


// Example no.2:
// Create type with some string keys:
type PersonKeys = 'firstName' | 'lastName' | 'hairColor'

// Create a Record using PersonKeys and type:
type Person = Record<PersonKeys, string>

// type Person is basically (personKeys are keys, string is a value):
// interface Person {
//   firstName: string;
//   lastName: string;
//   hairColor: string;
// }

const jane: Person = {
    firstName: 'Jane',
    lastName: 'Doe',
    hairColor: 'brown'
}

const james: Person = {
    firstName: 'James',
    lastName: 'Doe',
}
// TS error: Property 'hairColor' is missing in type '{ firstName: string; lastName: string; }' but required in type 'Person'.


// Example no.3:
type Titles = 'ZeroToOne' | 'Blitzscaling' | 'InnovatorsDilemma'

interface Book {
  title: string;
  author: string;
}

const books: Record<Titles, Book> = {
  ZeroToOne: {
    title: 'Zero to One',
    author: 'Peter Thiel, Blake Masters'
  },
  Blitzscaling: {
    title: 'Blitzscaling',
    author: 'Reid Hoffman, Chris Yeh'
  },
  InnovatorsDilemma: {
    title: 'The Innovator\'s Dilemma',
    author: 'Clayton M. Christensen'
  },
}

// Record<Titles, Book> basically translates to:
ZeroToOne: { // <= "ZeroToOne" key is specified in "Titles".
  title: string,
  author: string,
}, // <= Value of "ZeroToOne" is specified in "Book".
Blitzscaling: { // <= "Blitzscaling" key is specified in "Titles".
  title: string,
  author: string,
}, // <= Value of "Blitzscaling" is specified in "Book".
InnovatorsDilemma: { // <= "InnovatorsDilemma" key is specified in "Titles".
  title: string,
  author: string,
} // <= Value of "InnovatorsDilemma" is specified in "Book".
```

## Pick<Type, Keys>

Let's say you want to use only some properties of an existing interface. One thing you can do is to create new interface, with only those properties. Another options is to use `Pick<Type, Keys>`. Pick type allows you to take existing type (`Type`) and pick only some specific keys (`Keys`) from it, while ignoring the rest.

```TypeScript
// Create an interface
interface Beverage {
  name: string;
  taste: string;
  color: string;
  temperature: number;
  additives: string[] | [];
}

// Create type based from Beverage using
// only "name", "taste" and "color" properties:
type SimpleBeverage = Pick<Beverage, 'name' | 'taste' | 'color'>

// Basically translates to:
// interface SimpleBeverage {
//   name: string;
//   taste: string;
//   color: string;
// }

// Use SimpleBeverage type to create new object:
const water: SimpleBeverage = {
  name: 'Water',
  taste: 'bland',
  color: 'transparent',
}
```

## Omit<Type, Keys>

The `Omit<Type, Keys>` is basically an opposite of `Pick<Type, Keys>`. You specify some type as an argument for `Type`, but instead of picking properties you want, you choose properties you want to omit from existing type.

```TypeScript
// Create interface for car:
interface Car {
  model: string;
  bodyType: string;
  numOfWheels: number;
  numOfSeats: number;
  color: string;
}

// Create type for boat based on Car interface,
// but omit "numOfWheels" and "bodyType" properties:
type Boat = Omit<Car, 'numOfWheels' | 'bodyType'>

// Basically translates to:
// interface Boat {
//   model: string;
//   numOfSeats: number;
//   color: string;
// }

// Create new object based on Car:
const tesla: Car = {
  model: 'S',
  bodyType: 'sedan',
  numOfWheels: 4,
  numOfSeats: 5,
  color: 'grey',
}

// Create new object based on Boat:
const mosaic: Boat = {
  model: 'Mosaic',
  numOfSeats: 6,
  color: 'white'
}
```

## Exclude<Type, ExcludedUnion>

The `Exclude<Type, ExcludedUnion>` can be a bit confusing on the first sight. What this utility type does is it returns the type you used as an argument for `Type` without any type you mentioned as an argument for the `ExcludedUnion`.

```TypeScript
// Crete type Colors:
type Colors = 'white' | 'blue' | 'black' | 'red' | 'orange' | 'grey' | 'purple'

type ColorsWarm = Exclude<Colors, 'white' | 'blue' | 'black' | 'grey'>
// Translates to:
// type ColorsWarm = "red" | "orange" | "purple"

type ColorsCold = Exclude<Colors, 'red' | 'orange' | 'purple'>
// Translates to:
// type ColorsCold = "white" | "blue" | "black" | "grey"

// Create warm color:
const varmColor: ColorsWarm = 'red'

// Create cold color:
const coldColor: ColorsCold = 'blue'

// Try to mix it:
const coldColorTwp: ColorsCold = 'red'
// TS error: Type '"red"' is not assignable to type 'ColorsCold'.
```

## Extract<Type, Union>

The `Extract<Type, Union>` type does the opposite of the `Exclude<Type, ExcludedUnion>` type. It takes everything you specified as the `Type` argument and uses only parts that you've mentioned in the `Union` argument.

```TypeScript
type Food = 'banana' | 'pear' | 'spinach' | 'apple' | 'lettuce' | 'broccoli' | 'avocado'

type Fruit= Extract<Food, 'banana' | 'pear' | 'apple'>
// Translates to:
// type Fruit = "banana" | "pear" | "apple"

type Vegetable = Extract<Food, 'spinach' | 'lettuce' | 'broccoli' | 'avocado'>
// Translates to:
// type Vegetable = "spinach" | "lettuce" | "broccoli" | "avocado"

// Create warm color:
const someFruit: Fruit = 'pear'

// Create cold color:
const someVegetable: Vegetable = 'lettuce'

// Try to mix it:
const notReallyAFruit: Fruit = 'avocado'
// TS error: Type '"avocado"' is not assignable to type 'Fruit'.
```

## Conclusion: Getting started with TypeScript built-in utility types part 1

Advanced types in TypeScript, especially built-in utility types, can be very useful. That said, they may also seem daunting. I hope that this tutorial helped you learn about those eight types we discussed today, the `Partial`, `Required`, `Readonly`, `Record`, `Pick`, `Omit`, `Exclude` and `Extract`.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->

[type]: https://blog.scottlogic.com/2021/06/24/types-vs-interfaces.html
[interface]: https://www.typescriptlang.org/docs/handbook/typescript-tooling-in-5-minutes.html#interfaces

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
