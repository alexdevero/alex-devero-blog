# From JavaScript to Python – Learning a New Language Pt.3

The road to Python can be easier than you think. Use your knowledge of JavaScript and learn Python much faster. In this final part you will learn how to work with modules and classes. Then, we will take a look at regular expression and how to use it in Python. After that, I will give you three tips you use to learn any programming language in less time.

<!--
Table of Contents:
## From JavaScript to Python: Modules
## From JavaScript to Python: Classes
## Python and Regular Expression
## 3 Tips on learning new programming languages
### Connect everything to the dots you already know
### If you don't understand it, go deeper
### Focus on doing
## Epilogue: From JavaScript to Python Pt.3
-->

From JavaScript to Python [Part 1].

From JavaScript to Python [Part 2].

## From JavaScript to Python: Modules

Another thing you will probably know from JavaScript, that exist in Python and is used quite often, are modules. If not, the concept of modules is very simple. You split you code into smaller chunks, or modules, and save those chunks in separate files. You can think about modules as containers. Using modules is usually better than having all the code in one place.

It helps you organize your project. Also, you don't need everything all the time. With modules, you can pick specific snippet of code and use it where you need and when you need. And, if you don't need it, it will not bloat your project with unused code. Also, there will be times when you will need to use some functionality you currently don't have.

Then, you can use a package manager. Manager created for Python is called [pip]. Have you ever worked with [npm]? We can say that pip is a Python alternative of npm. It does the same thing. It allows you to download public packages created for Python by other programmers and install them on your computer. Then, you can import these packages as modules when you need. It is almost like using npm. Well, almost.

Anyway, there is one thing that is different in Python. In JavaScript, you have to always specify what code do you want to export from module. Otherwise, you will not be able to access the code. When you want some function or variable to be available outside the file, you have to export with `export` statement. Only then you can use `import` statement and it will work.

In Python, this is not necessary. When you save some code in a module it is exported as default. When you want to load code from some module, you can either import everything or you can import just some parts. You can do this using `import` statement, just like in [JavaScript].

```
// JavaScript example:
# example_module.js
export const greetingText = 'Hello world!'

export const greeting = function() {
  return greetingText
}

# Python example:
# example_module.py
greetingText = 'Hello world!'

def greeting():
  print(greetingText)

# import everything from 'example_module.py' module
import example_module

greeting() # 'Hello world!'

print(greetingText) # 'Hello world!'

# import just some parts from 'example_module.py' module
from example_module import greeting

greeting() # 'Hello world!'

print(greetingText) # 'Hello world!'
```

What if you imported one module in another, second, module and then imported this, second, module in a different, third, module? Can you use the code from the first module? The answer is yes. Even though you are working with the third module you can use the code from the first module. Remember that Python automatically exports all code.

This allows you to use code from other modules indirectly. The only condition is that one of the modules in the "module chain" contains import statement for the module you need. If this is true, that code is accessible from the first module with that import. What this means, in short, is that you can also import a module from another module. Let's take a look at a simple example.

```
# This is module_one.py:
greetingText = 'Hello world!'

def greeting():
  print(greetingText)

# This is module_two.py:
# import everything from module_one.py
import module_one

# This is module_three.py:
# import everything from module_two.py
import module_two

module_one.greeting() # 'Hello world!'
print(module_one.greetingText) # 'Hello world!'
```

## From JavaScript to Python: Classes

Another concept that will be familiar to you are `classes`. Unlike JavaScript, Python is object-oriented programming language from the very beginning. It is probably thanks to this why working with classes is very easy in Python. Just like in JavaScript, things such as methods, instances, inheritance and class and instance variables all exist in Python as well.

When you want to create a `class` you need to start with `class` statement. This statement is then followed by the name of the class. The name of the class is followed by colons, like you already saw in case of `if` statement and loops. It is worth mentioning again that indentation matters in Python, a lot. In other words, indent all the code you want to be contained in the class.

In Python, every class has something called documentation string. This is optional. You can access this string any time using `ClassName.__doc__`. What follows next are the statements, data attributes and methods and anything you want the class to contain. When you want to access some content of the class, you do it using dot notation-`ClassName.x`.

Few simple concepts worth mentioning. Let's start with class variables. These are variables you already know from [part 1] and also from JavaScript. The value of these classes is accessible for, or shared with, all instances of this class. Aside to class variables, there are also instance variables. These variables are the same as class variables, but exist in class instances.

Next is a class constructor, `__init__`, or initialization method. This is a special method Python calls every time when you create a new instance of the class. After this constructor, other methods you want to add to the class look like normal functions. The only exception is that the first argument for every method is `self`.

The good news is that Python adds this `self` argument to the list of arguments for you when you call the method. This means that you don't have to remember that there is some `self` when you want to use some method. When you want to create an instance of class, you use the class name of the class you want and the arguments you defined in `__init__` method.

When you want to change any data contained in the class? You again use dot notation to select the specific data you want to change and assign a new value to it.

```
// JavaScript example:
class Person {
  constructor(name, age) {
    this.name = name
    this.age = age
  }

  displayName() {
    console.log('My name is ' + this.name)
  }

  displayAge() {
    console.log('My age is ' + this.age)
  }
}

// Create instance of Person
const Adam = new Person('Adam', 28)

// Access methods in Adam, instance of Person class
Adam.displayName() // "My name is Adam"
Adam.displayAge() // "My age is 28"

# Change Adam's age
Adam.age = 20

Adam.displayAge() // "My age is 20"


# Python example:
class Person:
  # Documentation string.
  "Base class for all people"

  # Class variable - shared with all instances of this class.
  # If you want to access this variable and its value you use "Person.isAlive"
  isAlive = True

  # This is a class constructor or initialization method.
  def __init__(self, name, age):
    self.name = name
    self.age = age

  def displayName(self):
    print('My name is ', self.name)

  def displayAge(self):
    print('My age is ', self.age)

# Create instance of Person
Sofia = Person('Sofia', 21)

# Access methods in Sofia, instance of Person class
Sofia.displayName() # "My name is Sofia"
Sofia.displayAge() # "My age is 21"

# Change Sofia's age - assign new value to "age" attribute
Sofia.age = 25

Sofia.displayAge() # "My age is 25"
```

## Python and Regular Expression

One more subject some people consider to be tricky is regular expression, or regexp. We already explored this subject of working with regular expression on this blog. So, if you are not familiar with this topic, take a look at this two-part mini series-[first part] and [second part]. How regular expression works in Python?

In order to use regular expression you will need to import `re` module. Then, you can use the syntax of regular expression to achieve what do you need. Let's take a look at couple of examples using some basic methods such as `match`, `search` and `sub` (search and replace). You can find list of all available flags and special characters in [documentation] for `re` module. Or, you can use this [cheat sheet] (with downloadable PDF).

The `match` method checks for a match only at the beginning of the string. This is something very important. If you want to use `match`, it should be because you want to test if the string starts with specific character or word. When match is found, it will return `match` object. Otherwise, it will return `None`.

Next is `search`. This method is similar to `match`. The difference between `match` and `search` is that `match` checks for a match only at the beginning of the string. The `search` method will search through the whole string and return `match` object for a match anywhere in the string. No, that is not a typo. Both, `match` and `search` return `match` object.

Are you curious and want to know more about regular expression and how to use it in Python? Take a look at this comprehensive tutorial on [guru99]. For regexp and how to use it in JavaScript, take a look at Introduction to regular expression [pt1] and [pt2].

```
// JavaScript example:
const testText = 'Text for testing regular expression. You should know that regular expression is also called regexp.'


// match()
// Match existing word regular.
const testOne = testText.match(/regular/)

// Match non-existing word regular.
const testThree = testText.match(/Yeti/)

console.log(testOne) // ['regular']
console.log(testThree) // null


// search()
// Search for existing word 'Text' that is on the beginning of testText.
const testThree = testText.search(/Text/)

// Search for existing word 'should' that is not on the beginning of testText.
const testFour = testText.search(/should/)

console.log(testThree) // 17
console.log(testFour) // -1


// replace()
// Find word 'Text' and replace it with 'Content'.
const testFive = testText.replace(/Text/, 'Content')

console.log(testFive) // Content for testing regular expression. You should know that regular expression is also called regexp.


# Python example:
testText = 'Text for testing regular expression. You should know that regular expression is also called regexp.'


# match()
# Match existing word 'Text' that is on the beginning of testText.
testOne = re.match('Text', testText)

# Match existing word 'should' that is not on the beginning of testText.
testTwo = re.match('should', testText)

print(testOne) # re.Match object; span=(0, 4), match='Text'
print(testTwo) # None


# search()
# Search for existing word 'Text' that is on the beginning of testText.
testThree = re.search('Text', testText)

# Search for existing word 'should' that is not on the beginning of testText.
testFour = re.search('should', testText)

print(testThree) # <re.Match object; span=(0, 4), match='Text'>
print(testFour) # <re.Match object; span=(41, 47), match='should'>


# sub()
# Find word 'Text' and replace it with 'Content'.
testFive = re.sup('Text', 'Content', testText)

print(testFive) # Content for testing regular expression. You should know that regular expression is also called regexp.
```

## 3 Tips on learning new programming languages

Let's end this part, and the whole mini series, on a lighter note. What follows are some universal tips to help you learn not only Python, but any other language you want to learn.

### Connect everything to the dots you already know

Knowing another language is a big benefit when you want to learn another one. You can accelerate your learning by connecting concepts the new language to your first language. This is exactly why we used code example from both languages, Python and JavaScript, instead of just one. Our goal was to illustrate how those concepts look like in different syntax.

In many cases, you already know the semantics, or principles. Thanks to this, it is often not necessary to go over the theory again. You just need to know what is different and remember that. This will help you learn new programming in much less time than usually. It is similar to working with git. When you compare two files you don't need to know the whole code, only what changed.

### If you don't understand it, go deeper

When you decide to learn new programming language, never skip the parts you don't fully understand. This almost always causes a lot of troubles in the future. So, if you have troubles with understanding something, don't move on. Instead, do the opposite and go deeper. Read more theory, try more tutorials and ask more questions. Stick to that topic until you understand it on 100%.

Think about this process of learning as building a building. Whatever you skip now will only lead to cracks in the structure of that building. Then, something can happen and one of those cracks will cause the whole building to collapse. The only way to avoid this is by gaining complete understanding. Remember, if you don't understand something, go deeper.

### Focus on doing

There is nothing bad on learning the theory by reading articles and books. However, this approach is far from the most effective. What you should do instead is to focus on doing. This is the best way to learn anything. Think about it. How did you learn to walk, swim or ride a bike, or other many skills? You learned them by doing, trying and failing and trying again.

Use the same approach when you want to learn new language. Pick a language you want to learn, such as Python, and then search for the easiest tutorial you can try. It is okay if you don't understand something, or even if you don't understand anything at all. Your goal is not finding a tutorial you understand. Your goal is to play with the code and observe what happens.

You can often learn more and faster by using observation along with your common sense. And, if you still can't figure out what is happening? You can search on the web, reach out to someone on social media or forum, grab a book or anything else. Remember, this is not about learning only by doing, but about focusing on doing. If you are not making progress, use any resources available.

Focusing on doing is my favorite way to learn just anything. There are people saying that the best thing to start learning is by starting slowly, taking small steps and starting with theory. You don't want to overwhelm yourself. Focusing on doing is a much better approach. You just jump right into the language or topic you want to learn.

Let's use swimming or ride a bike as an example again. You can start slowly and take small steps. This can mean setting aside few minutes and read some basic theory about how to swim or ride a bike. The next day, you repeat the process, maybe add a bit of practice. And then again and again. Will you learn how to swim or ride a bike? Very likely. The problem is that it will take a lot of time. Now, consider focusing on doing.

You spend a few minutes learning about the basic theory. You find some quick info about what to do. Then, you buy a bike, or find pool deep enough to swim but not too deep so you will drown. Then, you take action. You get on the bike, or into the pool, and start trying and failing and trying again. Very soon, you will see you are making progress.

Which method will help you learn the desired skill faster? Focusing on doing is a very good candidate for a winner. True. This method often includes certain level of discomfort and even pain. However, this may not be the downside. Instead, we can use it as a motivation to focus more and learn faster. How fast will you learn to ride a bike to avoid falling on your face?

Fortunately, when it comes to programming the discomfort is usually much smaller. And, the only pain you have to endure is being "slapped" by errors, or blank screen if the code doesn't run at all. This is a risk worth taking. So, when you want to learn something, forget about learning tons of theory. Instead, jump right into it, focus on doing and learn on the go.

## Epilogue: From JavaScript to Python Pt.3

Congratulations! You've just finished this mini series. By now, you should have some understanding of the basic concepts of Python. There is still a lot you have to learn to become proficient in this language. However, thanks to your knowledge of JavaScript, getting deeper into the details and intricacies of Python and will be easier and more comfortable.

Where to go from here? I suggest working on tutorials. Next, you can follow online courses and schools that offer playgrounds and working with code. Some good choices are [CodeCademy] (offers free and paid courses), [SoloLearn] (offers free courses) and [Learn Python] (offers free courses). For online playground you can try [Python Fiddle]. Remember, focus on doing.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Part 1]: https://blog.alexdevero.com/javascript-python-pt1/
[Part 2]: https://blog.alexdevero.com/javascript-python-pt2/
[pip]: https://pip.pypa.io/en/stable/
[npm]: https://www.npmjs.com
[JavaScript]: https://eloquentjavascript.net/10_modules.html
[part 1]: https://blog.alexdevero.com/javascript-python-pt1/
[first part]: https://blog.alexdevero.com/regex-introduction-regular-expression-pt2/
[second part]: https://blog.alexdevero.com/regex-introduction-regular-expression-pt1/
[documentation]: https://docs.python.org/2/library/re.html
[cheat sheet]: https://www.dataquest.io/blog/regex-cheatsheet/
[guru99]: https://www.guru99.com/python-regular-expressions-complete-tutorial.html
[pt1]: https://blog.alexdevero.com/regex-introduction-regular-expression-pt2
[pt2]: https://blog.alexdevero.com/regex-introduction-regular-expression-pt1
[CodeCademy]: https://www.codecademy.com/catalog/language/python
[SoloLearn]: https://www.sololearn.com/Course/Python/
[Learn Python]: https://www.learnpython.org
[Python Fiddle]: http://pythonfiddle.com

<!--
#### Meta:
-
-->

<!--
#### Inspiration:
- https://dev.to/underdogio/python-for-javascript-developers
- https://docs.python.org/3/library/index.html
- https://www.tutorialspoint.com/python/python_classes_objects.htm
- https://developer.rhino3d.com/guides/rhinopython/primer-101/7-classes/
- https://developer.rhino3d.com/guides/rhinopython/python-datatypes/
- https://eloquentjavascript.net/10_modules.html
-->
