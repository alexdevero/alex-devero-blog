# Memory Life cycle, Heap, Stack and Call Stack in JavaScript

There are topics in JavaScript you as a developer may not know and still get the work done. However, knowing about these topics can help you write better code. Memory heap, stack and call stack are some them. In this tutorial, you will learn about these topics and a bit about how JavaScript works.
<!--more-->
<!--
Table of Contents:
-->

## A quick introduction

JavaScript is a very forgiving programming language. It allows you to do a lot, in many ways. It also does a lot of work for you. Memory management is one of these things. Ask yourself: how many time did you have to think about allocating memory for your variables or functions?

How many times did you have to think about releasing that memory when you no longer needed those variables or functions? Chances are not even once. The same applies to knowing how is heap, stack and call stack work, or what it even is. And yet, you can still work with JavaScript. You can still write code that works every day.

These things are not necessary for you to know. Nor are they required. However, knowing about them and how they work can help you understand how JavaScript works. This, in turn, can help you write better code and become a better JavaScript.

## Memory life cycle

Let's start with the easiest part. What is a memory life cycle, what it is about and how it works in JavaScript? Memory life cycle refers to how a programming language works with memory. Regardless of the language, memory life cycle is almost always the same. It is composed of three steps.

The first step is memory allocation. When you assign a variable or create a function or object some amount of memory has to be allocated for it. The second step is memory use. When you work with data in your code, read or write, you are using memory. Reading from variables or changing values is reading from, and write to, memory.

The third step is memory release. When you no longer use some function or object, that memory is can be released. Once it is released it can be used again. This is the memory life cycle in a nutshell. The nice thing on JavaScript is that it does these three steps for you.

JavaScript allocates memory as you need and want. It makes it easier for you to work with that allocated memory. Lastly, it also does the heaving lifting and cleans up all the mess. It uses [garbage collection] to continuously check memory and release it when it is no longer in use. The result?

As a JavaScript developer, you don't have to worry about allocating memory to your variables or functions. You also don't have to worry about selecting correct memory address before reading from it. And, you don't have to worry about releasing the memory you used somewhere in the past.

## The stack and memory heap

Now you know about the steps of memory life cycle. You know about memory allocation, use and release. One question you may ask is where are those variables, functions and objects actually stored? The answer is: it depends. JavaScript doesn't store all these things at the same place.

What JavaScript does instead is it uses two places. These places are stack and memory heap. Which of these places will be used depends on what you are currently working with.

### The stack

The stack is a place that JavaScript uses to store only static data. This includes primitive [data types] values. For example, numbers, strings, booleans, `undefined` and `null`. These static data also include references. These references point to objects and functions you've created.

These data have one thing in common. The size of these data is fixed and JavaScript knows this size at compile time. This also means that JavaScript knows how much memory it should allocate, and allocates that amount. This type of memory allocation is called "static memory allocation". It happens right before the code is executed.

There is one important thing about static data and memory. There is a limit to how large these primitive values can be. This is also true for the stack itself. That too has limits. How high are these limits depends on specific browser and engine.

## Conclusion: [...] ...

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[]:

<!--
### Meta:
-
-->

<!--
### Keywords:
-
-->

<!--
### Resources:
-
-->
