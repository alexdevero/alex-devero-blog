# 7 JavaScript ES2017 Features to Learn


<!--more-->
<!--
Table of Contents:
-->

## String padding with padStart() and padEnd()

Two smaller ES2017 features added to strings are `padStart()` and `padEnd()`. These two methods allow you to easily add characters to a string so it reaches a specific length. The `padStart()` adds characters at the beginning of the string. The `padEnd()` adds characters at the end.

Both methods accept two parameters. The first parameter is the length of the string you want to reach. The second parameter is the character you want to add. This character will be added repeatedly as long as is needed to reach the target length. If the string is already at the target length, or beyond it, nothing will happen.

This second parameter, the character to add, is optional. If you specify it, both methods will add it if necessary. If you omit it, both methods will add default character

```JavaScript
// padStart() example:
// Add '-' character at the beginning
// until the string reaches length of 9 characters.
'Hello'.padStart(9, '-')
// Output:
// '----Hello'

// Add 'A' character at the beginning
// until the string reaches length of 3 characters.
// Note: the string is already beyond this length
// so nothing will happen.
'Hello'.padStart(3, 'A')
// Output:
// 'Hello'

// Increase the length of a string to 11,
// but don't specify the character to add.
'Hello'.padStart(15)
// Output:
// '          Hello'


// padEnd() example:
// Add '-' character at the beginning
// until the string reaches length of 9 characters.
'Bye'.padEnd(9, '.')
// Output:
// 'Bye......'

// Add 'A' character at the beginning
// until the string reaches length of 3 characters.
// Note: the string is already beyond this length
// so nothing will happen.
'Bye'.padEnd(1, '?')
// Output:
// 'Bye'


// Increase the length of a string to 11,
// but don't specify the character to add.
'Bye'.padEnd(11)
// Output:
// 'Bye        '
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
