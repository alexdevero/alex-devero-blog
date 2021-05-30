# The React useMemo Hook Made Simple

Performance is important, especially in large-scale application. The React useMemo hook is one tool you can use to improve the performance of your React apps. This tutorial will help you understand what useMemo hook is and how it works. It will also show you how to use it.<!--more-->

## Introduction to React useMemo hook

The React useMemo hook is one of the [additional hooks] that are implemented in React. All these hooks serve different purposes. The purpose of useMemo hook is to memoize the output of a [function]. What this means is that it executes some function and remember the output of that function.

The important part comes when your component re-renders. After re-render, any function in the component would be normally created. If you are also calling the function, it would be also executed again. The useMemo hook helps you avoid this. It allows you to execute the memoized function only under specific conditions.

When these conditions are not met, the useMemo will not execute the function. Instead, it will return the value from the last execution. This simple thing can help you optimize your React application by avoiding expensive calculations every time one of your components re-render.

When you think about it, the useMemo hook is a bit like the [useCallback hook]. Both use memoization. The difference is that while useCallback hook memoizes whole function, the useMemo memoizes only the output of a function.


[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[additional hooks]: https://reactjs.org/docs/hooks-reference.html#additional-hooks
[function]: https://blog.alexdevero.com/javascript-functions-pt1/
[useCallback hook]: https://blog.alexdevero.com/react-usecallback-hook/
[useEffect hook]: https://blog.alexdevero.com/react-useeffect-hook/
[React docs]: https://reactjs.org/docs/hooks-reference.html#usememo

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
