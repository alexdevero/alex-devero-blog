# Getting Started With Ruby the Easy Way Pt6 - Methods

There are many interesting topics in Ruby. One of these topics are methods. If you don't know what are methods, don't worry. This part will help you fix this. Today, you will learn all you need to know in order to create and use methods so you can make them part of your toolkit. With that, you will get one step closer to becoming a Ruby programmer.

<!--
Table of Contents:
## A short intro
## Methods
### Calling methods
### Parameters
### Multiple parameters
### Default parameters
### Optional parameters
### Returning values
### Chaining methods
### Methods as arguments
## Epilogue: Getting Started With Ruby the Easy Way Pt6
-->

Getting Started With Ruby the Easy Way [Part 1] (Comments, Variables, Strings).

Getting Started With Ruby the Easy Way [Part 2] (Data Types Pt1).

Getting Started With Ruby the Easy Way [Part 3] (Data Types Pt2, Control Flow Pt1).

Getting Started With Ruby the Easy Way [Part 4] (Control Flow Pt2).

Getting Started With Ruby the Easy Way [Part 5] (Control Flow Pt3).

Getting Started With Ruby the Easy Way [Part 7] (Recursion, Scope, OOP Pt1).

Getting Started With Ruby the Easy Way [Part 8] (OOP Pt2).

Getting Started With Ruby the Easy Way [Part 9] (OOP Pt3).

Getting Started With Ruby the Easy Way [Part 10] (OOP Pt4 and Beyond).

## A short intro

After finishing the [fourth] and [fifth part], you have achieved a big milestone in your journey to the world of Ruby. You have learned about control flow. This is a very important concept everyone serious about learning Ruby has to know about. Learning about control flow is also a good preparation for more advanced and difficult concepts that will follow. These are the concepts you will learn about in this and the next part.

Today, you will learn about everything you need to know about methods. If you think that loops, and other tools from control flow, are great wait until you learn about methods. Methods will help you take your programming skills to another level. And also write much better code. Every Ruby developer will agree that methods will be one of those tools you will use literally every day. Enough of talking. Let's learn about methods.

## Methods

You probably didn't realize it, but you have already seen examples of methods. For example, the `put` and `print` you have learned about in the [first part] were methods. You saw another batch of methods in the [second part]. The `new`, `push` and other methods in the section about [arrays]. All these were built-in Ruby methods. Anyway, what are methods?

Put simply, a method is a set of statements, or block of code, that performs a specific task. As you saw, there are many methods built inside Ruby ready for you to use. However, you can also define your own methods to perform the tasks you want. This may sound good, but it is not the main argument for, and benefit of, using methods.

The best thing on methods is that you have to define them, or create, only once. Then, you can use them any time you want or need. You don't have to define them again. You just call them using their name. Then, Ruby will find the correct method and run the statements, or code, inside it. In short, define once, reuse any time.

This is the lingo developers use when they create methods. They talk about defining or declaring a method. And, when developers use methods, they talk about calling a method. The way you define a method a simple. Every method starts with `def` keyword. What follows next is the name of the method. Every method must have some name. In the end, how would you want to call the method if it has no name?

The statements, or code, you want to execute is on the next line and indented. This is just like statements and loops. The indentation is important because, as you know, white space matters in Ruby. So, make sure to indent the code inside methods properly. Lastly, you have to end every method with `end` keyword. Just like statements and loops.

One thing about naming methods you need to remember. Method name can contain upper-case and lower-case letters. It can also contain numbers and underscores (`_`) and even punctuation symbols such as `!`, `?` and `=`. However, it can't begin with punctuation signs or a number. It can begin only with letters underscores (`_`).

Lastly, method name can't contain space. If you want to use multiple words as the method name, use underscores or different case to separate the words.

```
##
# Method syntax
# 'def' keyword followed by name of the method
def methodName
  # code you want to execute
end
# 'end' keyword to mark end the method

##
# Example of a method called "greeting"
def greeting
  puts 'Hi! Ruby is on the line.'
end
```

The second example above, shows a definition of a method called "greeting". When you call this method it will print the 'Hi! Ruby is on the line.' message to the console.

_Side note: It is a good practice to start the name of the method with a lowercase letter. Otherwise, you or another Ruby developer could confuse it with a constant._

### Calling methods

Defining method is incredibly easy and fast. Calling them is even easier and faster. All you need is to choose the method you want to use and write its name. Ruby will then use that name to find the correct method and execute the code inside it. You can call methods as many times as you want or need.

Calling method is not limited only to global scope. You can also call methods inside other methods. When you define a method that should call another method, all you need is to use the correct method name you want to call. Then, when you call the parent method, Ruby will also automatically call the method inside it.

One thing to remember when you work with methods. Always define methods before you call them. If you try to call a method before you define it, Ruby will raise an error and warn you that the method doesn't exist.

```
##
# Example of calling a method
# Define a method called "greeting"
def greeting
  puts 'Hi! Ruby is on the line.'
end

# Call the "greeting" method
greeting
# Outputs: Hi! Ruby is on the line.

##
# Calling the method multiple times
greeting
greeting
greeting

##
# Example of calling a method from another method
# Define greeting method
def greeting
  puts 'Hi! Ruby is on the line.'
end

# Define sayItAgain method
def sayItAgain
  # Call greeting method
  greeting
end

# Call sayItAgain method
doAgain
# Outputs: Hi! Ruby is on the line.

##
# Example of calling a method before defining it
# Don't do this!
# Call the "greeting" method
greeting # Outputs: undefined local variable or method `greeting' for main:Object (NameError)

# Define the "greeting" method
def greeting
  puts 'Hi! Ruby is on the line.'
end
```

### Parameters

Methods are a great way to create reusable chunks of code. Thanks to methods you no longer have to write the same code over and over again. However, what if you need to make the code inside the method more flexible? For example, the greeting method could print a message with person's name. The problem is that people have different names. What then?

In that case, you can use method "parameters". When you define a method you can define parameters inside parentheses that follows the method name. Then, when you call the method, you "pass" the data as parameter value to the method using parentheses. So, in the example with the name, you can add `name` parameter. Then, you can use [string interpolation] to include the name in the message.

There are limitations in Ruby for naming parameters. You can name your parameters anything you like as long as the name is valid (naming methods).

```
##
# Example of a "greeting" method with parameter (name)
def greeting(name)
  # Include the name in the message
  # Remember that interpolation works only with double quotes
  puts "Hi! #{name} is on the line."
end

# Call greeting method with name passed as an argument
greeting('Jack')
# Outputs: Hi! Jack is on the line.

greeting('Tony')
# Outputs: Hi! Tony is on the line.

##
# Example of a "toSquare" method with parameter (x)
def toSquare(x)
  puts x * x
end

# Call toSquare method with number passed as an argument
toSquare(256)
# Outputs: 65536
```

You may have noticed in the example above that we referred to parameters as arguments. This is not a mistake. Parameters and arguments refer to the same thing. The only real difference is in the situation you are in. When you define a method you use and talk about parameters. When you call the method you use and talk about arguments.

So, in the example above, the "x" or "name" are both parameters of the method, while 256, "Jack" and "Tony" are arguments. This is often for hard to remember, especially for beginners. So, don't worry. Give it a time. One trick I like to use that may help you is to think about calling a method as a metaphorical discussion. In a discussion, you use arguments to convince the other side and win.


### Multiple parameters

There are no limits to how many parameters you can include in your methods. You can include as many as you want. Just make sure to separate all parameters by commas.

```
##
# Example of a "greeting" method with multiple parameters (first name, last name)
def greeting(firstName, lastName)
  puts "Hi! Mr. #{lastName} is on the line. You can call him #{firstName}."
end

greeting('Jack', 'Trout')
# Outputs: Hi! Mr. Trout is on the line. You can call him Jack.

##
# Example of a "sum" method with three parameters (x, y, z)
def sum(x, y, z)
  puts x + y + z
end

sum(7, 4, 9)
# Outputs: 20
```

When it comes to parameters, you don't have to always pass them directly. Meaning, you can also pass variable arguments.

```
##
# Example of a "greeting" method and variable arguments
# Define variables
personsFirstName = 'Tony'
personsLastName = 'Gadget'

# Define greeting method
def greeting(firstName, lastName)
  puts "Hi! Mr. #{lastName} is on the line. You can call him #{firstName}."
end

# Call greeting method passing variables as arguments
greeting(personsFirstName, personsLastName)
# Outputs: Hi! Mr. Gadget is on the line. You can call him Tony.

##
# Example of a "sum" method and variable arguments
def sum(x, y, z)
  puts x + y + z
end

numOne = 13
numTwo = 14
numThree = 872

sum(numOne, numTwo, numThree)
# Outputs: 899
```

Lastly, you can also omit the parentheses. This can lead to shorter and cleaner code. However, it can also backfire and make your code confusing. If you decide to omit the parentheses, make sure to include space before the method name and the first argument. The same applies to calling methods. The commas are still necessary to separate parameters.

```
##
# Example of a "greeting" method without parentheses
def greeting firstName, lastName
  puts "Hi! Mr. #{lastName} is on the line. You can call him #{firstName}."
end

# Call the "greeting" method without parentheses
greeting 'Jack', 'Trout'

##
# Example of a "sum" method without parentheses
def sum x, y, z
  puts x + y + z
end

# Call the "sum" method without parentheses
sum 7, 4, 9
```

### Default parameters

What if you don't want to use parameters every single time you call the method? In that case, you can set default values for the parameters. Then, when you call the method without providing all or any arguments it will still work. Ruby will execute the method and use the default values you specified. If you pass argument, Ruby will use it and ignore the default value.

You specify the default value inside the parentheses, right after the parameter name, after assignment symbol (`=`). Remember that, in Ruby, the order of parameters matters. Meaning, default parameters has to come next to each other. You can't mix them with parameters without default values. Otherwise, Ruby will return an error when it tries to execute the method.

This is a good thing because it makes using default parameters easier. You don't have to remember that first and fourth parameters has default value and second and third don't. Ruby will not allow this. You will have to include the first and fourth parameter, those with default values, first, before the rest of parameters.

```
##
# Example of a "sum" method with default values for y (8) and z (13) parameters
def sum(x, y = 8, z = 13)
  puts x + y + z
end

sum(7)
# Outputs: 28 (7 + 8 + 13)

sum(7, 15)
# Outputs: 35 (7 + 15 + 13)

sum(31, 62, 101)
# Outputs: 194 (31 + 62 + 101)

##
# Example of a parameters without default values preceding default parameters
# This will not work!
def sum(x = 8, y, z = 13, w)
  puts x + y + z
end

sum(7, 9, 5, 9)
# Outputs: syntax error, unexpected '=', expecting ')'
# def sum(x = 8, y, z = 13, w)

##
# Parameters with default value next to each other
# This will work
def sum(x = 8, z = 13, y, w)
  puts x + y + z
end

sum(7, 9, 5, 9)
# Outputs: 21

# or
def sum(y, w, x = 8, z = 13)
  puts x + y + z
end

sum(7, 9, 5, 9)
# Outputs: 21

# or
def sum(y, x = 8, z = 13, w)
  puts x + y + z
end

sum(7, 9, 5, 9)
# Outputs: 21
```

### Optional parameters

Default parameters are not the end. What if you want to define a method that accepts any number of arguments? Then, you can use optional parameters. The syntax is simple. You include a parameter and add asterisk symbol (`*`) before its name. When you do this, you can call the method and pass any number of arguments you want.

Ruby will pass all these arguments in the form of an array. The name of this array is the name of the parameter you specified. This also means that you can use index to pick specific argument passed to the method. If you call the method without any arguments, this array will be empty. Lastly, you can also mix parameters and optional parameters.

When you try to mix all three, parameters, default parameters and optional parameters. Remember what you've learned above about the order of parameters. In Ruby, the order matters. "Regular" parameters comes first, then the default and finally the optional. Try something else and Ruby will return an error when it tries to execute the method.

```
##
# Example of method with optional parameters
def someMethod(*x)
  puts x
end

someMethod(25, 'Ruby', true, 13)

##
# Example of picking an argument using index
def someMethod(*x)
  puts x[2]
end

someMethod(25, 'Ruby', true, 13)
# Outputs: true

##
# Example of "mixing" parameters
def someMethod(a, b, *c)
  puts "a is #{a}, b is #{b}. c is #{c}"
end

someMethod(true, "pirate ipsum", 13, 15, false)
# Outputs: a is true, b is pirate ipsum. c is [13, 15, false]

##
# Example of "mixing" all three
# This will not work!
def someMethod(a = 15, b, *c)
  puts "a is #{a}, b is #{b}, c is #{c}"
end

someMethod(true, "pirate ipsum", 13, 15, false)

# This will work
# "Regular" parameters first, then, default and then optional
def someMethod(a, b, c = 15, *d)
  puts "a is #{a}, b is #{b}, c is #{c}, d is #{d}"
end

someMethod(true, "pirate ipsum", 13, 15, false)
# Outputs: a is true, b is pirate ipsum, c is 13, d is [15, false]
```

### Returning values

Until now all the methods you have worked with output something to console. However, methods are not limited to this. You can also return the result using `return` keyword, followed by the value you want to return. Then, you can use the returned value further in the program. For example, you can assign the return value to a variable.

```
##
# Example of returning a value
def sum(x, y)
  # Return a value instead of printing it to console
  return x + y
end

puts sum(55, 21)
# Outputs: 76

##
# Example of returning a value and assigning it to variable
def sum(x, y)
  return x + y
end

result = sum(13, 98)
puts result
# Outputs: 111
```

When you want to return multiple values from a method, you have to separate them with commas, in the return statement.

```
##
# Example of returning multiple values
def squares(x, y, z)
  return x*x, y*y, z*z
end

result = squares(2, 3, 6)

print result
# Outputs: [4, 9, 36]
```

What if you forget to include the `return` statement in your method? No problem. Remember that Ruby always returns something. In case of methods, Ruby will return the evaluated result of the last line of the method you are calling.

```
##
# Example of method without return statement
def mathMagic(x, y)
  a = x - 50
  b = a + 98
  c = b - y
end

puts mathMagic(7, 18)
# Outputs: 37

# the same as
def mathMagic(x, y)
  a = x - 50
  b = a + 98
  c = b - y

  return c
end
```

One important thing about return statement you have to remember. Any code in the method that comes after the return statement will not execute. When Ruby reaches return statement it stops executing the code and returns the last thing it executed. The rest of the code is ignored. Programmers refer to this code as unreachable.

```
##
# Example of method with unreachable code
def someMethod(a)
  a = 5
  return a
  # code below is will be ignored
  a = 9
end

puts someMethod(0)
# Outputs: 5 (the value of "a" before the return statement)
```

### Chaining methods

As you know, in Ruby all methods return a value. This means that you can chain multiple methods together. And, you can also chain methods with [iterators]. Remember that if there is an error or `nil` anywhere along the chain, the entire chain will break down. Ruby will stop execution and return an error.

```
##
# Example of chaining method with an iterator
def square(x)
  x * x
end

##
# Example of chaining square method with to_s (conversion to string)
puts square(50).to_s
# "2500"

square(2).times {puts "Hi"}
# Outputs:
# Hi
# Hi
# Hi
# Hi
```

### Methods as arguments

Ruby also allows you to pass methods as arguments to other methods. For example, you can define method to sum two numbers. Then, you can define another one to multiple two numbers. Finally, you can combine these methods.

```
##
# Define a method to sum two numbers
def sum(x, y)
  x + y
end

##
# Define a method to multiply two numbers
def multiply(x, y)
  x * y
end

result = multiply(sum(2, 3), sum(4, 7))
puts result
# Outputs: 55
```

## Epilogue: Getting Started With Ruby the Easy Way Pt6

Congratulations! You've just finished another part of this series. What's more, you've also reached another milestone on your journey to learn programming Ruby. From now, not only that you know how to use Ruby built-in methods. You know how to create your own! And, you also know how to make your methods flexible with parameters.

With this knowledge, you can now write more complex code and create your own programs in Ruby. However, you are not at the end of the journey. There are still some topics you need to learn to become a real Ruby programmer. One of these topics are classes. This will be what you will learn about in the next part. Until then, practice what you've learned today.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Part 1]: https://blog.alexdevero.com/getting-started-ruby-pt1/
[Part 2]: https://blog.alexdevero.com/getting-started-ruby-pt2/
[Part 3]: https://blog.alexdevero.com/getting-started-ruby-pt3/
[Part 4]: https://blog.alexdevero.com/getting-started-ruby-pt4/
[Part 5]: https://blog.alexdevero.com/getting-started-ruby-pt5/
[Part 7]: https://blog.alexdevero.com/getting-started-ruby-pt7/
[Part 8]: https://blog.alexdevero.com/getting-started-ruby-pt8/
[Part 9]: https://blog.alexdevero.com/getting-started-ruby-pt9/
[Part 10]: https://blog.alexdevero.com/getting-started-ruby-pt10/
[fourth]: https://blog.alexdevero.com/getting-started-ruby-pt4
[fifth part]: https://blog.alexdevero.com/getting-started-ruby-pt5
[first part]: https://blog.alexdevero.com/getting-started-ruby-pt1/#it-all-starts-with-console
[second part]: blog.alexdevero.com/getting-started-ruby-pt2/
[arrays]: blog.alexdevero.com/getting-started-ruby-pt2/#arrays
[string interpolation]: https://blog.alexdevero.com/getting-started-ruby-pt1/#strings
[iterators]: https://blog.alexdevero.com/getting-started-ruby-pt5/#iterators

<!-- Resources: -->
<!--
- http://ruby-for-beginners.rubymonstas.org/blocks/iterators.html
- https://www.tutorialspoint.com/ruby/ruby_iterators.htm
- https://www.javatpoint.com/ruby-iterators
- http://www.zenruby.info/2016/06/ruby-iterators-enumerators-enumerable.html
- http://ruby-for-beginners.rubymonstas.org/built_in_classes.html
- https://www.eriktrautman.com/posts/ruby-explained-iteration
-->
