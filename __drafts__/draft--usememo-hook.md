# The React useMemo Hook Made Simple

Performance is important, especially in large-scale application. The React useMemo hook is one tool you can use to improve the performance of your React apps. This tutorial will help you understand what useMemo hook is and how it works. It will also show you how to use it.<!--more-->
<!--
Table of Contents:
## Introduction to React useMemo hook
## The syntax
## When to run
### No.1: Only after initial render
### No.2: Only when dependency changes
### No.3: After every re-render
## Use useMemo hook with caution
## Conclusion: The React useMemo hook made simple
-->

## Introduction to React useMemo hook

The React useMemo hook is one of the [additional hooks] that are implemented in React. All these hooks serve different purposes. The purpose of useMemo hook is to memoize the output of a [function]. What this means is that it executes some function and remember the output of that function.

The important part comes when your component re-renders. After re-render, any function in the component would be normally created. If you are also calling the function, it would be also executed again. The useMemo hook helps you avoid this. It allows you to execute the memoized function only under specific conditions.

When these conditions are not met, the useMemo will not execute the function. Instead, it will return the value from the last execution. This simple thing can help you optimize your React application by avoiding expensive calculations every time one of your components re-render.

When you think about it, the useMemo hook is a bit like the [useCallback hook]. Both use memoization. The main, and maybe only, difference between these two, is that while useCallback hook helps you memoize whole function, the useMemo helps you memoize only the output of functions.

## The syntax

The React useMemo hook accepts two parameters. These parameters are: some function whose output you want to memoize and array of dependencies. The useMemo hook will execute the function you passed as an argument after the initial render by default.

```jsx
// Import useMemo hook from React:
import { useMemo } from 'react'

export default function App() {
  // useMemo syntax example:
  const memoizedVal = useMemo(() => {/* Some function */}, [/* Dependencies */])

  return (
    <div className="App"></div>
  )
}
```

## When to run

When the useMemo hook runs, and executes the function you passed, is determined by the second argument the hook accepts, the dependency array. By changing this argument you change when the hook runs. There are currently three options.

### No.1: Only after initial render

The first option is to run the hook only after the initial render and never again. Then, when something causes the component to re-render, useMemo will not execute the function again. Instead, it will return the memoized output of the function. It will do this for every subsequent re-render.

If this is what you want, you have to specify the dependency array as empty. This means that there are no values the useMemo hook should watch. It should always returned the memoized output.

```jsx
// Import useMemo hook from React:
import { useEffect, useMemo, useState } from 'react'

export default function App() {
  // Create state for count:
  const [count, setCount] = useState(1)

  // Create computationally expensive function:
  const fibonacci = (num) => {
    return num === 2 ? 1 : num === 1 ? 0 : fibonacci(num - 1) + fibonacci(num - 2)
  }

  // Memoize fibonacci function:
  const memoizedVal = useMemo(() => fibonacci(count), [])
  // Above, the dependency array is empty. The useMemo will run only once.

  // Check if memoizedVal changes
  useEffect(() => {
    // This log will show only once because
    // useMemo will run only once.
    console.log(memoizedVal)
  }, [memoizedVal])

  return (
    <div className="App">
      <p>{count}</p>

      <button onClick={() => setCount(prevCount => prevCount += 1)}>Increase count</button>
    </div>
  )
}
```

The example above demonstrates that useMemo runs only after initial render. It will generate fibonacci number for the initial value of `count` state. When you increase the count, by clicking the button, value of `count` will increase. You can see this change in the paragraph above the button.

However, no log will show up. This is because the useMemo hook will not run the fibonacci function again. It will return the same value you got after the initial render. Since the value of `memoizedVal` is the same, the [useEffect hook] will not execute the `console.log()`. Remember, it watches only the `memoizedVal`.

### No.2: Only when dependency changes

The second option is to run useMemo, and execute the function you passed, again when specific value changes. This will be useful when the function you passed as an argument accepts some value from the outside. When this outside value changes you may want to re-calculate the output so the output is correct.

To do this, you have to specify the value you want to "watch" as one of the dependencies. useMemo will then watch this value and execute the function you passed every time the watched value changes. If it doesn't change, useMemo will return the memoized value, value from the last execution.

There is no limit to how many dependencies you can specify for the useMemo hook. If you want the hook to watch one, specify one. If you want it to watch 10, specify all ten. Just make sure to specify all dependencies you need and omit those you don't need. Otherwise, useMemo will re-execute the function too often or not often enough.

```jsx
// Import useMemo hook from React:
import { useEffect, useMemo, useState } from 'react'

export default function App() {
  // Create state for count:
  const [count, setCount] = useState(1)

  // Create computationally expensive function:
  const fibonacci = (num) => {
    return num === 2 ? 1 : num === 1 ? 0 : fibonacci(num - 1) + fibonacci(num - 2)
  }

  // Memoize fibonacci function:
  const memoizedVal = useMemo(() => fibonacci(count), [count])
  // Above, the "count" is specified as a dependency. When the value of "count" changes useMemo will run and execute fibonacci function.

  // Check if memoizedVal changes
  useEffect(() => {
    console.log(memoizedVal)
  }, [memoizedVal])

  return (
    <div className="App">
      <p>{count}</p>

      <button onClick={() => setCount(prevCount => prevCount += 1)}>Increase count</button>
    </div>
  )
}
```

In the second example, the useMemo watches the `count` value because it is specified as a dependency. Because of this, useMemo runs every time the `count` value changes and executes the fibonacci function. Every change of `count` also changes the input of the fibonacci function and also the output it returns.

Since execution of fibonacci function changes the `memoizedVal`, this also causes the useEffect hook to execute the `console.log`. As a result, new message with new value shows up in the console.

### No.3: After every re-render

The last option is to tell useMemo to re-run the function you passed on every re-render. This is kind of a nonsense. There is no reason to use useMemo to memoize something just to actually never memoize it. However, since this is possible, it is still an option. Warning: don't do this. It is dumb and waste of time.

Anyway... Let's say you are in a situation where this is the only option, which is incredibly unlikely to happen. In order to convince the useMemo hook to run on every render you have to omit the dependency array. Pass in only one argument, the function.

```jsx
// Import useMemo hook from React:
import { useEffect, useMemo, useState } from 'react'

export default function App() {
  // Create state for count:
  const [count, setCount] = useState(1)

  // Create computationally expensive function:
  const fibonacci = (num) => {
    return num === 2 ? 1 : num === 1 ? 0 : fibonacci(num - 1) + fibonacci(num - 2)
  }

  // Memoize fibonacci function:
  const memoizedVal = useMemo(() => fibonacci(count))
  // Above, no dependency array is specified. This will cause the useMemo to execute fibonacci function on every render.

  // Check if memoizedVal changes
  useEffect(() => {
    console.log(memoizedVal)
  }, [memoizedVal])

  return (
    <div className="App">
      <p>{count}</p>

      <button onClick={() => setCount(prevCount => prevCount += 1)}>Increase count</button>
    </div>
  )
}
```

In the last example, we removed the dependency array argument from the useMemo hook. The useMemo hook now watches basically everything that happens. When something happen, that will cause re-render, useMemo will also execute the fibonacci function. This will, in turn, change the `memoizedVal`.

This change will tell useEffect to execute the `console.log`. As a result, a new value of `memoizedVal` will show up in the console. To reiterate, don't do this. It doesn't make sense to use useMemo and then never let it memoize anything.

## Use useMemo hook with caution

Performance is important and it is easy to go over the edge when trying to optimizer everything. It is just as easy to over-use the React useMemo hook. Think before you decide to use useMemo hook. Remember that the hook itself introduces some overhead. The hook brings in new complex logic you have to take into account.

It can also create new performance issues, issue you didn't have before. When you memoize something, you store it in the memory. This gives more space for the CPU. However, there are still resources that are consumed. The only thing that changed is the type of resource it consumes.

So, use useMemo only for really expensive computations. Make sure you use that memory for things that can make a difference. Use profiling tools to identify those expensive computations, computations that use a lot of resources. Try to optimize these with useMemo and see if the profile changes for the better.

Additional warning. Don't rely on useMemo too much. As is mentioned in the [React docs], useMemo doesn't guarantee you to execute the function only when dependencies change. React may also choose to remove memoized values and recalculate them so it can free up memory. So, make sure your code works without useMemo as well.

One more thing. Don't use functions you passed to useMemo hook to create side effects. Side effects should be made inside the useEffect hook. Also, don't use useMemo to update state values. This is also a side effect, but it is important to mention it. Use useMemo only for what it is intended, to memoize output values.

## Conclusion: The React useMemo hook made simple

The React useMemo hook can be useful when you look for ways to improve performance of your React applications. It can help you optimize expensive computations. by memoizing output of these computations and re-run them only when necessary. I hope that this tutorial helped you understand what the useMemo hook is, how it works and also how to use it.

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
