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
