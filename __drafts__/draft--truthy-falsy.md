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
