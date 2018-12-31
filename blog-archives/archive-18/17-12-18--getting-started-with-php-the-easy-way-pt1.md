# Getting started with PHP - The Easy Way Pt1

PHP is one of the most popular programming languages in the world. It is a programming language with a long history and it is also very powerful programming language. PHP can help you get done a lot things. Use this short mini series to learn all you need to know about PHP to get started. As you will see, learning PHP is easier than you may think.

<!--
Table of Contents:
## Why PHP
## The basics
## Variables
### Variable scope
### Variable variables
### Predefined variables
### Constants
## Data types part 1
### Integers, floats and booleans
### Arrays
## Epilogue: Getting started with PHP - The Easy Way Pt1
-->

## Why PHP

One question you might be asking is why one should learn PHP. There are some people saying that PHP is on the decline. Some people directly say that PHP is dying. None of these claims is true. PHP is not on the decline or even dying. The opposite is true. According to [Tiobe index], PHP is currently (Dec 2018) the 8th most popular programming language in the world.

Sure, this index only says how popular a programming language is among programmers. This may not be the best evidence of how bright the future of the programming language is. Tiobe index includes many languages a lot of programmers and developers never heard about. ABAP, SAS, Apex, Logo, Awk? let's take a look at maybe more useful statistic.

According to some [sources], PHP is currently powering the server-side of 78% of websites. So, no. PHP is not on the decline. And, it is certainly not dying. What's more, PHP is getting [faster] with time. The difference in performance between version 5 and 7 is significant. Aside to these stats, PHP is very easy to learn. So, will you give it a chance?

## The basics

The best place to start are the basics. When you want to write some PHP code, you have to use correct opening and closing tags. These are `<?php` and `?>`. You will see these tags in all code examples in this tutorial. When you want to output or render some text you can do it by using a built-in language construct `echo`.

When you write PHP code, there is one thing you have to remember. Every statement has to end with semicolon (;). If you forget to add a semicolon at the end of a statement, the result will be an error. So, when you run into some error, chances are that the root cause of the problem might actually be just one missing semicolon.

One last thing about `echo`. You can also use it to output or render HTML code. All you have to do is to put the HTML tags inside the string that follows the `echo`. Then, PHP will output these tags not as a text, but as normal HTML markup. Finally, when you want to add a comment, or comment out some code, you can use `//` for single-line comment and `/* */` multi-line comment.

```
<?php // Opening tag
  // This is a single-line comment

  /*
   This is
   a multi-line
   comment.
  */

  // Using "echo" construct to output text
  echo "This will be rendered"; // Statement has to end with semicolon

  // Using "echo" construct to output HTML code
  echo "<p>This will be rendered in the form of <strong>HTML</strong> markup.</p>";

// Closing tag
?>
```

If you saw some examples of PHP code you may have noticed something. Many programmers are using double quotes. Sure, you could argue that this might be just a personal preference. However, there is more to it. Single and double quoted strings are not equal in PHP. If you are familiar with JavaScript, you can think about double quotes as an equivalent of backticks.

Just like backticks in JavaScript, double quotes allow to use code snippets inside strings. This also means that the example with outputting HTML code would not work with single quotes. Probably the best way to avoid potential problems and headaches is to stick to double quotes. Then, you will not need to think about this anymore.

## Variables

One of the basic building blocks of almost every programming language are variables. You use variables to store information for later use. In PHP, variables has to start with dollar sign (`$`) symbol. Then follows the name of the variable. There are few rules you have to remember when it comes to creating variables.

First, a variable name must start with a letter or an underscore. Second, it can't start with a number. Third, it can contain only alpha-numeric characters and underscores (A-z, 0-9, and _ ). Fourth, variable names are case-sensitive. Meaning, `$knock` and `$KNOCK` are two different variables. So, make sure to use correct case when you refer to existing variable.

```
<?php
  $var_one = "Say it again."; // Variable with a string

  $var_two = 25; // Variable with integer.
?>
```

### Variable scope

When it comes to PHP and variables, variables can be declared anywhere in your script. And, you can define them in two variable scopes are local, global. When you define variable outside a function, it has a global scope. On the other hand, a variable you declare inside a function has a local scope. This variable can then be accessed only within that function.

This is important to remember. It can help you avoid many potential headaches. However, you can change this defining the variable and then using `global` keyword to access this variable. This will, for example, allow you to access the global variable from within a function. To do this, use the `global` keyword within the function, before you refer to the variable.

```
<?php
  $name = "Tony";

  function getName() {
    echo $name;
  }

  getName();// Error: Undefined variable: name

  // Example with "global" keyword
  $name = "Tony";

  function getName() {
    // Using "global" keyword
    global $name;

    echo $name;
  }

  getName(); // Outputs "Tony"


?>
```

### Variable variables

PHP has one, or at least one, interesting quirk. You can use one variable to specify another variable's name. Then, this "variable variable" treats the value of the second variable as its name. This may sound weird. The example below will hopefully make it easier for you to wrap your head around it. You may not find this feature useful in your work, but it still at least good to know that there is such a thing.

Take a look at the example. The `$$example` is a variable that is using the value of another variable, `$example`, as its name. The value of `$example` is equal to "hello". The result is a variable `$hello` which now stores the value `"Hi!"`.

```
<?php
  $example = "hello";

  $hello = "Hi!";

  echo $$example;

  // Outputs "Hi!"
?>
```

### Predefined variables

Aside to "regular" variables, PHP also offers a large number of predefined variables, also called "superglobal" variables. These are `$_SERVER`, `$GLOBALS`, `$_REQUEST`, `$_POST`, `$_GET`, `$_FILES`, `$_ENV`, `$_COOKIE`, `$_SESSION` and more. What makes these "superglobal" variables is that each of them is always accessible. Scope doesn't matter in this case.

This means that you can access any of these "superglobal" variables any time you want or need, in any function, class or file. You will probably find some of these "superglobal" variables more useful while some less. For example, the `$_POST` and `$_GET` will be very handy if your current project requires working with forms, sending or receiving some data.

Talking about all these "superglobal" variables would make for an entire article. So, we will not discuss what each of these "superglobal" variables contains and how and when it can be useful. If you want to learn more about these variables, you can find the whole list, as well as what each of these variables contains, [here], in the official manual for PHP.

### Constants

There is one more thing related to variables. You can also create constants. Constants are similar to variables except one ting. You can't change them or make them undefined after you define them. In other words, they are immutable. How can you create or define new constant? You have to use PHP built-in function `define()`. This function accepts three parameters.

These parameters are `name`, `value` and whether is the constant `case-insensitive`. In other words, `define(name, value, case-insensitive)`. `name` specifies the name of the constant. `value` specifies the value of the constant. `case-insensitive` specifies whether the constant name should be case-insensitive. Here, the default value is `false`.

```
<?php
// Example of case-sensitive constant
  define("MESSAGE", "Hello world!");

  echo MESSAGE; // "Hello world!"
?>

// Example of case-insensitive constant
<?php
  define("MESSAGE", "Hello world!", true);

  echo message; // "Hello world!"
?>
```

## Data types part 1

When it comes to PHP, there are currently seven data types. These are strings, integers, floats (also called doubles), booleans, arrays, objects and NULLs. You've already seen example of string in the example above, the `$var_one`. Put simply, string is any sequence of characters surrounded by either single or double quotes. That's all.

One thing you should remember is what you learned about strings in the section about basics. As we discussed, single and double quotes are not equal in PHP. The difference is that double quotes allow you to include snippets of code inside the string. In other words, that doubles works in a similar way to backticks in JavaScript.

```
<?php
  // String example
  $string_example_s = 'A very simple string using single quotes.';

  $string_example_d = "A very simple string using double quotes.";
?>
```

### Integers, floats and booleans

An integer is a whole number. And, it has to fit some criteria. First, it has to be without decimals. So no decimal point. Second, it can't contain commas or blanks. Third, it can be either positive or negative. Fourth, it must have at least one digit, at least 0. Finally, valid integer can be specified in three formats: decimal, hexadecimal or octal.

The `$var_two` was an example of integer. Float is any number with decimal point, or in exponential form. Booleans can come in one of two possible states. A boolean is either `true` or `false`. There is no other option. Booleans are favorite data type programmers like to use for testing, using conditional statements.

```
<?php
  // Example of string
  $example_string = "This is a string.";

  // Example of integer in decimal format
  $example_integer_dec = 26;

  // Example of integer in hexadecimal format (26 as hexadecimal)
  $example_integer_hex = 1A;

  // Example of integer in octal format (266565 as octal)
  $example_integer_oc = 1010505;

  // Example of float
  $example_float = 3.14159;

  // Examples of booleans
  $example_boolean_true = true;

  $example_boolean_false = false;
?>
```

### Arrays

Next data type in PHP are arrays. Arrays allow you to store multiple values in one variable and you can create and use them in three forms-numeric (or indexed), associative and multi-dimensional. Numeric or indexed arrays associate their values with specific numeric `index`. This `index` is assigned automatically and you don't have to worry about this.

Index in array always starts at 0. When you want to access some value, you just have to use correct `index`. The difference between numeric and associative arrays is that associative use named keys that you assign to them. There are two ways to create any array. You can either use the `index`, or `named keys`, or built-in `array()` function. When you want to access the value, use the named keys.

Finally, the multi-dimensional array. The dimension of an array indicates the number of indices you would need to select an element. Meaning, you can create two-, three-, x-dimensional arrays. In case of a two-dimensional array, you need two indices to select an element. In case of a three-dimensional array, you need three indices to select an element.

For example, a two-dimensional array contains 3 arrays and has two indices: row and column. Row represents specific nested array. Column represents the index inside this array. When you want to access the elements of this array, you have to use these two indices.

```
<?php
  // Numeric array
  $example_names = array("Tony", "Joe", "Emil");

  // or using index
  $example_names[0] = "Tony";
  $example_names[1] = "Joe";
  $example_names[2] = "Emil";

  echo $example_names_two[1]; // "Joe"

  // Associative array
  $example_names_two = array("Tony" => "31", "Joe" => "18", "Emil" => "25");

  // or
  $example_names_two['Tony'] = "31";
  $example_names_two['Joe'] = "18";
  $example_names_two['Emil'] = "25";

  echo $example_names_two['Joe']; // "18"

  // Two-dimensional array with 3 arrays
  $example_team = array(
    'admins'=>array("John", "Rob", "Jack"),
    'testers'=>array("Jeremy", "Silvio"),
    'users'=>array("David", "Amy")
  );

  echo $example_team['admins'][0]; // "John" - row="admins", column="0"
  echo $example_team['testers'][0]; // "Jeremy" - row="testers", column="0"
  echo $example_team['users'][1]; // "Amy" - row="users", column="1"
?>
```

## Epilogue: Getting started with PHP - The Easy Way Pt1

This is where we will end this first part. You've done a good job and learned a lot. In a recap, we started with a brief review of the current state of PHP and potential reasons why to learn it. Then, you've learned learned about the absolute basics of PHP, the syntax, comments, `echo` and the difference between single and double quotes.

Then, you moved deeper into the world of PHP. You explored topics such as variables, scope, the variable variable quirk, predefined variables, constants, data types, integers, floats, and booleans. The last thing you've learned about was arrays. What's next? In the second part, you will learn about the rest of data types.

After that, you will also learn about if statements, switches, loops, include and require, functions, OOP and classes and how to handle files. This will provide you with solid foundation that will allow you to start using PHP in your projects. Now, practice what you've learned today. With that, thank you for your time.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Tiobe index]: https://www.tiobe.com/tiobe-index/
[sources]: https://w3techs.com/technologies/details/pl-php/all/all
[faster]: https://kinsta.com/blog/php-benchmarks/
[here]: https://secure.php.net/manual/en/reserved.variables.php
