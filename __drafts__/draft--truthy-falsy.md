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
