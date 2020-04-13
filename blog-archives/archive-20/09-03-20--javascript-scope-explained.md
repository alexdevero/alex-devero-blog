# JavaScript Scope Explained
Scope is one of the most important topics in JavaScript. In this tutorial, you will learn about what scope is. Then, you will learn about types of scope and how they work. You will also learn about ES6 variables, block statements, why they matter for scope. Lastly, you will also learn about closures.<!--more-->
<!--
Table of Contents:
## The basics of scope
## Benefits of scope
## Scope in JavaScript
### Global scope
### Local scope
### Lexical scope
### Lifetime of a scope
## Block statements, ES6 and scope
## Closures - A brief introduction
### Very simple closures
### More complex closures pt.1
### More complex closures pt.2
### Explanation of examples in more complex closures
### Calling returned function without assignment
## Conclusion: JavaScript Scope Explained
-->

## The basics of scope

So, what is scope? In programming, scope refers to the visibility and accessibility of variables, functions and objects during runtime. Put simply, scope says whether you can use particular variable, functions or object in your code at a specific location or not. And the runtime? Runtime is a time during which a computer program is executing.

This is important. It means that not all variables, functions and objects are always visible and accessible everywhere. Thanks to scope, variables, functions and objects may be visible and accessible everywhere, or they may not. It depends in what scope do you create them. If they are not visible, JavaScript will not let you use them.

What if you try to use some variable, function or object that is not accessible in your current scope? JavaScript will tell you that the variable, function or object is not defined. This is correct because that thing is really not defined. It doesn't exist in your current scope.

One more thing about scope. You can also create scope inside a scope, or let's say "child" scopes. These are called lexical scopes. In this case, these lexical scopes can access variables, functions or objects defined in a parent scope. However, parent scope can't access variables, functions or objects defined in a its lexical scopes.

Don't worry if this sounds too difficult now. We will talk more about all this, and more, later in this tutorial. There will also be examples that will help you understand all these concepts. But before that, let's first talk about some benefits of scope.

## Benefits of scope

Why is scope, and this limited accessibility and visibility, a good thing? First, it makes your code more secure. Imagine you have a system with different types of users. Some of these users are admins and others are users. Let's say you give them all full access to all parts of the system. What if something bad happens?

For example, what if someone delete some important files, change some records, or break the system? How will you find out who did it? This might be close to impossible, depending on the numer of users of the system. How can you prevent this from happening? You can limit the access each type of a user has.

You can give full access to admins and limited access to users. This will make accidents less likely to happen. And, if something does happen, you know who is responsible.

Second, limited accessibility and visibility makes your code safer. When all your code is visible and accessible everywhere it is easy to run into problems. For example, you may accidentally some variable or function name twice. In that case, the new variable, or function, will rewrite the older.

This is usually less likely to happen when you limit accessibility and visibility. With scope, you can use the same names safely, without having to worry about anything, as long as the scope is always different. That said, using the same names is not a practice I would recommend to follow.

Third, limited accessibility and visibility helps you use memory more efficiently. Imagine loading all variables, functions, objects, etc. all the time, no matter if you actually use them or not. This would quickly lead to high memory usage and lower performance. None of these are good things, and definitely not necessary.

Fourth, limited accessibility and visibility makes debugging easier. It is easier and faster to track and fix bugs when you work with small chunks of code, i.e. multiple small scopes, than when you work one large piece of code, i.e. one scope.

## Scope in JavaScript

Okay, that was about the "what" and "why". Now, it is time to learn about how scope actually works. In JavaScript, there are types of scope, global and local scope.

### Global scope

The first type of scope is a global scope. This scope is created automatically. Everything that is not defined inside a local scope is automatically in a global scope. If you run your code in a web browser, global scope will be a `window` object. In case of Node.js, it will be [global].

When something is defined in a global scope, it means that it is accessible and visible from anywhere in your code.

```JavaScript
// Global scope
// Variable declared in a global scope
var myVar = 'Global variable one.'
let myLet = 'Global variable two.'
const myConst = 'Global variable three.'

// Try to access global variable from a function
function readVariable() {
  // Return global variable myVar
  // myVar variable is accessible everywhere
  return myVar
}

// Call readVariable function
readVariable()
// 'Global variable one.'

// Log global variable myVar
console.log(myVar)
// 'Global variable one.'
```

As we discussed in the begging, defining variables, functions or objects in global scope is not a good practice, and it should be avoided. You should always, or almost always, use local scope.

### Local scope

The second type of scope is local scope. Variables, functions and objects defined in a local scope are visible and accessible only inside that scope. They are not visible and accessible outside it. The exception here are inner, or "child", scopes we briefly talked about in the beginning.

Unlike global scope, local scope is not created automatically. Well, almost. JavaScript will create local scope automatically if you give it a reason. How? By creating a [function]. In JavaScript, every function creates its own, local scope. This is also why "local" scope is sometimes called "function" scope.

When you create some function, and define a variable, object or another function inside it, that "thing" you defined will be defined in a local scope. It will be a local variable, object or function. This also means that it will be visible or accessible only inside the function, or a local scope, yu defined it in.

When you try to use that local variable, object, function, JavaScript will throw an error about something not being defined.

```JavaScript
// Local scope no.1:
// Different functions, different local scopes

// Create function to create new local scope
function myFunctionOne() {
  // Local scope no.1
}

// Create another function to create another new local scope
function myFunctionTwo() {
  // Local scope no.2
}

// Create another function to create another new local scope
function myFunctionThree() {
  // Local scope no.3
}


// Local scope no.2:
// Try to access variables in different local scopes
function myFunctionOne() {
  // Local scope no.1
  const myConstOne = 'I am inside local scope of myFunctionOne.'

  // Try to access myConstTwo variable
  // declared in local scope of myFunctionTwo
  // This doesn't work
  console.log(myConstTwo)
  // ReferenceError: myConstTwo is not defined
}

// Create another function to create another new local scope
function myFunctionTwo() {
  // Local scope no.2
  const myConstTwo = 'I am inside local scope of myFunctionTwo.'

  // Try to access myConstOne variable
  // declared in local scope of myFunctionOne
  // This doesn't work
  console.log(myConstOne)
  // ReferenceError: myConstOne is not defined
}
```

### Lexical scope

Functions are used in JavaScript to create local scope. Building on this idea, if you want to create another local scope inside existing function, inside existing local scope, all you have to do is define another function inside that function, right? Yes. This will create new scope that exists inside another, outer, local scope.

This type of scope is also called lexical scope. Imagine you have a nested group of functions. The inner functions have access to all variables, objects and functions that exist inside their parent scope, or their parent functions. On the other hand, the outer functions don't have access to variables, objects and functions that exist inside their child functions.

Translated into the lingo of developers, the child functions are lexically bound to the [execution context] of their parents.

```JavaScript
// Lexical scope no.1
// Create function to create new local scope
function myParentFunction() {
  // Local scope no.1
  const myParentConst = 'I am a local variable.'

  // Try to access local variable myParentConst
  // This works
  console.log(myParentConst)
  // 'I am a local variable.'

  function myChildFunction() {
    // Local scope no.2
    const myChildConst = 'I am a local local variable.'

    // Try to access local variable myChildConst
    // This works
    console.log(myChildConst)
    // 'I am a local local variable.'

    // Try to access local variable myParentConst
    // from the inside of myChildFunction
    // i.e: Try to access content of parent's scope from its child
    // This works
    console.log(myParentConst)
    // 'I am a local variable.'
  }

  // Try to access local variable myChildConst
  // from the outside of myChildFunction
  // i.e: Try to cess content of child's scope from its parent
  // This doesn't work
  console.log(myChildConst)
  // ReferenceError: myChildConst is not defined
}

// Try to access local variable myParentConst
// from the outside of myParentFunction
// This doesn't work
console.log(myParentConst)
// ReferenceError: myParentConst is not defined
```

### Lifetime of a scope

That was about global and local scope. One good thing to remember is how long each scope lives, how long it exists. Fortunately, the answer is easy. In case of a global scope, the scope lives as long as your application lives. So, if you have some global variables, functions or objects they will exist until you stop your app, or close browser.

In case of a local scope? Anything defined in a local scope lives as long as your function, that creates that local scope we are talking about, is called and executed. When the execution ends the function, and all its content, gets [garbage collected]. It no longer exists.

## Block statements, ES6 and scope

In JavaScript, there are also block statements. Some of them are `if...else` and `switch` conditions and `for`, `while`, `do...while`, `for...in` and `for...of` [loops]. None of these creates new scope. Well, unless you create new function inside them. However, that wouldn't change anything because it would mean we are using functions again.

Anyway, without creating inner function, there is no new local scope created inside block statements. This means that when you declare new variable, function or object inside a block statement it will be not a local variable, function or object. It will still be global variable, function or object.

Since that variable, function or object is global, you can access it from anywhere. Well, unless that block statement is inside a function. In that case, anything inside the block statement will be defined inside a local scope of that function, that also contains that block statement.

```JavaScript
// Block statement no.1: No local scope
// Create if..else statement with a var variable
if (true) {
  var myVar = 'I was supposed to be local.'
}

// Try to access variable myVar
// from the outside of if...else statement
// This works
console.log(myVar)
// 'I was supposed to be local.'
```

This was in pre-ES6 era. Things changed after the release of ES6 specification. ES6 didn't make any changes to scope or block statements themselves. What it did was it introduced new two types of variables, namely `let` and `const`. There are important differences between `var` and `let` and `const` and you learn about them [here].

For this tutorial, the important thing is this ... While the `var` does not respect the content of block statements as a new scope, `let` and `const` do. This means that when you declare `let` or `const` variable inside a block statement it will b accessible only inside that statement, not outside it.

```JavaScript
// Create if..else statement with a variable
if (true) {
  var myVar = 'I am var.'
  let myLet = 'I am let.'
  const myConst = 'I am const.'
}

// Try to log the var variable
// declared inside if...else statement
// This works
console.log(myVar)
// 'I am var.'


// Try to log the let variable
// declared inside if...else statement
// This doesn't work
console.log(myLet)
// ReferenceError: myLet is not defined

// Try to log the const variable
// declared inside if...else statement
// This doesn't work
console.log(myConst)
// ReferenceError: myConst is not defined
```

This is also one reason many JavaScript developers prefer to use `let` and `const` instead of `var`. Both, `let` and `const`, offer higher degree of control because of their behavior when they are used in block statements. It is a very good idea to start using `let` and `const` an slowly, or quickly, abandon `var`.

## Closures - A brief introduction

In JavaScript, functions are not just functions. They are also closures. This means that functions can access variables, and also arguments, defined outside them and work with them. Not only that. Not only functions have access to outer variables, they also always access the latest values of those variables.

When you create a function, and this function contains another function, this inner function is a closure. This closure, the inner function, is usually returned so you can use the outer function's variables later. You will see this in action on the examples below.

### Very simple closures

Imagine you have a function that accesses some variable from the outside scope. Now, let's say you call that function, then change that variable, and then call that function again. That function will read the new value of that variable, not the old one. This is important to note.

It means that the function is not merely copying the value of that variable and storing it somewhere for later use. Instead, it is actually accessing the specific variable, at the moment of execution.

```JavaScript
// Closure no.1
// Variable declared in a global scope
let name = 'Emmett Brown'

// Simple closure - function accessing outside variable
function introduceMe() {
  return `Hello, I am ${name}.`
}

// Call introduceMe function
introduceMe()
// 'Hello, I am Emmett Brown.'


// Test if introduceMe function
// has really access to "name" variable
// i.e. if it can read its current value
// Change the value of "name" variable
name = 'Marty McFly'

// Call introduceMe function again
introduceMe()
// 'Hello, I am Marty McFly.'
```

### More complex closures pt.1

In most cases, closures are more complex than the example above. These examples usually involve functions returning functions that return something. In this case, the cool thing is that the returned inner function can also access anything passed to the outer, parent, function as an argument, along with any outer variables.

In other words, the inner function actually remembers what was passed in the parent function. This is true even if the inner function is actually executed much later.

```JavaScript
// Closure no.2: function returning a function
// Create outer function that accepts one parameter
function outerFunction(outerParam) {
  // Create inner function that also accepts one parameter
  return function innerFunction(innerParam) {
    // Log the value passed as a parameter
    // to the outer, parent, function
    console.log(outerParam)

    // Log the value passed as a parameter
    // to the inner function
    console.log(innerParam)
  }
}

// Try to call outerFunction right away
outerFunction('This is the outer parameter.')
// ... Nothing

// Assign the "outerFunction" to a variable
// Pass something as a argument
// this is the "outerParam"
const myFunction = outerFunction('This is the outer parameter.')

// Call the "myFunction"
// Pass something as a argument
// this is the "innerParam"
myFunction('This is the inner parameter.')
// 'This is the outer parameter.'
// 'This is the inner parameter.'
```

### More complex closures pt.2

Another popular use case is when the outer function contains some variable and the inner function returns that variable. By the way, this is another example of lexical scope, i.e. inner functions can access variables defined inside their parent scope.

```JavaScript
// Closure no.3
// Create outer function
function collectStuff() {
  // Declare a local variable
  const stuff = ['paper', 'clips', 'pen', 'notebook']

  // Create, and return, inner function
  return function showStuff() {
    // Return the value of "stuff" variable
    // declared in parent scope
    return stuff
  }
}

// Try to call the "collectStuff" function right away
collectStuff()
// ... Nothing

// Assign the "collectStuff" to a variable
const myCollection = collectStuff()

// Call the function assigned to "myCollection"
myCollection()
// [ 'paper', 'clips', 'pen', 'notebook' ]
```

### Explanation of examples in more complex closures

Why trying to call the `outerFunction()` and `collectStuff()` function right away didn't work? Why it was necessary to first assign those functions to a variable and then call those variables? The answer is simple. In the examples above, we didn't call those inner functions. We only returned them.

So, when we called the outer functions they simply returned, but not called, the inner functions. Yes, those inner functions were created but, they were never called. When we assigned the outer functions to a variable, we also invoked them, the outer functions. When this happened, those functions returned the inner functions.

The result was that those variables actually contained reference to the, returned, inner functions, not the outer. So, when we called the variables, we actually, and finally, called the inner functions. This applies to both examples, with `outerFunction()` and with `collectStuff()`. Let's take a look at how this looks in code and let's also add some logs.

```JavaScript
// Create outer function
function collectStuff() {
  // Log a message when "collectStuff" function runs
  console.log('The "collectStuff" function is running!')

  // Declare a local variable
  const stuff = ['paper', 'clips', 'pen', 'notebook']

  // Create, and return, inner function
  return function showStuff() {
    // Log a message when "showStuff" function runs
    console.log('The "showStuff" function is running!')

    // Return the value of "stuff" variable
    // declared in parent scope
    return stuff
  }
}

// Try to call the "collectStuff" function right away
// This will call the "collectStuff" function
// that will return the "showStuff" function,
// but it will not call the "showStuff" function
// therefore the "showStuff" function will NOT run
collectStuff()
// 'The "collectStuff" function is running!'


// Assign the "collectStuff" to a variable
// This will also call the "collectStuff" function
// that will return the "showStuff" function
// reference to which will then be stored in "myCollection" variable
const myCollection = collectStuff()
// 'The "collectStuff" function is running!'
// Now, "myCollection" contains reference to "showStuff" function

// Call the function assigned to "myCollection"
// This will actually call the "showStuff" function
// because "myCollection" contains reference to "showStuff" function
myCollection()
// 'The "showStuff" function is running!'
// [ 'paper', 'clips', 'pen', 'notebook' ]
```

See? The important thing about returning an inner function from a function is that returned function will not be automatically called when you try to call the outer function. This is why you must first assign the outer function to a variable and then call the variable as a function. Only then will the inner function run.

### Calling returned function without assignment

There is a way to call the returned function without assigning it to a variable. This can be done using parenthesis two times, `()()`, at the time when you call the outer function. This will automatically call the inner function as well.

```JavaScript
// Create outer function
function outerFunction() {
  // Log a message when "outerFunction" function runs
  console.log('The "outerFunction" function is running!')

  // Create, and return, inner function
  return function innerFunction() {
    // Log a message when "innerFunction" function runs
    console.log('The "innerFunction" function is running!')
  }
}

// Call the "outerFunction" function right away
// using parenthesis two times '()()'
outerFunction()()
// 'The "outerFunction" function is running!'
// 'The "innerFunction" function is running!'
```

## Conclusion: JavaScript Scope Explained

That's it. You've just finished this tutorial about JavaScript scope. Today, you've learn a lot of things. You've learned the basics of scope and its benefits. Next, you've learned about two types of scope, global and local, and how they work. After that, you've also learned lexical scope and the lifetime of a scope.

After scope, you've also learned about how `var`, `let` and `const` work inside block statements. As the last thing, you've learned about closures and how they work. I hope you enjoyed this tutorial.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[global]: https://nodejs.org/api/globals.html#globals_global
[function]: https://blog.alexdevero.com/javascript-functions-pt1/
[loops]: https://blog.alexdevero.com/javascript-loops/
[here]: https://blog.alexdevero.com/javascript-variables-introduction/
[garbage collected]: https://javascript.info/garbage-collection
[execution context]: https://blog.bitsrc.io/understanding-execution-context-and-execution-stack-in-javascript-1c9ea8642dd0

<!--
#### Meta:
-
-->

<!--
#### Inspiration:
-
-->
