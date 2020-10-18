# Garbage Collection in JavaScript Made Simple

Garbage collection is nothing new under the sun. Yet, there are many JavaScript developers who don't know much about it. If you are one of them, don't worry. This tutorial will help you understand the basic of garbage collection in JavaScript. You will learn what it is and how it works.<!--more-->
<!--
Table of Contents:
-->

## A quick introduction

Chances are that you've already heard about this thing called "Garbage collection". If not, here is short version. JavaScript is a very unique language. Unlike other languages, JavaScript is able to automatically allocate memory when it is needed. it can also release that memory when it is not needed anymore.

When you create new object, you don't have to use special method to allocate memory for that object. When you no longer need that object, you don't have to use another special method to release that memory. JavaScript will do this for you. It will automatically check if there is a need for memory allocation or memory release.

If there is such a need, JavaScript will do the work necessary to fulfill that need. It will do all this without you even knowing about it. This a good and also a bad thing. It is good because you don't have to worry about this too much. It is a bad thing because it can make you think you don't have to worry about this at all.

The problem is that JavaScript can help you with this memory management only to some degree. It also can't help you if you start throwing obstacles in the way. Before we get to garbage collection, let's quickly talk about memory and memory management.

## Memory management and memory life cycle

One thing programming languages share is something called memory life cycle. This life cycle describes the way memory is managed. It is composed of three steps. The first step is about allocating the memory you need. This happens when you declare new variables and assign the values, call a function that creates values, etc.

All these new values need some space in memory. JavaScript allocates this space, and makes it available, for you. The second step is about using that allocated memory for tasks such as read and writing data. For example, when you want to read value of some variable, or object property, or when you want to change that value or property.

The third and final step is about releasing that allocated memory. You want to free up the allocated memory when it is no longer needed. For example, when you no loner need that variable why keeping it forever? You want JavaScript to get rid of that variable, so it doesn't take up space in memory.

This third step is critical. Without it, your program would continue to consume more and more memory until no more was available. Then, it would crash. It is also this final step that is the most difficult to do correctly. Whether is it for you as a developer in low-level language or the language itself.

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
- https://javascript.info/garbage-collection
-->
