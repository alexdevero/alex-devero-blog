# Getting started with Ruby Pt10 - OOP and Beyond
<!-- Getting started with Ruby Pt10 - OOP and Beyond -->

There are few things every serious Ruby programmer must know about. These things include concepts such as access modifiers, to_s method, modules, mixins, structs, procs and lambdas. Learn about all these concepts and more in this part of Getting started with Ruby. Expand your knowledge and become an advanced Ruby programmer!

<!--
Table of Contents:
## Ruby and OOP (Object-Oriented Programming) pt4
### Access modifiers
### Public
### Private
### Protected
### The to_s method
## OOP and beyond
### Modules
### Mixins
### The power of mixins
### Mixins and namespacing
### Mixins as method containers
### Structs
### OStruct
### Procs
### Lambdas
## Epilogue: Getting started with Ruby – The Easy Way Pt10
-->

Getting started with Ruby – The Easy Way [Part 1].

Getting started with Ruby – The Easy Way [Part 2].

Getting started with Ruby – The Easy Way [Part 3].

Getting started with Ruby – The Easy Way [Part 4].

Getting started with Ruby – The Easy Way [Part 5].

Getting started with Ruby – The Easy Way [Part 6].

Getting started with Ruby – The Easy Way [Part 7].

Getting started with Ruby – The Easy Way [Part 8].

Getting started with Ruby – The Easy Way [Part 9].

## Ruby and OOP (Object-Oriented Programming) pt4

### Access modifiers

So far, all the methods you have seen through this mini series were defined as publicly available. This means that you could call any of these methods from outside the class and they would work. However, there are situations where this behavior may not be what you want. In those situations you may want some methods to be visible only to the class.

One example of such a situation can be application for a Bank. Imagine you have a class containing methods to calculate values such as account balance, internal transactions, interests and so on. Making any of these methods available outside the class is not something you would want. That would be a significant security flaw.

Fortunately, Ruby provides a way to specify how visible your methods should be. In Ruby, this concept is called "access modifiers" and there are three access modifiers you can use-"public", "private" and "protected". These access modifiers can be applied only to methods. Instance variable are always private.

### Public

Any time you define a new class method, Ruby interprets it as public by default. The only exception is `initialize`. This means that any class method, other than `initialize`, is accessible and visible from both, the inside as well as the outside of the class.

### Private

When you want to make any class method accessible only inside the class in which it is defined, you can use the "private" access modifier. This means that you will use `private` keyword right above the class method you want to make private. Let's return to the example with the bank account to illustrate how this works.

In the code below, there is a `Bank`. This class contains the `initialize` and two other class methods. The `show_account_balance` method is public. Remember, if you don't use any access modifier, Ruby will interpret the method automatically as public. The `count_interest` method is private. There is the `private` keyword right above it.

Let's create new instance of the `Bank` class. Now, when you try to call the `show_account_balance` method on this instance, you will get what you expect. Ruby will output a short info about current account balance. However, when you try to call the `count_interest` method, Ruby will return an error.

```
##
# Create new Bank class
class Bank
  def initialize(account_balance)
    @account_balance = account_balance
  end

  # Public method "show_account_balance"
  def show_account_balance
    puts "There is currently #{@account_balance}$ on your bank."
  end

  # Private method "count_interest"
  private
  def count_interest
    @account_balance * 0.1
  end
end

# Create instance of Bank class
example = Bank.new(420)

# Call "show_account_balance" method (public method)
example.show_account_balance
# Outputs: There is currently 420$ on your bank.

# Call "count_interest" method (private)
example.count_interest
# Outputs: "private method `count_interest' called for #<Bank:0x0000000276c210 @account_balance=420> (NoMethodError)"
```

There is one important thing you must remember. When you use the `private` keyword in one of your classes, anything below it in the class will become private. In other words, all methods following the `private` keyword are private, not just the first one right after the keyword. If you want to negate this, use either `public` or `protected` keyword.

```
##
# Create new Bank class
class Bank
  def initialize(account_balance)
  end

  # Public method "show_account_balance"
  def show_account_balance
  end

  # Private method "count_interest"
  # Every method following "private" access modifier is private
  private
  def count_interest
  end

  # Also private method "count_debt"
  def count_debt
  end

  # Also private method "update_password"
  def update_password
  end

  # Public method "print_bank_info"
  # Use "public" to negate "private" access modifier
  public
  def print_bank_info
  end

  # Also public method "print_statement_info"
  public
  def print_statement_info
  end
end
```

### Protected

Protected methods are not accessible from outside code, just like private methods. However, you can call protected methods on an object of the same class or subclasses. There is one interesting thing on private methods in Ruby. You can't call private methods with an explicit receiver, even if that receiver is itself.

A "receiver" is the object that the method is being called from. Even if you try to call the private method with `self`, you will get an error. This might be actually good in some situations. Imagine, for example, that you  want to overload an operator to compare two objects using a private method.

In this example, you would define a new class, say Item with a private method `code`. Then, you can test if two items are equal, by comparing their codes. If codes are equal the items are equal as well.

```
##
# Create class Item
class Item
  # Add reader and writer methods for name and num
  attr_accessor :name, :num

  def initialize(name, num)
    @name = name
    @num = num
  end

  # == method to compare two instances of Item class
  def ==(other)
    self.code == other.code
  end

  # Private method code
  private
  def code
    name.length*num
  end
end

# Create two instances of Item class
lenovo = Item.new("Lenovo", 7)
macbook = Item.new("MacBook", 9)

# Compare the two instances
puts (lenovo == macbook)
# Outputs: "private method `code' called for #<Item:0x00000002647858 @name="Lenovo", @num=7> (NoMethodError)"
```

In the code above, when you tried to compare those two items, Ruby returned an error. This happened because you tried to call the private method `code` on `self` and the other object. One quick way to fix this is by making the `code` method public. That is not the ideal solution. You want the method to private for a reason.

Ruby offers another solution. You can use `protected` access modifier. When you change the `code` method from `private` to `protected` it will work. You will be able to call it and Ruby will not return an error. So, remember when you want some method to be accessible only from the inside use `protected`.

```
##
# Create class Item
class Item
  # Add reader and writer methods for name and num
  attr_accessor :name, :num

  def initialize(name, num)
    @name = name
    @num = num
  end

  # == method to compare two instances of Item class
  def ==(other)
    self.code == other.code
  end

  # Protected method code
  protected
  def code
    name.length*num
  end
end

# Create two instances of Item class
lenovo = Item.new("Lenovo", 7)
macbook = Item.new("MacBook", 9)

# Compare the two instances
puts (lenovo == macbook)
# Outputs: false
```

### The to_s method

The `to_s` method is one of those methods built-in in Ruby. It is included in all classes. This method gets called when you want to output the object. When you call the `to_s` method, it will print the object's class and an encoding of the object id. This is the default implementation defined in Ruby.

```
##
# Create class Human
class Human
  # Some code.
end

# Create instance of class Human
man = Human.new
puts man
# Outputs: "#<Human:0x0000000279e0d0>"
```

As you can see, when you call `puts man`, Ruby automatically calls the `to_s` method for the object `man`. Ruby will also call the `to_s` method when the object is used as a value in a string, for example `"#{man}"`. What if you want to change it? You can. You can define your own custom `to_s` method for a class. For example, you can add some more informative, useful and also readable data about the class.

```
##
# Create class Human
class Person
  def initialize(name, age, gender)
    @age = age
    @gender = gender
    @name = name
  end

  # Redefine the "to_s" method
  def to_s
    "#{@name} is a #{@gender} and is #{@age} years old."
  end
end

# Create instance of class Human
p = Person.new("Tony", 21, "man")
puts p
# Outputs: "Tony is a man and is 21 years old."
```

Defining the `to_s` method makes it easier and shorter to output the information of an object in the format you want. Other way to achieve the same result would be defining a custom method and then calling it on the object. When you define custom `to_s` method you call `puts` on your object, for example `puts obj`. With custom method, you would have to explicitly call it on the object, for example `puts obj.print_info`.

## OOP and beyond

So far, you've learned a lot about Ruby and object-oriented programming. However, this is not the end of your journey. There are few more concepts you need to know as well before you can start calling yourself a Ruby programming. Let's take a look these concepts.

### Modules

Extracting common methods to a superclass is a great way to keep your code organized, clean and short. It is also a great way to establish natural hierarchical structure. This is what you saw a couple of times throughout this series. Another way to achieve the same result in Ruby, grouping common methods together, is by using "modules".

A module is a collection of methods you can use in other classes. A module can include as many methods as you want. You can think modules as "libraries" providing common functionality you can "import" when you need. In Ruby, a module is defined using the `module` keyword that is then followed by the name of the module. Module name must be defined as a constant. It has to start with a capital letter.  The syntax is similar to classes.

There are two common naming conventions and good practices in Ruby for naming modules. First is to use verb that describes the behavior the module is modeling. Second is to use the "able" suffix on the verb. For example, you could have modules like "Drivable", "Flyable", "Runnable", "Walkable". Not all modules are named in this way. However, it is quite common.

```
##
# Create new module "Flyable"
module Flyable
  def fly
    puts "I can fly!"
  end
end
```

Why use modules instead of classes? Imagine having a number of subclasses with one superclass. For example, a superclass `Vehicle` and subclasses such as `Ship`, `Car`, `Motorcycle`, `Jet` and `Plane`. All these subclasses have some shared functionality and attributes they can inherit from the `Vehicle` superclass.

However, only `Jet` and `Plane` can fly, at least for now. One way to add this functionality is by defining separate `fly` methods for both subclasses, the `Jet` and `Plane`. Another is defining a module with this functionality and then include it in `Jet` and `Plane` subclasses. From now, all instances of `Jet` and `Plane` will be able to fly while instances of other classes won't. Programmers refer to it as "mix" it.

```
##
# Create new module "Flyable"
module Flyable
  def fly
    puts "I can fly!"
  end
end

# Create superclass Vehicle
class Vehicle
end

# Create subclass Ship that inherits from Vehicle
class Ship < Vehicle
end

# Create subclass Car that inherits from Vehicle
class Car < Vehicle
end

# Create subclass Motorcycle that inherits from Vehicle
class Motorcycle < Vehicle
end

# Create subclass Jet that inherits from Vehicle
class Jet < Vehicle
  # Include, or "mix", the "Flyable" module
  include Flyable
end

# Create subclass Plane that inherits from Vehicle
class Plane < Vehicle
  # Include, or "mix", the "Flyable" module
  include Flyable
end

# Create instance of Plane subclass
cesna = Plane.new

# Call fly method provided by "Flyable" module included in "Plane" subclass
cesna.fly
# Outputs: I can fly!
```

### Mixins

As you may remember, Ruby [does not allow] one class to inherit from multiple classes. This is why modules are so handy. This limit does not apply to them. In other words, a class can use, or "mix in", multiple modules. As many as you want. In Ruby, modules used this way are known and called as "mixins".

```
##
# Create some modules
module Thinkable
  # some code
end

module Speakable
  # some code
end

module Runnable
  # some code
end

module Walkable
  # some code
end

# Create class Human
class Human
  # Mix in all existing modules.
  include Thinkable
  include Speakable
  include Runnable
  include Walkable
end
```

Four things to remember. First, a class can only inherit from one class. However, class can mix in as many modules as you want. Second, you can't instantiate modules. You can't create an object from a module. Third, modules are used only for grouping common methods together. Fourth, classes are about objects while modules are about methods.

When to use modules and when class inheritance? If it's an "is-a/is-an" relationship, choose class inheritance. If it's a "has-a/has-an/is-able-to" relationship, choose modules. For example, a plane "is a" vehicle. Therefore, you would use class inheritance to create a subclass of a `Vehicle` superclass.

However, a plane "has an" ability to fly. Therefore, you would use a module to provide this specific functionality, not class inheritance.

### The power of mixins

Mixins are a great way to add functionality to classes while maintaining control. However, you will see the true power of mixins when you let mixins interact with code in the class that uses it. Ruby has a number of predefined mixins ready for you to use. For example, let's use one mixin already mixed in Ruby, the `Comparable`.

This mixin allows you to add standard comparison operators (`<`, `<=`, `==`, `>=` and `>`) to your classes. By default, the `Comparable` module assumes that any class that uses it also defines the operator `<=>`. Meaning, when you define the `<=>` method and include `Comparable` module you will get all six functions for comparison.

Let's illustrate how this works on a simple example. Imagine you have a `Cat` class and you want to make cats, instances of the `Cat` class, comparable based on their age. Then, all you have to do is include the `Comparable` module and implement the comparison operator `<=>`. Ruby will do the rest of the work for you.

```
##
# Create class Cat
class Cat
  # Add reader and writer methods for name, age and breed
  attr_accessor :name, :age, :breed

  # include "Comparable" module
  include Comparable

  def initialize(name, age, breed)
    self.name = name
    self.age = age
    self.breed = breed
  end

  # Create "<=>" method comparing age of two instances
  def <=>(other)
    self.age <=> other.age
  end
end

# Create two instances of Cat class
cindy = Cat.new("Cindy", 1, "Aegean")
tom = Cat.new("Tom", 5, "Aegean")

# Compare "cindy" and "tom" instances
puts cindy < tom
# Outputs: true
```

### Mixins and namespacing

So far, you've seen how to use modules to add, or mix-in, functionality to a class. Now, you will see another two uses for modules. The first one is using modules for namespacing. In this case, "namespacing" means organizing similar classes in a module. In other words, you will use modules to group related classes.

This is a good way to make it easier and faster for you to recognize which classes related. It also reduces the probability that one of your classes will collide with other because you used similar or even the same names. Meaning, you can have classes with the same names across different modules.

For example, let's say you have three classes, `Cat`, `Bear` and `Dog`. You can group these classes together in a single module called `Mammal`. Then, when you want to use any of these classes all you have to do is use the module name, followed by two colons(`::`), followed by the name of the class you want to use.

```
##
# Create module Mammal
module Mammal
  # Create class Dog
  class Dog
    def speak
      puts "Woof!"
    end
  end

  # Create class Cat
  class Cat
    def speak
      puts "Meow."
    end
  end

  # Create class Bear
  class Bear
    def speak
      puts "Roar!"
    end
  end
end

# Create instances of Cat, Dog and Bear
tom = Mammal::Cat.new
barry = Mammal::Dog.new
stuart = Mammal::Bear.new

# Let them speak
barry.speak
# Outputs: "Woof"

tom.speak
# Outputs: "Meow."

stuart.speak
# Outputs: "Roar"
```

### Mixins as method containers

Another good way to use modules is as containers for methods. Just like with class, you can group together similar methods so you can use them in our code. When you want to call a method contained in a module, you can use either the colon syntax (`::`) or the dot (`.`) syntax. In case of methods, the dot syntax is more common.

Remember that the dot syntax works only for methods. When you want to use some variable or constant that is inside a module you have to use the colon syntax. One simple example. Let's say you often need to work with some Math constants and methods. You can create a module and put all these constant and methods inside it. Then, you can use any of them exactly when you need.

```
##
# Create module MathSuit
module MathSuit
  # Add three constants
  PI = 3.14159265357987
  GOLDEN_RATIO = 1.6180339887498948482
  EULER_MASCHERONI = 0.57721

  # Add class method sum
  def self.sum(x, y)
    x + y
  end

  # Add class method square
  def self.square(x)
    x * x
  end

  # Add class method factorial
  def self.factorial(x)
     (1..x).inject(:*) || 1
  end
end

# Print the EULER_MASCHERONI constant
puts MathSuit::EULER_MASCHERONI
# Outputs: 3.14159265357987

# Call sum method
puts MathSuit.sum(13, 15)
# Outputs: 28

# Call factorial method
puts MathSuit.factorial(8)
# Outputs: 40320
```

As with classes, the main advantages of using modules to group methods and variables or constants is preventing name collisions. Modules allow you to use the same method names as long as these methods are not in the same module.

### Structs

In some cases, you don't really need to defining a class with a complete structure. All you need is just a group of attributes all in the same place. For example, let's say you are working with geometry. All that you need is to define points in a 2D space using "x" and "y" coordinates.

You could create a new class with necessary instance variables and methods. However, this is not necessary. Ruby gives you a way to avoid this. You can group together a number of attributes with a "Struct". This is a built-in Ruby class that makes it easier, faster and shorter to define simple classes, accessors and their initialize methods.

Let's go back to the example with geometry. You can create a new Struct called `Point`. This Struct will have two attribute accessors, one for "x" and one for "y" coordinate. With this, Struct will automatically create its initialize method for those defined accessors. As a result, you can now use `Points` just like a regular class. This also includes creating new instances from it.

```
##
# Create new Struct called "Point" with "x" and "y" attribute accessors.
Point = Struct.new(:x, :y)

# Create two new instances of Point Struct
center = Point.new(0, 0)
edge = Point.new(22, 78)

# Print the coordinates
puts center.x
# Outputs: 0
puts center.y
# Outputs: 0

puts edge.x
# Outputs: 22
puts edge.y
# Outputs: 78
```

### OStruct

Something very similar to Struct is OpenStruct, or OStruct. The difference is that OStruct doesn't have a defined list of attributes and you have to include it using `require` statement first. Since it doesn't have a defined list of attributes you can define them any time. This makes OStruct more flexible than Struct. However, it is slower.

```
##
# Require OStruct
require "ostruct"

# Create new OStruct called "person"
person = OpenStruct.new

# Add some attributes to "person" OStruct
person.name = "Victoria"
person.age = 27

# Print the person's attributes
puts person.name
# Outputs: Victoria
puts person.age
# Outputs: 27
```

Ruby also allows you to create new OStruct using a hash.

```
##
# Require OStruct
require "ostruct"

# Create new OStruct called "person" using hash
person = OpenStruct.new(name: "Victoria", age: 27)

# Print the person's name
puts person.name
# Outputs: Victoria
```

Both, the Struct and the OStruct, provide a very good way for you to create objects that behave like a class with the need to write only a minimum amount of code. In the case of OStruct, remember that you always have to require it before you can use it.

### Procs

Imagine a following scenario. You need to take a block of code, wrap it up inside an object, store it in a variable, and run the code in the block whenever and how many times you want. This may be less likely to happen but it still can happen. And, Ruby has a way to do this. It is called a "proc".

Procs are similar to methods. You can use them to perform operations and they can also include parameters. A Procs takes blocks of code and allows it to be reused whenever you need. The main advantage of Procs is that you can pass them into methods. This is possible because Procs are objects. There are no limits to how many Procs you can pass to your methods. When you want to run the code in the proc you use the `call` method.

Let's create a simple Proc called "greet". This Proc will take one parameter, `name`, and output a short message that will include the variable. Now, you can use the `call` method to call it.

```
##
# Create a new Proc Greet
greet = Proc.new do |name|
  puts "Hello #{name}! How are you doing?"
end

greet.call "Tommy"
# Outputs: "Hello Tommy! How are you doing?"
```

Let's take this further. Let's add a method called `greetGroup`. This method will take an array of strings and a Proc as its parameters. Then, it will call the Proc for every item in the array.

```
##
# Create a new Proc greet
greet = Proc.new do |name|
  puts "Hello #{name}! How are you doing?"
end

# Create another Proc greetGroup
def greetGroup(arrayOfNames, proc)
  arrayOfNames.each { |name| proc.call name}
end

people = ["Tommy", "Victoria", "Sebastian"]

# Call greetGroup method
greetGroup(people, greet)
# Outputs:
# Hello Tommy! How are you doing?
# Hello Victoria! How are you doing?
# Hello Sebastian! How are you doing?
```

As you can see, Procs can make your code more flexible. You can reuse code blocks across your project, without the need to write the code again and again from scratch every time. One last thing. "Proc" is short for "procedure".

### Lambdas

In other programming languages, a lambda is commonly referred to as an anonymous function. In Ruby, lambda is a variation of Procs. It is an instance of the Proc class to be specific. Just like with Procs, when you want to execute the lambda you use the `call` method. When you want to create a lambda in Ruby, you can use one of two syntax.

```
##
# Create a new lambda called "greet"
greet = lambda { puts "Hello Ruby!" }

# Alternative syntax for creating a lambda
greet = ->() { puts "Hello Ruby!" }

# Call lambda
greet.call
```

Lambdas and Procs are very similar. However, there are some important differences. First, lambdas and Procs handle arguments in a different way. When you use lambdas they will always check the number of arguments. Procs will not. When the number of arguments is correct lambdas and Procs work in the same way.

However, when the number of arguments is wrong lambda will return an error. On the other hand, the missing argument in Proc will automatically default to `nil` and Proc will continue executing the code.

```
##
# Lambda VS Proc Pt1
greet_lambda = lambda { | name | puts "Good morning #{name}!" }

greet_proc = Proc.new { | name | puts "Good morning #{name}!" }

# Call lambda and Proc with correct number of arguments
greet_lambda.call "Thomas"
# Outputs: "Good morning Thomas!"

greet_proc.call "Carol"
# Outputs: "Good morning Carol!"

# Call lambda and Proc with incorrect number of arguments
greet_lambda.call
# Outputs: Error: wrong number of arguments (given 0, expected 1)

greet_proc.call
# Outputs: "Good morning !"
```

The second difference between a lambda and a Proc is how they handle the `return` statement. When a lambda encounters a `return` statement it returns execution to the enclosing method. Meaning, `return` statement will stop lambda from executing and trigger the code right outside the lambda code.

When a Proc encounters a `return` statement it "jumps out" of itself, as well as the enclosing method. Meaning, it will not only stop executing the Proc itself, but also the enclosing method. One last thing. The name "Lambda" was inspired by Lambda calculus.

```
##
# Lambda VS Proc Pt2
def test_lambda
  # Create new lambda
  lambdaExample = lambda { return }

  # Call the lambda
  lambdaExample.call

  puts "Hello Lambda!"
end

def test_proc
  # Create new Proc
  procExample = Proc.new { return }

  # Call the Proc
  procExample.call

  puts "Hello Proc!"
end

# Call test_lambda method to test the lambda
test_lambda


# Call test_proc method to test the proc
test_proc
```

## Epilogue: Getting started with Ruby – The Easy Way Pt10

Congratulations! You've just finished another part of Getting started with Ruby series. Let's do a quick recap, today you've learned about public, private and protected access modifiers. Next, you've learned how to define your own custom `to_s` method.  After that, you've learned about modules and mixins and how and when to use them.

At the end, you've also learned about Structs, OStructs, Procs and Lambdas. Having all this knowledge, you can finally start calling yourself a Ruby programmer! You've done a good work! The next step is to take what you know and practice. Remember, it is only through diligent practice how one can become a true master. Write some code.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Part 1]: https://blog.alexdevero.com/getting-started-ruby-pt1
[Part 2]: https://blog.alexdevero.com/getting-started-ruby-pt2
[Part 3]: https://blog.alexdevero.com/getting-started-ruby-pt3
[Part 4]: https://blog.alexdevero.com/getting-started-ruby-pt4
[Part 5]: https://blog.alexdevero.com/getting-started-ruby-pt5
[Part 6]: https://blog.alexdevero.com/getting-started-ruby-pt6
[Part 7]: https://blog.alexdevero.com/getting-started-ruby-pt7
[Part 8]: https://blog.alexdevero.com/getting-started-ruby-pt8
[Part 9]: https://blog.alexdevero.com/getting-started-ruby-pt9
[does not allow]: https://blog.alexdevero.com/getting-started-ruby-pt9/#inheritance-on-multiple-levels

<!-- Resources: -->
<!--
- http://ruby-for-beginners.rubymonstas.org/blocks/iterators.html
- https://www.tutorialspoint.com/ruby/ruby_iterators.htm
- https://www.javatpoint.com/ruby-iterators
- http://www.zenruby.info/2016/06/ruby-iterators-enumerators-enumerable.html
- http://ruby-for-beginners.rubymonstas.org/built_in_classes.html
- https://www.eriktrautman.com/posts/ruby-explained-iteration
- http://nicholasjohnson.com/ruby/ruby-course/exercises/operator-overloading/
-->
