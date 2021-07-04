# Getting Started With Built-in Utility Types in TypeScript Part 2

TypeScript comes with a number of built-in utility types. These types can be very useful. They can help you create new, and also very advanced, types from existing with only a bit of code. In this article, you will learn about some of these utility types, how they work and also how to use them.<!--more-->

<!--
Table of Contents:
## A quick introduction
## Note on availability
## Note on syntax
## NonNullable<Type>
## Parameters<Type>
## ConstructorParameters<Type>
## ReturnType<Type>
## InstanceType<Type>
## ThisParameterType<Type>
## OmitThisParameter<Type>
## ThisType<Type>
## Conclusion: Getting started with built-in utility types in TypeScript part 2
-->

## A quick introduction

The goal of this two-part article is to help you understand TypeScript built-in utility types. In this second part, you will learn about the last eight of these types. These are `NonNullable`, `Parameters`, `ConstructorParameters`, `ReturnType`, `InstanceType`, `ThisParameterType`, `OmitThisParameter` and `ThisType`.

If you want to learn about the previous eight, take a look at the [part 1]. Part 1 will help you understand and work with `Partial`, `Required`, `Readonly`, `Record`, `Pick`, `Omit`, `Exclude` and `Extract`. Otherwise, keep reading.

## Note on availability

The types we will talk about in this part are available in TypeScript version 4.0 and newer. Make sure you use this version to avoid potential issues due to compatibility.

## Note on syntax

The utility types in TypeScript we will talk about today all use very similar syntax. It is almost identical. The only difference being the name of each utility type. As we discussed in [previous part], utility types can be confusing at first. What can help you understand them is trying to see these types as [functions].

This is what these types basically are. They are functions that take some input and return some output. In this case, input and output are types. The rest is just a plain function. The types you will learn about in this part all require a single parameter, some type. You pass this parameter between angle brackets.

These angle brackets, the left- and right-pointing (`<>`), follow right after the name of the utility type. The name of the type always starts with capital letter. This is very similar to calling a normal JavaScript function. You only swapped the parentheses for brackets and started the function name with a capital letter.

Sometimes, TypeScript utility types require more than one parameter. In that case, you pass these parameters between the angle brackets a usually and separate them with a colon (`,`). That's about the syntax. Now, let's talk about the actual types.

## NonNullable<Type>

The `NonNullable` utility type works similarly to the [exclude]. It takes some type you specified and returns that type excluding all `null` and `undefined` types.

```TypeScript
// Create a type:
type prop = string | number | string[] | number[] | null | undefined

// Create new type based on previous type
// excluding null and undefined:
type validProp = NonNullable<prop>
// Translates to:
// type validProp = string | number | string[] | number[]

// This is valid:
let use1: validProp = 'Jack'

let use2: validProp = null
// TS error: Type 'null' is not assignable to type 'validProp'.
```

## Parameters<Type>

The `Parameters` type returns a [tuple] type that contains the types of the parameters function you passed as `Type`. These parameters are returned in the same order in which they appear in the function. Note that the `Type` argument, in case of this and following types, is a function (`(...args) => type`), not a type such as `string`.

```TypeScript
// Declare a function type:
declare function myFunc(num1: number, num2: number): number

// Use Parameter type to create new tuple type
// from parameters of myFunc function:
type myFuncParams = Parameters<typeof myFunc>
// Translates to:
// type myFuncParams = [num1: number, num2: number]

//  This is valid.
let someNumbers: myFuncParams = [13, 15]

let someMix: myFuncParams = [9, 'Hello']
// TS error: Type 'string' is not assignable to type 'number'.


// Use Parameter type to create new tuple type
// from function type:
type StringOnlyParams = Parameters<(foo: string, fizz: string) => void>
// Translates to:
// type StringOnlyParams = [foo: string, fizz: string]

//  This is valid.
let validNamesParams: StringOnlyParams = ['Jill', 'Sandy']

let invalidNamesParams: StringOnlyParams = [false, true]
// TS error: Type 'boolean' is not assignable to type 'string'.
```

## ConstructorParameters<Type>

The `ConstructorParameters` type is very similar to the `Parameters` type. The difference between these two is that while `Parameters` gets types from function arguments, the `ConstructorParameters` gets types from the constructor you pass as the `Type` argument.

```TypeScript
// Create a class:
class Human {
  public name
  public age
  public gender

  constructor(name: string, age: number, gender: string) {
    this.name = name;
    this.age = age;
    this.gender = gender;
  }
}

// Create type based on Human constructor:
type HumanTypes = ConstructorParameters<typeof Human>
// Translates to:
// type HumanTypes = [name: string, age: number, gender: string]

const joe: HumanType = ['Joe', 33, 'male']
const sandra: HumanType = ['Sandra', 41, 'female']
const thomas: HumanType = ['Thomas', 51]
// TS error: Type '[string, number]' is not assignable to type '[name: string, age: number, gender: string]'.
// Source has 2 element(s) but target requires 3.


// Create type based on Human constructor:
type StringType = ConstructorParameters<StringConstructor>
// Translates to:
// type StringType = [value?: any]
```

## ReturnType<Type>

The `ReturnType` is also similar to the `Parameters` type. Difference here is that the `ReturnType` extracts the return type of a function you pass as the `Type` argument.

```TypeScript
// Declare type for function:
declare function myFunc(name: string): string

// Use ReturnType to extract return type
// from myFunc type.
type MyFuncReturnType = ReturnType<typeof myFunc>
// Translates to:
// type MyFuncReturnType = string

// This is valid:
let name1: MyFuncReturnType = 'Victoria'

// This is valid:
let name2: MyFuncReturnType = 42
// TS error: Type 'number' is not assignable to type 'string'.

type MyReturnTypeBoolean = ReturnType<() => boolean>
// Translates to:
// type MyReturnTypeBoolean = boolean

type MyReturnTypeStringArr = ReturnType<(num: number) => string[]>
// Translates to:
// type MyReturnTypeStringArr = string[]

type MyReturnTypeVoid = ReturnType<(num: number, word: string) => void>
// Translates to:
// type MyReturnTypeVoid = void
```

## InstanceType<Type>

The `InstanceType` is a bit complicated. What it does is it creates a new type from the instance type of a constructor function you passed as argument for `Type`. You will probably don't need this utility type if you work class with a regular class. You can just use the class name to get the instance type you want.

```TypeScript
class Dog {
  name = 'Sam'
  age = 1
}

type DogInstanceType = InstanceType<typeof Dog>
// Translates to:
// type DogInstanceType = Dog

// Similar to using the class declaration:
type DogType = Dog
// Translates to:
// type DogType = Dog
```

## ThisParameterType<Type>

The `ThisParameterType` extracts the type of use for the `this` parameter for the function you passed as the `Type` argument. If the function doesn't have `this` parameter, the utility type will return `unknown`.

```TypeScript
// Create a function with this parameter:
function capitalizeString(this: String) {
  return this[0].toUpperCase + this.substring(1).toLowerCase()
}

// Create type based on capitalizeString function this parameter:
type CapitalizeStringType = ThisParameterType<typeof capitalizeString>
// Translates to:
// type CapitalizeStringType = String
```

## OmitThisParameter<Type>

The `OmitThisParameter` utility type does the opposite of the previous type. It takes a function type as an argument, via the `Type`, and returns the function type without `this` parameter.

```TypeScript
// Create a function with this parameter:
function capitalize(this: String) {
  return this[0].toUpperCase + this.substring(1).toLowerCase()
}

// Create type based on capitalizeString function:
type CapitalizeType = OmitThisParameter<typeof capitalize>
// Translates to:
// type CapitalizeType = () => string


// Create a function without this parameter:
function sayHi(name: string) {
  return `Hello, ${name}.`
}

// Create type based on sayHi function:
type SayHiType = OmitThisParameter<typeof sayHi>
// Translates to:
// type SayHiType = (name: String) => string
```

## ThisType<Type>

The `ThisType` utility type allows you to explicitly set the `this` context. You can use it to set `this` for whole object literals or just a single function. Before you try this, make sure you have the compiler flag `—-noImplicitThis` enabled.

```TypeScript
// Create interface for this in user object:
interface User {
    username: string;
    email: string;
    isActivated: boolean;
    printUserName(): string;
    printEmail(): string;
    printStatus(): boolean;
}

// Create user object and set this type to User interface:
const userObj: ThisType<User> = {
  username: 'Andreas',
  email: 'andreas@foo.com',
  isActivated: false,
  printUserName() {
    return this.username
  },
  printEmail() {
    return this.email
  },
  printStatus() {
    return this.isActivated
  }
}
```

## Combining utility types

One nice thing on TypeScript built-in utility types is that you can also combine them. You can combine one utility type with another utility type. You can also combine one utility type with other types. For example, you can combine types with [union] or intersection types. This allows you to create even more advanced types.

```TypeScript
// Create User interface:
interface User {
  username: string;
  password: string;
}

// Create SuperUser interface:
interface SuperUser {
  clearanceLevel: string;
  accesses: string[];
}

// Create type RegularUser by combining User and SuperUser.
// Make properties in User required
// and properties in SuperUser optional:
type RegularUser = Required<User> & Partial<SuperUser>

// This is valid:
const joeJoe: RegularUser = {
  username: 'joejoe',
  password: 'some_secret_password_unlike_123456',
}

// Also valid:
const jane: RegularUser = {
  username: 'jane',
  password: 'foo_bar_usually-doesnt_work-that_well',
  clearanceLevel: 'A'
}

// This will not work:
const pietro: RegularUser = {
  username: 'pietro'
}
// TS error: Type '{ username: string; }' is not assignable to type 'RegularUser'.
// Property 'password' is missing in type '{ username: string; }' but required in type 'Required<User>'.(
```

## Conclusion: Getting started with built-in utility types in TypeScript part 2

These were the last eight built-in utility types in TypeScript. As you can see, these utility types can help you get a lot of work with types done. This, while making it easier for you and doing all the heavy lifting. I hope that this article helped you understand how these built-in utility types work and how to use them.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->

[part 1]: https://blog.alexdevero.com/typescript-utility-types-part-1/
[previous part]: https://blog.alexdevero.com/typescript-utility-types-part-1/#about-the-syntax
[functions]: https://blog.alexdevero.com/javascript-functions-pt1/
[exclude]: https://blog.alexdevero.com/typescript-utility-types-part-1/#excludelttype-excludeduniongt
[tuple]: https://www.typescriptlang.org/play#example/tuples
[union]: https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#union-types

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
