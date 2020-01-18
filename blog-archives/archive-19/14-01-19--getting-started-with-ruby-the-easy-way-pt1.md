# Getting Started With [Ruby] the Easy Way Pt1 - Comments, Variables, Strings

Have you ever heard about Ruby? Ruby is one of the most popular programming languages in the World. It is also a programming language that is incredibly easy to learn. This will be the goal of this mini series. It will help you learn core concepts of Ruby and become proficient in this interesting programming language. Your journey to learn Ruby starts now.

<!--
Table of Contents:
## A brief introduction
## It all starts with console
## Comments
## Variables
## Strings
## Ruby and Math
## Epilogue: Getting Started With Ruby the Easy Way Pt1
-->

Getting Started With Ruby the Easy Way [Part 2] (Data Types Pt1).

Getting Started With Ruby the Easy Way [Part 3] (Data Types Pt2, Control Flow Pt1).

Getting Started With Ruby the Easy Way [Part 4] (Control Flow Pt2).

Getting Started With Ruby the Easy Way [Part 5] (Control Flow Pt3).

Getting Started With Ruby the Easy Way [Part 6] (Methods).

Getting Started With Ruby the Easy Way [Part 7] (Recursion, Scope, OOP Pt1).

Getting Started With Ruby the Easy Way [Part 8] (OOP Pt2).

Getting Started With Ruby the Easy Way [Part 9] (OOP Pt3).

Getting Started With Ruby the Easy Way [Part 10] (OOP Pt4 and Beyond).

## A brief introduction

Ruby is one of the most used programming languages in the World. It is regularly placed in top 10 positions on [TIOBE index]. In 2006 it even won the highest position of the list. What makes Ruby so popular? There are at least two reasons. First, Ruby is very easy to learn and use. If you know and like Python, another popular programming language, you will probably also like Ruby.

Both these languages have minimalist syntax. Both are designed with productivity in mind. It is designed to make programming an activity you enjoy. This is especially true about Ruby. It looks quite similar to English. Yet another reason why many programmers chose Ruby as their first programming language. The second reason is Ruby on Rails.

This is a server-side web application framework written in Ruby created by [David Heinemeier Hansson], co-founder of [Basecamp]. This relationship between Ruby and Ruby on Rails is similar to the relationship between PHP and WordPress. Another popular programming and another popular framework. One benefits from and helps the other.

There is a big community of passionate developers concentrated around both. This is also why Ruby is not going away any time soon. Let's take a look at Ruby more closely. Ruby first appeared in 1995. It was created by programmer Yukihiro "Matz" Matsumoto. It is a dynamic and object-oriented programming language. It is also a general-purpose programming language.

This means that you can use Ruby in various ways. For example, you can use it for creating web applications, with or without some framework. You can also use it for writing software and applications. Ruby is also cross-platform. You can use it on any platform you want after you install it, just like Python.

One interesting thing is that, in Ruby, everything is an object. Yes, this also includes even numbers. If you are not familiar with the concept of objects, don't worry. You will learn about them in this mini series. Another interesting thing is that in Ruby, everything has a "return value". Methods like `puts` that don't have any useful return value will return `nil`. Enough of talking about the history. Let's dive into the world of Ruby, starting with basics.

## It all starts with console

Let's start learning Ruby the easy way. The console will be probably the best for this. As in case of many other programming languages, Ruby also comes with built-in console. Console is a very useful tool for debugging your code. It can also help you understand how various concepts of specific programming language work, what is under the hood.

In Ruby, there are two ways, or methods you can use, to output something in console. The first way is by using `puts` method. The second way is by using `print` method. There are two differences between these two methods. First, the first, `puts`, adds a new line to the end of each argument if there is not one already. The second, `print` doesn't. It will print everything on the same line.

The second difference is how `puts` and `print` handles arrays. When you use `print` you will get the whole array, including square brackets and `NIL`, if there is one. When you use `put` you will get only the elements inside the array. It will not print the brackets, or `NIL`. Remember these differences so you can choose which method is more appropriate to use at the moment.

Fortunately, there is a way to use `puts` to print an array and get the same result as with `print`. If this is what you want to achieve, all you need is to use string interpolation. You will learn about string interpolation later. For now, take a look at the last example in the code below.

```
##
# Using "puts" method
puts "This is your first line of code written in Ruby."

# Outputs: This is your first line of code written in Ruby

##
# Using "print" method
print "This is your first line of code written in Ruby."

# Outputs: This is your first line of code written in Ruby

##
# Example of automatic line insertion
puts "Hello"
puts " World"
puts " in"
puts " Ruby"
puts "."

# Outputs:
# Hello
#  World
#  in
#  Ruby
# .

print "Hello"
print " World"
print " in"
print " Ruby"
print "."

# Outputs:
# Hello World in Ruby.

##
# Example of printing an array using "puts"
# Notice the first empty line in output.
puts [nil, 0, 1, 2]

# Outputs:
#
# 0
# 1
# 2

##
# Example of printing an array using "print"
print [nil, 0, 1, 2]

# Outputs: [nil, 0, 1, 2]

##
# Printing an array using "puts"
# with the result you would get using "print"
puts "#{[nil, 0, 1, 2]}"

# Outputs: [nil, 0, 1, 2]
```

## Comments

Next are comments. Comments are lines of text within Ruby code, or just any code, that are ignored when you run the code. Programmers often use comments to document and annotate their code. In other words, to make the code more readable. Another good use of comments is to "comment out" or "disable" parts of code. You don't want the code to be executed, but you don't want to remove it.

In Ruby, there are two types of comments, single- and multi-line. Single-line comments start with the hashtag symbol (`#`). Multi-line comments start with `=begin` and end with `=end` keywords. Everything you write between these two keywords will be interpreted by Ruby as a comment.

```
# This is an example of a single-line comment.

=begin
   This an example
   of a multi-line
   comment
=end
```

_Side note: the code examples throughout this mini series will sometimes use two hashtag symbols `##`. This is not another type of comment. It is just to make the individual examples more distinguishable. In other words, there is no difference between `#` and `##`._

## Variables

One fundamental part of almost every programming language are variables. This is also true for Ruby. You can think about a variable as a storage with a name that holds some value. When you want to assign a variable a value, you use the equal sign (`=`). Then, when you want to access the value stored inside the variables, you use the variable name.

It is called variable because the information stored in that location can be changed when the program is running. The only exception to this rule are constants. Constants are special type of variables that begin with a capital letter. When you assign value to a constant variable you can't change it later.

```
##
# Examples of a variable
x = 8
name = "Ruby"

puts x # Outputs: 8
puts name # Outputs: Ruby

##
# Examples of a constant variable
ExampleConstant = "This is a constant"

# Trying to re-assign constant variable
ExampleConstant = "This will not work"

# :5: warning: already initialized constant ExampleConstant
# :2: warning: previous definition of ExampleConstant was here

##
# Declaring constant using normal variable.
exampleVariable = "Hello World!"

ExampleConstant = exampleVariable # This is a constant

puts ExampleConstant # Outputs: "Hello World!"
```

One intersecting thing about variables. Ruby also supports something called parallel assignment of variables. This enables you to create multiple variables and assign values to them with a single line of code. Parallel assignment is also useful when you want to swap the values already stored in two variables.

```
##
# Step-by-step assignment
x = 1
y = 1
z = 2
w = 3

##
# Parallel assignment
x, y, z, w = 1, 1, 2, 3

##
# Example of swapping variable values
a = "Hello "
b = "Ruby."

puts a+b # Outputs: Hello Ruby.

# swapping the values
a, b = b, a

puts a+b # Outputs: Ruby.Hello
```

## Strings

Next key concept are strings. A string is any text between single or double quotation marks. However, there are some characters that can't be directly included in a string. For example, you can't include single quotes directly inside a single quote string. This additional quote would mark the end of the string. The same is true about double quotes.

Fortunately, there is a way to include characters like these in a string. You can achieve this by using an escape sequence, or escape the characters. This escape sequence is indicated by a backslash (`\`). Backslash has to precede the character you want to escape. This is not need when you create string with double quotes and want to include single quote, or the other way around.

A string created with double quotation marks can also include the `\n` escape sequence, which represents a new line. When it comes to single-quote strings, only the \' and \\ escape sequences will work.

```
##
# Example of a single- and double-quote string
textSingle = 'Ruby is fun.'
textDouble = "Ruby is fun."

##
# Example of single quote inside double-quote string
text = "Ruby's syntax is simple."

##
# Example of incorrect single quote inside single-quote string
textError = 'Ruby's syntax is simple.'

# :1: syntax error, unexpected tIDENTIFIER, expecting end-of-input
textError = 'Ruby's syntax is simple.'

##
# Example of correct (escaped) single quote inside single-quote string
textError = 'Ruby\'s syntax is simple.'

##
# Example of double-quote strings with escaped character for a new line
text = "Hello \n World."

puts text

# Outputs:
# Hello
#  World.

##
# Example of single-quote strings with escaped character for a new line
text = 'Hello \n World.'

puts text

# Outputs: Hello \n World.
```

There is also something called string interpolation. String interpolation allows you to include any Ruby expression inside a double quote string using `#{ }`. Ruby will then evaluate this placeholder and replace it with correct value. One thing to remember is that there is no space between the hash symbol (`#`) and the opening curly brace (`{`). Otherwise, it would be interpreted as literal text.

```
##
# Example of string interpolation (correct)
a = 5
b = 2

puts "The sum of #{a} and #{b} is #{a+b}."
# Outputs: "The sum of 5 and 2 is 7."

##
# Example of string interpolation (incorrect)
puts "The sum of # {a} and # {b} is # {a+b}."
# Outputs: "The sum of # {a} and # {b} is # {a+b}."
```

Next, you can also concatenate strings. Meaning, you can join strings using the plus symbol (`+`). When you want to concatenate strings, it doesn't matter whether you created them with single or double quotes. String concatenation also works even if your string contains numbers. Any numbers will be added as string, rather than an integer.

However, concatenation will not work when you try to add a string to a number. This will result in an error. String and number are two different entities. "0" is a string, whereas 0 is an integer.

```
##
# Example of string concatenation (correct)
a = "Hello "
b = 'there '
c = "Ruby."

puts a+b+c
# Outputs: Hello there Ruby.

# or
puts "Hello " + 'there ' + "Ruby."
# Outputs: Hello there Ruby.

##
# Example of string concatenation (incorrect)
a = "Hello "
b = 3
c = " Ruby."

puts a+b+c
# Outputs: :5:in `+': no implicit conversion of Fixnum into String (TypeError)
```

Finally, Ruby also allows you to repeat strings using the asterisk symbol, or symbol for multiplication, (`*`) and some integer. Just remember that the order of the string and the integer matters. The string has to always come first. And, that strings can't be multiplied by other strings.

```
##
# Example of repeating a string
a = "xyz"

puts a*3
# Outputs: "xyzxyzxyz"

# or
puts "xyz"*3
# Outputs: "xyzxyzxyz"

##
# Example of a string multiplied by other string
puts "xyz"*"abc"

# Outputs: :3:in `*': no implicit conversion of String into Integer (TypeError)
```

## Ruby and Math

Let's end this first part a bit of Mathematics. Math is an important part of programming. Ruby supports all usual arithmetic operators for addition, subtraction, multiplication, division, modulus operator and exponent. The modulus operator is represented by the percentage symbol (`%`). It represents the remainder of a division. The Exponent operator is represented by two asterisk symbols, or symbols for multiplication, (`**`).

One thing about numbers and Ruby. When you divide two integers, the result will be an integer. If you want the number to have a floating point, make it a decimal number, you have to add the floating point to one of the numbers.

```
x = 5
y = 2

##
# Addition
puts x+y # Outputs: 7

##
# Subtraction
puts x-y # Outputs: 3

##
# Multiplication
puts x*y # Outputs: 10

##
# Division
puts x/y # Outputs: 2

##
# Modulus Operator
puts x%y # Outputs: 5

##
# Exponent
puts x**y # Outputs: 25

##
# Creating result with floating point
x = 5.0
y = 2

puts x/y # Outputs: 2.5
```

All of arithmetic operators also have corresponding shorthand forms for assignment you can use. These operators are also called self-assignment operators. The reason for this name is that they perform an assignment and an arithmetic operation at the same time.

```
##
# Addition
x += y  # the same as: x=x+y

##
# Subtraction
x -= y  # the same as: x=x-y

##
# Multiplication
x *= y  # the same as: x=x*y

##
# Division
x /= y  # the same as: x=x/y

##
# Modulus Operator
x %= y  # the same as: x=x%y

##
# Exponent
x **= y  # the same as: x=x**y
```

One last thing about Mathematics and Ruby. Operator precedence. Ruby evaluates every mathematical expression using an order of operations based on operator precedence. Exponentiation has the highest precedence. This is then followed by multiplication, division. Next is modulus from left to right and then addition and subtraction from left to right. When you want to change this order of operations, you can do so by using parentheses.

```
##
# Example of operator precedence
x = 10 + 2 - 8 * 8 - 2

puts x # Outputs: -54

##
# Changing the order of operations
x = ((10 + 2) - 8) * (8 - 2)

puts x # Outputs: 24
```

## Epilogue: Getting Started With Ruby the Easy Way Pt1

Congratulations! You've just finished the first part of this mini series about learning Ruby! You've learned a lot of things about Ruby itself and some of its core concepts. I hope you enjoyed it. In a recap, you've learned about how to use console, comments, variables and strings. And, you've also learned how to perform mathematical operations in Ruby.

In the next part you will go deeper and explore other parts of Ruby. For example, you will learn about things such as data types, user input and also about control structures. For now, go back to what you've learned today and play with the examples you practiced with. Remember that the more diligently you practice the faster and better you learn.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Part 2]: https://blog.alexdevero.com/getting-started-ruby-pt2/
[Part 3]: https://blog.alexdevero.com/getting-started-ruby-pt3/
[Part 4]: https://blog.alexdevero.com/getting-started-ruby-pt4/
[Part 5]: https://blog.alexdevero.com/getting-started-ruby-pt5/
[Part 6]: https://blog.alexdevero.com/getting-started-ruby-pt6/
[Part 7]: https://blog.alexdevero.com/getting-started-ruby-pt7/
[Part 8]: https://blog.alexdevero.com/getting-started-ruby-pt8/
[Part 9]: https://blog.alexdevero.com/getting-started-ruby-pt9/
[Part 10]: https://blog.alexdevero.com/getting-started-ruby-pt10/
[TIOBE index]: https://www.tiobe.com/tiobe-index/
[David Heinemeier Hansson]: https://en.wikipedia.org/wiki/David_Heinemeier_Hansson
[Basecamp]: https://basecamp.com
