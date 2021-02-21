# X JavaScript ES2020 Features You Should Know
<!--more-->
<!--
Table of Contents:
-->

## BigInt

This ES2020 feature, new data type called `BigInt`, can seem like like a minor. It might be for many JavaScript developers. However, it will be big for developers who have to deal with large numbers. In JavaScript, there is a [limit] for the size of a number you can work with. This limit is 2^53 – 1.

Before the `BigInt` type, you could not go above this limit because the `Number` data type just can't handle these big numbers. With `BigInt` you can create, store and work with these large numbers. This includes even numbers that exceed the safe integer limit. There are two ways to create a `BigInt`.

The first way is by using `BigInt()` constructor. This constructor takes a number you want to convert to `BigInt` as a parameter and returns the `BigInt`. The second way is by adding "n" at the end of an integer. In both cases, JavaScript will add the "n" to the number you want to convert to `BigInt`.

This "n" tells JavaScript that the number at hand is a `BigInt` and it should not be treated as a `Number`. This also means one thing. Remember that `BigInt` is not a `Number` data type. It is `BigInt` data type. Strict comparison with `Number` will always fail.

```JavaScript
// Create the largest integer
let myMaxSafeInt = Number.MAX_SAFE_INTEGER

// Log the value of "myMaxSafeInt":
console.log(myMaxSafeInt)
// Output:
// 9007199254740991

// Check the type of "myMaxSafeInt":
console.log(typeof myMaxSafeInt)
// Output:
// 'number'

// Create BigInt with BigInt() function
let myBigInt = BigInt(myMaxSafeInt)

// Log the value of "myBigInt":
console.log(myBigInt)
// Output:
// 9007199254740991n

// Check the type of "myBigInt":
console.log(typeof myBigInt)
// Output:
// 'bigint'


// Compare "myMaxSafeInt" and "myBigInt":
console.log(myMaxSafeInt === myBigInt)
// Output:
// false


// Try to increase the integer:
++myMaxSafeInt
// Output:
// 9007199254740992

++myMaxSafeInt
// Output:
// 9007199254740992

++myMaxSafeInt
// Output:
// 9007199254740992


// Try to increase the BIgInt:
++myBigInt
// Output:
// 9007199254741007n

++myBigInt
// Output:
// 9007199254741008n

++myBigInt
// Output:
// 9007199254741009n
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
