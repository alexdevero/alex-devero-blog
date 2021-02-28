# 7 Useful JavaScript ES2020 Features to Learn About
<!--more-->
<!--
Table of Contents:
-->

## String.prototype.trimStart() and String.prototype.trimEnd()

If you've ever worked with strings there is chance you had to deal with unwanted white space. From now on, there will be two ES2020 features that will help you with this issue. These features are .`trimStart()` and `trimEnd()` string methods. These methods do what their names imply.

They both help you trim, or remove, white space from given string. The first one, the `trimStart()` will remove all white space from the start of the string. The second, the `trimEnd()` will remove all white space from the end of the string. If you need to remove white spaces on both sides?

This gives you two options. The first option is using both these ES2019 features together. The second option is to use another string method [trim()]. Both will give you the result you want.

```JavaScript
// String.prototype.trimStart() examples:
// Try string without white space:
'JavaScript'.trimStart()
// Output:
//'JavaScript'

// Try string with white space at the beginning:
' JavaScript'.trimStart()
// Output:
//'JavaScript'

// Try string with white space on both sides
' JavaScript '.trimStart()
// Output:
//'JavaScript '

// Try string with white space at the emd
'JavaScript '.trimStart()
// Output:
//'JavaScript '


// String.prototype.trimEnd() examples:
// Try string without white space:
'JavaScript'.trimEnd()
// Output:
//'JavaScript'

// Try string with white space at the beginning:
' JavaScript'.trimEnd()
// Output:
//' JavaScript'

// Try string with white space on both sides
' JavaScript '.trimEnd()
// Output:
//' JavaScript'

// Try string with white space at the emd
'JavaScript '.trimEnd()
// Output:
//'JavaScript'
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
