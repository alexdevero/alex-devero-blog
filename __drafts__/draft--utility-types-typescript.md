# Getting Started With Built-in Utility Types in TypeScript Part 1

TypeScript can be difficult to understand for many developers. One area causing troubles are advanced type. Part of this area are built-in utility types provided by TypeScript. They can help you create new types from existing. In this article, you will learn how utility types work and how to use them.

<!--more-->
<!--
Table of Contents:
## h2
### h3
### h3
## h2
## Conclusion: [...] ...
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


## h2

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
