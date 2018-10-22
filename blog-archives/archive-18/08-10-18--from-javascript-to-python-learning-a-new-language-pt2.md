# From JavaScript to Python – Learning a New Language Pt.2

Do you know JavaScript? What about learning Python? Knowing multiple programming languages is very beneficial. It helps you see problems from different angles, think more clearly, creatively and find more and better solutions. Use what you know from JavaScript to learn Python easier and faster.

<!--
Table of Contents:
## From JavaScript to Python: Types
### Boolean
### Numbers
### Strings
### Lists
### Tuples
### Dictionaries
### Sets
### None
## Epilogue: From JavaScript to Python Pt.2
-->

## From JavaScript to Python: Types

Let's start with something quite simple. If you read the [first part], you already know that Python is very similar to JavaScript. When you think back to some code examples we worked with in first part, they look a lot alike. Just like in case of other languages such as Java, C and C#, types are another thing you can see and use in Python.

That being said, it is important to mention that it is not necessary to declare types of variables in Python. Python does this heavy lifting for you automatically. Every time you declare a new variable and assign some value to it, Python will set appropriate variable type. This also means that if you change the value of the variable Python will also change the variable type.

In other words, you don't have to remember, or worry about, what variable type did you use for this or that variable. When you decide to change the value of some variable, let's say from `number` to `string`, there is nothing saying you can't do this. Remember this if you are used to strongly typed variables from TypeScript or languages using this concept.

### Boolean

This will be very quick. Just like JavaScript, and probably any other programming language, Python has two `boolean` types. These are `True` and `False`. One thing to remember is that Python is case sensitive. So, make sure to use boolean with capital "T" and "F" letters. Seriously, push this into your memory. Lowercase "t" or "f" caused me a lot of errors.

### Numbers

The next type we will take a look at numbers. In Python, there are some differences when it comes to numbers. In JavaScript, we can work only with two types of numbers. These types are `integers` and `floats`. Unlike JavaScript, Python has three types of numbers. These types are `int`, `float` and `complex`. When you want to check for type, you can use built-in function `type()`.

Automatic conversion of variable type, we talked about above, applies also to numbers. This again means that you don't have to think about what format of number should a variable be. Python will decide this automatically for you and convert the number from one format to another if necessary. However, if you do want to specify the format you can use built-in conversion functions such as `int()`, `float()` and `complex()`.

_Side note: It used to be that Python worked with four number types. Aside to integers, there were also long integers. However, this is no longer true. This changed around year 2001 with [PEP 237] (Python Enhancement Proposal 237) when long integers and integers were unified. From this moment, any time you try to check if something is long integer the answer will always be `integer`._

```
// JavaScript example:
let numberOne = 159 // integer
let numberTwo = 1.618 // float

console.log(typeof numberOne) // 'number'
console.log(typeof numberTwo) // 'number'

// Test for floats
console.log(numberOne === parseInt(numberOne)) // true - is integer (159 === 159)
console.log(numberTwo === parseInt(numberTwo)) // false - is float (1.618 === 1)

# Python example:
numberInt = 33
numberFloat = 92.33
numberComplex = (345+0j)

type(numberInt) # is an integer
type(numberFloat) # is a float
type(numberComplex) # is a complex number

# Conversion example:
int(numberFloat) # converts numberFloat to integer - 92
float(numberInt) # converts to float - 33.0
complex(numberInt) # converts to complex number - (33+0j)
```

### Strings

Another type you already know very well from JavaScript is `string`. This is also one of the most popular and often used types. As you may guess, strings work in Python just like in JavaScript. One thing. First, Python doesn't care at all whether you use single or double quotes. Just make sure you don't mix single and double quotes as that would lead to errors or code not running.

Just like in JavaScript, you can also perform various operations with strings. You can concatenate strings using `+` operator. You can also repeat string for a specific number of time using `*` operator. Next, you can get a specific character from a string using `[index]`. Or, if you want to get part of the string you can use `[startingIndex:endingIndex]`.

If you want to know if string contains a specific character you can use `in`. Negation is done by `not in`. Keep in mind that these two are case sensitive.  What if you have a string with some escaped characters and you want to print them as they are? In that case, using `r` or `R` will do the work. You can also use something called [formatting operator]. This allows you to use strings together with a set of variables.

One last thing. You can also create a string that spans across multiple lines. In order to do this, you have to use triple single or double quotes at the beginning and end of the string.

```
// JavaScript example:
let stringOne = 'One for single quotes.'
let stringTwo = "One for double quotes."

console.log(stringOne) // One for single quotes.
console.log(stringTwo) // One for double quotes.

# Python example:
stringOne = 'One for single quotes.'
stringTwo = "One for double quotes."

print(stringOne) # One for single quotes.
print(stringTwo) # One for double quotes.

# Concatenation example 1:
x = 'This is just the beginning'
y = ' and this is the end.'
z = x + y

print(z) # This is just the beginning and this is the end.

# Concatenation example 2:
a = 'Head' + ' and ' + 'tail.'

print(a) # Head and tail.

# Repetition example 1:
x = 'One step.'

x*5 # 'One step.One step.One step.One step.One step.'

# Repetition example 2:
print('Speak truth '*3) # Speak truth Speak truth Speak truth

# Getting a character example:
'This is not false.'[5] # 'i'

# Slicing string example:
'This is not true.'[8:11] # 'not'

# Testing if string contains specific character example:
characterFromVariable = 'w'

characterFromVariable in 'Let me test this.' # False

'e' in 'Let me test this.' # True

't' in 'Let me test this.' # True - case sensitive!
'T' in 'Let me test this.' # False - case sensitive!

# Testing if string doesn't contain specific character example:
'W' not in 'Let me test this.' # True

# Printing escaped characters example:
r'This is supposed to be escaped \n character.' # 'This is supposed to be escaped \\n character.'

# String formatting example:
name = 'Tony Stein'
age = 21

print("%s is %d years old." % (name, age)) # Tony Stein is 21 years old.

# String on multiple lines example:
""" This is the first line
of a longer paragraph of text
which may not make sense."""
```

### Lists

The fourth type are lists. List are what you know from JavaScript as Arrays. Aside to the name, there is no difference. Just like `strings`, `lists` allow you to do various operations such as concatenating, repeating, testing if element is in a `list`. Then, you can also get the length of the `list` (number of items inside it) iterate over it, access it, slice it, update it and delete specific items. Yu can also delete the `list` using `del`.

```
// JavaScript example:
let arrayExample = [1, 5.16, true, 'String', { name: 'Sei' }]

# Python example:
listExample = [1, 5.16, True, 'String', ('name', 'Sei')]

# Accessing item example:
print(listExample[3]) # String

# Check length
listExample = [1, 5.16, True, 'String', ('name', 'Sei')]

len(listExample) # 5

# Update list example:
listExample[1] = 99.8

print(listExample) # [1, 99.8, True, 'String', ('name', 'Sei')]

# Concatenate lists example 1:
listOne = [1, 2, 3]
listTwo = [4, 5, 6]
listThree = listOne + listTwo

print(listThree) # [1, 2, 3, 4, 5, 6]

# Concatenate lists example 2:
print(['a', 'b', 'c'] + ['x', 'y', 'z']) # ['a', 'b', 'c', 'x', 'y', 'z']

# Remove item example:
del listExample[4]

# Delete whole list example:
del listExample

print(listExample) # [1, 5.16, True, 'String', ('name', 'Sei')]

# Repeat list example:
repeatList = [1, 'two', True]

print(repeatList*4) # [1, 'two', True, 1, 'two', True, 1, 'two', True, 1, 'two', True]

# Iterate over list example:
listExample = ['alpha', 'beta', 'gamma']

for word in listExample:
  print(word)

# alpha
# beta
# gamma
```

### Tuples

This type will be completely new if your previous experience with programming includes only JavaScript. As far as I know, there is nothing like `tuples` in JavaScript. However, that will not be a problem. `Tuples` are very similar to `lists`, or `arrays` in JavaScript. There are only two differences. First, `tuples` use parenthesis instead of square brackets.

Second, and more important, `tuples` are immutable. This means that once you create a `tuple` you can't change it. Like with `lists`, you can concatenate two or more tuples into a new one. You can also repeat them and check for existence of specific items. Just like `lists`, `tuples` can contain all other valid types. Finally, you can delete tuples using `del`.

```
# Tuple example:
tupleOne = () # Empty tuple
tupleTwo = (8) # Tuple with only one item
tupleFour = (8, 'string', False, [1], ('inner tuple')) # Tuple with other valid types

# Accessing item example:
print(tupleFour[2]) # String

# Check length
len(tupleFour) # 5

# Concatenate tuples example 1:
tupleOne = (20, False, 'not a number')
tupleTwo = (0.5, 91, '9')
tupleThree = tupleOne + tupleTwo

print(tupleThree) # (20, False, 'not a number', 0.5, 91, '9')

# Concatenate tuples example 2:
print((True, 'omega', 56) + (False, 'beta', 'phi')) # (True, 'omega', 56, False, 'beta', 'phi')

# Delete tuple example:
del tupleFour

# Repeat tuple example:
repeatTuple = ('Alphabet', 1, True)

print(repeatTuple*3) # ('Alphabet', 1, True, 'Alphabet', 1, True, 'Alphabet', 1, True)

# Iterate over tuple example:
tupleExample = ('one', 'two', 'three')

for item in tupleExample:
  print(item)

# one
# two
# three
```

### Dictionaries

`Dictionary` is another type you will know from JavaScript, but under a different name. In Python, `dictionary` is an equivalent of what you know from JavaScript as `object`. It also looks like a regular `object`. Every `dictionary` contains `key` and `value` pair(s) separated by a colon (`:`). The whole thing is then wrapped in curly brackets `{}`.

Dictionaries are mutable. Or, in simple terms, you can change dictionary any time after you create it. Dictionaries can't be concatenated or repeated. You can access entries in a `dictionary` like in JavaScript's `object`, using square brackets (`[]`). You can also delete an entry from `dictionary`.

Aside to that, you can even delete all entries and keep an empty `dictionary` using `clear()`. And, you can delete the entire `dictionary` using `del`.

```
// JavaScript example:
let objExample = {
  'name': 'Tony',
  'age': 32,
  'living': true
}

# Python example:
dictExample = {
  'name': 'Tony',
  'age': 32,
  'living': True
}

# Access entry example:
dictExample['age'] # 32

# Update entry example:
dictExample['name'] = 'Cindy'

print(dictExample) # {'name': 'Cindy', 'age': 32, 'living': True}

# Delete entry from dictionary example:
del dictExample['living']

print(dictExample) # {'name': 'Tony', 'age': 32}

# Remove all entries example:
dictExample.clear()

print(dictExample) # {}

# Delete entire dictionary example:
del dictExample

print(dictExample) # NameError: name 'dictExample' is not defined
```

### Sets

Another brand new type is `set`. This type something between a `list` and `dictionary`. It contains items like a `list`, but it wraps them inside curly brackets (`{}`) like a `dictionary`. Aside to this, there is one thing you need to know and remember. It can't contain duplicate items. When you try to create a `set` with duplicates, Python will keep only one instance of the item and remove the rest.

Similarly to a `dictionary`, `set` doesn't support repeating or concatenation or delete individual items. However, you can use `clear()` to remove all items inside a `a` or `del` to remove the entire `set`.

```
# Set example (notice two 'table' items):
setExample = {'table', 'notebook', 'IDE', 'headphones', 'podcasts', 'table'}

print(setExample) # {'notebook', 'IDE', 'headphones', 'podcasts', 'table'}
# notice that Python removed the first 'table' item.

# Remove all items example:
setExample.clear()

print(setExample) # {}

# Delete entire set example:
del setExample

print(setExample) # NameError: name 'setExample' is not defined
```

### None

Finally, there is `None` which is an equivalent of JavaScript's `null`. If you want to test if something is `None`, you can use `is None`. Just like with booleans, make sure to always use capital 'N'. This can help you avoid many potential problems and headaches.

```
// JavaScript example:
let x = null

# Python example:
noneExample = None

print(noneExample) # None

# Test if noneExample is 'None' example:
print(noneExample is None) # True
```

## Epilogue: From JavaScript to Python Pt.2

Congratulations! You've just finished the second part of this mini series. Today, you've learned about all types Python has to offer. We discussed booleans, numbers, strings, lists, tuples, dictionaries, sets and none. After we got familiar with the theory, we practiced working with all these types on a number of code examples so you could see them in action.

That being said, this is not the end of this journey. There are still some concepts in Python we didn't have a chance to explore yet. However, you don't have to worry about this. We will talk about these concepts in the following, and also last, part of this mini series. These concepts include classes, regexp, handling input (I/O) and more.

What can you do now? I have two suggestions. First, go back to the examples we worked on today and play with them. Change the code and observe what happens. Second, create challenges based on what you've learned today and practice and test your skills. This will help you consolidate what you've learned in your memory. Remember, the best way to learn programming is by writing code.

Aside to this, work on what you've learned in the [first part] and also on your knowledge in JavaScript. Remember, practice, practice and practice. And then some more. This will help you prepare ready for what will come in the last part. With that, thank you very much for your time. I look forward to seeing you here again the next week. Until then, have a great day!

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[first part]: https://blog.alexdevero.com/javascript-python-pt1/
[PEP 237]: https://www.python.org/dev/peps/pep-0237/#id1
[formatting operator]: https://www.learnpython.org/en/String_Formatting

<!--
#### Meta:
-
-->

<!--
#### Inspiration:
- https://dev.to/underdogio/python-for-javascript-developers
- https://docs.python.org/3/library/index.html
- https://www.tutorialspoint.com/python/python_variable_types.htm
- https://developer.rhino3d.com/guides/rhinopython/python-datatypes/
- https://docs.python.org/2/library/stdtypes.html#id2
-->
