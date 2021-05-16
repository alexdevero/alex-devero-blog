# A Quick Guide to React useCallback Hook

The React useCallback hook can help you improve performance of your React apps. It is weird that useCallback hook is one of the hooks that are not discussed as often as they should be. In this tutorial, you will learn about what React useCallback is, how it works and how to use it.<!--more-->
<!--
Table of Contents:
## h2
### h3
### h3
## h2
## Conclusion: [...] ...
-->

## Introduction to React useCallback hook

The main purpose of React useCallback hook is to memoize functions. The main reason for this is increasing performance of your React applications. How is this related? Every time your component re-renders it also re-creates functions that are defined inside it. Memoizing functions helps you prevent this.

When you [memoize] a function with useCallback hook that function is basically stored in cache. Quick example. Imagine that something causes your component to re-render. Let's say there is a change of state. Usually, this re-render would, by default, also cause React to re-create all functions defined in your component.

This may not happen with useCallback hook and memoization. When you memoize a function React may not re-create that function just because the component re-rendered. Instead, React can skip the re-creation and return the memoized function. This can help you save resources and time and improve performance of your application.

## The syntax of useCallback hook

If you already know the React [useEffect hook] you will find the syntax of useCallback familiar. They are actually almost the same. Similarly to useEffect hook, useCallback also accepts two parameters. The first parameter is the function you want to memoize. The second parameter is an array of dependencies.

This array of dependencies specifies values React should watch. When any of these values changes, React should re-create the function. Otherwise, it should return the memoized version of the function.

```jsx
// Import useCallback hook from React:
import { useCallback } from 'react'

export default function App() {
  // Use useCallback to memoize function:
  const memoizedFunc = useCallback(() => {
    someFunction() // Function that will be memoized.
  }, [/* depOne, depTwo, ...dep */]) // <= Dependency array.

  // A bit shorter version:
  const memoizedFunc = useCallback(() => someFunction(), [])

  return (
    <div className="App">
      {/* Your component */}
    </div>
  )
}
```

## The power of dependencies

The array of dependencies is important. It helps React understand when to return the memoized function and when to re-create it. Why re-create it? Wasn't the purpose of memoization preventing this from happening? Well, yes and no. Yes, you want to prevent the function from being re-created.

However, if the function depends on some input, you want to re-create that function when the input changes. Otherwise, you would execute the function with old input that is no longer relevant. For example, let's say you have a function that greets the user using their name.

This function will depend on the name of the current user. If you memoize it the first time you create it, it will remember the first name. When the name changes, it will not register it. It will greet every subsequent user using the first name. Solution for this is adding the name as a dependency.

When you specify the name as dependency, React will automatically re-create the function when the name changes. When new user arrives, and the name changes, the function will be re-created. It will update its input, use the latest value of name, and greet the user using a correct name.


### h3

### h3

## h2

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
