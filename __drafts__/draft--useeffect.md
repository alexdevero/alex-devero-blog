# React useEffect Hook Demystified: What You Need to Know

The React useEffect Hook helps you manage side-effects in functional React components. It also makes this task much easier than it used to be. In this tutorial you will learn about what useEffect hook is and how it works. You will also learn how to use it in your React applications.<!--more-->

## Introduction to React useEffect hook

If you are familiar with React class components you know there are lifecycle methods available to use. You can use these methods to execute code at a specific moment you need. You can execute your code only when on component's initial render. You can also execute it on very re-render of the component, or if only some data change.

These lifecycle methods, along with other features of class components, don't work with functions. These methods doesn't exist in their scope or environment. React hooks made it possible to bring many of these features from classes to functional components so you can use them here as well.

The React useEffect hook is a hook that brings the functionality of lifecycle methods to functional components. To make this easier, you can think about the useEffect hook as `componentDidMount`, `componentDidUpdate` and `componentWillUnmount` lifecycle methods in one package.

That said, there are some differences between useEffect hook and lifecycle method. One difference is that useEffect hook runs after render. It runs after the first render, and also after every next update. It doesn't run before it. This makes it easy to execute any code right after a component is rendered.

Another difference is that, by default, useEffect hook runs after every render. Fortunately, there is a way to prevent this behavior. When you use the useEffect hook, there is an option you can use to say when you want the useEffect hook to run. The hook will than run only under correct conditions and ignore others.

Another useful feature of useEffect hook is that it can also clean up after itself. This cleanup happens automatically before the hook is executed again. One example when cleanup can be handy is removing attached event listeners when you "change" page in your React application.

## Conclusion: [...] ...

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[side-effects]: https://dzone.com/articles/side-effects-1

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
