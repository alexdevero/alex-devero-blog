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
