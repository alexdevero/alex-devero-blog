# How to Create Your Own React Custom Hooks

React offers a number of built-in hooks you can use right away. Aside to these, you can also create your own custom hooks. In this tutorial, you will learn what React custom hooks are and how to create your own. You will also learn what rules you have to follow when creating custom hooks.

<!--more-->
<!--
Table of Contents:
-->

## A quick overview of React hooks

It was in [React v16.8] when React hooks were introduced by React team. Since then, hooks quickly rose in popularity among React developers, and even beyond. Until then, when you wanted to use state and lifecycle methods inside React components you had to use [JavaScript classes].

React hooks changed this paradigm. With hooks, you no longer have to create components with classes just so you can use state. You can just as well create functional components. Then, you can use hooks to "enhance" these components with whatever feature you need, be it a state, lifecycle method or something else.

The word "hook" may sound a bit vague. To make it easier, think about hooks simply as functions. This is what hooks are, plain [JavaScript functions]. These functions allow you "hook into" various React features, such as state and lifecycle. Most popular examples are [useState] and [useEffect] hooks.

The useState hooks allows you to bring state to function components. With useEffect hook, you can work with component lifecycle. There is a couple of React [hooks] ready to use. However, these hooks can't do everything. They can't cover every possible scenario. Fortunately, these hooks are not the only option.

## An introduction to React custom hooks

Aside to releasing a number of official React hooks, React team made it also possible to create React custom hooks. So, if you can't find a hook that would solve some problem you have, you can create your own. You can also use React custom hooks to make your code that involves stateful logic reusable.

As we already discussed, hooks are basically plain JavaScript functions. One difference is that hooks are used for a specific purpose. Another is that React hooks allow you to use other React hooks, such as useState, and even other custom hooks. So, don't worry that creating custom hooks will be difficult.

Creating custom hooks will be similar to writing regular JavaScript functions. You will probably get a grasp on it quickly. It will be even faster if you know how to use hooks such as useState and useEffect because you are likely to use these hooks in your custom hooks. But before we get into that, there are some rules to learn.

## Rules of hooks

Before you create your first custom hook, there are two rules you should know. These rules are called [Rules of hooks]. First, you can call hooks only at the top level. Never call hooks inside nested functions, conditions or loops. If you want to use conditions, or loops, use them inside the hook, not the other way around.

The second rule is that you should call hooks only from React function components or other hooks. There is also one practice for creating custom hooks. Always start the name of the hook with "use" prefix. This is a best practice, not a rule. It is good to follow and it can make your code more readable, but it is not required.

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
