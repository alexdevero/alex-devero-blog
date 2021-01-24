Objects are one area every JavaScript developer must know very well. Accessing object properties belongs to this area as well. In this tutorial, you will learn how to access object properties in three ways. You will learn how to use dot notation, bracket notation and destructuring.<!--more-->
<!--
Table of Contents:
-->

## Introduction to how to access object properties

Objects are one of the data types in JavaScript. They allow you to store data in key-value pairs. Those "keys" in those pairs are also called properties. If you are not familiar with [objects] yet, you can think about them as [variables]. These variables exist only on the object that contains them, not anywhere outside these objects.

In JavaScript there are multiple ways you can use to access one of those properties. These are dot notation, bracket notation and destructuring. Dot notation is sometimes also called dot property accessor. Another name for bracket notation is square brackets property access. There is one important thing to mention.

All these ways assume you know the name of the property you want to access. If you don't know it, nothing is lost. You can [loops] to iterate over object to get all properties, including the one you want. You will get to this as well. But first, let's take a look at those three ways you can use to access object properties.

## Dot notation

Dot notation, or dot property accessor, is probably the most popular way to access object properties in JavaScript. This method is very easy to learn and just as easy to use. The syntax is as follows. First, you specify some object. Second, you specify the name of the property. Between the object and property name goes a dot (`.`).

You can use the same process also to access deeper properties. In this case, you chain multiple properties together. You chain them in the way they are nested. So, the most shallow property will come as first, right after the object name. The deepest property will come as the last one: `obj.shallowProp.deeperProp.DeepestProp`.

Let's say you want to access property whose value is an array. You want to access specific item in that array. In this case, you can do what you would normally do if the array was a variable. You use the dot notation to access the property you want. After that, you use square brackets and index to get the item in the array you want.

```JavaScript
// Create an object using object literal:
const myObj = {
  name: 'Anthony Edward Stark',
  alias: 'Iron Man',
  gender: 'male',
  education: 'MIT',
  affiliation: {
    current: 'Avengers'
  },
  creators: ['Stan Lee', 'Larry Lieber', 'Don Heck', 'Jack Kirby']
}


// Accessing object properties with dot notation:
// First: name of the object.
// Second: name of the property to access.
// Third: dot character between the object and property.
console.log(myObj.name)
// Output:
// 'Anthony Edward Stark'

console.log(myObj.alias)
// Output:
// 'Iron Man'


// Accessing deeper object properties:
// Access the "current" property that exists
// in nested object assigned to "affiliation" property
console.log(myObj.affiliation.current)
// Output:
// 'Avengers'


// Accessing array items in objects:
// Access the first item inside the array
// assigned to "creators" property.
console.log(myObj.creators[0])
// Output:
// 'Stan Lee'
```

### Dot notation and valid property names

In JavaScript, there are rules saying what is and what is not a valid identifier. A valid identifier can contain Unicode letters, `$`, `_`, and digits 0-9. However, it can't start with a digit. Following these rules is necessary especially when you want to declare new variables.

These rules are also important for when you want to access object properties. This is especially true for dot notation. Dot notation works only with valid identifiers. It will not work if the property at hand violates these rules. For example, if it starts with number, or contains only number. Or, if it contains `-`.

If you want to access some property that violates these rules, don't use dot notation. Instead, use bracket notation. This way, you will still be able to work with that property as usually. You will learn about bracket notation in the next section.

```JavaScript
// Create an object:
myObj = {
  1: 'First property',
  'first-name': 'Bruce',
}

// Try to use dot notation
// to access properties on "myObj".
console.log(myObj.1)
// Output:
// SyntaxError: Unexpected token

console.log(myObj.first-name)
// Output:
// NaN


// Try to use bracket notation
// to access properties on "myObj".
console.log(myObj['1'])
// Output:
// 'First property'

console.log(myObj[1])
// Output:
// 'First property'

console.log(myObj['first-name'])
// Output:
// 'Bruce'
```

## Bracket notation

The second way you can use to access object properties is bracket notation. The main characteristic of method this method are square brackets. The syntax is similar to the dot notation. However, there are some important differences. You again start with the name of the object you are working with.

As second comes the name of the property. Here, you have to wrap the name of the property with quotes and square brackets. It doesn't matter if you use single or double quotes. What matters is that you use them to wrap the name of the property. Then, you wrap this with square brackets and put it after the object. And, no dot in-between.

Bracket notation also allows you to access deeper properties. This works similarly to dot notation. All properties are chained together, from the most shallow to the deepest. In case of brackets, there are no dots between properties. Furthermore, you must wrap all properties with quotes and square brackets.

Accessing items inside arrays assigned to properties works similarly. First, specify the property name and wrap it with quotes and square brackets. Then, add additional pair of square bracket with the index of the item you want to access.

```JavaScript
// Create object with object literal:
const myObj = {
  name: 'Bruce Thomas Wayne',
  alias: 'Batman',
  affiliation: ['Batman Family', 'Justice League', 'Outsiders', 'Guild of Detection'],
  status: {
    alignment: 'good',
    occupation: 'businessman'
  }
}


// Accessing object properties with bracket notation:
// First: name of the object.
// Second: name of the property to access.
// Note: property name must be wrapped with quotes
// and then with square brackets.
console.log(myObj['name'])
// Output:
// 'Bruce Thomas Wayne'


// Accessing deeper object properties:
// Access the "alignment" property that exists
// in nested object assigned to "status" property
console.log(myObj['status']['alignment'])
// Output:
// 'good'


// Accessing array items in objects:
// Access the second item inside the array
// assigned to "affiliation" property.
console.log(myObj['affiliation'][1])
// Output:
// 'Justice League'
```

## Object destructuring

Object destructuring is the last way to access object properties. It is also the newest. Dot and bracket notation have been around for a long time. Destructuring was added to JavaScript quite recently as part of the ES6 specification. Nonetheless, it quickly became very popular among JavaScript developers due to simplicity and usability.

You use it when you declare new variable. On the left side of the assignment, you specify the name of the property and wrap it with curly brackets. On the right side, you reference the object you want to work with. This will assign the variable with the value of the property you specified.

```JavaScript
// Create an object:
const myObj = {
  name: 'Unknown',
  alias: 'The Joker',
  affiliation: ['Black Glove', 'Injustice Gang', 'Injustice League', 'Joker League of Anarchy', 'Justice League of Arkham'],
  status: {
    alignment: 'bad',
    occupation: 'criminal'
  }
}


// Extract the value of "alias" property:
const { alias } = myObj

// Log the value of new "alias" variable:
console.log(alias)
// Output:
// 'The Joker'


// Extract the value of "affiliation" property:
const { affiliation } = myObj

// Log the value of new "affiliation" variable:
console.log(affiliation)
// Output:
// [
//   'Black Glove',
//   'Injustice Gang',
//   'Injustice League',
//   'Joker League of Anarchy',
//   'Justice League of Arkham'
// ]


// Extract the value of "status" property:
const { status } = myObj

// Log the value of new "status" variable:
console.log(status)
// Output:
// { alignment: 'bad', occupation: 'criminal' }
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
