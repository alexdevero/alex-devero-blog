# Getting Started with PHP the Easy Way Pt2 - Control Flow

PHP is one of the programming languages that are very easy to learn. You can learn the basic in just a few days. This mini series will show you how. In this part, you will learn all you need about conditional statements, loops and `break`, `continue`, `include` and `require` statements. Make another step towards reaching PHP mastery!

<!--
Table of Contents:
## PHP and control structures
### Conditional statements
### Switch
### The while loop
### The do-while loop
### The for loop
### The foreach loop
### The continue statement
### Include & require statements
## Epilogue: Getting Started with PHP the Easy Way Pt2
-->

Getting Started with PHP the Easy Way [Part 1] (Variables & Data types).

Getting Started with PHP the Easy Way [Part 3] (OOP Pt1).

Getting Started with PHP the Easy Way [Part 4] (OOP Pt2 and Beyond).

## PHP and control structures

Let's start with set of PHP goodies called control structures. These goodies allows you to write code that will react differently depending on current situation. This can be anything. For example, it can be a change that occurred somewhere in the code or that was caused by user input. The primary types of control structures are conditional statements and loops. Let's take a look at them.

### Conditional statements

Imagine that you want to execute two different actions. What action should be executed depends on some condition. This is where you can use something called conditional statement, also called `if else` statement. In order to use this, you need two things. First, you need to specify the condition. Second, you need to specify the first action to be executed, if the condition is `true`.

When you are done with that, you can also specify the second action to be executed, if the condition is `false`. However, this is not necessary. In other words, you can emit the `else` part.

```
// Default if statement (with else part)
<?php
  if (condition) {
    // Code to be executed;
  }
?>

// Default if else statement
<?php
  if (condition) {
    // Code to be executed;
  } else {
    // Code to be executed;
  }
?>

// Simple example of if else statement
<?php
  $x = 3;
  $y = 21;

  if ($x <= $y) {
    echo "Variable 'x' is smaller or equal than variable 'y'";
  } else {
    echo "Variable 'x' is bigger than variable 'y'";
  }

  // Outputs "Variable 'x' is smaller or equal than variable 'y'"
?>
```

Okay, but what if you want something more complex? For example, what if you want to specify another condition if the first one is `false`? In that case, you can do two things. First, you use another `if else` statement, nested inside the `else`. Second, you can use `elseif` statement. This statement allows you to use more than one condition without the nesting one statement inside another.

```
// Example with nested statement
<?php
  $x = 34;
  $y = 21;
  $z = 51;

  if ($x <= $y) {
    echo "Variable 'x' is smaller or equal than variable 'y'";
  } else {
    if ($x <= $z) {
      echo "Variable 'x' is bigger than variable 'y' and smaller or equal than variable 'z'";
    } else {
      echo "Variable 'x' is bigger than variable 'y' and 'z'";
    }

    echo "Variable 'x' is bigger than variable 'y'";
  }

  // Outputs "Variable 'x' is bigger than variable 'y' and smaller or equal than variable 'z'"
?>

// Example with elseif statement
<?php
  $x = 34;
  $y = 21;
  $z = 51;

  if ($x <= $y) {
    echo "Variable 'x' is smaller or equal than variable 'y'";
  } elseif ($x <= $z) {
      echo "Variable 'x' is bigger than variable 'y' and smaller or equal than variable 'z'";
  } else {
    echo "Variable 'x' is bigger than variable 'y' and 'z'";
  }

  // Outputs "Variable 'x' is bigger than variable 'y' and smaller or equal than variable 'z'"
?>
```

One benefit of using the `elseif` statement is that it is cleaner than the one with nested `if else` statement. This may not be as obvious one the example above. However, imagine that you have three, four or even more conditions. Then, your code could quickly become barely readable.

```
// Example with nested statement
<?php
  if (condition) {
    ... some action ...
  } else {
    if (condition) {
      ... some action ...
    } else {
      if (condition) {
        ... some action ...
      } else {
        if (condition) {
          ... some action ...
        } else {
          ... some action ...
        }
      }
    }

    ... some action ...
  }
?>

// Example with elseif statement
<?php
  if (condition) {
    ... some action ...
  } elseif (condition) {
      ... some action ...
  } elseif (condition) {
    ... some action ...
  } elseif (condition) {
    ... some action ...
  } else {
    ... some action ...
  }
?>
```

### Switch

Conditional statements, or the `if else` and `elseif`, are quite useful and powerful. However, there will be situations when you will need something better. Imagine you want to test for a specific case to execute specific code. The problem is that this case has many variants. For example, imagine a calendar app where the case you want to test for is the day of the week.

Sure. You can still use `elseif`. However, it is not the most elegant solution. A better option, offered by PHP, is to use `switch` statement. `switch` allows to test for a specific expression, usually some variable. Next, it compares the value of the expression with the value of each case defined inside it. If it finds a match, the block of code inside that case is executed.

What if none of the case fits the expression? Then, there are two options. First, `switch` will go test all cases, finds no match, and nothing happens. Or, you can add additional case called `default`. Then, if `switch` doesn't find any match, it will execute the code inside this `default` case. One last thing. Every case should be ended with `break` keyword.

You can think about this as a brake. It will prevent `switch` from automatically running into the next case. If you forget the `break`, PHP will automatically continue through the next case, even when the case doesn't match. If you don't have any `break` inside your `switch`, PHP will run through all cases and execute code in all of them.

Let's use the example of calendar app again. In this example, the expression, or the variable, `switch` will test will be the day of the week. Next, there will be case for each day, with additional `default` case if the day doesn't exist. So, eight cases in total. Remember to include the `break` statement at the end of every case.

```
// Default switch statement
<?php
  switch (expression) {
  case value1:
    //code to be executed if expression = value1

    break;
  case value2:
     //code to be executed if expression = value2

     break;
  ...
  default:
    // code to be executed if 'expression' doesn't fit any case
}
?>

// Simple example of calendar app with switch statement
<?php
  $day = "fri";

  switch ($day) {
    case "mon":
      echo "Today is Monday.";

      break;
    case "tue":
      echo "Today is Tuesday.";

      break;
    case "wed":
      echo "Today is Wednesday.";

      break;
    case "thu":
      echo "Today is Thursday.";

      break;
    case "fri":
      echo "Today is Friday.";

      break;
    case "sat":
      echo "Today is Saturday.";

      break;
    case "sun":
      echo "Today is Sunday.";

      break;
    default:
      echo "This day doesn't seem to exist.";
  }

  // Outputs "Today is Friday."
?>
```

One last thing. Let's take a look at what would happen if you forgot to add the `break` statement in each case. As you will see, `switch` will cycle through every case, and check if the expression fits the variable, the day. If not, it will skip the case as. So for good. What happens next? The `switch` will not be terminated when it finds a match.

Instead, it will go to the next case, after the match, and execute the code inside this case. And, the same will happen with every case that follows the match. `switch` will execute code inside all these cases. In the case of the calendar app, it will print message for every day starting with the day that matches the day specified in `$day` variable.

```
// Example of switch statement without break statement
<?php
  $day = "fri";

  switch ($day) {
    case "mon":
      echo "Today is Monday.";

    case "tue":
      echo "Today is Tuesday.";

    case "wed":
      echo "Today is Wednesday.";

    case "thu":
      echo "Today is Thursday.";

    case "fri":
      echo "Today is Friday.";

    case "sat":
      echo "Today is Saturday.";

    case "sun":
      echo "Today is Sunday.";

    default:
      echo "This day doesn't seem to exist.";
  }

  // Outputs "Today is Friday.Today is Saturday.Today is Sunday.This day doesn't seem to exist."
?>
```

### The while loop

Aside to conditional statements, you can also use loops. These loops can be quite useful when you want the same block of code to run over and over again. You don't have to copy the same code over and over again. Instead, you can use loops to do the work for you. You will probably agree that this will result in much cleaner and more elegant code.

The first loop PHP offers is `while` loop. The way `while` works is very simple. It executes a block of code as long as the condition you specified is `true`. When the condition evaluates to `false`, the `while` loop is terminated. This also makes `while` loop potentially dangerous. Imagine you forget to add code that will change the condition at some point. What will happen?

The `while` loop will never stop. It will continue executing the code over and over again. In other words, you will create something called infinite loop. In the example below, you will create `$num` variable and set its value to "1". Then, you will use `while` loop to output the value of this variable, and increase its value, as long as the value is smaller than 7.

Increasing the value of `$num` variable will ensure that the condition used for `while` will evaluate to `false` at some point. Without this, you would create the infinite loop you read about above. How? If you don't increase the value `$num` variable, it will be always smaller than 7 and the condition for `while` loop will always evaluate to `true`.

```
// Default while loop
<?php
  while (condition) {
    // your code to be executed;
  }
?>

// A simple example of while loop
<?php
  $num = 1;

  while ($num < 7) {
    echo "The number is $num <br />"; // Output current value of $num variable

    $num++; // Increase the value of $num variable
  }
?>
```

### The do-while loop

PHP offers a more advanced version of `while` loop. This one is called `do-while` loop. What is the difference between the `while` and `do-while` loop? The `do-while` loop will always execute the block of code at least once. It doesn't matter if the condition you specified is `true` or `false`. The `do-while` loop executes the code before it checks the condition.

If the condition is evaluates to `false`, it will not run again. Otherwise, it will repeat the loop as long as the condition evaluates to `true`. Just like a regular `while` loop.

```
// Default do-while loop
<?php
  do {
    // Code here will be executed at least once;
  } while (condition);
?>

// A simple example of do-while loop
<?php
  $num = 3;

  do {
    echo "The number is " . $num . "<br/>";

    $num++;
  } while($num <= 5);

  //Output
  // The number is 3
  // The number is 4
  // The number is 5
?>
```

### The for loop

Next loop you can use in PHP is `for` loop. This loop is a good choice when you know how many times the code inside the loop should be executed. The `for` loop requires three parameters. These parameters are `init` (starting loop counter value), `test` (test evaluated each time the loop is iterated, continuing if `true` and ending if `false`) and `increment` (increases the loop counter value).

When you use a `for` loop, there are few things to remember. First, each of the parameters can be empty. Second, each of the parameters can also contain multiple expressions. These expressions must be separated with commas. Third,
all parameters of the `for` loop must be separated with semicolons. Let's take a look at a simple example of `for` loop.

The loop in the example below first creates new variable `$i` and sets its value to 0. Then, it checks for the condition, in this case if `$i < 6`. If the condition is `true`, loop runs the code. After that, the loop automatically increments the `$i` variable (`$i++`) and next iteration follows.

```
// Default for loop
<?php
  for (init; test; increment) {
    // Code to be executed;
  };
?>

// Simple example of for loop
<?php
  for ($i = 0; $i < 6; $i++) {
    echo "Value of i: ". $i . "<br />";
  }

  // Outputs "Value of i: 0."
  // Outputs "Value of i: 1."
  // Outputs "Value of i: 2."
  // Outputs "Value of i: 3."
  // Outputs "Value of i: 4."
  // Outputs "Value of i: 5."
?>
```

### The foreach loop

The `foreach` is the last loop you can use in PHP. Three thing you must know about this loop. First, this loop works only on arrays. Second, you can use it only to loop through `key/value` pair inside the array. Third, you can write `foreach` loop using two different forms of syntax. As you will see, the difference between those two forms is very small, but the result can be significant.

The first "form" of a syntax loops over the array. On each iteration, the value of the current element is assigned to `$value`. Then, the array pointer is moved by one. This repeats until the loop reaches the last array element. The second "form" will do the same as first, but it will also assign the current element's key to the `$key` variable, on each iteration.

```
// Default foreach loop
<?php
  foreach (array as $value) {
    // code to be executed;
  }

  // or
  foreach (array as $key => $value) {
    // code to be executed;
  }
?>

// Simple example of foreach loop (the first form)
<?php
  $names = array("Adam", "Cindy", "Eric", "Geraldo", "Massimo");

  foreach ($names as $name) {
    echo $name.'<br />';
  }

  // Outputs:
  // Adam
  // Cindy
  // Eric
  // Geraldo
  // Massimo
?>

// Simple example of foreach loop (the second form)
<?php
  $names = array("Adam", "Cindy", "Eric", "Geraldo", "Massimo");

  foreach ($names as $name => $value) {
    echo "Value of \$name is:" . $name . " and value of \$value is:" . $value . ".<br />";
  }

  // Outputs:
  // Value of $name is:0 and value of $value is:Adam.
  // Value of $name is:1 and value of $value is:Cindy.
  // Value of $name is:2 and value of $value is:Eric.
  // Value of $name is:3 and value of $value is:Geraldo.
  // Value of $name is:4 and value of $value is:Massimo.
?>
```

### The continue statement

One last thing related to control structures. There might be a situation when you will want to use a loop, but you will also want to skip some code execution in some cases. This is exactly when `continue` statement will be useful. Put simply, when you use `continue` statement inside a loop structure, you can skip code execution in current loop iteration.

So far, it looks like what `break` statement does. However, `continue` will not stop or terminate the loop. The loop will continue with the next iteration. Well, if there is one. Let's take a look at a simple example. The `for` loop below will iterate through numbers in range from 0 to 9. Next, there is an `if` statement that will check if the number in current iteration is even or odd.

When the number is even, the condition in `if` statement is `true`, `continue` statement will be executed. This will cause the `for` loop to skip the code that follows the `if` statement. In other words, the `for` loop will not output the number if the number is even. Instead, it will continue with next iteration.

```
// Example of continue statement
<?php
  for ($num = 0; $num < 10; $num++) {
    if ($num % 2 == 0) {
      continue;
    }

    echo $num . ', ';
  }

  // Output: 1, 3, 5, 7, 9,
?>
```

## Include & require statements

When you work on a big project, the codebase can quickly become quite large. This will make the code harder to work with, organize and maintain. Fortunately, PHP can help you here. What you can do is to use `include` and `require` statements. These statements allow you to insert content inside one PHP file into another, before the server executes the code.

This is a common practice in WordPress development. Developers create small PHP components for headers, footers, sidebars and other parts of the website. Then, they `include` or `require` the component when they need it. This makes their work quite easy and fast. When the developer needs to change some PHP component, he has to update only the file with that component file. The change will propagate everywhere.

What is the difference between `include` and `require`? They are almost identical. The difference is that when you use `require` to include some file, the script will produce an error when the file is not found. On the other hand, if you use `include`, it will skip the file and code will continue to execute. So, if some file is necessary, use `require`. Otherwise, use `include`.

```
// File "header.php"
<?php
  echo '<h1>Welcome</h1>';
?>

// File index.html
<html>
  <head></head>

  <body>
    <!-- Include the content of "header.php" -->
    <?php include "header.php"; ?>

    <!-- Or, require it -->
    <?php require "header.php"; ?>
  </body>
</html>
```

## Epilogue: Getting Started with PHP the Easy Way Pt2

Congratulations! You've just finished the second part of this mini series about PHP. Today, you've learned about conditional statements, or the `if else`, `elseif` and `switch`. Then, you've learned about `while`, `do-while`, `for` and `foreach` loops. At the end, you've also learned about `break`, `continue`, `include` and `require` statements. What's next?

In the third and final part, you will learn about PHP functions, OOP and classes and how to work with files. This will provide you with a solid foundation to start using PHP in your projects. It will also make it easier for you to complete your PHP learning path and reach PHP mastery. Now, practice what you've learn today as well as in [the first part]. Thank you for your time.

[xyz-ihs snippet="thank-you-message"]

<!-- Links -->
[the first part]: https://blog.alexdevero.com/getting-started-php-pt1/
[Part 1]: https://blog.alexdevero.com/getting-started-php-pt1/
[Part 3]: https://blog.alexdevero.com/getting-started-php-pt3/
[Part 4]: https://blog.alexdevero.com/getting-started-php-pt4/
