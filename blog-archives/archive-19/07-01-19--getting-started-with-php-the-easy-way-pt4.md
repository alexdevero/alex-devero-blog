# Getting Started with PHP the Easy Way Pt4 - OOP Pt2 and Beyond

PHP is one of the most widely used programming languages, with large community of dedicated developers and rich ecosystem of frameworks. If that is not enough, the incredibly popular WordPress platform and CMS is based on it. This makes PHP a very good language to learn. So, give it a try. Learn all you need to become a PHP programmer. This series will help you with that.

<!--
Table of Contents:
## PHP, OOP and classes pt2
### Class Constructor
### Class destructor
### Abstract classes
### The static keyword
### The final keyword
## Working with files
## What to do now
## Going further and deeper
## Epilogue: Getting Started with PHP the Easy Way Pt4
-->

Getting Started with PHP the Easy Way [Part 1] (Variables & Data types).

Getting Started with PHP the Easy Way [Part 2] (Control Flow).

Getting Started with PHP the Easy Way [Part 3] (OOP Pt1).

## PHP, OOP and classes Pt2

In the [previous part], you've learned a lot about OOP in PHP and classes. You learned about class instances the `$this` keyword, inheritance and visibility. However, this is not all. There is still a lot PHP has to offer. So, let's take a look at what you can learn about OOP in PHP.

### Class Constructor

Let's say that you need some code to be executed automatically whenever you instantiate a new object. PHP Constructor method `__construct()` is exactly what you are looking for. When you include this method in one of your classes it will be automatically called whenever you use that `class` to create an instance of a new object, when new object is instantiated.

Thanks to this feature `__construct()` method is often used by PHP developers for initialization of anything the object may need before it can be used. Another feature of this constructor method is that it also supports parameters. So, if some parameters are necessary, you can include them in `__construct()`. This will allow the object to accept values when it is created.

There is one thing you have to remember. You can't write multiple `__construct()` methods, with different numbers of parameters. When you want some object to behave differently, for example based on parameters, you have to handle this logic inside the same `__construct()` method.

Let's take a look at simple example. You will create a new `class` called "Person". This person will contain some public `properties` and the constructor `__construct()` method. The `__construct()` method will accept those `properties` as parameters initialize them and output a simple message. Then, you will use that `class` to instantiate new object called "$jack". As you will see, the message specified `__construct()` method will immediately appear.

```
<?php
  // Basic example of __construct() method
  class someClass {
    public function __construct() {
      // your code that should be initialized before new object is created
    }
  }

  // Person class example
  class Person {
    public $age;
    public $name;

    public function __construct($name, $age) {
      $this->age = $age;
      $this->name = $name;

      echo "New instance of Person class has been created";
    }
  }

  $jack = new Person("Jack", 21);// New instance of Person class has been created
?>
```

### Class destructor

Aside to class constructor, there is also a class destructor. This is a destructor method `__destruct()`. This method is called automatically when an object is destroyed. You can also trigger the destructor method explicitly. To do that you can use `unset()` function. For example, `unset($jack);`. A good use for destructors is performing certain tasks when the object finishes its lifecycle, such as release resources, write log files, close a database connection, etc.

```
<?php
  // Basic example of __destruct() method
  class someClass {
    public function __destruct() {
      // your code that should be initialized before new object is destroyed
    }
  }

  // Person class example
  class Person {
    public function __destruct() {
      echo "Instance of Person class has been destroyed";
    }
  }

  $jack = new Person("Jack", 21);// Instance of Person class has been destroyed

  // Or
  unset($jack);
?>
```

### Abstract classes

Next thing PHP has to offer is something called abstract classes. What is the difference? The difference between "regular" and abstract `class` is that abstract `class` can be inherited, but it can't be instantiated. It can also contain abstract methods. These are methods without any actual code in it. You use only the `abstract` keyword, method name and the parameters.

From this point of view, abstract `class` looks very similar to class interface. The reason you may use abstract class is that you want to create something like a template. Then, other classes can use this "template", or inherit it. This will basically force those classes to implement the abstract methods you declared inside the abstract `class`.

There are two important things related to methods declared inside abstract to remember. First, when a `class` inherits from an abstract `class` it has to implement all its abstract methods. Second, abstract methods can be used only in abstract classes.

```
<?php
  abstract class Dog {
    private $age;

    abstract public function bark();
  }

  class Bulldog extends Dog {
    public function bark() {
      echo "Woof";
    }
  }

  $sammy = new Bulldog();

  $sammy->bark(); // Woof
?>
```

### The static keyword

Next thing, related to PHP classes, are two keywords. The first one is `static`. This keyword defines `properties` and `methods` of a class that can be accessed without creating new object, or instance, of that class. What if you want to access any `static` `property` or `method`? You have to use `::`. This is something called scope resolution operator. You insert it between the class name and the `property` or `method` name.

```
<?php
  class Dog {
    // Create static property $age
    static $age = 5;

    // Create static methodbark()
    static function bark() {
      echo "Woof";
    }
  }

  // Access static property $age
  echo Dog::$age; // 5

  // Access static method bark()
  Dog::bark(); // Woof
?>
```

When you want to access a `static` `property` from a `static` `method` you need to use another keyword, `self`.

```
<?php
  class Person {
    // Create static property $age
    static $age = 42;

    // Create static property tellAge()
    static function tellAge() {
      // Access the static property $age
      echo self::$age;
    }
  }

  // Access static method tellAge()
  Person::tellAge(); // 42
?>
```

### The final keyword

The second keyword is `final`. This keyword defines methods that cannot be overridden in child classes. You can also use this keyword when you declare new classes. These classes, those you declared with the `final` keyword, can't be inherited. Let's take a look at a simple example of both, trying to change `final` `method` and trying to inherit `final` `class`.

```
<?php
  // Create new class Person with method specifyIdentity() marked as final
  class Person {
    final function specifyIdentity() {
      echo "Human";
    }
  }

  // Create a child class of Person called Man
  // and try to override the specifyIdentity() method
  class Man extends Person {
    function specifyIdentity() {
      echo "Man"; // Fatal error: Cannot override final method Person::specifyIdentity()
    }
  }

  // Create new class Person as final
  final class Person {}

  // Try to inherit from final class Person
  class Man extends Person {} // Fatal error: Class Man may not inherit from final class (Person)
?>
```

## Working with files

That was what you need to know about PHP class. The last thing you should know is how to work with files. PHP offers a number of functions you can use to create, read, upload and edit files. When you want to open file you use `fopen()`, using file name as parameter. You will also use this function when you want to create new file. If the file you specified doesn't exist, PHP will create it.

Well, PHP will create the file with the file name you specified if you opened it in writing (`w`) or appending (`a`) mode. This mode is a second argument you pass to `fopen()` function. There are eight modes you can use to open files. These modes are `r`, `w`, `a`, `x`, `r+`, `w+`, `a+` and `x+`. You will find description for each mode in the example code below.

When you want to write to a file use `fwrite()` function. This function has two parameters. The first parameter is the file to write to. The second is the content, some string, you want to write into that file. When you want to close a file, you use `fclose()`. This function also returns `TRUE` when file is successfully closed or `FALSE` when closing failed. It is considered a good practice to close all your opened files after you have finished working with them.

```
<?php
  // r: Opens file only for reading.
  // w: Opens file only for writing. It will erase the contents of the file. If the file doesn't exist it will create it.
  // a: Opens file only for writing. It will append new content to existing.
  // x: Creates new file only for writing.
  // r+: Opens file for reading or writing.
  // w+: Opens file for reading or writing. It will erase the contents of the file. If the file doesn't exist it will create it.
  // a+: Opens file for reading or writing and also creates a new file if the file doesn't exist.
  // x+: Creates new file for reading or writing.

  // Open existing file in writing mode
  // Remember that "w" erase existing content of the file.
  $myFile = fopen("example.txt", "w");

  // Or create a new file in writing mode,
  // using file name of a file that doesn't exist.
  $newFile = fopen("new.txt", "w");

  // Write to the first (existing) file
  fwrite($myFile, "This text will replace any existing content of the file.");

  // Write to the second (new) file using variable
  $txt = "This is a text for the second file";
  fwrite($newFile, $txt);

  // Close the first (existing) file
  fclose($myFile);

  // Close the second (new) file
  fclose($newFile);
?>
```

Pay attention to the mode you are using. Remember that the `w` mode will erase all existing content of the file. If you want to append content to a file, you need to open the file in append mode (`a`).

```
<?php
  // Open existing file in append mode
  $file = fopen($myFile, 'a');

  // Add some content to already existing
  fwrite($file, "Some additional text");

  // Close the file
  fclose($file);
?>
```

You may just want to read from file without opening it. In that case, you can use `file()` function. This function will read the entire file in the form of an `array`. Each element within the `array` corresponds to one line in the file.

```
<?php
  // Read from file and save the content
  // in the form of an array in variable
  $content = file('example.txt');

  // Loop through the $content array
  // and output every line
  foreach ($content as $line) {
    echo $line .", ";
  }
?>
```

## What to do now

You've learned a lot of things about PHP. Yet, that doesn't mean there is nothing more left. Rather the opposite. It doesn't matter how deep you went through this mini series. There is still a lot of options and ways you can take to improve your skills. This is especially true if achieving true mastery of PHP is your goal.

The first thing you can do, and should, is reviewing this whole mini series, and all its parts, again. It is usually not enough to go through learning material just once or twice. Or, even three times, in case you are learning some harder subject. Multiple iterations and repetitions are beneficial. They often lead to better retention of knowledge and gaining a deeper understanding.

So, don't think about doing this in the terms of wasting your time. The more time and effort you invest in training your knowledge and skills the better you can get. This is especially true if you are not sure, or in doubt, about some topics. Remember that any gap in your knowledge will prevent you from achieving a true mastery in any language, and not just PHP.

The only way you can find and fill any potential gaps is through diligent study and practice.  Work on all code examples you've trained on thorough this mini series. Then, create your own. Give yourself challenges. And, always raise the bar and increase the difficulty when you complete the challenge. Remember that progress is not automatic. You have to constantly push yourself.

So, the best thing you can do now is to find a way to practice programming PHP. What if you don't have any opportunities to do so in your current work or project? The solution is simple. Create your own project. Start with something small, especially if you are not confident in your skills. It can be a form or a simple website. Then, when you complete the project, go bigger.

Remember that mastery of any skill or subject is doable only through practice. If you want to truly master PHP there is only one way. You have to write more code in PHP. No excuses or shortcuts.

## Going further and deeper

Re-reading and practice are only two ways you can take to get better in PHP programming. Another good thing you can do is learning a framework. This can be especially useful if you want to use PHP to find new job opportunities. Knowing how to program in pure PHP is one thing. Knowing how to work with some popular PHP framework is another, very attractive to employees and clients.

What are some popular options in the terms of to PHP? Let's take a look at top three. The first one is [Laravel]. This framework has become the most popular open-source PHP framework in the world. The reason? It can handle complex web applications better and faster than other frameworks and doing it securely. It simplifies development process by making common tasks such as routing, sessions, caching and authentication easier.

The second one, popular choice for large-scale enterprise projects, is [Symfony]. This PHP framework has been around since 2005. This long life makes it a reliable, mature and stable platform. Symfony is a very extensive and flexible PHP MVC framework composed of many components. It is also one of the frameworks well-known for following PHP and web standards and best practices.

The third? The last on the list of top three is [CodeIgniter]. The biggest benefit of this PHP framework is that it is incredibly small. Its size is somewhere about 2 MB. And, yes, this also includes the user guide. This makes CodeIgniter a very good choice when you want to develop robust dynamic websites while keeping them lightweight.

Don't let the small size deceive you. Yes, CodeIgniter is small. However, it still offers many pre-built modules ready for you to use. Another benefits are MVC architecture, very good error handling, inbuilt security tools and simple documentation. The downside is that releases are less regular. If you need high-level security CodeIgniter might not be the best choice for you.

Any other frameworks worth mentioning? You can also take a look at [Phalcon], [CakePHP], [Zend Framework], [FuelPHP], [PHPixie] and [Slim]. Each of these, and the top three, PHP frameworks has its benefits. Try them out and find that fits your needs and taste the best. If you are looking for a job or clients, take into account how popular each framework is on marketplace. Don't waste your time learning a framework nobody wants to use.

## Epilogue: Getting Started with PHP the Easy Way Pt4

Congratulations to completing this mini series. Now you know everything you need to start implementing PHP into your projects and work with it on a daily basis. Now, you can follow what we discussed in the "what to do now" part. Or, you can choose the "going further and deeper" and start tinkering with PHP frameworks. Or, you can do something different. Next steps are up to you.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Part 1]: https://blog.alexdevero.com/getting-started-php-pt1/
[Part 2]: https://blog.alexdevero.com/getting-started-php-pt2/
[Part 3]: https://blog.alexdevero.com/getting-started-php-pt3/
[previous part]: https://blog.alexdevero.com/getting-started-php-pt3/
[Laravel]: https://laravel.com
[Symfony]: https://symfony.com
[CodeIgniter]: https://www.codeigniter.com
[Phalcon]: https://phalconphp.com
[CakePHP]: https://cakephp.org
[Zend Framework]: https://framework.zend.com
[FuelPHP]: https://fuelphp.com
[PHPixie]: https://phpixie.com
[Slim]: https://www.slimframework.com
