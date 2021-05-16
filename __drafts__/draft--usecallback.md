# A Quick Guide to React useCallback Hook

The React useCallback hook can help you improve performance of your React apps. It is weird that useCallback hook is one of the hooks that are not discussed as often. In this tutorial, you will learn about what React useCallback is, how it works and how to use it. You will also learn a bit about memoization.<!--more-->
<!--
Table of Contents:
## Introduction to React useCallback hook
## The syntax of useCallback hook
## The power of dependencies
### A simple example
## Working with dependencies and when to re-create memoized function
### After every render
### Only after initial render
### When specific value(s) change
## A word of caution
## Conclusion: A quick guide to React useCallback hook
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

### A simple example

Let's demonstrate the power of dependencies and memoization on a simple example. Imagine you have a simple component that contains input and button. The input allows the user to specify her name. This name will be stored in local state created with [useState hook]. Click on the button logs the name to the console.

The handler function for the button will be memoized with useCallback hook. On the first try, you forget to include the name as a dependency for the hook. What you do instead is specify the dependency array as an empty array. This tells React that it should create the function only on the initial render.

When something happens that causes a subsequent re-render of the component, it should return the memoized version of the function. Remember that changing state causes React to re-render. This helps keep everything in sync. What happens when the user write her name in the input and clicks the button?

The user will be probably surprised. The console will show the initial value of the "name" state. The reason is that when the function was created, the value of name was the initial value. When the name changed React didn't re-create the function and the function didn't know the name has changed.

```jsx
// Note: this will not work as you may expect:
// Import useCallback and useState hooks from React.
import { useCallback, useState } from 'react'

export default function App() {
  // Create state for name:
  const [name, setName] = useState('')

  // Create and memoize function for logging name:
  const handleShowName = useCallback(() => {
    console.log(name)
  }, []) // <= Notice the empty array with dependencies.

  // Each click on the button will log
  // the initial value of "name" state, i.e. the ''.

  return (
    <div className="App">
      {/* Change "name" state when input changes: */}
      <input value={name} onChange={(event) => setName(event.target.value)} />

      {/* Attach handleShowName function */}
      <button onClick={handleShowName}>Show name</button>
    </div>
  )
}
```

A simple way to fix this is adding the "name" state as a dependency. Now, React will watch this value and re-create the function whenever the name changes. This will ensure that when the user changes the name the function will always have the latest information and log correct value.

```jsx
// Note: this will not work as you may expect:
import { useCallback, useState } from 'react'

export default function App() {
  // Create state for name
  const [name, setName] = useState('')

  // Create and memoize function for logging name:
  const handleShowName = useCallback(() => {
    console.log(name)
  }, [name]) // <= Add "name" state as dependency.

  return (
    <div className="App">
      {/* Change name state when input changes: */}
      <input value={name} onChange={(event) => setName(event.target.value)} />

      {/* Attach handleShowName function */}
      <button onClick={handleShowName}>Show name</button>
    </div>
  )
}
```

## Working with dependencies and when to re-create memoized function

The array of dependency, the second parameter, tells React when memoized function should be re-created. There are basically three options.

### After every render

First, React can re-create the function after every render of your component. This pretty much defeats the whole purpose of useCallback hook, but it is still something you can do. For this, all you have to do is to omit the dependencies array. Use useCallback hook only with the function you want to memoize.

```jsx
// Import useCallback hook from React:
import { useCallback } from 'react'

export default function App() {
  // Use useCallback to memoize function:
  const memoizedFunc = useCallback(() => someFunction())
  // Omit the dependency parameter (array).

  return (
    <div className="App">
      {/* Your component */}
    </div>
  )
}
```

If you really want to do this, you can simply skip using the useCallback hook. This option will lead to same result as declaring a function without the useCallback hook. The function will be re-created on every re-render and never memoized.

```jsx
// Import useCallback hook from React:
import { useCallback } from 'react'

export default function App() {
  // Normal function:
  const someFunction = () => (/* Do something */)

  return (
    <div className="App">
      {/* Your component */}
    </div>
  )
}
```

### Only after initial render

The second option is to create the function only after the initial render. When a subsequent re-render happens, React will return the memoized version of the function. This can be useful in two cases. First, when the function should always return the same result and probably doesn't work with external input.

The second case is when the function works with external input(s), but that input doesn't change. If the input doesn't change or the function doesn't depend on any external input, you may think about memoizing it. To do this, pass an empty array as the dependency parameter.

```jsx
// Import useCallback hook from React:
import { useCallback } from 'react'

export default function App() {
  // Use useCallback to memoize function:
  const memoizedFunc = useCallback(() => someFunction(), [])
  // Pass an empty array as dependency parameter.

  return (
    <div className="App">
      {/* Your component */}
    </div>
  )
}
```

### When specific value(s) change

The last option is to re-create the function when only specific value or values change. If some of the values change React will re-create the function to ensure it has the latest data. Otherwise, it will return the memoized version of the function. For this, specify the values you want to watch in the dependency array as a parameter.

From now, when any of these watched values change React will automatically re-create the function. Otherwise, it will return the memoized version. Remember that only one value you specified as a dependency has to change for React to re-create the function, not all of them.

```jsx
// Import useCallback hook from React:
import { useCallback, useState } from 'react'

export default function App() {
  const [name, setName] = useState('')
  const [email, setEmail] = useState('')
  const [isValid, setIsValid] = useState(false)

  // Create and memoize form handler
  const handleFormSubmit = useCallback(
    () => {
      // Submit form.
    },
    [name, email, isValid], // <= Watch "name", "email" and "isValid".
  )

  return (
    <form className="App">
      {/* Your form component */}

      <button onClick={handleFormSubmit}></button>
    </form>
  )
}
```

## A word of caution

Just because there is some tool doesn't mean you have to use it. The same also applies to React useCallback hook. The purpose of this hook is to improve performance of heavy components. It is not intended to be a default "wrapper" for every single function you declare in your component.

So, don't assume that you have to use useCallback every time you declare a function. You don't. Use this hook in heavy components that use multiple functions and these functions don't have to be re-created on every render. Even then, consider the potential gain and loses.

Will memoization help you measurably improve performance? Or, will it only introduce more complexity to your code, while any performance gains will be barely noticeable? For small and light components useCallback might not make a difference.

## Conclusion: A quick guide to React useCallback hook

The React useCallback hook can be useful for improving performance of your apps, by storing your functions for later use, instead of re-creating them on every re-render. This can improve re-rendering behavior and performance of heavy components. I hope this tutorial helped you understand how useCallback hook works and how to use it.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[memoize]: https://en.wikipedia.org/wiki/Memoization
[useEffect hook]: https://blog.alexdevero.com/react-useeffect-hook/
[useState hook]: https://blog.alexdevero.com/react-usestate-hook-in-action/

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
