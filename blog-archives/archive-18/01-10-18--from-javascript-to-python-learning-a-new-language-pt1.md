# From JavaScript to Python – Learning a New Language Pt.1

Have you ever wanted to learn new programming language? What about Python? This is a language that is easy to learn and universal. You can use it almost everywhere. It is also very popular language in machine learning. Will you give it a chance? Great! This mini series will help you learn all you need!

<!--
Table of Contents:
## A few questions
### Learning multiple languages at once?
### Should I learn another programming language?
### Why Python?
## From JavaScript to Python: Comments, variables, functions, loops
### Comments
### Variables
### Functions ... or blocks
### If/else
### While
### For
## Epilogue: From JavaScript to Python Pt.1
-->

## A few questions

Let's start by answering the question you may be asking right now. Why should I learn Python? Well, you might be asking a couple of questions. For example, should I learn another programming language? There is one specific thing you should consider before you attempt to learn a new programming language. Let's assume that you already know at least one programming language, a JavaScript for example.

### Learning multiple languages at once?

How proficient are you in you in the programming language you already know? Think about a simple scale from one to five. One is a complete beginner, three is advanced and five is master. How would you evaluate your skills on this scale? If you think are somewhere between one and three, it might not be the right time to learn a new language.

When you are a beginner to programming trying to learn a programming language, it is better to stick to that language until you reach advanced level. In this case, you could easily get into a situation where knowledge from your first language will start to mix with material from the second language you are trying to learn. The result is often confusion, slower learning rate and problem to use any of the languages you are trying to learn.

I know this because I tried it. It cost me a lot of time. Don't do the same mistake. An exception is when you surpass this level in at least one language. If you are already proficient in at least one programming language your current knowledge is more resilient. Meaning, it will not mix together with new material. What's more, your current knowledge can even help you learn new language.

If this is true, then, yes, go ahead and try to learn two or even more programming languages simultaneously. Otherwise, work on your first language and add Python on your to do list. Just remember that you are not wasting your time by focusing on your first language. As I mentioned, a solid knowledge of one language will help you learn another one. So, have patience.

### Should I learn another programming language?

I think that learning another language is a good thing. When you know only one programming language you are limited by the constraints of that language. Every programming language has specific benefits, best practices, paradigms and quirks. When you know only one language you are thinking in a specific way, a way that is unique to that language.

This is not bad because it helps you use that programming language better and solve problems more efficiently. However, it still limits your creativity. Who says that this or that way is the best way to solve this particular problem? When you know more than one programming language, you can look at the problem from different perspective. This, in turn, can help you find a better solution.

When you think about it from this perspective, learning another language can help you explore new possibilities. It can introduce you to a whole new world and show you how much there is still to discover. It is like when [Alice] decided to take the risk and enter the rabbit hole. You can do the same. Enter the rabbit hole and learn a new programming language, such as Python.

And, if you are afraid that multiple programming will create a mess in your head, don't be. Programming languages are just like spoken languages. When you learn one language really well, you can add another and then smoothly switch between them without experiencing any problems. The key is to learn the first programming language very well before you attempt to learn second.

### Why Python?

Now, let's answer the original question. Why should you learn specifically Python? There are at least four reasons for choosing Python as one of the programming languages to learn. First, it is beginner-friendly. Python is very easy to learn even for people with no prior experience in programming. This is why Python is often recommended as the first language to learn.

So, if you already know one programming language, or even more, learning Python should be very easy for you. The second reason is that Python is one of these languages able to sustain growth and popularity over many years. Python appeared in 1990. Not only it is not dying, rather the opposite. According to [Tiobe index] it is regularly one of the most popular programming languages.

In other words, Python is nothing new under the sun. It is a language with a very long history and a large amount programmers loves it and uses it. It is safe to say that you don't have to worry it will suddenly disappear any time soon. The third reason is that it is a good language for web development. Python is often a preferred choice for back-end programming.

This is thanks to its simplicity, popularity, scalability, amount of resources that are available and number of good frameworks such as django. Finally, the fourth reason. Python is one of the most popular languages for [machine learning] and data science. This makes it even better choice if you are curious about any of these topics. It is also another reason why Python is here to stay.

Learning new programming language always takes some time, even if it is very easy one. And, as we discussed, it is better to use that time deliberately and focus solely on that one language, instead of trying to tackle more at once. So, take your time, think about these four reasons and decide for yourself. If you are willing to enter this rabbit hole, let's get our hands on Python.

## From JavaScript to Python: Comments, variables, functions, loops

I will assuming you already know at least one programming language, JavaScript. With that, let's make the start easier by discussing the basics of Python while comparing it to JavaScript. Before we start, make sure you have Python installed on your computer. If not, head on [Python website] and download the version you want and that is right for your environment. When you are done with that, and installing it, we can continue.

### Comments

Let's start with something very simple and quite useful, especially if you want to write [clean code]. How can we write comments in Python? In JavaScript, we have two options. We can use a single-line comment `//` or multi-line comment `/**/`. In Python, there is just one choice. When we want to write a comment, or comment out some code, the comment has to start with hash (`#`).

```
// This is a single-line comment in JavaScript.

/*
  This is a multi-line
  comment in JavaScript.
*/

# This is a ... comment in Python.
```

_Side note: There are people saying that Python actually has multi-line comments. They are wrong. What they are talking about is using `"""`. Unfortunately, there is really no such a thing as multi-line comment in Python. This is only a small "workaround" using multi-line strings as comments. This workaround takes the advantage of garbage collection._

_Those triple quotes are treated as regular strings. The exception is that they can span multiple lines. And, since these strings are not assigned to a variable they will be immediately garbage collected when the code executes. Put simply, they will be removed. However, they are not ignored by the interpreter in the same way real comments (`#`) are._

```
"""
This is NOT a real
multi-line comment
in Python.
"""

def mythBuster():
  """
  And neither is this
  a real multi-line comment
  in Python.
  """

# This is the only real comment.
```

### Variables

The second easiest thing are variables. In JavaScript, we can work with three "types" of variables. Or, we can declare variables in three ways. These are `var`, `let` and `const`. The difference is in scope and mutability. In Python, this is easier. There is only one way or "type" to declare a variable. This also means two things. First, in Python you can change any variable you declared.

The second thing is that there is just one scope and that is block. Every variable you declare exists inside the block where you declare it. It is, therefore, accessible only inside that block. If you try to access some variable declared inside a function for example from the outside, the result will be an error.

```
// JavaScript example:
var x = 'String'
let y = 'This will be only temporary.'
const z = 'Try to change me.'

# Python example:
x = 'String'
y = 'This will be only temporary.'
z = 'Try to change me.'

# change x variable
x = 15

# block scope example
x = 15

def hi():
  a = 'I exist only inside this function.'
  b = 'Try it by yourself'
  print(a)

print(x) # 15
hi() # # I exist only inside this function
print(b) # NameError: name 'b' is not defined
```

### Functions ... or blocks

Next on the line are functions. Well, they are actually called blocks in Python. This can make it easier for some people to understand what "block scoped" variable means, since "function" is "block". Unlike in JavaScript, there is no such a thing as curly brackets in Python. So, how can we create a block with anything inside so it is interpreted as the content of that block?

The answer is by using space, or rather indentation to more specific. When we create a block with some code we have to use `def` keyword and indent the code inside. This also means one thing. When you write code in Python, you have to be careful about how you indent it. One extra space here or there will result in errors or the code will not even execute. So, watch the space at the beginning of lines.

```
// JavaScript example 1:
function printThis() {
  let x = 'Yet another temporary variable.'

  return x
}

// JavaScript example 2:
let printThis = () => {
  let x = 'Yet another temporary variable.'

  return x
}

# Python example 1:
def printThis():
  x = 'Yet another variable.'
  print(x)

printThis() # Yet another variable.

# Python example 2: wrong indentation
def printThis():
  x = 'Yet another variable.'
    y = # wrong indentation
print(x) # wrong indentation - puts print in a different scope, outside the block "printThis"

# NameError: name 'x' is not defined
printThis() # Prints nothing because "print(x) statement is outside the block."
```

A quick recap. Remember these four things. First, there are no curly brackets. Second, functions are called blocks. Third, create a block by using `def` keyword followed by brackets (`()`), with our without the parameter, followed by colon (`:`). Fourth, indent the code that is supposed to be inside the block for one level. And, make sure to keep the indentation consistent.

### If/else

Next, let's take a look at `if/else` statements. Just a quick side note. In Python, `if/else` statement is also called "block". It looks very similar to `if/else` you know from JavaScript, almost identically. There are only four small differences. First, again, no curly brackets. Indentation is used to distinguish between the code inside the block and outside it.

Second, there are no brackets (`()`) around the condition. Third, the condition is followed by colon (`:`). Finally, there is no `else if`. Python uses `elif`. What about the `else`? That is the same, with a very small exception of additional colon (`:`). And, the same also applies to `elif`.

```
// JavaScript example:
if (x > 15) {
  return 'Bigger than 15!'
} else if (x > 25) {
  return 'Bigger than 25!'
} else {
  return 'You are not thinking big enough.'
}

# Python example:
if x > 15:
  print('Bigger than 15!')
elif x > 25:
  print('Bigger than 25!')
else:
  print('You are not thinking big enough.')
```

### While

When it comes to `while` loops, there is not so much to talk about. They look almost the same as their counterparts from JavaScript. There are only few exceptions we discussed when we talked about `if/else` statements, or blocks.

```
// JavaScript example 1:
while (x > 0) {
  return 'You should not try to run this ...'
}

// JavaScript example 2:
let x = 0
while (x < 10) {
  x += 1
  return 'Yes, this is safer.'
}

# Python example 1:
while x > 0:
  print('You should not try to run this ...')

# Python example 2:
x = 0
while x < 10:
  print 'Yes, this is safer.'
  x += 1
```

### For

The last thing we will take a look at today will be `for` loops. When it comes to `for` loops in Python, they look more similar to JavaScript `for...in` rather than the good old `for`.

```
// JavaScript example:
let list = [1, 2, 3]

for (let number in list) {
  console.log(number)
}

# 1
# 2
# 3

# Python example 1:
list = [1, 2, 3]

for number in list:
  print(number)

# 1
# 2
# 3

# Python example 2:
for number in range(0, 7):
  print(number)

# 0
# 1
# 2
# 3
# 4
# 5
# 6
```

## Epilogue: From JavaScript to Python Pt.1

Congratulations! You've just finished the first part of this mini series. Today, we took a look at and discussed the absolute basics. In the beginning, we started by talking about the topic of learning another programming language and why Python is a very good choice. Then, we explored topics such as comments, variables, functions or blocks, `if/else` and `while` and `for` loops.

This is just the beginning, only the basic. However, it will give you a good place to start. So, take the examples we used today and play with them. Try to run them, customize them and run them again to see what happens. This will help you get the grasp of the syntax and memorize it faster. The best way to learn Python is by writing code in Python. In the end, the best way to learn anything is by doing.

What's next? In the second part of this mini series we will discuss concepts such as types, numbers, strings, lists, dictionaries, classes and more. We will again use examples of both, JavaScript and Python, to help you understand how the code looks in Python and what are the differences. Soon, you will be as good in Python as you are in JavaScript. With that, I look forward to seeing you here again the next week. Until then, have a great day!

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Python website]: https://www.python.org
[Alice]: http://aliceinwonderland.wikia.com/wiki/Alice's_Adventures_in_Wonderland
[Tiobe index]: https://www.tiobe.com/tiobe-index/
[machine learning]: https://blog.alexdevero.com/machine-learning-easy-way/
[clean code]: https://blog.alexdevero.com/6-simple-tips-writing-clean-code/

<!--
#### Meta:
-
-->

<!--
#### Inspiration:
- https://dev.to/underdogio/python-for-javascript-developers
- https://docs.python.org/3/library/index.html
-->
