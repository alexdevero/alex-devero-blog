# Getting started with Ruby – The Easy Way Pt9

So far, you've learned mostly about the basics of Ruby and object-oriented programming. Now, it is time to take your skills further and explore more advanced concepts of OOP. In this part, you will learn about inheritance, method overriding, super and operator overloading. This will bring you closer to becoming a Ruby programmer!

<!--
Table of Contents:
## Ruby and OOP (Object-Oriented Programming) pt3
### Inheritance
### Inheritance and additional methods and attributes
### Method overriding
### Inheritance on multiple levels
### Super
### Operator overloading
## Epilogue: Getting started with Ruby – The Easy Way Pt9
-->

Getting started with Ruby – The Easy Way [Part 1].

Getting started with Ruby – The Easy Way [Part 2].

Getting started with Ruby – The Easy Way [Part 3].

Getting started with Ruby – The Easy Way [Part 4].

Getting started with Ruby – The Easy Way [Part 5].

Getting started with Ruby – The Easy Way [Part 6].

Getting started with Ruby – The Easy Way [Part 7].

Getting started with Ruby – The Easy Way [Part 8].

## Ruby and OOP (Object-Oriented Programming) pt3

### Inheritance

You know how to create [classes] and their [instances]. Next is inheritance. Inheritance is when one class receives, or inherits, attributes and behavior from another. When this happens, the class that is inheriting behavior is called a "subclass", also called "derived" class. The class it inherits from is called the "superclass", also called "base" class.

Imagine you have a number of classes. Each of these classes represents some animal. For example, cat, dog, armadillo, bird, bear and so on. All these animals are less or more different. For example, a dog can bark while cat and armadillo can't. Bird can fly while bear and dog can't. Nonetheless, there are still some attributes and behaviors these animals may share.

For example, they all can be alive. They all have specific color and name. You can implement this similarity creating one "superclass" Animal and let all these animals inherit from it, i.e.: make them "subclasses" of Animal "superclass". This allows you to specify these general attributes and behaviors only once and use them as you need.

When you want to tell Ruby that some class should inherit from another class, or be its "subclass", you use the "less than" symbol (`<`). You do this when you declare the class. This means that you use the `class` keyword, followed by the name of the "subclass" followed by `<` which is then followed by the name of the "superclass".

Let's take a look at how you could write the example with animals in Ruby using inheritance. First, you will define the "superclass" `Animal`. This "superclass" will contain the attributes and functionality you want to share with its "subclasses". Then, you will define class for each animal and let it inherit from `Animal`, become its "subclasses".

```
##
# Create a superclass Animal
class Animal
  def initialize(name, color)
    @name = name
    @color = color
  end

  def printInfo
    puts "This is #{@name}, and its color is #{@color}."
  end
end

# Create a class Armadillo, make it a subclass of Animal
class Armadillo < Animal
end

# Create a class Bear, make it a subclass of Animal
class Bear < Animal
end

# Create a class Bird, make it a subclass of Animal
class Bird < Animal
end

# Create a class Cat, make it a subclass of Animal
class Cat < Animal
end

# Create a class Dog, make it a subclass of Animal
class Dog < Animal
end

# Create instance of Bear class
grizzly = Bear.new("Grizzly", "brown")
grizzly.printInfo
# outputs "This is Grizzly, and its color is brown."

# Create instance of Cat class
akita = Cat.new("Akita", "white")
akita.printInfo
# outputs "This is Akita, and its color is white."
```

### Inheritance and additional methods and attributes

As you can see on the previous example, both `Bear` and `Cat` can use the attributes and methods of the `Animal` class, such as the `printInfo` method. This is true about the rest of "subclasses" as well. However, this doesn't mean that Ruby will now restrict these subclasses to use only attributes and methods of their "superclass".

Every "subclass" can also have its own methods and attributes. For example, you can add one method to the subclass `Cat` that will output "Meow" and another to the subclass `Dog` that will output "Woof". Let's call both these methods simply `speak`. You can do the same with the rest of subclasses if you want, and if you figure out what "noise" armadillo, bear and bird do.

```
##
# Superclass Animal
class Animal
  def initialize(name, color)
    @name = name
    @color = color
  end

  def printInfo
    puts "This is #{@name}, and its color is #{@color}."
  end

  def speak
    puts "Roar!"
  end
end

# Subclass Cat
class Cat < Animal
  attr_accessor :age

  def speak
    puts "Meow."
  end
end

# Create instance of Cat class
akita = Cat.new("Lucy", "white")
akita.age = 1

akita.printInfo
# outputs "This is Lucy, and its color is white."

# Output Lucy's age
puts akita.age
# outputs "1"

akita.speak
# outputs "Meow."

# Subclass Dog
class Dog < Animal
  attr_accessor :age

  def speak
    puts "Woof!"
  end
end

# Create instance of Dog class
husky = Dog.new("Max", "black")
husky.age = 3

husky.printInfo
# outputs "This is Max, and its color is black."

# Output Max's age
puts husky.age
# outputs "3"

husky.speak
# outputs "Woof!"
```

### Method overriding

In the previous example, both `Cat` and `Dog` inherit from Animal. And, they both also have their own instance variable `age` and `speak` method. As you probably noticed, the `Animal` superclass also has its own `speak` method. However, when you call this method on the `akita` and `husky` instances, the output you get is the output specified in `Cat` and `Dog` subclasses.

In Ruby, this is called "method overriding". Put simply, this means that method defined in a "subclass" overrides, or replaces, the original method defined in the "superclass". In our example, `speak` method in `Cat` and `Dog` subclasses overrides the `speak` method in the `Animal` superclass.

So, this is why when you called `speak` method on the `akita` and `husky` you get different output. However, if you try to call this method on instance of `Armadillo`, `Bear` or `Bird`, you will get the output you specified in `Animal` superclass. These subclasses didn't override the method.

```
##
# Superclass Animal
class Animal
  def initialize(name, color)
    @name = name
    @color = color
  end

  def printInfo
    puts "This is #{@name}, and its color is #{@color}."
  end

  def speak
    puts "Roar!"
  end
end

# Class Armadillo
class Armadillo < Animal
end

# Class Bear
class Bear < Animal
  attr_accessor :age
end

# Create instance of Bear class
grizzly = Bear.new("Grizzly", "brown")
grizzly.age = 6

puts grizzly.age
# outputs 6

grizzly.speak
# outputs "Roar!"

# Create instance of Cat class
marley = Armadillo.new("Marley", "gray")

marley.speak
# outputs "Roar!"
```

### Inheritance on multiple levels

Inheritance is a great way to remove duplicates in your code. You can write the shared, or general, functionality and attributes in the "superclass" and then implement additional functionality in specific subclass when you need it. This can help you keep your code simple, clean, succinct and maintainable.

In addition, you can take the concept of inheritance one step further. Ruby allows you to have multiple levels of inheritance. For example, you can create a superclass `Animal`. Then, you can create new classes `Bird`, `Fish`, `Mammal` and `Reptile` as its subclasses. Finally, you can create another classes as subclasses of these subclasses.

```
# Superclass Animal
class Animal
end

# Class Bird, subclass of Animal
class Bird < Animal
end

# Class Fish, subclass of Animal
class Fish < Animal
end

# Class Mammal, subclass of Animal
class Mammal < Animal
end

# Class Reptile, subclass of Animal
class Reptile < Animal
end

# Class Dog, subclass of Mammal
class Dog < Mammal
end

# Class Cat, subclass of Mammal
class Cat < Mammal
end

# Class Snake, subclass of Reptile
class Snake < Reptile
end

# Class Turtle, subclass of Reptile
class Turtle < Reptile
end
```

In the code above, the `Turtle` and `Snake` classes inherits from class `Reptile` which inherits from Animal. This can be also described as an "is a" (or "is an") relationship. Meaning, a `Turtle` is a `Reptile`, which "is an" `Animal`. This is an example of a single inheritance with multiple levels of hierarchy. When it comes to inheritance, there is basically no limit in Ruby to how long this "inheritance chain" can be. So, it is only up to you what you consider to be extreme and what not.

However, there is one thing Ruby will not allow. Ruby doesn't support multiple inheritance. This means that one class can't inherit from multiple classes simultaneously. In other words, class cannot have multiple superclasses. However, there is a way to achieve this in Ruby. It is by using "mixins". You will learn about mixins in the [next part].

### Super

Another thing that can be handy is Ruby built-in method called "super". When you use "super" in a method of the subclass, the method of the same name will get called from the superclass. For example, in the code example with `Animal` superclass you used method overriding to change the `speak` method in its subclasses.

With "super" you can first call the "original" `speak` method from the `Animal` superclass. Then, you can call the "new" `speak` method in from the subclass. To do this, add the `super` into the block of code inside `speak` method, above the new `puts` statement. This is also how you tell Ruby what method you want to call with "super".

You add the "super" into the method with the same name. Ruby will then find the method with this name in the superclass and call it. Back to the `Animal`. Now, if you create a new instance of class `Dog`, and call its `speak` method, you will get both, "Roar!" form the "original" `speak` and "Woof!" from the "new" `speak`.

```
# Superclass Animal
class Animal
  def speak
    puts "Roar!"
  end
end

# Subclass Dog
class Dog < Animal
  def speak
    # Add super to call speak from Animal superclass
    super

    # new puts statement
    puts "Woof!"
  end
end

rex = Dog.new

# Call speak method on rex
rex.speak
# Outputs:
# Roar!
# Woof!
```

Among Ruby developers, "super" is more often used in the `initialize` method. Let's say that you have a superclass. This superclass has a `initialize` method that takes one argument and initializes an instance variable, say, `@name`. Next, you have a subclass. This subclass also needs to have its own instance variable, say, `@age`.

This means that you will need to define new `initialize` method for this subclass. The problem is that the subclass needs both instance variables, `@name` and `@age`. Now, you have two options. First, you can copy the `initialize` method from the superclass and create its duplicate in the subclass, and add `@age` instance variable.

The second option is to use "super". Meaning, instead of repeating the whole `initialize` method, and setting the `@name` instance variable in the subclass, you can use `initialize` from the superclass and add the new `@age` instance variable. Remember that if the "original" `initialize` takes the variable as a parameter, you must also include it when you declare new `initialize` and when you use "super".

```
# Superclass Animal
class Animal
  # Original "initialize" method with instance variable "@name"
  def initialize(name)
    @name = name
  end
end

# Subclass Cat
class Cat  < Animal
  # New "initialize" method with instance variable "@age"
  def initialize(name, age)
    # Using the "name" as parameter for "super" (required by th original initialize method)
    super(name)

    # Additional instance variable for subclass Cat
    @age = age
  end

  def printInfo
    puts "Cat #{@name} is #{@age} years old."
  end
end

cindy = Cat.new("Cindy", 3)
cindy.printInfo
# Outputs: Cat Cindy is 3 years old.
```

### Operator overloading

Imagine a scenario where you would want to add together two instances, or objects, and create new one. Fortunately, Ruby allows you to use something called "operator overloading". As you know, everything in Ruby is an object. This applies also to operators, such as `+`, `-`, `*` and `/`. In a fact, all these operators are methods.

You can define and redefine methods. Since operators are just another bunch of built-in Ruby methods, you can define and redefine them as well. This means that Ruby allows you to do things such as adding two objects together. Let's say you have a class `Shape`. This object has two properties, width and height.

What you want is to combine two `Shape` objects in a way that you will get a new object. This new object will have the width and height equal to the sum of the width and height properties of the two objects you combined. All you need to do to achieve this result is to define the correct operator, the `+` in this case, as a method.

```
# Class Shape
class Shape
  attr_accessor :height, :width

  def initialize(height, width)
    self.height = height
    self.width = width
  end

  # The "+" method that will allow to combine two objects.
  # The "self" is the current, first, object and the "other" is the second.
  def +(other)
    Shape.new(self.height + other.height, self.width + other.width)
  end
end

# Create first two instances of Shape
shapeX = Shape.new(3, 7)
shapeY = Shape.new(12, 11)

# Combine the previous instances of Shape to create new one
shapeZ = shapeX + shapeY

puts shapeZ.height
# Outputs: 15 (3 + 12)

puts shapeZ.width
# Outputs: 18 (7 + 11)
```

## Epilogue: Getting started with Ruby – The Easy Way Pt9

Congratulations! You've just finished another part of Getting started with Ruby series. Today, you've made big progress on your journey to learn Ruby. A large part of object-oriented programming is no longer a mystery for you. You can define new classes and their instances with confidence and achieve what do you need.

By now, you also know what is inheritance and how to use it to create superclasses and subclasses. You also know how to use method overriding and super when you need. Lastly, you also know that weird thing called "operator overloading", as well as how to use it. This means writing more powerful, but also cleaner and maintainable code in Ruby.

In the next part, you will learn about concepts such as access modifiers and to_s method. This will make your journey to the world of Ruby and object-oriented programming complete. Next, you will learn about modules, mixins and other interesting things Ruby has to offer. For now, practice what you've learned today.

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
[previous part]: https://blog.alexdevero.com/getting-started-ruby-pt8
[classes]: https://blog.alexdevero.com/getting-started-ruby-pt7/#classes
[instances]: https://blog.alexdevero.com/getting-started-ruby-pt7/
#objects
<!-- [next part]: https://blog.alexdevero.com/getting-started-ruby-pt10 -->

<!-- Resources: -->
<!--
- http://ruby-for-beginners.rubymonstas.org/blocks/iterators.html
- https://www.tutorialspoint.com/ruby/ruby_iterators.htm
- https://www.javatpoint.com/ruby-iterators
- http://www.zenruby.info/2016/06/ruby-iterators-enumerators-enumerable.html
- http://ruby-for-beginners.rubymonstas.org/built_in_classes.html
- https://www.eriktrautman.com/posts/ruby-explained-iteration
-->
