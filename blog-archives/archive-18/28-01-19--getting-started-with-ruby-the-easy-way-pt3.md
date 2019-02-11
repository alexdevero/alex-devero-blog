# Getting started with Ruby – The Easy Way Pt3

Ruby is dynamic, flexible and robust programming language. It is also very easy language to start with. If you are new to programming Ruby will help you start the easy way. Take the next step on your journey to learn Ruby. Learn about topics such as hashes, symbols and control flow.

<!--
Table of Contents:
## Data Types Pt2
### Hashes
### Symbols
## Control flow Pt1
### Conditionals
## Epilogue: Getting started with Ruby – The Easy Way Pt3
-->

Getting started with Ruby – The Easy Way [Part 2].

## Data Types Pt2

In the [the first part], you've learned about the first two primary data types available in Ruby, strings and constants. Then, in the [second part], you've learned about the another four, integers, floats, booleans and arrays. There are eight of them in total. This means that there are two more you need to learn about. Namely, hashes and `symbols`.

### Hashes

Hashes are another very useful data type. Ruby developers like to use them in cases when arrays are not sufficient to get the job done. This is due to the fact that hashes, to some degree, look similar to arrays. They too allow you to store other objects, in any data type. Just like arrays. In arrays, you store data using indexes. This is where hashes are different.

When you want to store some data in a hash, you do it in the form of a `key/value` pair. When you want to retrieve, or access, specific data (the `value`) you don't use index. Instead, you use specific `key` you previously assigned to that `value`. One way to think about hashes is to imagine areal dictionary. Here, the original word is a `key`. The translation of that word is a `value`.

For example, let's say you have a dictionary that translates from English to Spanish. You want to translate the word "computer". In that case, the word "computer" is the `key` while the Spanish version, "computadora", is the `value`. You would use the "computer" `key` to retrieve the "computadora" `value` from the hypothetical hash called "dictionary".

When you want to create a new hash, and populate it with data, the syntax is simple. You assign a `key` to a `value` using `=>`. Some Ruby developers like to call this a "hashrocket". When you want the hash to contain more than one pair, you separate these pairs with commas (`,`). Then, you wrap all these pairs with curly braces (`{}`). This is the next difference between hashes and arrays. Arrays use square brackets (`[]`) and hashes curly braces (`{}`).

This is not actually the only way to create a hash. You can also create it using `Hash` object and `new` method. This will create new empty hash. Then, when you want to add a new `key/value` pair you use the name of the hash, followed by square brackets with the `key` inside, followed by assignment operator (`=`), followed by the `value` you want to assign to that `key`.

This is almost the same thing you do in case you work with an array. At this moment, you are the only difference is that you are replacing the array `index` inside the brackets with a `key`. Remember that you can use any kind of data type, or object, as a `key`. And, you can store any kind of data type or object as a value. When you want to retrieve the `value`?

Then, you use the same syntax, but omit the assignment part. Meaning, you use the name of the hash, followed by square brackets with specific `key`. Another way to retrieve a `value` is using `fetch` method with the `key` as an argument, inside the parentheses. If you try to retrieve a value from pair that doesn't exist, Ruby will return `nil`. What if you want to change existing `value`?

You use the same syntax as you would if you would want to create a new `key/value` pair. Now, you will just override the existing `value` in existing pair, instead of adding a new pair. That was creating, retrieving and changing. What if you want to delete some pair? There are two options you can choose from. First, you can delete a pair by just changing the `value` to `nil`, using specific `key`. Second option is calling the `delete` method, with the `key` as an argument inside the parentheses.

Just like with arrays, there are a lot of things your can do with hashes. For example, you can merge hashes together using `merge` method. You can also retrieve all `values` using `keys` method. This will return the `values` inside the hash in the form of an array. You can also use `length` or `size` when you want to find out how many `key/value` pairs specific hash contains. You can find all available methods in [Ruby docs] for hashes.

_Side note: Starting with Ruby 1.9, there is another, "modern", syntax you can use to create a hash. You can replace the "hashrocket" (`=>`) with colons (`:`). However, there is a catch. Using colons will tell Ruby that you want the `keys` to be `symbols`. This also means that you can't use this "modern" syntax if you want to use `symbols` for `keys`._

_There is one more, important, thing to remember. When you use modern syntax you have to use `symbols` to retrieve data from hash. This is logical. Ruby created all `keys` as `symbols`. Therefore, when you want to retrieve any `value` assign to specific `key` you also have to use a `symbol`._

```
##
# Create an empty hash
emptyHashExample = Hash.new

# or
emptyHashExample = {}

puts emptyHashExample # Outputs: {}

##
# Add new key/value pairs an empty hash
emptyHashExample["one"] = "uno"
emptyHashExample["two"] = "dos"
emptyHashExample["three"] = "tres"

# Print the content of emptyHashExample to console
puts emptyHashExample # Outputs: {"one"=>"uno", "two"=>"dos", "three"=>"tres"}

puts emptyHashExample["one"] # Outputs: uno

##
# Create hash with content
germanHashExample = {
  "one"=>"ein",
  "two"=>"zwei",
  "three"=>"drei"
}

# Print the content of germanHashExample to console
puts germanHashExample # Outputs: {"one"=>"ein", "two"=>"zwei", "three"=>"drei"}
puts germanHashExample["three"] # Outputs: drei

# or with "modern" syntax, using ":"
germanHashExample = {
  one: "ein",
  two: "zwei",
  three: "drei"
}

# Print the content of germanHashExample to console
# Notice that when you use the modern syntax you also
# have to use `symbols` when you want to retrieve the data
# germanHashExample[:two] instead of germanHashExample["two"]
# using germanHashExample["two"] will return nothing.
puts germanHashExample # Outputs: {:one=>"ein", :two=>"zwei", :three=>"drei"}
puts germanHashExample[:two] # Outputs: zwei

##
# Change the content of existing hash
hashExample = {
  "one"=>"Change this."
}

puts hashExample # Outputs: {"one"=>"Change this"}

# change the value of "one"
hashExample["one"] = "This is a new value"

puts hashExample # Outputs: {"one"=>"This is a new value"}

##
# Delete content from hash
hashExample = {
  "name"=>"Anthony",
  "age"=>35
}

puts hashExample # Outputs: {"name"=>"Anthony", "age"=>35}

# delete the "age" pair
hashExample.delete("age")

puts hashExample # Outputs: {"name"=>"Anthony"}

# or if you use the modern syntax
hashExample = {
  name: "Anthony",
  age: 35
}

puts hashExample # Outputs: {:name=>"Anthony", :age=>35}

hashExample.delete(:age) # you must use symbol (notice the ":")
puts hashExample # Outputs: {:name=>"Anthony"}

##
# Merge two hashes
hashOne = {
  "foo"=>"bar"
}

hashTwo = {
  "bar"=>"bazz"
}

# merge hashOne and hashTwo into a new hash, hashThree
hashThree = hashOne.merge(hashTwo)

puts hashThree # Outputs: {"foo"=>"bar", "bar"=>"bazz"}

##
# Print all keys stored in the hash
hashFoo = {
  "foo"=>"bar",
  "bar"=>"bazz"
}

puts hashFoo.keys

# Outputs:
# foo
# bar

hashFoo = {
  "foo"=>"bar",
  "bar"=>"bazz"
}

##
# Print all values stored in the hash
puts hashFoo.values

# Outputs:
# bar
# bazz

##
# Get the length or size of a hash
hashFoo = {
  "foo"=>"bar",
  "bar"=>"bazz"
}

puts hashFoo.size # Outputs: 2
puts hashFoo.length # Outputs: 2
```

### Symbols

The last primary data type in Ruby are `symbols`. `Symbols` are used quite often by Ruby developers. Nonetheless, they are still a bit odd. This is especially true for beginners. You will probably don't need to use `symbols` on a daily basis in your project. However, you may see them somewhere else. So, it will be good for you to be at least familiar with this data type.

In short, `symbols` are something like a special variation of strings just different `class`. The difference is that `symbols` are not data, but code. And, they are immutable. `Symbols` can't be changed. You can think about `symbols` as a type that is identifying something important, while `string` is a type usually used to store some piece of text you probably want to work with in the future.

You've already seen `symbols` above in the examples with hashes. `Symbols` were those words starting with colons (`:`). Colons are also what you use when you want to create a new symbol-`:word`. When you want the symbol to contain more than one word you can't use spaces. You can either use different case or you can concatenate the words with underscores (`_`)-`:another_longer_symbol`.

One question you might be asking is, when should you use `symbols` and when `strings`. Well, there is no specific definition nor a perfect use case. One good rule of thumb, suggested by some Ruby developers, is that if the text you work with is "data" then use a `string`. When the text can change and it is not identifying something.

As mentioned above, `symbols` are usually identifying something important. This is another good way to use them, as immutable (unchangeable) identifier. For example, you can use them for `keys` in `hashes`. Another frequent use of `symbols` is as the name parameters of a method. You can also use `symbols` when you want to the status of some thing.

Imagine you are working on a project that also includes managing users. In this case, you can use `symbols` to identify different statuses or activity of these users. For example, you can create `symbols` for statuses such as `:logged_in`, `:logged_out`, `:active`, `:inactive`, `:free_user`, `:pro_user`, `:working`, `:slacking`, `:typing` and so on.

If you are still trying to wrap your head around `symbols`, don't worry. This is normal. Many people starting with Ruby find this data type confusing, even those more advanced. Maybe you just need to give it a time to let it settle. Also, you keep in mind that you will probably understand symbols better as you learn more about Ruby and as you write more code in Ruby. So, give it a time.

## Control flow Pt1

Let's leave data types behind and focus on another fundamental concept in Ruby. This is about conditionals and flow control. Put simply, a flow control is about controlling how Ruby moves through your code and what code it chooses to execute. This is done using booleans. These are the `true` and `false` you've learned about in the [second part]. There are several "tools" you can use to control this flow.

### Conditionals

There are many ways to control flow in Ruby. The easiest and probably most common are conditional. Another name that very frequently used for conditionals is `if` statements. These two names are interchangeable. It doesn't matter which one you use. Whether you use conditional or `if` statement, any Ruby developer will know what you are talking about. So, choose the one you like.

The work `if` statement does is simple. It checks if some condition is `true` or `false`. Then, depending on the result of that check, it executes your code. So, if this is `true` do this. Otherwise, do that. In both cases, Ruby will ignore the code that didn't meet the condition. So, if condition evaluates to `true`, Ruby will ignore code for `false`. Otherwise, Ruby will ignore the code for `true`.

The second option is not necessary. You can use `if` statement to execute some code only if condition is `true`, or only if it is `false`. The syntax of `if` statement is very easy. Every statement starts with the `if` keyword, followed by some condition, and ends with `end` keyword. The code you want Ruby to execute goes to something called `if` branch.

This branch is a block of code that comes after the line with the `if` keyword and it is indented by two spaces. This branch contains code only for one situation, if condition is `true` or `false`. When you want to cover both situations, you need to add `else` statement and branch. This statement goes right after the branch for `if` statement, before the `end` keyword. No indentation.

Lastly, you can check or test for more than one condition. You can do this using `elsif` statement. The syntax of `elsif` is the same as `if`-the keyword followed by condition. The only difference is that you need to replace the `if` keyword with `elsif`. However, the `else` and `elsif` statements, and related branches, are optional. You don't need to have them.

You can have an `if` statement without `elsif` or `else`. Or, you can have an `if` statement only with an else. You can also have an `if` statement with one or more `elsif`. Lastly, you can combine all of them. It depends on what do you need at the moment. Just remember three rules. First, you must have at least one `if` statement with a branch for it.

Second, you can have as many `elsif` statements, and branches, as you want. There is no limit, other than your taste for clean code. Third, you can have only one `else` statement, and branch. One more thing. You can also nest one `if` statement inside another one. This way you to test for one condition. Then, when this one is `true` you can test for another condition.

This will allow you to write more complex code because you can have multiple options to execute for a single condition. When you use nesting, remember that every statement must end with the `end` keyword. And, pay attention to indentation. That was a lot of information and it can be difficult to grasp everything. So, let's take a look at some examples.

```
##
# Simple if statement
x = 3

if x == 3 # condition for the statement (x == 3)
  # this is the if branch
  # code here will be executed
  # if condition is "true"
  puts "x is equal to 3"
end # marks end of the statement

# Outputs: x is equal to 3

##
# If statement with "else" statement and branch
x = 6

if x == 3
  # this is the if branch
  puts "x is equal to 3."
else # this is the else statement
  # this is the else branch
  # code here will be executed
  # if condition is "false"
  # otherwise, Ruby will ignore it
  puts "x is not equal to 3."
end

# Outputs: x is not equal to 3.

##
# If statement with "elsif" and "else" statements and branches
x = 5

if x < 3
  # the if branch
  puts "x is smaller than 3."
elsif x < 8 # the elsif statement with new condition
  # the elsif branch
  puts "x is bigger than 3 and smaller than 8."
else
  # the else branch
  puts "x is bigger than 3 and 8."
end

# Outputs: x is bigger than 3 and smaller than 8.

##
# Nested If statements
x = 5

if x > 3
  # another, nested, if statement
  if x < 8
      puts "x is bigger than 3 and smaller than 8."
  else
      puts "x is bigger than 3 and 8. "
  end # marks the end of the nested, inner, if statement
else
  puts "x is smaller than 3."
end # marks the end of the outer if statement

# Outputs: x is bigger than 3 and smaller than 8.

x = 11

##
# Nested If statements with elsif statement and branch
if x > 3
    if x < 8
        puts "x is bigger than 3 and smaller than 8."
    elsif x < 12
        puts "x is bigger than 3 and 8, but smaller than 12."
    else
        puts "x is bigger than 3, 8 and 12. "
    end
else
    puts "x is smaller than 3."
end

# Outputs: x is bigger than 3 and 8, but smaller than 12.
```

## Epilogue: Getting started with Ruby – The Easy Way Pt3

Congratulations! You've just finished the third part of this mini series. Let's quickly recap. First, you've learned about the last two primary data types. These were `hashes` and `symbols`. After that, you've learned about control flow and how to use conditionals, or `if` statements. This was just the tip of an iceberg. There is much more to learn.

However, there is no reason to rush it. Take some time and let all you've learned today settle. Revisit what you've learned today and practice on examples. Make sure you really understand everything. Only this will help you create solid foundation you build on later. No shortcuts or cheating. Remember that every master was once a beginner. With that, thank you for your time.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Part 1]: https://blog.alexdevero.com/getting-started-ruby-pt1
[Part 2]: https://blog.alexdevero.com/getting-started-ruby-pt2
[the first part]: https://blog.alexdevero.com/getting-started-ruby-pt1
[second part]: https://blog.alexdevero.com/getting-started-ruby-pt2
[Ruby docs]: https://ruby-doc.org/core-2.6/Hash.html

<!-- Resources: -->
<!--
- http://ruby-for-beginners.rubymonstas.org/built_in_classes.html
- https://en.wikibooks.org/wiki/Ruby_Programming/Data_types
- http://ruby-for-beginners.rubymonstas.org/built_in_classes/symbols.html
- https://www.culttt.com/2015/04/22/what-are-symbols-in-ruby/
- https://www.eriktrautman.com/posts/ruby-explained-conditionals-and-flow-control
-->
