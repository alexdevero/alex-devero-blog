# Getting Started With React and TypeScript Pt.4 - Tips on Getting Started
Getting started with React and TypeScript can be difficult. There are so many things to learn. Fortunately, it doesn't have to be. In this article, I will share with you few tips that will help you make this easier. Use these tips and start with React and TypeScript faster.
<!--
Table of Contents:
## Take it slowly
### Create a "learning" project
### Disable the strict rule (just for now)
## Avoid using any
## Don't be afraid of using interfaces (or type aliases)
## Interfaces, type aliases... Don't over-think, just be consistent
## Don't annotate everything, embrace automatic type inference
## Remember, it is still JavaScript
## If in doubt, work on your JavaScript skills
## Conclusion: Getting Started With React and TypeScript
-->

Getting Started With React and TypeScript [Part 1].

Getting Started With React and TypeScript [Part 2].

Getting Started With React and TypeScript [Part 3].

## Take it slowly

When you are just starting with React and TypeScript, take it slowly. It might be tempting to enable all recommended rules in your tsconfig. This may work for some people. For other people it doesn't work at all. Using all recommended rules can help you learn how to work with React and TypeScript faster.

This is true especially when you start playing with React and TypeScript in a new project. When you start building something from scratch, for the purpose to learn and practice working with React and TypeScript. In that case, there is nothing that can break. On the other hand, what if you do this in an existing project?

In an existing project, a lot of things can break. When I started with TypeScript I decided to implement TypeScript in one of my projects. It was a small project. That didn't matter. Small project or not, it still took me a couple of days before I was able to fix all issues, following the recommended TypeScript configuration.

True, it did help me learn a lot of things faster, much faster. This is what learning the "hard way" does very well. However, it also took a lot of patience to go from one failing build to another. This can be discouraging for many people. If this doesn't sound like something you would want to go through, then there are other approaches that work.

### Create a "learning" project

One option is to create new project from scratch, solely for the purpose of learning about React and TypeScript and how to work with both. When you start from scratch, there is nothing that can break. There is nothing that could cause avalanche of errors and warnings you would have to fix over a couple of days.

This will make it easier for you to get into React and TypeScript. One step at the time, you will learn how to work with components, hooks and JavaScript the "TypeScript" way. This may take longer than going all-in. That doesn't matter. What matters is to use approach that works for you, regardless of the time it takes.

### Disable the strict rule (just for now)

Another option is to try implementing TypeScript in one of your existing project with the [strict] rule disabled. Disabling this rule will disable all strict type checking options. These are: `--noImplicitAny`, `--noImplicitThis`, `--alwaysStrict`, `--strictBindCallApply`, `--strictNullChecks`, `--strictFunctionTypes` and `--strictPropertyInitialization`.

When you disable this rule TypeScript compile your code even if one of the strict type checking will not pass the test. If you use IDE with intellisense support for TypeScript, such as [VS Code], IDE will still show you issues in your code. Another option, to see issues in your code, is to use [typescript-eslint].

With the strict option disabled, you can gradually fix and annotate your code as necessary. This will be more friendly way to add TypeScript to your project, not that hard slap, or punch, in the face after you start the dev server. When you are done, don't forget to enable the strict option.

## Avoid using any

Some developers like to use the [any] type almost everywhere. This is supposed to make it easier to start with TypeScript. This is not a good idea and definitely not a good practice. What is the point of using typed language, or typed superset of language, if you don't use its type system properly?

One purpose of using typed language is to use proper types to prevent errors. Using `any` goes against this. When you use `any` it means that that thing can be of any type. It can be `string`, `number`, `boolean`, `object`, `array`, whatever. Also, using `any` allows to change the type of that thing.

For example, let's say you infer something as `any` you can then assign it a `string`. Later, you can change your mind and assign it a `number`. A bit more later, you can change your mind again and change it to `boolean`. You don't have to start using TypeScript to create this mess. JavaScript will be more than enough to do that.

If you do want to start using TypeScript you should also use its type system properly. This means avoiding `any` when you can, which will be very often. There are some situations where using `any` is an option.  One such as situation is when you work with 3rd party packages, libraries, modules or APIs.

In situations like these, you may not always know what to expect. This is especially true if the package, module or library you are working with doesn't have type definitions. In that case, using `any` will let your code compile without the need to spend hours trying to figure out all necessary types.

Another situation where `any` can be used is when you want to rewrite your JavaScript code to TypeScript. In case of React app, when you want to migrate to React and TypeScript. Using `any` will suppress many errors you would have to deal with otherwise. With `any`, you can solve them one by one without breaking your app.

That said, I would still rather disable the strict rule, in this case, annotate your code properly. Then, enable the strict rule again. The reason is that using `any` can lead to bad habits and practices. As the saying goes, "do it once, do it twice and it becomes a habit". Once you start using `any` it might be difficult to stop with it.

## Don't be afraid of using interfaces (or type aliases)

Some JavaScript and React developers don't like the idea of using [interfaces], or [type aliases]. They see more code in their editor and they automatically assume the compiled code will also become bigger. It will be cluttered by the code created for interfaces. This is not going to happen.

When you create and use an interface in your code, TypeScript will use that code only to do type checking during the runtime and compilation. However, it will not compile that code. Not a single line of your code for interfaces will end up in compiled JavaScript. Let's take a look at a simple example.

Let's create an `interface` with four properties, `name` (string), `age` (number), `occupation` (string) and `yearOfBirth` (number). Next, let's declare new variable, an object, called `stan` and initialize it with some data, using the interface to define the shape of this variable. When you compile this code, only the variable `stan` will remain.

```ts
// This:
interface UserInterface {
    name: string;
    age: number;
    occupation: string;
    yearOfBirth: number;
}

const stan: UserInterface = {
    name: 'Stan Drake',
    age: 29,
    occupation: 'programmer',
    yearOfBirth: 1990
}

// Will compile to this:
"use strict";
const stan = {
    name: 'Stan Drake',
    age: 29,
    occupation: 'programmer',
    yearOfBirth: 1990
};
```

The same is also true for type aliases. They will also not be compiled.

```ts
// This:
type Book = {
    title: string,
    author: string,
    numberOfPages: number,
    publicationDate: number,
}

const warAndPeace: Book = {
    title: 'War and Peace',
    author: 'Leo Tolstoy',
    numberOfPages: 1296,
    publicationDate: 1869,
}

// Will compile to this:
"use strict";
const warAndPeace = {
    title: 'War and Peace',
    author: 'Leo Tolstoy',
    numberOfPages: 1296,
    publicationDate: 1869,
};
```

As you can see, interfaces and type aliases don't lead to clutter in compile code. They will not make your compiled code bigger. Your compiled code will stay the same no matter how many interfaces and type aliases you use. So, don't worry about this and keep using interfaces and type aliases to annotate your code.

## Interfaces, type aliases... Don't over-think, just be consistent

Sooner or later, when you start with React and TypeScript, or just TypeScript, you will hear about the discussion about interfaces and type aliases. There are some developers who prefer to use interfaces. Others like to use type aliases. Both these groups have their reasons for doing so.

I suggest that you ignore those things, at least in the beginning. There are more important things to learn, practice or debate than interfaces vs type aliases. This is like having a discussion about semicolons vs no semicolons. These discussions are not that important for learning how to use JavaScript, or TypeScript.

Yes, there are some [differences] between interfaces and type aliases. Both have their pros and cons. However, both will help you get the job done. So, don't overthink it. Read about interfaces, type aliases and their differences, try both, and see which one you like more. Then, stick to that choice.

For example, I like to use interfaces. I am comfortable working with them and they make the code more readable, for me. You may not like this. You may like type aliases. Then, be my guest. Another approach is using both. Some people prefer using interfaces for defining APIs for libraries and 3rd party type definitions.

Then, they use type aliases for React components and props. Others use interfaces for React components and props and type aliases only for variables and functions. Try all approaches, learn about the pros and cons and make your decision. In the end, this is what matters. Sticking to one thing and not constantly switching.

If you decide to use solely interfaces, do that and use only them. If type aliases, the same thing. If you decide to use both, each in special scenarios go ahead. Interfaces or type aliases... Remember, it is your code. Write it the way you like, assuming you follow good practices and the result will not be a pile of mess.

## Don't annotate everything, embrace automatic type inference

Developers starting with TypeScript sometimes think it is necessary to annotate all their code. I thought the same thing. This is not true. When you start using TypeScript it doesn't mean you have to annotate every single line of your code. It doesn't mean you have to infer the type of every single variable, function, etc.

This is a nice thing on TypeScript. It will do a lot of work for you. Part of this work is automatically inferring types, in specific situations. This is something we discussed this in the [second part]. Quick recap. TypeScript will infer (and expect) the type for you if you declare and also initialize a variable.

When you do this, TypeScript will automatically use the type of the value you assigned to that variable to infer its value. For example, if you initialize some variable with number, you assign a number to it, TypeScript will automatically infer (and expect) type of number. The same with string, boolean or any [other type].

Another situation when TypeScript will automatically infer type for you is if you set default value(s) for function parameter(s). In that case, TypeScript will use the default value to infer the type. So, if some parameter has default value a `string`, TypeScript will infer (and expect) type of `string`.

The third situation is when function returns some value. In that case, you don't have to infer the return type yourself. Well, if it doesn't return anything, TypeScript will infer type of `void`. So, it works as well. If you remember these three situations it is unlikely you will waste your time annotating code that doesn't need to be annotated.

```ts
///
// No.1: Declaring and initializing variables
// Note: let and const doesn't make a difference
const name = 'Jackie'
// TypeScript will automatically infer type of 'string'

let year = 2020
// TypeScript will automatically infer type of 'number'

const isReady = true
// TypeScript will automatically infer type of 'boolean'

let subjects = ['Math', 'History', 'English']
// TypeScript will automatically infer type of 'string[]'


///
// No.2: Function with parameter(s) with default value(s)
function defaultParam(age = 18) {
  // ...
}
// TypeScript will automatically infer function defaultParam(age?: number): void
// Function not returning anything with a parameter type of number

const defaultParam = (name = 'anonymous') => {
  // ...
}
// TypeScript will automatically infer const defaultParam: (name?: string) => void
// Function not returning anything with a parameter type of string


///
// No.3: Function returning something
function returnAString() {
  return 'This is gonna be heavy!'
}
// TypeScript will automatically infer function returnAString(): string
// Function with a return type of string

const returnANumber = () => {
  return 2**15
}
// TypeScript will automatically infer const returnANumber: () => number
// Function with a return type of number
```

## Remember, it is still JavaScript

Yes, we have been talking about React and TypeScript for some time. However, remember that you are still working with JavaScript. Remember that neither React nor TypeScript are new languages. The first is just a framework and the second is a superset. Under the hood, it is still good old JavaScript.

It is still the same language and, in case of TypeScript, almost the same syntax. TypeScript only adds the type system and some features. If you know JavaScript, which you should assuming you are working with React, adopting TypeScript should not be too difficult. So, don't worry. If you know JavaScript you can handle React and TypeScript.

## If in doubt, work on your JavaScript skills

What if you don't know JavaScript that well. If you have some things to learn in JavaScript, adopting TypeScript will be harder. The same also applies to React. Trying to learn React and TypeScript without learning JavaScript is not a good idea. I recommend learning JavaScript first, before you try to add anything.

When you learn JavaScript, it will be much easier for you to adopt TypeScript. It will be also easier to write better and cleaner code in React. So, if you are in doubt about anything, work on your JavaScript skills. Make sure you have solid understanding of how JavaScript and how to use it. This will later help you with both, React and TypeScript.

## Conclusion: Getting Started With React and TypeScript

This is the end of this mini series. I hope this series made it at least a bit easier for you to get started with React and TypeScript. There is still a lot of things to learn before you become really proficient in TypeScript. So, don't stop now. Revisit and practice what you've learned so far so you remember it and get better at it.

I also recommend diving deeper into TypeScript. For this, there are three good places to look at. The first one is the [official documentation] for TypeScript. This is a very good documentation. It will help you learn all you need to know about TypeScript, or all you can learn about it.

The second place is [TypeScript Deep Dive]. This is a free ebook on TypeScript available as EPUB, MOBI and PDF on Gitbook and also on [GitHub]. It is regularly updated and well written. The last one is [React+TypeScript Cheatsheets]. This GitHub repository is one of my go-to sources for all things React and TypeScript.

It contains code examples demonstrating how to use TypeScript with React. This makes it a good place to go when you need to look up something. It is also a good place for learning about React and TypeScript because it uses the best practices. Beginner or advanced developer, I highly recommend checking it out. Now, back to practice.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Part 1]: https://blog.alexdevero.com/react-and-typescript-pt1/
[Part 2]: https://blog.alexdevero.com/react-and-typescript-pt2/
[Part 3]: https://blog.alexdevero.com/react-and-typescript-pt3/
[strict]: https://www.typescriptlang.org/docs/handbook/compiler-options.html
[VS Code]: https://code.visualstudio.com/
[typescript-eslint]: https://github.com/typescript-eslint/typescript-eslint
[any]: https://blog.alexdevero.com/react-and-typescript-pt2/#any
[interfaces]: https://blog.alexdevero.com/react-and-typescript-pt3/#interfaces
[type aliases]: https://www.typescriptlang.org/docs/handbook/advanced-types.html#type-aliases
[differences]: https://medium.com/@martin_hotell/interface-vs-type-alias-in-typescript-2-7-2a8f1777af4c
[second part]: https://blog.alexdevero.com/react-and-typescript-pt2/#type-inference
[other type]: https://blog.alexdevero.com/react-and-typescript-pt2/#types
[official documentation]: https://www.typescriptlang.org/docs/home.html
[TypeScript Deep Dive]: https://basarat.gitbooks.io/typescript/content/
[GitHub]: https://github.com/basarat/typescript-book
[React+TypeScript Cheatsheets]: https://github.com/typescript-cheatsheets/react-typescript-cheatsheet

<!--
### Meta:
-
-->

<!--
#### Resources:
-
-->
