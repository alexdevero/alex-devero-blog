# Nullish Coalescing Operator Explained

Nullish coalescing operator

<!--more-->
<!--
Table of Contents:
-->

## The problem with logical operators

For a long time JavaScript supported only three logical operators. These operators are the [OR] (`||`), [AND] (`&&`) and [NOT] (`!`). These operators are very useful as they allow you to dynamically execute different tasks, based on current conditions. The problem is that these operators have their gotchas.

### Logical operators and truthy and falsy values

These logical operators work well with [boolean] values, in conditional statements for example. When you use these operators with different data types, JavaScript will sometimes convert those data types to booleans. This is possible because every data type in JavaScript is also either [truthy] or [falsy].

This is usually not a problem if you work with truthy values or `null` and `undefined`. The OR operator, and also AND, work very well with both, `null` and `undefined`. Problems may arise if you work with falsy values such as `0` or `""` (empty string). In that case, JavaScript will convert those values to `false`.

When these values are converted to `false` logical operators has no other option than to return the default values. This is something you may neither expect nor desire. Let's illustrate this on one simple example. Let's say you want to access some object property only if it has some value. If it doesn't have any value you want to use some default. You can do this with the logical OR operator.

What happens if that property has value, but that value is falsy? Just to remind you, falsy values in JavaScript are `false`, `0`, `-0`, `0n`, `""` (empty string), `null`, `undefined` and `NaN`. Any other value than these is truthy. When you use OR operator to check if the value exists, it will convert that value to boolean. If the value is falsy the result will be `false`.

What if the value exists, but it 0 or ""? In that case, JavaScript convert that value to `false` and OR operator will return your default value. It doesn't matter there is value actually some value. The only thing that matters for OR operator is that the value is falsy.

```JavaScript
const userProfile = {
  name: 'Justin Lambert',
  age: 0, // 0 is a falsy value
  jobTitle: '', // Empty string is a falsy value
  hobbies: null // Null is also a falsy value
}

// Log the value of name property
// this will work as you expect
console.log(userProfile.name || 'Anonymous')
// 'Justin Lambert'

// Log the value of age property
// this not will work as you expect
console.log(userProfile.age || 29)
// 29

// Log the value of jobTitle property
// this not will work as you expect
console.log(userProfile.jobTitle || 'Unemployed')
// 'Unemployed'

// Log the value of property hobbies
// this will work as you expect
console.log(userProfile.hobbies || 'No hobbies.')
// 'No hobbies.'

// Log the value of non-existing property height
// this will work as you expect
console.log(userProfile.height || 'Height is unknown.')
// 'No hobbies.'
```

## Nullish coalescing operator to the rescue


## Conclusion: [...] ...

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[OR]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_OR
[AND]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_AND
[NOT]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_NOT
[boolean]: https://blog.alexdevero.com/javascript-basics-data-types-pt2/#boolean-logical-type
[truthy]: https://developer.mozilla.org/en-US/docs/Glossary/truthy
[falsy]: https://developer.mozilla.org/en-US/docs/Glossary/falsy

<!--
### Meta:
-
-->

<!--
### Keywords:
- nullish coalescing operator
- nullish coalescing
-->

<!--
### Resources:
-
-->
