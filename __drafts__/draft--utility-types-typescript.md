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


### h3

### h3

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
