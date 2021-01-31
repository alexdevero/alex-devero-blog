# undefined and null in JavaScript Explained
<!--more-->
<!--
Table of Contents:
-->

## The basics

Both, `undefined` and `null`, are primitive [data types] that exist in JavaScript. These data types are Boolean, Number, String, Symbol, Null and Undefined. The rest of values in JavaScript are objects. Another thing `undefined` and `null` have in common is that they are both [falsy] values.

This means that when you use `undefined` in a boolean context it will be considered `false`. Boolean context is a context which evaluates to boolean value, either `true` or `false`. One example of boolean context is condition in [if...else] statement. This is also why you should avoid testing for loose equality.

When you test for loose equality there is [type coercion] happening on the background. Both, `undefined` and `null`, are falsy and this is what they will be considered as. The result of test for [loose equality] will result in match. The result of this test will be `true`. However, this is not really correct.

These two data types are not the same. If you want to avoid many problems, avoid testing for loose equality. Instead of loose equality, test for strict equality. When you test for [strict equality] JavaScript doesn't perform type coercion. Strict check will compare not only the value but also the data type.

`undefined` and `null` in JavaScript are different data types. This means that strict equality test will tell you, correctly, that these two are not the same. Let's take a look at each data type separately.

```JavaScript
// Testing for loose equality:
console.log(null == undefined)
// Output:
// true


// Testing for strict equality:
console.log(null === undefined)
// Output:
// false
```

## Conclusion: undefined and null in JavaScript Explained

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[data types]: https://blog.alexdevero.com/javascript-basics-data-types-pt1/
[falsy]: https://developer.mozilla.org/en-us/docs/Glossary/Falsy
[if...else]: https://blog.alexdevero.com/javascript-if-else-statement/

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
