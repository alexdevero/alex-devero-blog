# Getting Started With Ruby the Easy Way Pt8 - OOP Pt2

Another part of Getting started with Ruby series just arrived! Learn about concepts such as instance and class variables and methods, accessors and ... The self. Expand your knowledge of Ruby and object-oriented programming. Take the next step to becoming a Ruby programmer. You are closer than ever before!

<!--
Table of Contents:
## Ruby and OOP (Object-Oriented Programming) pt2
### Instance variables
### Instance methods
### Accessors
### Getter methods
### Setter methods
### Accessors and the attr_accessor
### Self
### Class variables
### Class methods
### Class constants
## Epilogue: Getting Started With Ruby the Easy Way Pt8
-->

Getting Started With Ruby the Easy Way [Part 1] (Comments, Variables, Strings).

Getting Started With Ruby the Easy Way [Part 2] (Data Types Pt1).

Getting Started With Ruby the Easy Way [Part 3] (Data Types Pt2, Control Flow Pt1).

Getting Started With Ruby the Easy Way [Part 4] (Control Flow Pt2).

Getting Started With Ruby the Easy Way [Part 5] (Control Flow Pt3).

Getting Started With Ruby the Easy Way [Part 6] (Methods).

Getting Started With Ruby the Easy Way [Part 7] (Recursion, Scope, OOP Pt1).

Getting Started With Ruby the Easy Way [Part 9] (OOP Pt3).

Getting Started With Ruby the Easy Way [Part 10] (OOP Pt4 and Beyond).

## Ruby and OOP (Object-Oriented Programming) pt2

### Instance variables

In Ruby, there are more than just one type of a variable you can define in a `class`. One of these variables are instance variables. As you've learned in the [previous part], every object of a class is called an `instance`. Every one of these instances can have a separate copy of the instance variables.

These variables are independent. They exist only in specific instance. Let's say that you have two `instances` and both contain one instance variable and these variables share the same name. Even in this example these instance variables are still independent. When you change the variable in one instance, the second instance will stay unchanged.

Creating an instance variable is simple. All you have to do is "prefix" the variable name with the "at" sign (`@`). For example, `@age`. Let's take the example of the `Car` class from the [previous part]. In this example, we can pass a parameter to the `initialize` method of the `Car` class and assign it to an instance variable for a new object.

```
##
# Example of an instance variable
class Car
  def initialize(model)
    @model = model
  end
end
```

In the code snippet above, the `@name` is an instance variable for the class `Car`. Next, you can create new instances, or objects, of the `Car` class and pass an argument to the new method. For example, you can create `car1` and `car2` with different values for the instance variable `@model`.

```
##
# Create new instances of Car class
car1 = Car.new("Ferrari")

car2 = Car.new("Tesla")
```

Remember that both values exist only for the specific instance.  It doesn't matter that both instances use the same instance variable and `class`. Each instance still has its own unique instance variables that store values associated with that instance. Why can't you just use [local variables] instead of instance variables?

Instance variables are better because their scope is the entire object, or instance. This means that they are accessible inside every method you define for the object. Local variables are accessible only within the scope they are declared. For example, inside a single method. Lastly, a class can have multiple instance variables.

```
##
# Example of a class with multiple instance variables
class Car
  @condition = "new"

  def initialize(model, condition)
    @model = model
    @condition = condition
  end

  def print_info
      puts "This car is #{@model}. It is #{@condition}."
  end
end

# Create new instance of Car class
car1 = Car.new("BMW", "Used")

car1.print_info
# Outputs: This car is BMW. It is Used.
```

### Instance methods

When you take a look at the object around you, in the "real" world, they all behave in their own way. For example, a car on the street moves and your phone rings or vibrates. The same applies to objects in programming. This behavior, specific to the object's type, is defined by methods you define in the class.

This meaning that you can declare instance methods that are available to an object of the class. Just like with any method, instance methods can also include multiple parameters. These methods can also return values. For example, let's create a class "Cat" with instance method called "meow" that Outputs text.

Next, you can create one or more instances of this class "Cat". Then, you can call the "meow" method on these instances. To do this, you use the Ruby dot syntax.

```
##
# Example of a class with instance method
class Cat
  def meow
    puts "Meow!"
  end
end

# Create new instances of Cat class
cindy = Cat.new

# Call the meow method
cindy.meow
# Outputs "Meow!"
```

### Accessors

Another way to use an instance method is to access the instance variables from outside the object. You did something very similar in the Car example. Here, the instance method "print_info" returns the value of the `@model` and `@condition` instance variables, in the form of a short message.

In Ruby, this type of method, that is used to retrieve the value of the variable, is called a "getter" method. There is more. You can also define an instance method that modifies the value of some instance variable. This type of method is called a "setter" method. "Getter" and "setter" methods are called "accessors".

### Getter methods

Let's take a look at how we can re-write the example of `Car` class. The change will be quick. You will add two new getter methods, `get_model` and `get_condition`. Both these methods will return the value of `model` and `condition` variables. Nothing more and nothing less. Remember that you will now need to use `puts` or `print` when you call these "getter" methods in order to print the values.

```
##
# Example of getter methods
class Car
  @condition = "new"

  def initialize(model, condition)
    @model = model
    @condition = condition
  end

  # Getter method get_model
  def get_model
      @model
  end

  # Getter method get_condition
  def get_condition
      @condition
  end
end

# Create new instance of Car class
toyota = Car.new("Toyota", "New")

# Call both getter methods
puts toyota.get_model

# Outputs "Toyota"

puts toyota.get_condition
# Outputs "New"
```

### Setter methods

Creating with "getter" methods is very easy. The same is also true for "setter" methods, methods that will allow you to modify instance variables. There is just one caveat. In Ruby, there is a special syntax for defining "setter" methods. The name of the "setter" method is always followed by an "equal" sign (`=`). Then, what follows is the parameter that will provide new value for the instance variable.

```
##
# Example of setter methods
class Car
  @condition = "new"

  def initialize(model, condition)
    @model = model
    @condition = condition
  end

  # Getter method get_model
  def get_model
      @model
  end

  # Getter method get_condition
  def get_condition
      @condition
  end

  # Setter method set_model
  def set_model=(model)
      @model = model
  end

  # Setter method set_condition
  def set_condition=(condition)
      @condition = condition
  end
end

# Create new instance of Car class
mini = Car.new("Mini", "Used")

# Call setter method to change condition
mini.set_condition = "New"

# Call getter method to get condition
puts mini.get_condition

# Outputs "New"
```

In the code above, the `set_model` and `set_condition` are "setter" methods that set the value of the `@model` and `@condition` instance variables to the value of their parameter names.

Notice the special syntax you used for calling those "setter" methods: `mini.set_condition = "New"`. Normally, in order to call a method, you would use something like `mini.set_condition=("New")`. Here, the entire "set_condition=" is the method name. The string "New" is the argument you are passing into the method.

However, when it comes to "setter" methods, Ruby allows you to use this slightly different syntax. The reason might be that it feels more natural, like an assignment syntax: `mini.set_condition = "New"`. From now, when you will see code like this, remember that there is a "setter" method working behind the scenes.

In Ruby programming, it is a common practice to define the "getter" and "setter" methods with the same name as the instance variables they are working with, or accessing. For example, you could call the "getter" method for accessing the `@model` instance variable inside the`"` "`class` "model" while setter would be "model". The same for `@condition`.

```
##
# Example of getter and setter methods
class Car
  @condition = "new"

  def initialize(model, condition)
    @model = model
    @condition = condition
  end

  # Getter method get_model
  def model
      @model
  end

  # Getter method get_condition
  def condition
      @condition
  end

  # Setter method set_model
  def model=(model)
      @model = model
  end

  # Setter method set_condition
  def condition=(condition)
      @condition = condition
  end
end
```

### Accessors and the attr_accessor

Imagine for a moment that you have some object with a lot of instance variables, and their "setter" and "getter" methods. As you may guess, this code would be really long. Fortunately, Ruby has a built-in way to automatically create these "getter" and "setter" methods. It uses a method called `attr_accessor` method.

The `attr_accessor` method takes a symbol of the instance variable name as an argument. It then uses this symbol to create "getter" and "setter" methods. This can be very handy. It can help you write shorter code. You no longer need to define two accessor methods, the "setter" and "getter". You just use the `attr_accessor` method.

Let's take the `Car` class and replace the `model` "setter" and "getter" methods with the `attr_accessor` method. As you can see on the example below, the difference can be significant.

```
##
# Before
class Car
  def initialize(model, condition)
    @model = model
    @condition = condition
  end

  # Getter method get_model
  def model
      @model
  end

  # Setter method set_model
  def model=(model)
      @model = model
  end
end

##
# After
class Car
  # Setter and getter methods for "model" are replaced with attr_accessor
  attr_accessor :model

  def initialize(model, condition)
    @model = model
    @condition = condition
  end
end

# Create new instance of Car class
honda = Car.new("Honda", "New")

# Call setter method to change the model
honda.model = "Used"

# Call getter method to get the model
puts honda.model
# Outputs: Used
```

However, the `attr_accessor` method is not the end. Ruby also offers the `attr_reader` and `attr_writer` methods. You can use these methods when you want to automatically create only a "getter" or only a "setter" method.

```
##
# Example of attr_reader
class Car
  attr_reader :model

  def initialize(model, condition)
    @model = model
    @condition = condition
  end
end

# Create new instance of Car class
honda = Car.new("Honda", "New")

# Call getter method to get the model
puts honda.model
# Outputs: Honda

##
# Example of attr_writer
class Car
  attr_writer :model

  def initialize(model, condition)
    @model = model
    @condition = condition
  end
end

# Create new instance of Car class
caravan = Car.new("Honda", "New")

# Call setter method to change the model
caravan.model = "Mercedes"
```

These methods are not limited to only one symbol. Ruby allows you to pass as many symbols to the `attr_accessor`, `attr_reader` and `attr_writer` methods as you want. It works just like parameters and methods. In the case of the `Car` class for example, you can write `attr_accessor :model, :condition`.

### Self

You can also call the accessor methods inside the class by using the `self` keyword. Remember that `self` represents the current object. It is used to call the instance methods and accessors of the object. One of the benefits of using `self` is for disambiguation. For example, if you have a variable and a method both called "model", `self.model` would make it clear that you are referring to the method.

```
##
# Example of using "self"
class Car
  attr_accessor :model, :condition

  def initialize(model, condition)
    @model = model
    @condition = condition
  end

  def update(model, condition)
    self.model = model
    self.condition = condition
  end

  def show_info
    puts "#{self.model} is #{self.condition}."
  end
end

sedan = Car.new("Chevrolet", "New")
sedan.update("Tesla", "New")
sedan.show_info

# Outputs "Tesla is new."
```

In the code above, you defined a method called `update`. This method changes the `@model` and `@condition` instance variables via their accessor methods. The `show_info` method Outputs the values of these instance variables.

### Class variables

Similar to instances, classes too have variables. Similar to methods, these class variables are also accessible to every instance, or object, of the class. When you want to declare a class variable you use two "at" signs (`@@`). For example, `@@age`. Programmers usually use class variables when they need information about the class, not the individual instances.

One use case for using class methods is when you want to keep track of how many instances of that class you have, for example. Le's create new class `Person`. This class will have `@@count` class variable and `initialize` method. Remember, the `initialize` method is called every time new object is created.

This means that you can use this method to update, or increment, the value of `@@count`. You can also define a class method to return the value of the `@@count` class variable. For example, a class method called `get_count`. To see the change, call the `get_count` class method right after defining the `Person` class.

The value you will get will be "0" because there is no instance of this class. Next, create two new instances and call the `get_count` class method again, on the `Person` class and not the instances. Now, the value of the `@@count` variable will be "2" because you previously created two instances of `Person` class.

```
##
# Example of a class variable
class Person
  # Define "@@count" class variable to keep track of the number of class instances
  @@count = 0

  def initialize
    # Increase the value of "@@count" when new instance is created
    @@count +=1
  end

  def self.get_count
    @@count
  end
end

# Call the get_count class method
puts Person.get_count
# Outputs 0 - no instance of Person class exists

# Create two new instances of Person class
person1 = Person.new
person2 = Person.new

# Call the get_count class method
puts Person.get_count
# Outputs 2 - two instances of Person class exist: person1, person2
```

### Class methods

Classes in Ruby also have their own methods. These class methods are methods you can call directly on the class itself. This means that you don't have to create any instances, or objects. This can be useful when you have no real need to create an instance of the class. For example, when you use a class group similar methods and functionality.

One example of this is the Ruby built-in `Math` class. This class includes a `square` method which returns the square of its parameter. There is no need to create new instance of the `Math` class every time you want to call the `square` method, or any other. Instead, you just use class methods and Ruby will take care of the rest. The syntax of class methods is simple. They always being with the `self` keyword.

Let's create a new class `Person`, enough of cars, with class method called `introduction`. This method will Output a short message. After this, you can call the `introduction` method directly from the class, without the need to create any instance.

```
##
# Example of a class method
class Person
  def self.introduction
    puts "I am a person."
  end
end

Person.introduction
# Outputs "I am a person."
```

_Side note: Remember, the `self` keyword used inside instance methods is representing the current instance, or object, of that class. When you define class methods, the `self` is referring to the class itself, and not to the instance of the class._

### Class constants

Lastly, a class in Ruby can also contain constants. Remember that constant variables can't change their value. Also, they must always start with a capital letter. It is common practice to define constants with uppercase names. This can help you make it clear when you work with a constant and when with usual variable.

When you want to access class constants you use the class name, followed by two colon symbols (`::`) and the constant name.

```
##
# Example of a class constant
class Calculator
  PI = 3.14159265358979323846
end

# Accessing the PI constant
puts Calculator::PI
# Outputs 3.14159265358979323846
```

## Epilogue: Getting Started With Ruby the Easy Way Pt8

Congratulations! You've finished the eight part of the Getting started with Ruby series. Today, you've learned a lot new concepts from the world of Ruby and OOP. From now, instance and class variables and methods (and constants) and accessors will no longer be a puzzle for you. You will recognize them when you will see them in code.

This will make it easier for you to read code of other Ruby programmers and understand what it does. What's next? In the next part, you will learn about concepts such as inheritance, super, access modifiers and overload operators. This will help you get closer to becoming a Ruby programmer. Until then, practice what you’ve learned today and have a great day.


[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Part 1]: https://blog.alexdevero.com/getting-started-ruby-pt1/
[Part 2]: https://blog.alexdevero.com/getting-started-ruby-pt2/
[Part 3]: https://blog.alexdevero.com/getting-started-ruby-pt3/
[Part 4]: https://blog.alexdevero.com/getting-started-ruby-pt4/
[Part 5]: https://blog.alexdevero.com/getting-started-ruby-pt5/
[Part 6]: https://blog.alexdevero.com/getting-started-ruby-pt6/
[Part 7]: https://blog.alexdevero.com/getting-started-ruby-pt7/
[Part 9]: https://blog.alexdevero.com/getting-started-ruby-pt9/
[Part 10]: https://blog.alexdevero.com/getting-started-ruby-pt10/
[previous part]: https://blog.alexdevero.com/getting-started-ruby-pt7/#objects
[local variables]: https://blog.alexdevero.com/getting-started-ruby-pt7/#local-scope

<!-- Resources: -->
<!--
- http://ruby-for-beginners.rubymonstas.org/blocks/iterators.html
- https://www.tutorialspoint.com/ruby/ruby_iterators.htm
- https://www.javatpoint.com/ruby-iterators
- http://www.zenruby.info/2016/06/ruby-iterators-enumerators-enumerable.html
- http://ruby-for-beginners.rubymonstas.org/built_in_classes.html
- https://www.eriktrautman.com/posts/ruby-explained-iteration
-->
