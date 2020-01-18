# Getting Started With Ruby the Easy Way Pt4 - Control Flow Pt2

Ruby is one of the programming languages you can use almost everywhere. It is also simple and very easy to learn. This makes it a very good choice if you want to learn new programming language, especially if it is your first programming language. Will you give Ruby a chance? If so, you are on the right place. This series will teach you all you need to learn this programming language.

<!--
Table of Contents:
## Control flow Pt2
### Ternary operators
### Logical operators
### Case statements
### While and until loops
### For loop
### Loop do
## Epilogue: Getting Started With Ruby the Easy Way Pt4
-->

Getting Started With Ruby the Easy Way [Part 1] (Comments, Variables, Strings).

Getting Started With Ruby the Easy Way [Part 2] (Data Types Pt1).

Getting Started With Ruby the Easy Way [Part 3] (Data Types Pt2, Control Flow Pt1).

Getting Started With Ruby the Easy Way [Part 5] (Control Flow Pt3).

Getting Started With Ruby the Easy Way [Part 6] (Methods).

Getting Started With Ruby the Easy Way [Part 7] (Recursion, Scope, OOP Pt1).

Getting Started With Ruby the Easy Way [Part 8] (OOP Pt2).

Getting Started With Ruby the Easy Way [Part 9] (OOP Pt3).

Getting Started With Ruby the Easy Way [Part 10] (OOP Pt4 and Beyond).

## Control flow Pt2

The `if` statement is not the only tool you can use to control how Ruby executes your code. The palette is much richer. Let's take a look what other control flow tools, or structures, you can use in Ruby.

### Ternary operators

In the [previous part], you've learned about `if` statements. The `if` statement can is very useful and powerful Although it is still very simple. However, you can take its simplicity to another level, and make your code shorter, if you want. How? You can achieve this by using something called ternary operator. Ternary operator does the same job as `if` statement.

It evaluates if some specific expression, or condition, is true of false. Then, it returns one value if the expression is true, and another value if the expression is false. You can think about it as a shorthand for `if` statement. Or, its compact version. The format of ternary operator is following one-liner: `conditional ? true : false`. This can be better illustrated on example.

Let's say that you want to ask the user for a number between zero and ten. Then, you want to print a short message based on this input. Below are two examples. One uses `if` statement. The second uses ternary operator. As you will see, on the example below, the ternary operator example is much shorter while the result is the same. When is it better to use ternary operator instead of `if` statement?

Ruby developers usually use ternary operator where conditionals unnecessarily long. The code below can be a good example. Another way to use it is for variable assignment, when you want to quickly select between two values. As a rule of thumb, use this operator to select between two values with a simple conditional. Otherwise, if you are working with something more complex, `if` statement will be a better choice.

```
###
# If statement example
###
puts "Please enter a number between 0 and 10: "

# Ask user for input and convert it to an integer
i = gets.to_i

# Print message
if i > 5
  puts "The number you chose is greater than 5."
else
  puts "The number you chose is less than or equal to 5."
end

###
# Ternary operator example
###
puts "Please enter a number between 0 and 10: "

# Ask user for input and convert it to an integer
i = gets.to_i

# Print message using ternary operator
puts "The number you chose " + (i > 5 ? "is greater than 5." : "is less than or equal to 5.")

###
# Ternary operator and variable assignment
###
b = 5

x = b > 10 ? "bigger" : "smaller"
# the "b > 10" is the expression, or condition
# "bigger" : "smaller" are values when expression is true and false
```

_Side note: In the example above, the one in which you ask for a number, the ternary operator is in parentheses. This is not necessary. Here, parentheses ensure that the ternary operator will not interfere with the string concatenation operators (`+`) surrounding it._

### Logical operators

There is one more thing, related to `if` statements and ternary operators, you should know. You can use something called logical operators. This is handy when you want to create more complex expressions that test more than one condition. Ruby has three logical operators. These operators are "and" (`&&`), "or" (`||`) and "not" (`!`). The "not" is sometimes also called negation.

In Ruby, you can also use words instead of the logical operator symbols-`and`, `or` and `not` if you want. However, there is one thing you need to remember. Logical operator in the form of words have lower precedence than symbols. They can also sometimes make code less readable. Ruby developers usually prefer to use symbols. Now, let's quickly take a look at each of these operators.

The `and` (`&&`) operator evaluates to `true` if and only if both operands, expressions on both sides of the operator, are true. Otherwise, the condition evaluates to `false`. The `or` (`||`) operator evaluates to `true` if one or both of its operands, expressions on both sides of the operator, are true. When both are false it evaluates to `false`.

The `not` (`!`) operator reverses, or negates, the state of a single operand. Hence the negation. The result of `not true` is `false` and `not false` is `true`. Remember that when you want to reverse, or negate, some expression you need to surround it with parentheses and put the `not` operator before them.

Finally, you can also use multiple conditions with logical operators, and chain them together, to check for multiple conditions. When you do this, you can use parentheses group individual conditions. This will help you keep your code readable. It will also give you more control over the order of operations.

```
###
# Example of and (&&) operator
###
x = 0
y = 10
z = 31

if y > x && x < z
  puts "It is true."
else
  puts "It is false."
end

# Outputs: It is true.
# y is bigger than x and x is smaller than z

###
# Example of or (||) operator
###
x = 111
y = 25

if x == 2 || y > 10
  puts "It is true."
else
  puts "It is false."
end

# Outputs: It is true.
# x is not equal to 2, but b is bigger than 10
# One of the operands is still true.
# Therefore, the condition evaluates to true.

###
# Example of not (!) operator
###
x = 5

puts !(x > 1)
# Outputs: false

###
# Example of chaining multiple conditions with logical operators
###
a = 111
b = 25
c = 5

puts (a == 2 || b > 10) || (c > 1)
# Outputs: true
```

### Case statements

As you know, you can test for multiple conditions using the `if` statement, along with `elsif` and `else`. This is good and you can do a lot with. However, there is a more simplified and flexible alternative. This is where Ruby can help you with something called `case` expression. The `case` expression lets you test a specific value and execute code for multiple scenarios, or cases.

Code for each case is defined inside `when` statements. You can have as many `when` statements as you need. If you want to test multiple values, with a single `when` statement, you need to separate the values with commas. You can also use ranges. You will learn about ranges and how to use them in the next, fifth, part.

Lastly, you can also use the `else` statement. Ruby will execute the code inside if none of the `when` statements matches the condition. One thing you need to remember. Every `case` expression must be closed with the `end` keyword. This is similar to `if` statement. The last question is, when is it better to use `if` and when `case` statement?

The best scenarios when you should use `if` statements are when you want to determine if a conditional is true. Basically binary operations (not literally) when you have two options, one for `true` and one for `false`. Otherwise, when you need to make different decisions based on a value, use case statements.

```
###
# Syntax of case statement
###
case value
when value
  # code to execute if "when" matches the value
end

###
# Example of case statement
###
day = "Wednesday"

case day
when "Monday"
  puts "Today is Monday."
when "Tuesday"
  puts "Today is Tuesday."
when "Wednesday"
  puts "Today is Wednesday."
when "Thursday"
  puts "Today is Thursday."
when "Friday"
  puts "Today is Friday."
when "Saturday"
  puts "Today is Saturday."
when "Sunday"
  puts "Today is Sunday."
end

# Outputs: Today is Wednesday.

###
# Syntax of case statement with else
###
case value
when value
  # code to execute if "when" matches the value
else
 # code to execute if "when" doesn't match the value
end

###
# Example of case statement with else,
# multiple values and also with ranges
###
age = 16

case age
when 1, 2
  puts "Baby."
when 3
  puts "Toddler."
when 4..6
  puts "Preschooler."
when 7..12
  puts "Preschooler."
when 13..17
  puts "Teenager."
else
  puts "Adult."
end

# Outputs: Teenager.
```

### While and until loops

After statements, another way to control flow in Ruby is with loops. Loops are used to execute the same block of code as many times as you want. In Ruby, there are couple of different loops you can use, four to be more specific. These loops are `while`, `until`, `for` and `loop do`. As you can guess by the names, the first two loops, the `while` and `until` are mutual opposites.

The `while` loop executes a block of code while its condition evaluates to `true`. When the condition changes and evaluate to `false`, the `while` loop will automatically stop. On the other hand, the `until` does the opposite of a `while` loop. This loop will run as long as its condition evaluates to `false` and stop when the condition changes and evaluate to `true`.

This is important to remember when you work with `while` and `until`. You have to always add code that will change the condition and stop the loop. If you forget to do this, and run the loop, it will run forever because the condition will remain true. This situation is called an infinite loop.

```
###
# Syntax of while loop
###
while condition
  # code to execute while the condition is true
end

###
# Example of a simple while loop
# This loop will run until x is smaller than 10.
# Loop will increase the value of x every time it runs.
###
x = 0

while x < 10
  puts x # print current value of x
  x += 1 # increase value of x to avoid infinite loop
end

# Outputs:
# 0
# 1
# 2
# 3
# 4
# 5
# 6
# 7
# 8
# 9

###
# Syntax of until loop
###
until condition
  # code to execute until the condition is false
end

x = 0

until x > 10
  puts "x = #{x}"
  x +=2
end

# Outputs:
# x = 0
# x = 2
# x = 4
# x = 6
# x = 8
# x = 10
```

### For loop

The third type of loop you can use in Ruby is `for` loop. This loop executes a block of code for every iteration in a specific range. The `for` loop is composed of an empty variable and a range. Every time the loop iterates it assigns the current value of the range to the empty variable. So, during the first iteration the variable will be assigned the first value of the range.

On the second loop, it will be assigned to the new value. This will repeat until the end of the range. When you want to stop the loop, you can use `break` statement. If you want to skip one iteration of the loop and continue with the next one, you can use the `next` statement. You can also repeat the current iteration using `redo` statement.

Finally, when you want to restart the whole loop, and force it to start again from the beginning, you can use `retry` statement. The `for` loop is very useful when you need to loop over a specific set of values.

```
###
# Syntax of for loop
###
for emptyVariable in (range)
  # code to execute during every iteration
end

###
# Example of for loop
# It will run seven times and print the value of i variable.
###
for i in (1..7)
  puts i
end

# Outputs:
# 1
# 2
# 3
# 4
# 5
# 6
# 7

###
# Example of for loop with break statement
# Loop will stop if the variable is bigger than 4.
###
for i in 1..10
  break if i > 4
  puts i
end

# Outputs:
# 1
# 2
# 3
# 4

###
# Example of for loop and next statement
# Loop will output odd numbers from 0 to 10
# and skip the iteration for even numbers.
###
for i in 0..10
  next if i %2 == 0 # skip even numbers
  puts i # print the value of "i" variable
end

# Outputs:
# 1
# 3
# 5
# 7
# 9
```

### Loop do

The last type of loop in Ruby is the `loop do`. This loop executes your code until it meets the break condition. This is important to remember. Every time you use this loop, make sure to specify condition that will stop it at some point. Otherwise, if you forget to include the break condition, the loop will run forever, just like the `while` and `until` loops.

```
###
# Syntax of loop do
###
loop do
  # code to execute
  break condition # condition that will stop the loop
end

###
# Example of loop do
###
x = 0

loop do
  puts x # print value of "i" variable
  x += 1 # increase the the value of "x" variable
  break if x > 7 # stop the loop when "#" is bigger than 7
end

# Outputs:
# 1
# 2
# 3
# 4
# 5
# 6
# 7
```

## Epilogue: Getting Started With Ruby the Easy Way Pt4

Congratulations! You've just finished another part of this series and made progress on your way to learn how to program in Ruby. Let's do a quick recap. First, you've learned about what are ternary and logical operators. Next, you've learned about `case` statements. After that, you've learned about loops. These were the `while`, `until`, `for` and `loop do`.

In the next, fifth, part you will learn about ranges, iterators, functions and much more. This will bring you one step closer to learning how to program in Ruby and becoming a Ruby developer. Until then, review what you've learned today and practice on the examples above. Remember that the best way to learn programming is by writing the code by yourself.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Part 1]: https://blog.alexdevero.com/getting-started-ruby-pt1
[Part 2]: https://blog.alexdevero.com/getting-started-ruby-pt2
[Part 3]: https://blog.alexdevero.com/getting-started-ruby-pt3
<!-- [Part 5]: https://blog.alexdevero.com/getting-started-ruby-pt5 -->
[previous part]: https://blog.alexdevero.com/getting-started-ruby-pt3

<!-- Resources: -->
<!--
- http://ruby-for-beginners.rubymonstas.org/built_in_classes.html
- https://www.eriktrautman.com/posts/ruby-explained-iteration
-->
