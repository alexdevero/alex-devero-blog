# Getting Started with PHP the Easy Way Pt3 - OOP Pt1

Do you want to learn PHP? Or, do you want to improve your current knowledge of PHP? This mini series will help you with both! In this part, you will learn about functions, OOP, classes. You will also learn about things such as class instances, inheritance and visibility types. Make the step towards PHP mastery!

<!--
Table of Contents:
## Functions
## PHP, OOP and classes pt1
### PHP & classes
### PHP & class instances
### Classes & $this
### Classes and inheritance
### Classes & visibility
### PHP Interfaces
## Epilogue: Getting Started with PHP the Easy Way Pt3
-->

Getting Started with PHP the Easy Way [Part 1] (Variables & Data types).

Getting Started with PHP the Easy Way [Part 2] (Control Flow).

Getting Started with PHP the Easy Way [Part 4] (OOP Pt2 and Beyond).

## Functions

Control structures such as conditional statements and loops are very useful. They make code less repetitive and more maintainable. These structures will also allow you to write more complex scripts and programs. Now, it is time for the next step on your learning path in PHP. This step is about functions. Or, user-defined because PHP offers a lot of built-in function.

So, what is a function? Put simply, a function is a block of code, or statements. You write this code once and then can use it repeatedly thorough your code, or project. As always, there are a few things you need to know about. First, when you declare, or create, a new function, you need to use the word `function`. This tells PHP that you want to create a function.

Second, you need to use a name for your function, name that will be valid. This is similar to defining a new variable. Valid function name can start with a letter or an underscore. However, it can't start with a number or a special symbol. Function names are not case-sensitive. Function name is followed by parentheses (`()`). Third, you can "allow" the function to accept information.

This can be user input, variables, other functions, etc. You can do this by adding parameters to the function. Parameters are like PHP variables. You specify them right after the function name, within the parentheses. Your function can have as many parameters as you want, or need. There are two things you need to remember. First, parameters must be separated with commas.

Second, parameters must follow the naming rules for variables. In other words, use the dollar sign (`$`) and allowed characters. Fourth, the function name, and parenthesis with or without parameters, is then followed with curly braces (`{}`). What about your code? The code you want the function to execute when it runs goes inside these braces.

The opening curly brace (`{`) indicates that this is the beginning of the function code, block of code that will be executed. The closing curly brace (`}`) indicates the end of function code. This is basically all you need to know to declare new function. However, when you declare function it will not execute itself automatically, when the page loads.

When you want to execute the function, you need to do it "manually" by calling it. This is also called invoking the function. You do this by using the function name followed by parenthesis, and arguments if the function accepts any. One thing. When you want the function to output some text that contains function parameters, use double quotes, as you learned in the [first part].

```
<?php
  // Default function
  function functionName() {
    // Your code that will be executed.
  }

  // A simple example of function without any parameters
  function helloWorld() {
    echo "Hello world! This is my first function in PHP!";
  }

  // Call the function "helloWorld"
  helloWorld(); // Outputs: "Hello world! This is my first function in PHP!"

  // A simple example of function with four parameters
  function sayHi($firstName, $lastName, $age, $nick) {
    echo "Hello. My name is $firstName $lastName and I am $age years old. You can call me $nick.";
  }

  sayHi("Jackie", "Jones", 23, "JJ") // Outputs: "Hello. My name is Jackie Jones and I am 23 years old. You can call me JJ."
?>
```

_Side note: You probably noticed that I referred to "parameters" as "arguments", when you read about how to call the function. These two terms, "parameter" and "argument" are often used interchangeably. A lot of people don't distinguish between them. However, there is a small difference. You use "parameter" when you talk about declaring function._

_When you talk about calling or invoking the function, you use "argument". This is also called "passing". So, when you create function you specify "parameters". When you use the function, and pass some value, you are using, or passing, "argument". One good trick to remember this is by thinking about "arguing" with the function when you call it. When you argue, you need to use arguments._

## PHP, OOP and classes pt1

You will probably work with functions on a daily basis. Well, if your projects includes writing PHP. However, functions are not everything. There is one important concept you need to learn to master PHP. This is OOP, or object-oriented programming. PHP is not the only programming language with OOP features. There are many many [more]. Anyway, what is OOP about?

Object-oriented programming is a programming style. This style intends to change the way you write programs. It intends to make you think about programming as about the real world. In OOP, you work with objects, instead of just data. When you want to create new object you do it with classes. Classes are the fundamental part of OOP.

You can think about `class` as some kind of a blueprint or archetype. It describes what the object will be and what it can do. It contains available properties, methods and so on. However, it is separate from any specific object. A simple example of a `class` can be building. The `class` building defines the features of a generic building, and how it should work.

You can use this building `class` to create a concrete building. For example, The Empire State Building. This concrete building is a specific object. In OOP, this object is called `instance` of the `class`. In this case, The Empire State Building is an `instance` of `class` building. Another example, is a generic dog and specific breed. The dog is a `class` and every breed is its `instance`.

### PHP & classes

Let's take a look at classes. In PHP, a class can contain "member" variables. These variables are called properties. You use these properties to define the features of an object. When you want to define behavior, you use methods. Methods are something you already know, under the name of functions. A function declared inside object is method. Different name, but works in the same way.

Every class has to begin with the keyword `class`. This is then followed by a class name. A valid class name starts with a letter or underscore, followed by any number of letters, numbers, or underscores. Finally, there are curly braces (`{}`) that contains the properties and methods available in that class.

```
<?php
  // Default class
  class className {
    // Class properties and methods
  }

  // Example of a Building class
  class Building {
    public $architect; // Property of the class
    public $height;
    public $location;
    public $name;

    public function getInfo() { // Method of the class
      echo "The architect of this building is $this->architect. Its name is $this->name and its height is $this->height. It is in $this->location.";
    }
  }

  // Example of a Dog class
  class Dog {
    public $age; // Property of the class
    public $height;
    public $numOfLegs = 4; // Property of the class with a value
    public $weight;

    public function bark() { // Method of the class
      echo "Woof!";
    }
  }
?>
```

_Side note: The keyword `public` in front of all properties and the bark method is a visibility specifier. It says that the property or method can be accessed from anywhere in the code. Another visibility specifiers are `protected` and `private`. You will learn about these specifiers later._

### PHP & class instances

When you create new object of a class, or its instance, it is called "instantiation". To instantiate an object of a class, you must use the keyword `new`. When you want to access the properties and methods of the object, or instance, you must use the arrow (`->`) construct. If you want to assign a value to a property use the assignment operator (`=`), as you would with a variable.

Let's demonstrate this on an example with a building. First, you will create new `class` called "Building". This class will have a couple of properties, such as "architect", "height", "location", "name", and one method "getInfo". Next, you will create a new instance of this class called "$EmpireStateBuilding". Remember the [rules] for naming variables.

After that, you will assign specific values to all properties available in Building `class`, and your new "$EmpireStateBuilding" `instance`. lastly, you will call the `getInfo()` method on "$EmpireStateBuilding" to get information about your new instance.

```
<?php
  // Example of a Building class
  class Building {
    public $architect;
    public $height;
    public $location;
    public $name;

    public function getInfo() {
      echo "The architect of this building is $this->architect. Its name is $this->name and its height is $this->height. It is in $this->location.";
    }
  }

  // Creating new instance of building class - instantiation
  $EmpireStateBuilding = new Building();

  // Assign new values to properties of $EmpireStateBuilding object, or instance
  $EmpireStateBuilding -> architect = "Shreve, Lamb and Harmon";
  $EmpireStateBuilding -> height = "443.2 m";
  $EmpireStateBuilding -> location = "New York";
  $EmpireStateBuilding -> name = "Empire State Building";

  // Call getInfo() method
  $EmpireStateBuilding -> getInfo(); // Outputs: The architect of this building is Shreve, Lamb and Harmon. Its name is Empire State Building and its height is 443.2 m. It is in New York.
?>
```

### Classes & $this

You probably notice that you used `$this`, in `getInfo()` method, to access all properties. The `$this` is a pseudo-variable. It is a reference to the object, or class, you are working with. You can "translate" `$this` into "of this object or class". In other words, `$this->height` is like saying "the height property of this object or class".

### Classes and inheritance

PHP classes can inherit properties and methods of another `class`. When one `class` inherits properties or methods of another one it is called a `subclass`. The `class` the `subclass` inherits from is called a `parent class`. When you want one class to inherit properties or methods from another, what you need to do is to use `extends` keyword.

Let's take a look at a simple example to demonstrate how inheritance works. First, you will create `class` "Person". This `class` will contain a number of public properties and one method. Then, you will use `extends` to create two `subclasses` called "Man" and "Woman".

```
<?php
  // Parent class
  class Person {
    public $name;
    public $age;
    public $isHuman = true;

    public function sayHi() {
      echo "Hi, my name is $this->name.";
    }
  }

  // Subclass Man that extends parent class "Person"
  // Inherits $name, $age, $isHuman and sayHi()
  // from parent class "Person" and adds $sex property.
  class Man extends Person {
    public $sex = "man";
  }

  // Subclass Woman that extends parent class "Person"
  // Inherits $name, $age, $isHuman and sayHi()
  // from parent class "Person" and adds $sex property.
  class Woman extends Person {
    public $sex = "woman";
  }

  // New instance of "Man" subclass
  $jack = new Man;

  // Assign new values to available properties
  $jack->name = "Jack";
  $jack->age = "27";

  // Call sayHi() method
  $jack->sayHi(); // Outputs: Hi, my name is Jack.

  // New instance of "Woman" subclass
  $jully = new Woman;

  // Assign new values to available properties
  $jully->name = "Jully";
  $jully->age = "21";

  // Call sayHi() method
  $jully->sayHi(); // Outputs: Hi, my name is Jully.
?>
```

### Classes & visibility

As you already know, PHP includes something called visibility specifier, or visibility type. This specifier controls how and from where specific property and method can be accessed. So far, you've used the `public`. This keyword specifies that the property or method you are working with is accessible from anywhere. Aside to `public`, there are two additional specifiers.

These specifiers are `protected` and `private`. The `protected` specifier makes properties and methods accessible only within the `class` itself, by inheriting and by parent classes. The `private` makes properties and methods accessible only by the class that defines them. Remember that in PHP every class property must have a visibility type.

This is not true for methods. You can declare a method without any explicit visibility type. When you do this, PHP will automatically declare that method as public. Let's use the example above to demonstrate this. You will add new `private` method called "isHuman" to "Person" `parent class`. Then, you will try to call this method from "Man" and "Woman" `subclasses`. Both will cause error.

```
<?php
  class Person {
    public $name;
    public $age;
    public $isHuman = true;

    public function sayHi() {
      echo "Hi, my name is $this->name.";
    }

    private function isHuman() {
      echo "Is $this->name human: $this->isHuman";
    }
  }

  class Man extends Person {
      public $sex = "man";
  }

  class Woman extends Person {
      public $sex = "woman";
  }

  $jack = new Man;

  $jack->isHuman(); // Uncaught Error: Call to protected method Person::isHuman()

  $jully = new Woman;

  $jully->isHuman(); // Uncaught Error: Call to protected method Person::isHuman()
?>
```

### PHP Interfaces

Let's say that you declare a new `class`. You may also want to specify a list of methods this `class` has to implement. This is exactly what `interface` will do for you. Again, you use it to specify a list of methods some `class` has to implement. You can define new `interface` by using `interface` keyword. The syntax of `interface` looks like the syntax of `class`.

How do you implement the `interface`? You create new class and use `implements` keyword, followed by the name of the interface. This is right after class name and before the opening curly bracket. Three things to remember, First, the interface itself doesn't contain implementation of any method. This allows every `class` that uses the interface to handle the method differently.

Let's take a look at one simple example to illustrate how `interface` works. You will create new `interface` called "PersonInterface". This `interface` will contain public method "sayHi". Then, you will create two classes, "Englishman" and "Frenchman". Both will implement the "PersonInterface", but both will handle the `sayHi()` differently.

```
<?php
  // Create new interface
  interface PersonInterface {
    public function sayHi();
  }

  // First class that implements PersonInterface interface
  class Englishman implements PersonInterface {
    public function sayHi() {
      echo "Hello!";
    }
  }

  // Second class that implements PersonInterface interface
  class Frenchman implements PersonInterface {
    public function sayHi() {
      echo "Bonjour!";
    }
  }

  $johny = new Englishman();
  $johny->sayHi(); // Outputs: "Hello!"

  $louis = new Frenchman();
  $louis->sayHi(); // Outputs: "Bonjour!"
?>
```

_Side note: interface name doesn't have to include the "Interface" word. I used it only to keep the code more readable. You can use any name for interface you want, using valid characters. So, the "PersonInterface" can as well be "PersonTraits", "Foo", "fooBar" or whatever you like. Just make sure to use the correct name when you want to implement the interface._

The second thing is that one `interface` can be inherited by another `interface`, just like a `class`. You will achieve this by using the `extends` keyword. So, `interface Foo extends Bar`. The third thing to remember is that `class` can implement more than one `interface`. There is no limit to how many interfaces can `class` implement. When you want a `class` to implement interfaces, separate them with commas.

```
<?php
  // Create first interface
  interface FirstInterface {
    public function foo();
  }

  // Create second interface
  interface SecondInterface {
    public function bar();
  }

  // Create another interface using inheritance
  interface ThirdInterface extends SecondInterface {
    public function bazz();
  }

  // Class implementing first and second interface
  class FooBar implements FirstInterface, SecondInterface {}
?>
```

## Epilogue: Getting Started with PHP the Easy Way Pt3

Congratulations! You've just completed another part of this mini series about PHP. Today, you've learned a lot about how to work with functions and classes. Knowing this will help you write more complex and advanced PHP code and work on more complex projects. This makes your learning path to learn PHP almost complete. There are only a couple more topics you need to know about.

You will learn about all these topics in the next and final part. More specifically, you will learn about things such as abstract classes, `static` and `final` keyword and how to work with files. At the end, you will also learn about some tips to help you improve your PHP skills even further. Until then, practice what you've learned today. And, with that, have a great day!

[xyz-ihs snippet="thank-you-message"]

<!-- Links -->
[Part 1]: https://blog.alexdevero.com/getting-started-php-pt1/
[Part 2]: https://blog.alexdevero.com/getting-started-php-pt2/
[Part 4]: https://blog.alexdevero.com/getting-started-php-pt4/
[first part]: https://blog.alexdevero.com/getting-started-php-pt1/#the-basics
[more]: https://en.wikipedia.org/wiki/List_of_object-oriented_programming_languages
[rules]: https://blog.alexdevero.com/getting-started-php-pt1/#variables
