# Blog post title [...]

<!--more-->
<!--
Table of Contents:
-->

## Booleans, true, false and beyond

As you probably already know boolean, `true` and `false`, is one of the primitive data types that exist in JavaScript. Then, there are other primitive values such as strings, numbers, BigInt, null, undefined and symbols. Aside to these, there are objects. Objects also include arrays. However, there is more than that.

All these primitive data types also have boolean representation. What this means is that JavaScript can take each of these data types, their values, and evaluate them as boolean. JavaScript can "convert" their vales to boolean, either `true` or `false`. Which boolean will it be depends on the data type you are working with.

Boolean has only two possible values, `true` and `false`. This also creates a limit for how JavaScript can "convert" values. When JavaScript "converts" values to be either or false it uses specific set of rules. These rules are implemented at the core of the language and are very unlikely to change. Let's take a look at them.

## Truthy and falsy values

There are currently seven primitive data types in JavaScript. These are numbers, strings, boolean, BigInt, null, undefined and symbols. Values of some data types are always truthy and of others always falsy, regardless of the actual value. This is not necessarily true for other values.

There are also data types whose values can be truthy in one scenario and falsy in another. What makes the difference, and determines the truthy / falsy status, is the actual value.

### Falsy values

Falsy values are values that evaluate to `false` when JavaScript "converts" them to their boolean alternatives. First, let's take a look at values that are falsy in all situations. In other words, it doesn't matter what their actual value is. These values are `null`, `undefined` and `NaN`. These three will be always falsy.

Aside to these two, other falsy values are boolean `false`, number `0`, BigInt `0n`, empty single-quote string (`''`), empty string with backticks (` `` `) and empty double-quote string (`""`). These values will be falsy as long as they don't change.

```JavaScript
// Falsy values
false
null
undefined
NaN
0
0n // BigInt 0
"" // empty single-quote string
'' // empty string with backticks
`` // empty double-quote string
```

### Truthy values

On the other side are truthy values. These values will be evaluated as `true` when JavaScript "converts" them to boolean. First, there are five values that will be always truthy, no matter the situation. These are arrays (empty, non-empty), objects (empty, non-empty), `new Date()` and `Infinity`, both positive and negative.

Values that will be truthy are also boolean `true`, positive and negative numbers (integers and floats) and non-zero BigInt. Truthy will also be non-empty strings created with single quotes, double quotes and backticks. Truthy value will also be `0` as a string (`"0"`). This is because it is no longer 0 but non-empty string.

```JavaScript
// Truthy values
true
[] // Array, empty and non-empty
{} // Object, empty and non-empty
new Date()
42
-42
3.14
-3.14
12n // Non-zero BigInt
Infinity // Number infinity positive
-Infinity // Number infinity negative
"0" // 0 as a string
'non-empty single-quote string'
`non-empty string with backticks`
"non-empty double-quote string"
```

## A note on Boolean context

As you now know, JavaScript can convert values to Boolean. This happens automatically, but only in a specific situation. This situation is called a Boolean context. Boolean context basically means that JavaScript needs to know the "Boolean" value of a value in order to get the work done.

A simple example of this situation is when you use [if...else] statement. When you use some value in `if...else` statement, and only that value, JavaScript has to convert that value to boolean. It has no other option because the condition of `if...else` has to be a boolean. Well, unless that value is already a boolean.

```JavaScript
// If...else statement
if (/* Boolean context */) { /* Some code to execute */ }

if (0) {
  console.log('truthy')
} else {
  console.log('falsy')
}
// Output:
// 'falsy'

if (0n) {
  console.log('truthy')
} else {
  console.log('falsy')
}
// Output:
// 'falsy'

if (null) {
  console.log('truthy')
} else {
  console.log('falsy')
}
// Output:
// 'falsy'

if (undefined) {
  console.log('truthy')
} else {
  console.log('falsy')
}
// Output:
// 'falsy'

if (-59) {
  console.log('truthy')
} else {
  console.log('falsy')
}
// Output:
// 'truthy'

if ('hello') {
  console.log('truthy')
} else {
  console.log('falsy')
}
// Output:
// 'truthy'

if ({}) {
  console.log('truthy')
} else {
  console.log('falsy')
}
// Output:
// 'truthy'

if ([]) {
  console.log('truthy')
} else {
  console.log('falsy')
}
// Output:
// 'truthy'
```

## Converting values to Boolean

JavaScript converts values to Boolean automatically in a Boolean context. That said, you can also convert values to Boolean by yourself, when you want. There are at least two ways to do this.

### The Boolean constructor

The first way to do this is by using the [Boolean()] constructor. This is an object constructor that creates new Boolean object. This object is a wrapper for a Boolean value. This is not important. What is important is that the `Boolean()` constructor accepts a value as a parameter. It takes that value and returns it as a Boolean.

```JavaScript
Boolean(55)
// Output:
// true

Boolean(8n)
// Output:
// true

Boolean(-Infinity)
// Output:
// true

Boolean('')
// Output:
// false

Boolean('Hello!')
// Output:
// true

Boolean(['James', 'Joyce'])
// Output:
// true

Boolean({ name: 'James' })
// Output:
// true

Boolean(undefined)
// Output:
// false

Boolean(null)
// Output:
// false
```

### The NOT NOT, or double bang, operator

Your second option to convert values to Boolean is by using the "NOT NOT" operator. This operator is also called a "double bang" operator. You may already know the logical NOT operator (`!`), also called "bang". This operator, if you place it in front of a Boolean value, will reverse it to the opposite.

For example, `!true` will give you `false` and `!false` will give you `true`. Nice and simple. When you use this operator twice, it will not reverse the value. What it will do is it will convert that value to Boolean. If you use it with Boolean, it will do nothing. A very simple and fast way to convert any value to Boolean.

```JavaScript
console.log(!!true)
// Output:
// true

console.log(!!0)
// Output:
// false

console.log(!!15)
// Output:
// true

console.log(!!'')
// Output:
// false

console.log(!!'Code')
// Output:
// true

console.log(!!3.14)
// Output:
// true

console.log(!!undefined)
// Output:
// false

console.log(!!null)
// Output:
// false

console.log(!!{})
// Output:
// true

console.log(!![])
// Output:
// true
```

### Which one to use

Both NOT NOT and `Boolean()` constructor will get the job done and give you the same result. Any performance differences will be probably negligible. So, this basically means that there is no right or wrong choice. You should use what you prefer and what is more readable for you. If you like `Boolean()` use it. If `!!` use that.

### Avoid new Boolean

One last thing you should now. There is the `Boolean` constructor and there is also the `new Boolean` object. The `new Boolean` is an object type for the Boolean. It is an instance of Boolean object. You should avoid use it, as well as other object types such as `new Number`, `new String` and so on.

The reason is that while primitives (primitive data types) are cheap objects are expensive. Primitives are immutable and can share references. They also don't have to hold any state for each instance. This is not true for objects. Objects have their own unique memory address and can hold their own unique internal state.

All this means that JavaScript needs more resources to create and work with objects than with primitives. When you use object type, such as `new Boolean` you not creating a simple primitive, `true` or `false`. You are creating whole new `Boolean()` object. Save some memory and use the `Boolean` constructor, or NOT NOT (`!!`).

## Filtering arrays of strings with Boolean

The `Boolean` constructor can also help you remove empty strings from an array. Let's say you have an array with strings and you want to remove all empty strings. One thing you can do is to use the [filter()] method and check for length of each string. If the length is 0 you can discard that string.

Another thing you can do is use the `Boolean` constructor. You can use the `filter()` method and pass in the Boolean constructor as the callback function. The result will be an array with only non-empty strings. The reason this works is simple. The callback function for `filter()` method always returns Boolean.

When you pass in the `Boolean()` constructor the filter method will take each item in the array and convert it into Boolean. As you now know, non-empty strings are truthy. So, every with non-0 length string will return `true`. Empty strings are falsy. So, every empty string will return `false`.

The `filter()` method discards all items for which the callback function returned `false`. This means that it will discard all empty strings because they are falsy.

```JavaScript
// Create an array with empty and non-empty strings:
const arr = [ 'Java', 'coffee', '', 'team', '', '', 'tea' ]

// Use Boolean constructor to create clean copy:
let arrClean = arr.filter(Boolean)

// Log the clean array:
console.log(arrClean)
// Output:
// [ 'Java', 'coffee', 'team', 'tea' ]
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
