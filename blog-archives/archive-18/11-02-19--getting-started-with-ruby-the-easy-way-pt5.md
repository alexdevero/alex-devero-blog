# Getting started with Ruby – The Easy Way Pt5

Ruby is incredibly simple, powerful and beautiful language. It is also a language that is easy to learn, even for people who are new to programming. If you want to start with programming, or learn another programming language, this is your chance. This series will help you learn all you need to start programming in Ruby.

<!--
Table of Contents:
## Control flow Pt3
### Ranges
### Iterators
### Final note on iterators
## Epilogue: Getting started with Ruby – The Easy Way Pt5
-->

Getting started with Ruby – The Easy Way [Part 1].

Getting started with Ruby – The Easy Way [Part 2].

Getting started with Ruby – The Easy Way [Part 3].

Getting started with Ruby – The Easy Way [Part 4].

<!-- Getting started with Ruby – The Easy Way [Part 5]. -->

## Control flow Pt3

In the [previous part], you've learned about how to control flow in your Ruby code with case statement and loops. However, this is still not everything. There are two additional control flow tools in Ruby you can use to write more complex code and build bigger project. These tools are `ranges` and `iterators`. Let's take a look at both.

### Ranges

A range represents a sequence. This sequence can be composed of numbers or characters. For example, you can have range from 0 to 10, or from 56 to 82 or from "A" to "Z". All these are examples of valid ranges. In Ruby, there are two ways, or special operators, you can use when you want to create range. These range operators are `..` and `...`.

The first operator, the two-dot form, is also called "inclusive range". The second one, the three-dot form, "exclusive range". These alternative names also suggest where lies the difference. The inclusive range creates a range that includes the high value of the range you specified. The three-dot form creates a range that excludes this value.

Some people learning Ruby find it easier to work with ranges when they use these alternative names. It is much easier to recall that the inclusive range includes high value while the exclusive range excludes it. You will probably agree with it. If you want, remember the alternative names for ranges. I can make it easier for yourself to learn this piece of Ruby syntax so you can choose the right operator for a specific situation.

```
##
# Example of range with integers using inclusive range
a = (1..10).to_a
print a # [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Example of range with integers using exclusive range
aa = (1...10).to_a
print aa # [1, 2, 3, 4, 5, 6, 7, 8, 9]

# Example of range with negative integers using inclusive range
b = (-15..-1).to_a
print b # [-15, -14, -13, -12, -11, -10, -9, -8, -7, -6, -5, -4, -3, -2, -1]

# Example of range with characters using exclusive range
bb = (-15...-1).to_a
print bb # [-15, -14, -13, -12, -11, -10, -9, -8, -7, -6, -5, -4, -3, -2]

# Example of range with characters using inclusive range
c = ("a".."z").to_a
print c # ["a", "b", "c", "d", "e", "f", "g", "h", "i", "j", "k", "l", "m", "n", "o", "p", "q", "r", "s", "t", "u", "v", "w", "x", "y", "z"]

# Example of range with characters using exclusive range
cc = ("a"..."z").to_a
print cc # ["a", "b", "c", "d", "e", "f", "g", "h", "i", "j", "k", "l", "m", "n", "o", "p", "q", "r", "s", "t", "u", "v", "w", "x", "y"]

# This will not work
c = ("z".."a").to_a
print c # []
```

_Side note no.1: The `to_a` method in the example above is used to convert the ranges to an array. You've learned about arrays in the [second part] of this series. If you try to output the values without this method, you will get exactly the code you wrote. For example, you will get `1..10` instead of an array with all numbers between "1" and "10"._

_Side note no.2: Remember that you can output some value to console in Ruby in two ways. You can use either `put` or `print` method. You've learned about them and console in the [first part]. The example above uses `print` because it prints everything on the same line. And, in case of arrays, it also includes the square brackets._

A very good case for using ranges is when you work with `case statements`. Then, you can use ranges for `when` values. You've actually already used ranges for this example. Where? You've done this in the [fourth part], the example with age. Let's take a look at it.

Here, you are using exclusive ranges to create a case statement that returns development period based on child's age. For example, this statement will return the code inside the first `when` case when the child is older than "0" and younger than "14". Or, the age is smaller than "0" and bigger than "14". Otherwise, it will skip this `when` case.

```
# Example of a case statement
# using ranges for when values.
age = 42

case age
when 0..14
  puts "Child"
when 15..24
  puts "Youth"
when 25..64
  puts "Adult"
else
  puts "Senior"
end
```

There is another situation when using range, the inclusive, is quite handy. This is when you quickly want to generate all characters of the alphabet. You've done this in the first example above, using `("a".."z").to_a`. This is much faster than writing the whole alphabet by hand. It is at least ten times faster, unless you are a very fast typist.

### Iterators

As you've seen and learned in the previous lessons, you can loop over [arrays] and [hashes] using [for loops]. However, Ruby offers another, more elegant, looping methods to achieve the same result. These methods are called `iterators`. Iterators are used to create loops. These loops then return all the elements of inside the `array` or `hash`.

One great thing on iterators is that they are "chainable". You can use one iterator on top of another and add functionality to your code. You can also use other methods on iterators to further process the result returned by the iterator(s). There are [many] iterators you can use in Ruby. For now, let's take a look at six you may find the most useful.

These iterators are `each`, `times`, `collect`, `upto`, `downto` and `step`. All these iterator use similar syntax. This syntax might seem confusing. It always begins with the iterator name and `do` keyword. This keyword is then followed by "pipe" symbols (`| | `) with a variable inside. This variable is called the "block parameter". You can use any name for your variables. What follows next is a block of code you want to execute during each iteration.

The last thing is that every iterator ends with `end` keyword. Also, remember that in Ruby indentation matters. Block of code you want to execute must be indented for one level. If the code you want to execute is short, Ruby provides a way to write it as a one-liner. You can use curly braces (`{}`) to start and end code blocks. Braces replace the `do` and `end` keywords.

The `each` iterator loops through all elements of the array and, with each iteration, assigns the corresponding element to the variable inside the pipes. The second is the `times` iterator. This iterator loops over a `hash` or an `array` specified number of times. You specify this through a variable called "times iterator". This variable is a number that precedes the iterator.

Remember that `times` iterator will always start from zero and run until it reaches one less than specified number. The third iterator is `collect`. This iterator loops over the hash or array and returns all the elements inside. You will usually use the `collect` iterator when you want to do something with each of the values to get the new array.

For example, let's say you have an array with numbers. You want to multiply all numbers by ten and store them in another array. This could be a good time for using collect `iterator`. The fourth and fifth iterators are `upto` and `downto`. These are mutual opposites. Both these iterators iterate from number "x" to number "y".

Similar to `times`, the "x" number is a number that precedes the iterator. The "y" number is provided as an argument for the iterator, inside parenthesis (`()`) right after the iterator name. In case of the `upto` iterator, the "x" number is the smaller value and the "y" is the higher. In case of the `downto` it is the other way around.

Remember this when you work with one of these iterators. Let's say that you accidentally switch the values. You use `downto` and make the "x" smaller than the "y". This would work with `upto` because it starts with lower value and moves up. However, it will not work with `downto`,  which starts with upper value and moves down.

The problem here is that when this happens Ruby will not show any error message. If you try this, iterator will not run. And, the only message Ruby will return will nothing at all. This can make it harder to debug your Ruby code and the root cause of the problem. So, pay close attention to what iterator and variables you use.

The last iterator you will learn about today is the `step` iterator. This iterator becomes very useful when you want to iterate over a range and skip some values. In this situation you could use [if statement], [ternary operators] or something similar. However, you can achieve the same result if you use the `step` iterator.

The syntax of `step` iterator is similar to the syntax of `upto` and `downto` iterators. You need to specify two numbers. Lower number, the "x", the iterator will start with and higher, the "y" that will stop the loop. "x" number precedes the iterator. "y" is again provided as an argument, inside parenthesis (`()`).

Then, you need a third number to specify the steps. This number also comes inside the parenthesis right after the "y", as a second argument. Remember that method arguments has to be separated by commas. The rest of the syntax follows the usual form.

```
##
# Example of the each iterator and array
arr = [1, 3, 5, 7, 9, 11]
sum = 0

arr.each do | x |
  sum += x
end

puts sum # Outputs: 36

# Shorthand version
arr.each { | x | sum += x }

##
# Example of the each iterator and hash
hashExample = { small: 480, medium: 768, large: 1190 }

hashExample.each do | key, value|
  puts "#{key} => #{value}"
end

# Outputs
# small => 480
# medium => 768
# large => 1190

# Shorthand version
hashExample.each { | key, value| puts "#{key} => #{value}" }

##
# Example of the times iterator
7.times do | x |
  puts "This is iteration number #{x}."
end

# Outputs:
# This is iteration number 0.
# This is iteration number 1.
# This is iteration number 2.
# This is iteration number 3.
# This is iteration number 4.
# This is iteration number 5.
# This is iteration number 6.

# Shorthand version
7.times { | x | puts "This is iteration number #{x}." }

##
# Example of the collect iterator
a = [1,2,3,4,5]
b = Array.new # Create empty array

# Populate "b" array with the values inside
# the "a" array multiplied by ten.
b = a.collect do | number |
  number *10
end

puts b

# Outputs:
# 10
# 20
# 30
# 40
# 50

# Shorthand version
b = a.collect { | number | number *10 }

##
# Example of the upto iterator
1.upto(6) do | x |
  puts "Round number #{x}."
end

# Outputs:
# Round number 1.
# Round number 2.
# Round number 3.
# Round number 4.
# Round number 5.
# Round number 6.

# Shorthand version
1.upto(6) { | x | puts "Round number #{x}." }

##
# Example of the downto iterator
5.downto(1) do | x |
  puts "Round number #{x}."
end

# Outputs:
Round number 5.
Round number 4.
Round number 3.
Round number 2.
Round number 1.

# Shorthand version
5.downto(1) { | x | puts "Round number #{x}." }

# Example of the downto and upto iterators done wrong
# This will not work.
1.downto(5) do | x |
  puts "Round number #{x}."
end

# This will also not work.
5.upto(1) do | x |
  puts "Round number #{x}."
end

##
# Example of the step iterator
# Run from 0 to 10 in step of 3
0.step(10, 3) do | x |
  puts x
end

# Outputs
# 0
# 3
# 6
# 9

# Shorthand version
0.step(10, 3) { | x | puts x }
```

### Final note on iterators

When you work with iterators, remember that you can't use all of them for every data type. The majority of iterators usually works only with one or few data types, or classes. For example, the `each` and `collect` will work perfectly with arrays and hashes. However, they will not work with types such as [strings] or [numbers].

On the other hand, the `times`, `upto`, `downto` and `step` will work like a charm with numbers, but not strings, hashes or arrays. The good thing is that when you try to use iterator with wrong data type Ruby will return an error message. This will make it easier to debug the problem and solve it. Remember this when you choose what iterator to use.

```
##
# Example of using iterators with wrong types no.1
[1, 2, 3].times do | x |
  puts "This is iteration number #{x}."
end

# Outputs: undefined method `times' for [1, 2, 3]:Array (NoMethodError)

##
# Example of using iterators with wrong types no.2
a = { name: 'Murphy', surname: 'Roddick' }

a.step(10, 3) do | x |
  puts x
end
# Outputs: undefined method `step' for {:name=>"Murphy", :surname=>"Roddick"}:Hash (NoMethodError)

##
# Example of using iterators with wrong types no.3
'A'.step('Z', 3) do | x |
  puts x
end

# Outputs: undefined method `step' for "A":String (NoMethodError)
```

## Epilogue: Getting started with Ruby – The Easy Way Pt5

Congratulations! You've just finished another lesson and made another step to learn programming in Ruby. Today, you've learned about ranges and iterators, when to use which, and what to pay attention to. This also means that you've just finished the fundamentals of control flow, a major milestone on your path to learn Ruby.

Now, you are ready to proceed to the next stage. At this stage, you will learn all there is to learn about methods in Ruby. You will learn what are methods and how to work with them, this includes parameters and arguments. You will also learn how to create your own. This will be another major milestone on your path to become a Ruby programming.

When you finish this, you will dive into the world of OOP in Ruby, or object-oriented programming. Here, you will learn about classes, instances, inheritance and much much more. This will be the topics for the next part of this series. So, stay tuned. You are very close to Ruby mastery. With that, thank you for your time and have a great day!

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Part 1]: https://blog.alexdevero.com/getting-started-ruby-pt1
[Part 2]: https://blog.alexdevero.com/getting-started-ruby-pt2
[Part 3]: https://blog.alexdevero.com/getting-started-ruby-pt3
[Part 4]: https://blog.alexdevero.com/getting-started-ruby-pt4
<!-- [Part 5]: https://blog.alexdevero.com/getting-started-ruby-pt5 -->
[previous part]: https://blog.alexdevero.com/getting-started-ruby-pt4
[second part]: https://blog.alexdevero.com/getting-started-ruby-pt2/#arrays
[first part]: https://blog.alexdevero.com/getting-started-ruby-pt1/#it-all-starts-with-console
[fourth part]: https://blog.alexdevero.com/getting-started-ruby-pt4/#case-statements
[arrays]: https://blog.alexdevero.com/getting-started-ruby-pt2/#arrays
[hashes]: https://blog.alexdevero.com/getting-started-ruby-pt3/#hashes
[for loops]: https://blog.alexdevero.com/getting-started-ruby-pt4/#for-loop
[many]: http://www.zenruby.info/2016/06/ruby-iterators-enumerators-enumerable.html
[if statement]: https://blog.alexdevero.com/getting-started-ruby-pt3/#conditionals
[ternary operators]: https://blog.alexdevero.com/getting-started-ruby-pt4/#ternary-operators
[strings]: https://blog.alexdevero.com/getting-started-ruby-pt1/#strings
[numbers]: https://blog.alexdevero.com/getting-started-ruby-pt2/#numbers

<!-- Resources: -->
<!--
- http://ruby-for-beginners.rubymonstas.org/blocks/iterators.html
- https://www.tutorialspoint.com/ruby/ruby_iterators.htm
- https://www.javatpoint.com/ruby-iterators
- http://www.zenruby.info/2016/06/ruby-iterators-enumerators-enumerable.html
- http://ruby-for-beginners.rubymonstas.org/built_in_classes.html
- https://www.eriktrautman.com/posts/ruby-explained-iteration
-->
