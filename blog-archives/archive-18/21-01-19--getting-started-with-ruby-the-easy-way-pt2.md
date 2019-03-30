# Getting Started With [Ruby] the Easy Way Pt2 - Data Types Pt1

Some programming languages are hard to learn and some are easy. Ruby is one of the later. Although Ruby has simple syntax it is very powerful programming language. What's more, it is also quite versatile. You can use it to for web projects as well as for desktop applications. Give a Ruby a chance. Learn what you need to become a Ruby programmer. This article will help you with it.

<!--
Table of Contents:
## Getting User Input
## Data Types Pt1
### Numbers
### Booleans
### Nill
### Arrays
## Epilogue: Getting Started With Ruby the Easy Way Pt2
-->

Getting Started With Ruby the Easy Way [Part 1] (Comments, Variables, Strings).

Getting Started With Ruby the Easy Way [Part 3] (Data Types Pt2, Control Flow Pt1).

Getting Started With Ruby the Easy Way [Part 4] (Control Flow Pt2).

Getting Started With Ruby the Easy Way [Part 5] (Control Flow Pt3).

Getting Started With Ruby the Easy Way [Part 6] (Methods).

Getting Started With Ruby the Easy Way [Part 7] (Recursion, Scope, OOP Pt1).

Getting Started With Ruby the Easy Way [Part 8] (OOP Pt2).

Getting Started With Ruby the Easy Way [Part 9] (OOP Pt3).

Getting Started With Ruby the Easy Way [Part 10] (OOP Pt4 and Beyond).

## Getting User Input

Every programming language should provide some way to get input from the user. This also applies to Ruby. When you want to get user's input in Ruby, all you need is to use the `gets` method. This method will then return what the user types as a string. If you want to store the input you got for later, you can do it by assigning the return value of the `gets` method to a variable.

As you learned, the default value you will get when you use `gets` method is a string. What if the input you are asking for is a number and you need to get it in this data type? Fortunately, Ruby offers a quick and easy way to solve this issue. The solution is to use `gets.to_i` method. This will again get the input as a string, but Ruby will immediately automatically convert it to an integer.

There is one more thing you need to about the `gets` method. When you use it, you will get a line of text. And, this includes the new line at the end. This is a good thing if you ask for input multiple times and want to have each result on separate line. However, there might be situations when this will not be desirable. Then, in order to remove the new line, use the `gets.chomp` method.

```
##
# Example of "gets" method
# and assigning the return value to a variable
x = gets

# Print the value to console
puts x

##
# Example of the "issue" with new line
# Print instructions to console
puts "Please enter your name:"

# Ask for user's input
name = gets

# Print the result to console, using string interpolation
puts "Welcome, #{name}."

# Output when the input is "Tommy" (notice the dot ending the sentence on a new line):
# Please enter your name:
# Welcome, Tommy
# .

##
# Example of solving "issue" with new line using "gets.chomp"
# Print instructions to console
puts "Please enter your name:"

# Ask for user's input
name = gets.chomp

# Print the result to console, using string interpolation
puts "Welcome, #{name}."

# Output when the input is "Tommy" (notice the dot right after the name):
# Please enter your name:
# Welcome, Tommy.
```

## Data Types Pt1

Now, it is time for one of the most important topic in both, Ruby and also programming in general. Data types. What are data types? These are types of "things" in your code that are used to represent data. These data include numbers, text and other values. IT is basically what you, as a Ruby programmer, will work with the majority of time.

In Ruby, there are many less or more exotic data types, eight primary and 3 additional. Those eight primary Ruby data types are those you will probably use the most often. So, let's focus on those. What data types are we talking about? These primary data types are constants, integers, floats, strings (text), booleans, symbols, arrays and hashes.

Before you learn about all individual types, there is one thing you need to know about. You don't need to remember what data is which type when you work with it. Every time you assign some value to variable Ruby will do the heavy lifting. Meaning, Ruby will automatically determine and set appropriate data type for you. Now, let's talk about individual data types.

### Numbers

In Ruby, and many other programming languages, there are two types of numbers. First type is an integer. Integers are numbers probably in the simplest form possible. Integers are numbers without a fraction. They don't have a dot, or comma, and decimal places. And, just like in you are used to in the real world, integers can be either positive or negative.

The second type of number is a floating point number. Programmers usually refer to a floating point number as a float or float number. As the name suggests, these numbers contain either dot or comma and at least one decimal place. Floats can also be positive or negative. One interesting thing about numbers is that Ruby allows you to use underscore (`_`) to separate thousands places.

However, this is not something you have to remember because it is optional, not required. So, it is up to you whether you use this "feature" or not. If you find it useful, to use the underscore (`_`), use it. Otherwise, don't use it. One more thing you need to know about numbers. When you do calculations with numbers, remember that numbers in the form of integers and floats are the same.

What is the difference between these two? You will get different result when you do calculations with integers and when with floats. If any of the numbers involved in the calculation is a float, then you will also get a float as a result. When all numbers involved in calculation are integers you will get ... Yes, your guess is correct. You will also get an integer. Why is this important?

Think about some simple calculation, such as division. As you now know, if you divide two integers you will get an integer. On the other hand, if you divide two floats you will get a float. Finally, if you divide an integer with a float you will get a float. What will happen when you try to divide, say, 5 by 2? What will be the result you will get?

Both numbers are integers. Therefore, you will get an integer. In this case, you will get 2. Notice that you will not get the most accurate result, which would be 2.5. This would mean the result would be a float. However, you calculated with integers. So, you can't get float as a result. At this moment, this may look like a minor detail.

However, what if your program requires accuracy? What if you it requires the number to be as accurate as possible. Then, this minor detail could potentially cause you a lot of trouble. The lesson? It is better to use at least one float, or decimal number, when you want to do mathematical operations such as divisions. Then, you will always get a float.

```
##
# Example of an integer
x = 42

##
# Example of a floating point number, or float
y = 1.58

##
# Example of an integer using underscore (`_`)
# to separate thousands places.
z = 1_234

# same as
z = 1234

##
# Catch with numbers involved in mathematical operations
puts 5/2 # 2

# fix - at least one number is a float
puts 5/2.0 # 2.5
```

_Side note: When you work with numbers, it is good to remember that different countries use different punctuation for decimal and thousands separators. The punctuation Ruby uses is the same as is used in the USA. Interestingly, this is the exact opposite of the notation used in Germany for example. So, remember that geography can play a role even in programming._

### Booleans

Next data type would be strings. However, you already know everything you need because you learned about strings in [the first part]. The same applies to Mathematics. That's why the math in previous section was so brief. So, if you are not sure about how well do you understand any of these topics, take a look at the first part of this mini series. Now, it is time for booleans.

Boolean is a data type you will see, and probably also use, quite often. This data type comes in two possible "forms", `true` and `false`. As their names suggest, `true` represents something that is considered true, or "truthy". The `false` represents the direct opposite, something that is considered false, or "falsy".

You can use booleans just like other data types such as numbers, strings, arrays and hashes. You can assign them to variables, pass them to methods, or whatever you want. You will probably use booleans most often in control structures, for testing and debugging your code. These are some areas where booleans are incredibly handy and make programming much easier.

### Nill

As you learned in [the first part], in Ruby, everything has some "return value". If there is anything useful to return, the Ruby will return `nil`. This `nil` represents "nothing". Or, the absence of anything. This might be a bit difficult to understand at first. What is the point of having a "nothing" value for something that doesn't have a value?

You are correct. There is no reason to have this. However, as you know, Ruby always has to have something to return. Every operation must have some return value. So, it makes some sense to have this "nothing" as a return value. For now, just remember that `nil` represents "nothing". Sooner or later, this will start to feel natural to you as get more familiar with programming in Ruby.

One last thing about `nil`. Some Ruby programmers may tell you that `nil` is also a boolean. This is not true. There are only two booleans, `true` and `false`. The `nil` is just another object in Ruby, just like a number or string.

### Arrays

Next data type are arrays. Arrays are great you want to store multiple values, or items, in a single variable. You can think about arrays as bags you fill with various different things. You can use arrays to store other data type and even other arrays. These types of arrays, arrays that contain other arrays, are called multi-dimensional arrays. For example, you can create 2- or 3-dimensional arrays.

Values, or objects, inside an array are separated by commas (`,`) and enclosed by square brackets (`[]`). Another way is using `Array.new` method. This will create empty array. If you want to create array with some values, you add brackets with value(s) inside them. When it comes to arrays, remember two things. First, arrays have defined order keeps.

This means that you create an array you will always get that array in that "shape" and "form". Unless you take that array and change it, or the order of its object, manually. The second thing is that Ruby automatically assigns to all objects inside an array a specific index, or position. Without this, it would be difficult to access a specific value.

Index in an array always starts at 0. In other words, the first value inside an array is on index 0, second is on 1 and so on. When you want to access the value you need to know the correct index. How to access, or retrieve, a value in an array? You use the name of the array followed by square brackets. You put the index of the value between the square brackets.

When you try to access value that doesn't exist in an array, you will get `nil`. For example, if you have array with 3 values (values on index 0, 1 and 2) and you try to retrieve value on third index. Another way to retrieve a value with index is using `at()` method with the index between the brackets. You can also use index to set a value to a specific index.

This is similar to retrieving a value from an array. You use the name of the array, followed by square brackets with the index inside, followed by assignment operator (`=`), followed by the data you want to store at that index. Another way is by using `insert` method. This method accepts two arguments, index and values you want to add. One thing. When you retrieve a value, or set value to index, there are no spaces inside the square brackets.

As you know by now, arrays can store other arrays and these "parent" arrays are called multi-dimensional arrays. You can think about this multi-dimensional array, the outer one, as a "table". Then, you can think about every array inside it is as one "row". These inner arrays are also called nested arrays. Finally, every value inside every inner array, or "row", represents a "cell".

Retrieving value from nested array is easy. You will use the usual syntax for retrieving a value. But now you will add another set of square brackets, surrounding an index. The first set of brackets will specify the index of the inner array. The second will specify the value you want to retrieve. Remember that the deeper your array is, the more sets of brackets you will need to use.

When you already have an existing array you can also add, or append, a value to it. You can do it by using `<<`. This is also called "shovel" operator. You specify the name of the array and use the shovel operator followed by the data you want to add. Here, the shovel operator is basically a replacement for assignment operator (`=`). Remember that this will add the value at the end.

Another way to add a value at the end of an array is by using `push` method. What if you want to add value to the beginning of an array? The easiest way to get this done is by using `unshift` method, immediately followed by brackets with the value. Okay that was about adding. What if you want to remove some value? There are three ways to get this done.

First, you can use `pop` method. This method will automatically remove the last value. The thing about removing the last value is set in stone. You can't change it. Second, you can use `shift` method. This is basically the opposite of `pop`. It will automatically remove the first value. This is again something set in stone and you can't change it.

Lastly, there is the third way. This last option is using `delete_at` method. Fortunately, this method will finally allow you to specify the index so you can remove any value you want. You specify the index by adding brackets right after the name of the method, with value(s) inside them. That was a lot of information. Let's take a look at some examples.

```
##
# Example of creating an empty array
arrayExample =[]

# same as
arrayExample = Array.new

##
# Example of creating an array with values
arrayExample = ["string", 2, true, :symbol, ["nested array"]]

# same as
arrayExample = []
arrayExample[0] = "string"
arrayExample[1] = 2
arrayExample[2] = true
arrayExample[3] = :symbol
arrayExample[4] = ["nested array"]

##
# Example of creating an array with predefined length without values
arrayExample = Array.new(5)

# Result: arrayExample = [nil, nil, nil]

##
# Example of creating an array with predefined length with same values
arrayExample = Array.new(5, "string")

# Result: arrayExample = ["string", "string", "string", "string", "string"]

##
# Retrieving, or accessing, a value from an array
puts arrayExample[0] # Outputs: string

# or
arrayExample.at(0) # Outputs: string

##
# Appending, or adding, a value to an array using shovel operator
arrayExample << "another value"

puts arrayExample[5] # Outputs: another value

##
# Appending, or adding, a value to an array using push
arrayExample.push("another value")

puts arrayExample[5] # Outputs: another value

##
# Appending, or adding, a value to an array using unshift
arrayExample.unshift("another value")

puts arrayExample[5] # Outputs: another value

##
# Adding a value to an array using insert
arrayExample.insert(5, "another value")

puts arrayExample[5] # Outputs: another value

##
# Removing a value to an array using pop
arrayExample.pop

##
# Removing a value to an array using shift
arrayExample.shift

##
# Removing a value to an array using delete_at
arrayExample.delete_at(1) # removes value on 2nd index

##
# Example of a multidimensional array (2-dimensional)
arrayExample = [
  [1, 2],
  [4, false, 6],
  [7, 8, 9],
  ["string", true]
]

##
# Retrieving, or accessing, a value from a multidimensional array
puts arrayExample[1][2] # Outputs: 6
puts arrayExample[3][0] # Outputs: string
```

There are also some interesting things you can do with arrays in Ruby. For example, you can add, subtract and multiply arrays. You can also find an intersection of arrays. There is also a way to retrieve the first or last element quickly. Even if you don't know how many values the array has. Since we talk about number of values, you can also check for the length of the array.

What if your array contains some `nil` values you want to remove? Ruby has a method for that as well. There are also methods for rotating and sorting arrays. These are only a small sample of methods you can use with arrays. I recommend you take a look at Ruby documentation for array.

```
##
# Adding arrays
[1, 2] + [7, 8] # Result: [1, 2, 7, 8]

##
# Subtracting arrays
["five", "six", "seven", "eight"] - ["six", "seven"] # Result: ["five", "eight"]

##
# Multiplying arrays
["string", true] * 3 # Result: ["string", true, "string", true, "string", true]

##
# Finding intersection of arrays
[1, 2, 3] & [2, 3, 4] Result: [2, 3]

##
# Retrieving the first and last value
["five", "six", "seven"].first # Result: "five"
["five", "six", "seven"].last # Result: "seven"

##
# Checking the length of an array
[1, 2, 3, false, 5].length # Result: 5

##
# Sorting an array
[3, 1, 2].sort # Result: [1, 2, 3]

##
# Removing all nils from an array
[1, nil, 2, 3, nil].compact # Result: [1, 2, 3]

##
# Rotating an array
[1, 2, 3, 4, 5].rotate(2) # Result: [3, 4, 5, 1, 2]
[1, 2, 3, 4, 5].rotate(4) # Result: [5, 1, 2, 3, 4]
```

## Epilogue: Getting Started With Ruby the Easy Way Pt2

This is all for today. To quickly recap, you've learned how to ask users for input. Then, you've learned about the first four primary data types that exist in Ruby. These were numbers, booleans, nill and arrays. You will learn about the rest and much more in the next part. For now, give yourself a break so you can digest what you've learned today. With that, thank your for your time.

[xyz-ihs snippet="thank-you-message"]

[Part 1]: https://blog.alexdevero.com/getting-started-ruby-pt1/
[Part 3]: https://blog.alexdevero.com/getting-started-ruby-pt3/
[Part 4]: https://blog.alexdevero.com/getting-started-ruby-pt4/
[Part 5]: https://blog.alexdevero.com/getting-started-ruby-pt5/
[Part 6]: https://blog.alexdevero.com/getting-started-ruby-pt6/
[Part 7]: https://blog.alexdevero.com/getting-started-ruby-pt7/
[Part 8]: https://blog.alexdevero.com/getting-started-ruby-pt8/
[Part 9]: https://blog.alexdevero.com/getting-started-ruby-pt9/
[Part 10]: https://blog.alexdevero.com/getting-started-ruby-pt10/

<!-- ### Links -->
[the first part]: https://blog.alexdevero.com/getting-started-ruby-pt1/
