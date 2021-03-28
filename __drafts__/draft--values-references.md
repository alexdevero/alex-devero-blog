# Blog post title [...]
<!--more-->
<!--
Table of Contents:
-->

## A short introduction

In JavaScript, there are the two categories of data types you can work with. First category are primitive data types. At this moment, there exist [seven primitive types]. These primitive data types are number, string, boolean, `null`, `undefined`, BigInt and Symbol. The BigInt and Symbol are newer data types.

Symbol was introduced in [ES6] specification. The BigInt was introduced later, in [ES2020] specification. When something is not one of these primitive data types it is technically an object. This applies to actual objects as well as arrays and even functions. From the view of JavaScript, these are all objects.

This distinction between primitive data types and objects is important because JavaScript handles each differently.

```JavaScript
// Primitive data types:
const numberVal = 5
const strVal = 'Hello!'
const boolVal = true
const nullVal = null
const undefinedVal = undefined
const bigIntVal = 9007123254550972n
const symbolVal = Symbol('label')

// Objects:
const myObjLiteral = {
  name: 'Toby'
}

const myArray = [9, 'book', true, null]

function myFunction(num1, num2) {
  return num1 / num2
}
```

## Primitive data types

Let's start with the first category, primitive data types. Values that contain these primitive data types are called static data. As static data, JavaScript stores them on the [stack]. One important thing about these primitive values is that their size is fixed. JavaScript knows how much memory these data types need.

Let's say you assign some variable a primitive data type as a value. From now on, this variable will contain that value. If you manipulate with that variable, you manipulate directly with the value you assigned to it. A simple way to test this, and the consequences, is assigning the variable to another variable.

When you assign one variable to another, and the value of first is primitive data type, JavaScript will copy that value. When you do this you are copying the values "by value". So, now, if you change the value of the first variable, the second will remain the same. This is because even though you created one variable from another they both have their own, separate, values.

So, if you change the value of one variable it will not change the second. The second variable is a separate entity. Let's go back to the stack. When you assign the first variable, JavaScript will store its value on the stack. When you assign the variable to another variable its value will be also added on the stack.

At this moment, the stack will now contain two values, one for each variable. It doesn't matter that both values are the same. Nor does it matter that you created the second variable from the first. For JavaScript, these are two separate entities. These two variables have no relationship with each other.

This is also why you can safely work with each of these variables as you want. Why you can change one variable without changing the other.

```JavaScript
// Create a variable and assign it
// a primitive value:
let x = 'Hello'

// Assign "x" to another variable:
let y = x

// Change the value of "x":
// NOTE: this will not change "y".
x = 'Bye'

// Log the value of "x":
console.log(x)
// Output:
// 'Bye'

// Log the value of "x":
console.log(y)
// Output:
// 'Hello'

// Assign "y" to another variable:
let z = y

// Assign "z" to another variable:
let w = z

// Change the value of "y":
// NOTE: this will not change "z" and "w".
y = 'Eloquent'

// Log the value of "x":
console.log(z)
// Output:
// 'Hello'

// Log the value of "x":
console.log(w)
// Output:
// 'Hello'
```

## Objects and references

Objects are a different story. When you assign variable an object JavaScript will handle it differently. The value, the object, will not be added to the stack. Instead, it will be added to [memory heap]. There is another very important difference. That variable will not contain the value, the object, but a reference to that object.

Think about this reference as a link, or chain. It is a link that connects specific variable with specific object. This has one major consequence. If you manipulate with that variable, you work with the reference and, through this reference, with the object itself. What if you copy that object by assigning that variable to another variable?

You may think that this will create another object, copy of the first, just like in case of primitive value. This is not what will happen. What will actually happen is that JavaScript will create new reference. JavaScript will only create new reference, or link, to the original object.

There will be still only one object in the memory heap, the original. This is called copying "by reference" and it happens every time you copy an object. Copying this way, by reference, results in creating [shallow copies] of objects. This type of copying also has one serious consequence.

If you manipulate with any of these variables you also manipulate with the same object. So, if you change the object by changing one variable you change the other variable as well. They are both different variables, but they both reference, or link to, the same object.

```JavaScript
// Create a variable and assign it
// a simple object:
let a = { name: 'Stan' }

// Assign "a" to another variable:
let b = a

// Change the value of "a"
// by adding new property "age" to the object:
a.age = 44

// Log the value of "a":
// console.log(a)
// Output:
// { name: 'Stan', age: 44 }

// Log the value of "b":
// console.log(b)
// Output:
// { name: 'Stan', age: 44 }

// Assign "b" to another variable:
let c = b

// Assign "c" to another variable:
let d = c

// Change the value of "d"
// by adding another property
// "favoriteAnimal" to the object:
d.favoriteAnimal = 'elephant'

// Log the value of "a":
console.log(a)
// Output:
// {
//   name: 'Stan',
//   age: 44,
//   favoriteAnimal: 'elephant'
// }

// Log the value of "b":
console.log(b)
// Output:
// {
//   name: 'Stan',
//   age: 44,
//   favoriteAnimal: 'elephant'
// }

// Log the value of "c":
console.log(c)
// Output:
// {
//   name: 'Stan',
//   age: 44,
//   favoriteAnimal: 'elephant'
// }

// Log the value of "d":
console.log(c)
// Output:
// {
//   name: 'Stan',
//   age: 44,
//   favoriteAnimal: 'elephant'
// }
```

*Note: One way to understand how copying by reference works is by thinking about keys and houses. When you copy you key, you are not also creating a new house. There is still only one house, but there are now two keys that can unlock that house. Variables are those keys, object is that house.*

## Quick summary of primitive data types, objects, values and references

Now you know what is the difference between primitive values and references. When you assign primitive data types and then copy them you are copying by values. Each of these copies (variables) is a separate entity that has no relationship to another. You can change one without changing any other.

When you assign and then copy an object, you are copying by reference. You are creating new references for each copy. As a result, there are multiple references (variables). However, there is still only one object. If you change one of these variables, you change the original object. This will affect all references (variables).

## Primitive values, references and comparison

Knowing the difference between value and reference is important when you want to do comparison.

### Comparing primitive values

Comparing two primitive values is usually simple. The only catch is knowing the difference between [equal] and [strict equal] and which one to use (it will usually be strict equal). Comparing primitive values with strict equal will check for value and type. If both are the same, you will get `true`. If not, you will get `false`.

```JavaScript
// One primitive value:
// Create one variable and assign it primitive value:
const str1 = 'JavaScript'

// Create another variable and assign it "str1":
const str2 = str1

// Compare "str1" and "str2":
console.log(str1 === str2)
// Output:
// true


// Two identical primitive values:
// Create two variables and assign them
// the same primitive values:
const num1 = 15
const num2 = 15

// Compare "num1" and "num2":
console.log(num1 === num2)
// Output:
// true
```

### Comparing objects and references

References work differently. If you compare two different objects, and the content is the same, the comparison will still result in `false`. Comparison will result in `true` only if you compare references to the same object.

```JavaScript
// One object:
// Create a variable and assign it an object:
const a = { name: 'Jack' }

// Assign "a" to another variable:
const b = a

// Compare "a" and "b":
console.log(a === b)
// Output:
// true

// Two identical objects:
// Create a variable and assign it an object:
const a = { name: 'George' }

// Create another variable and assign it the same object:
const b = { name: 'George' }

// Compare "a" and "b":
console.log(a === b)
// Output:
// false
```

Remember that arrays, and functions as well, are technically objects. This means that if you compare variables with identical arrays the result will be always `false`. Those variables will be the same only if they both reference the same array.

```JavaScript
// One array:
// Create a variable and assign it an array:
const x = [1, 2, 3, 4]

// Create another variable and assign it "x":
const y = x

// Compare "x" and "y":
console.log(x === y)
// Output:
// true


// Two identical arrays:
// Create a variable and assign it an array:
const x = [1, 2, 3, 4]

// Create another variable and assign it the same array:
const y = [1, 2, 3, 4]

// Compare "x" and "y":
console.log(x === y)
// Output:
// false
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
