# Getting started with Ruby – The Easy Way Pt7

Have you ever heard about scope, recursion or OOP? If not, don't worry. You will learn about these topics in this part of Getting started with Ruby series. Today, you will learn about what recursion is and how to use it. Next, you will learn about scope and its types. Lastly, you will learn about classes and objects. Without further ado, let's begin!

<!--
Table of Contents:
## Recursion
## Variable scope
### Local scope
### Global scope
### Class scope
### Instance scope
### Why different scopes?
## Ruby and OOP Pt1
### Classes
### Objects
## Epilogue: Getting started with Ruby – The Easy Way Pt7
-->

Getting started with Ruby – The Easy Way [Part 1].

Getting started with Ruby – The Easy Way [Part 2].

Getting started with Ruby – The Easy Way [Part 3].

Getting started with Ruby – The Easy Way [Part 4].

Getting started with Ruby – The Easy Way [Part 5].

Getting started with Ruby – The Easy Way [Part 6].

## Recursion

You know how to use loops. However, loops are not the only way to loop over some object. Remember, in Ruby, everything is an object. Another way to do that is with recursion. Recursions is basically about methods that call themselves. This approach is often used by programmers to solve problems that can be broken into easier sub-problems of the same type.

One simple and often used example of recursion is the factorial method.
This goal of this method is to find the product of all positive integers below a specified number. For example, let's say you want to find factorial of 5 (`5!`). Then, the math equation is `5 * 4 * 3 * 2 * 1` which is equal to 120. How can you solve this with recursion?

Take a look at the equation. Notice that `5!` is the same as `5 * 4!`. The `4!` is the same as `4 * 3!`. The `3!` is the same as `3 * 2!` and so on. This gives us a simple equation `n! = n * (n-1)!`.
Furthermore, `1! = 1`. This is also known as the base case. Meaning, it can be calculated without performing any more factorials.

Let's now create a `factorial` method and implement what we discussed above. The `factorial` method will contain `if` block that will check if `n` is smaller or equal to 1 (`n<=1`). This is the base case. If this condition is `true` the it will stop `factorial` method. Otherwise, it will run `factorial` method again with `n` decreased by 1 and multiple `n` by the result. This will repeat as long as the base case is `false`.

```
##
# Example of recursion
def factorial(n)
  if n <= 1
    1
  else
    n * factorial(n - 1)
  end
end

puts factorial(5)
# outputs 120
```

As with any loops, recursive methods too can become infinite. These situations will happen when you forget to implement the base case. So, make sure to check your code before you execute it. And, any time you work with recursion, define and include the base case that makes the recursion stop. Below is example of the factorial method done wrong-it has no base case.

```
##
# Example of recursion done wrong
def factorial(n)
  n * fact(n - 1)
end

puts factorial(5)
# outputs "stack level too deep (SystemStackError)"
```

## Variable scope

Scope defines where in a program a variable is accessible. In Ruby, there are types of variable scope. These are local, global, instance and class. Each type is handy in different situations, as you will learn in a moment. Don't worry about what classes and instances are. Also, don't worry that you may not understand all code in examples. You will learn about classes and instances soon.

### Local scope

When you declare variable in a local Local this variable will be available to the block of code in which it is declared. For example, let's say that you declared a local variable inside a loop or a method. You can access and use this variable only inside this loop, or method. Remember that variable will not accessible anywhere in your program outside the loop or the method.

What if you try to use local variable outside the scope you declared it, such as the loop, or method? Ruby will throw an error "undefined local variable or method" or something similar. This makes sense. In Ruby and other programming languages supporting local scope, local variable exists only inside the local scope. It doesn't exist for the rest of the code.

Imagine you have two locked rooms. You are in the first and someone else is in the second. These rooms are different local scopes. You can use only the stuff inside the first room because you are the same local scope, or location. The same applies for the person in another room. She can use only stuff present in her room, but not yours.

How can you tell Ruby that you want to declare local variable? The name of the variable must begin with one of two things, either an underscore (`_`) or a lowercase letter. That's all Ruby needs from you. Let's take a look at an example. Declare a `randomMethod` method that will accept one parameter `x`, multiply its value by the value of local variable `y` and output the result.

```
##
# Example of local scope and method
# Define a method "randomMethod" with local variable "y"
def randomMethod(x)
  # local variable "y"
  y = 2

  puts x * y
end

randomMethod(15)
# Outputs: 30

# Try to output the value of "y" outside the scope of the "randomMethod"
puts y
# Outputs: undefined local variable or method 'y'
```

In the code in the example above `x` and `y` are both local variables. They are both accessible only inside the randomMethod method. They don't exist outside it. When we tried to access the value of `y` variable we got an error. The same applies to loops and iterators. In the example below `i` is a local variable available only in the iterator block.

```
##
# Example of local scope and iterator
exampleArr = [1, 2, 3, 4, 5]

exampleArr.each { |i| puts i }
```

### Global scope

In case of global variables, it doesn't matter where they are declared. Any variable you declare in global scope will make that variable accessible anywhere in your Ruby code. When you want to define global variable in Ruby, you have to prefix its name with a dollar sign (`$`).

```
##
# Example of a global variable
$x = 13

# Example of a global variable declared inside method
def randomMethod
  $x = 8
end

puts $x
# Outputs: 13

# Execute "randomMethod" and change the value of global variable "$x"
randomMethod

puts $x
# Outputs: 8
```

As can see on the example above, the `$x` global variable is accessible in the whole program. Meaning, the `$x` at the top and the `$x` inside `randomMethod` are one and the same. This is why when you tell Ruby to execute the `randomMethod` the value of `$x` will change, from "13" to "8". This is also why use of global variables is strongly discouraged.

Global variables are visible anywhere in your Ruby code. However, they can also be changed from anywhere in your code. This can result in colliding variables one overwriting another. If you work with complex code, debugging these issues will be a nightmare. There are only two solutions for this problem.

First, you can declare variables in global scope as you want. However, you have to remember to always use unique variable name in order to avoid conflicts. Second, declare your variables as local, class or instance. Reserve global variables only for special cases, cases when you really need to have that value accessible anywhere.

### Class scope

Variable declared in class scope is accessible in all instances of that class. This also means that you can have only one variable value with that specific variable name in all objects instantiated from that class. Otherwise, you are risking that you will run into the same problems as with global variables.

Imagine you have multiple instances of a specific class. This class also contains some class variables. Somewhere in the program, one of these instances will change the value of one of these class variables. Then, this new value will change the value of this variable in all other instances of that class.

One way to think about class variables is to think about them as global variables, but within the context of a single class. When you want to declare class variables in Ruby you have to prefixing the variable name with two "at" signs (`@@`). One more thing. Class variables must be initialized at creation time.

```
##
# Example of a class variable
class Person
  def initialize(name)
    # Declare class variable
    @@class_variable = name
  end

  def introduceYourself
    # Output a simple message, including the value of the class variable
    puts "Hi, I am #{@@class_variable}."
  end
end

# Create instance of Person class
joe = Person.new("Timothy")

# Execute the "introduceYourself" method on "joe" instance
joe.introduceYourself
# Outputs: Hi, I am Timothy.
```

### Instance scope

Instance variables are similar to class variables. The difference between them is that their values are "local" to a specific instance. For example, let's say that one class contains an instance variable called `@name`. Then, if one instance of this class changes the current value of `@name` the change will manifest only inside that one instance.

Any other instance of the same class will keep their own local copies of the `@name` variable with the original value. In other words, these variables are independent and no changes made in any other instance have any influence on them. From this point of view, instance variables are similar to local variables.

The difference between these two is that instance variables exist within a specific instance of a class, or object. Local variables exist within a specific scope. You have access to instance variables as long as you are in that instance. In the case of local variables, as long as you are in that scope.

When you want to declare instance variables in Ruby you have to pref the variable name with a single "at" sign (`@`). In the example below, the `@gender` variable inside `initialize` method of `Male` class is the instance variable. It is accessible only in this, `Male`, class.

```
##
# Example of a instance variable
class Person
    def initialize(name)
        @@class_variable = name
    end

    def introduceYourself
        puts "Hi, I am #{@@class_variable}."
    end
end

# Create Male class that inherits from Person class
class Male < Person
    def initialize(name)
        super(name)
        #
        # DECLARE INSTANCE VARIABLE HERE
        @gender = "male"
    end

    def introduceYourself
        puts "Hi, I am #{@@class_variable} and I am a #{@gender}."
    end
end

jack = Male.new('Jack')
jack.introduceYourself
# Outputs: Hi, I am Jack and I am a male.
```

### Why different scopes?

You might be asking some questions. For example, why there are multiple scope in Ruby? You could have all variables accessible everywhere. One problem is the naming issues we discussed. If you work with a big codebase, you'd have to give all of your variables unique names to avoid conflicts. Imagine remembering of hundreds of variable names.

The second issue is about access. Imagine keeping track of what piece of code changed what when literally every piece of your code can do so. Then, imagine trying to debug anything. Mission impossible and a lot of headaches. This is why there are different scopes in Ruby. Scopes makes your code more predictable, maintainable easier to debug and secure.

## Ruby and OOP (Object-Oriented Programming) Pt1

Ruby is a pure object-oriented language. This means that everything in Ruby is an object. It doesn't matter if you work with something as simple as numbers, strings and booleans or something complex as classes. In the world of Ruby, all these things are objects. This brings a question. What are objects?

In programming, objects are independent things, if you want. Each of these things has its own identity. You can think about these things as just as the objects in the real world, the world around you. For example, a cat is one object. A cup is another one. Both these objects are different. They both have their own unique identity.

You can have multiple cats, or cups, and they may even look the same. However, that doesn't change the fact that they are still different unique objects. When you want to create an object in Ruby, you use concept called `classes`. A class defines the data and actions associated with an object, but it keeps them separate from the object itself.

One way to think about a class is to imagine a blueprint of some object. It is the definition of that object, if you want. Let's go back to the cat example. You can have many cat objects of the single class Cat. In the real world, you can use a blueprint to build multiple buildings. In the world of programming, you can use the same class as a blueprint to create multiple objects.

### Classes

As you now know, a class is something as a blueprint. It is a basic outlines of what an object should be made of as well as what it should be able to do. Let's take a car for example. Object of class Car should have a color. It should be able to make and specific model. And, should also be able to move. You can also add a horn if you want.

When you want to create a class in Ruby, you must always start with the `class` keyword. This keyword is then followed by the name of the class. The name of the class should always start with capital letter. And, just like with loops and methods, you must close, or terminate, every class with the `end` keyword. Let's create a simple class "Person".

```
##
# Example of a class
class Person
  // content of the class
end
```

A class can contain variables and methods. These are also called "data members" of the class. It is these data members what describes the attributes of the objects. Let's go back to the car. A car have four doors, roadster and electric. All these, and any other, attributes are the data members of the class Car.

In Ruby, there is a special method available for all classes. This method is called `initialize` and it is called when the object is created. This `initialize` method is defined inside a class, just like any other additional class method. If you already know other object-oriented programming language, you may hear about the `initialize` method as a "constructor".

The purpose of the `initialize` method is to initialize, or create, the class variables for a new object. Think about these variables as defaults of the class. For example, when you create a new Car object, the `initialize` method can set the number of wheels to "4" and the type of the car to "electric".

```
##
# Example of a class and initialize method
class Car
  def initialize
    number_of_wheels = 4
    type = "electric"

    puts "This car has #{number_of_wheels} wheels and it is #{type}."
  end
end
```

### Objects

Creating a class is only the first step. When the class and the initialize methods are defined, you can start creating objects of that class. You do this by using the `new` method. Don't worry. This method comes with Ruby. So, you don't have to add it manually every time you create a new class. Ruby will handle this for you.

The syntax for using `new` method is simple. You use the class name followed by a dot and followed by the method name, the `new`. Let's take the class Car from the example above and use it to create two new objects. Notice that the code below will output "This car has 4 and it is electric." twice. This is because you created two objects of the class and each called the `initialize` method, containing a `put` statement.

```
##
# Example of a class Car
class Car
  def initialize
    number_of_wheels = 4
    type = "electric"

    puts "This car has #{number_of_wheels} and it is #{type}."
  end
end

# Create two new objects from Car class
ford = Car.new
tesla = Car.new

# Output:
# This car has 4 and it is electric.
# This car has 4 and it is electric.
```

In Ruby, and other object-oriented programming languages, objects are also called "instances" of a class. The process of creating an object of a class is called "instantiation". So, when you hear object of a class and "instances" of a class, or instantiation and creating an object of a class, remember that it is about the same thing.

## Epilogue: Getting started with Ruby – The Easy Way Pt7

This is where we will end it today. You've learned a lot. In a recap, you've learned how to create loops with recursion. Then, you've learned about different types of variable scope, their differences and why some types are better then others. Lastly, you've learned the basics about classes and objects, or instances.

You will learn about the rest in the next part. For now, revisit what you've learned today. Make sure you understand everything and invest some time in practice. Remember that the only way to really learn any programming is by writing code. So, go and write some code in Ruby! With that, thank you for your time and see you here again the next week.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Part 1]: https://blog.alexdevero.com/getting-started-ruby-pt1
[Part 2]: https://blog.alexdevero.com/getting-started-ruby-pt2
[Part 3]: https://blog.alexdevero.com/getting-started-ruby-pt3
[Part 4]: https://blog.alexdevero.com/getting-started-ruby-pt4
[Part 5]: https://blog.alexdevero.com/getting-started-ruby-pt5
[Part 6]: https://blog.alexdevero.com/getting-started-ruby-pt6

<!-- Resources: -->
<!--
- http://ruby-for-beginners.rubymonstas.org/blocks/iterators.html
- https://www.tutorialspoint.com/ruby/ruby_iterators.htm
- https://www.javatpoint.com/ruby-iterators
- http://www.zenruby.info/2016/06/ruby-iterators-enumerators-enumerable.html
- http://ruby-for-beginners.rubymonstas.org/built_in_classes.html
- https://www.eriktrautman.com/posts/ruby-explained-iteration
-->
