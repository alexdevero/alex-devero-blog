# How to Create Your Own React Custom Hooks

React offers a number of built-in hooks you can use right away. Aside to these, you can also create your own custom hooks. In this tutorial, you will learn what React custom hooks are and how to create your own. You will also learn what rules you have to follow when creating custom hooks.

<!--more-->
<!--
Table of Contents:
## A quick overview of React hooks
## An introduction to React custom hooks
## Rules of hooks
## Building your own React custom hooks
### Example no.1: useWindowSize hook
### Example no.2: useToggle hook
### Example no.3: useLocalStorage hook
## Conclusion: How to create your own React custom hooks
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

The second rule is that you should call hooks only from React function components or other hooks. There is also one practice for creating custom hooks. Always start the name of the hook with "use" prefix. This is more like a good rule of thumb than a rule. It is good to follow to make code more readable, but it is not required.

## Building your own React custom hooks

React custom hooks are JavaScript functions. This means few things. First, when you create a custom hook you are writing a function. Second, function name should start with "use". Remember, this is a good rule of thumb for creating custom hooks. Third, you can use other React hooks inside your custom hooks.

These are the things to remember. To make this more hands-on, let's put this together and create few examples of React custom hooks. This can make it easier to understand how custom hooks work and how to create them.

### Example no.1: useWindowSize hook

The first example will be a hook that will return current window size. First, the name. The name should be descriptive and start with "use". Something like "useWindowSize" sounds like a good candidate. Second, the logic of the hook. When you call this hook, it will do few things.

The first thing it will do is getting the current window size and returning it. Second, it will attach event listener to `window` object and listen to `resize` event. When this event happens, the hook will detect the new window size and return it again. This will repeat every time the `resize` event happens.

Custom hooks can use other React hooks. This means that we can use useState hook to store the latest window dimension in a state and return the value of this state. We can also use useEffect hook to attach the event listener for `resize` event. We can use this useEffect hook to remove the event listener.

We can do this by returning a clean up function. This function will call the `removeEventListener` method, passing the `resize` event and function for handling the resize.

```JavaScript
// Import useEffect and useState hooks from React:
import { useEffect, useState } from 'react'

// Create custom useWindowSize hook function:
export function useWindowSize() {
  // Create function to get current window size:
  const getWindowSize = () => ({
    innerHeight: window.innerHeight,
    innerWidth: window.innerWidth,
    outerHeight: window.outerHeight,
    outerWidth: window.outerWidth,
  })

  // Create state for window size data:
  const [windowSize, setWindowSize] = useState(getWindowSize())
  // It also uses the getWindowSize() to set the initial state.

  // Create handler function for resize event:
  function handleResize() {
    // Update state value:
    setWindowSize(getWindowSize())
  }

  // Create a side-effect
  useEffect(() => {
    // Attach event listener for "resize" event:
    window.addEventListener('resize', handleResize)

    return () => {
      // Remove event listener for "resize" event:
      window.removeEventListener('resize', handleResize)
    }
  }, [])

  // Return current window size:
  return windowSize
}
```

When you want to use this hook, import it in your React component and call it. Remember to assign that call to variable so that you can get the window size every time it changes.

```jsx
// Import the useWindowSize hook:
import { useWindowSize } from './hook'

export default function App() {
  // Call the useWindowSize hook and assign it to variable:
  const windowSize = useWindowSize()

  // Display the current window size:
  return (
    <div>
      <ul>
        <li>window inner width: {windowSize.innerWidth}</li>
        <li>window inner height: {windowSize.innerHeight}</li>
        <li>window outer width: {windowSize.outerWidth}</li>
        <li>window outer height: {windowSize.outerHeight}</li>
      </ul>
    </div>
  )
}
```

### Example no.2: useToggle hook

Another simple but useful hook can be hook for managing toggle state. Such a hook could be useful for creating collapsible components for example. It could help you check for current toggle state and switching between "on" and "off" state. It could also allow to reset the state or set it manually.

This hook will be simple. It will use useState hook to store toggle state. Aside to this, it will have two functions, `handleReset` and `handleToggle`. The `handleReset` will reset the toggle state to the initial value. The `handleToggle` will reverse current toggle state. It switch from "on" to "off" and the other way around.

The value we will return from this hook will be an object. This object will contain all these methods and current value of the toggle state. We will also return the setter method for state to allow setting custom state. When you import this hook, you will be able to import anything inside the object it returns.

```JavaScript
// Import useEffect and useState hooks from React:
import { useState } from 'react'

// Create custom useToggle hook function:
export function useToggle(initialState = false) {
  // Create toggle state:
  const [toggle, setToggle] = useState(initialState)

  // Create handler function for resetting the state:
  const handleReset = () => setToggle(initialState)

  // Create handler function for toggling the state:
  const handleToggle = () => setToggle(prevState => !prevState)

  // Return the state, state setter function and handler functions:
  return {
    on: toggle,
    set: setToggle,
    reset: handleReset,
    toggle: handleToggle
  }
}
```

Just like with the previous hook, you can now import this useToggle in your React component. When you call it, you can use [destructuring assignment] to assign anything from the object this hook returns to a variable so you can use it.

```jsx
// Import the useToggle hook:
import { useToggle } from './hook'

export default function App() {
  // Call the useToggle hook and assign variables,
  // using destructuring assignment:
  const { on, set, reset, toggle } = useToggle()

  // Use any method or state returned from the hook:
  return (
    <div>
      <p>On: {on ? 'true' : 'false'}</p>

      <button onClick={() => set(true)}>Set to on</button>
      <button onClick={reset}>Reset</button>
      <button onClick={toggle}>Toggle</button>
    </div>
  )
}
```

### Example no.3: useLocalStorage hook

Third and last example. It became popular to store application or website data in local or session storage. This hook will accept two parameters: name of the key to store and initial value for this key. When called, this hook will first check if local storage is available in the browser.

If local storage is not available, it will return the initial value passed as argument. If local storage is available, it will check if any key with the same name exists. If it does, it will retrieve its data. Otherwise, it will return the initial value. Whatever is returned will become the state of the hook.

This all will happen during the initial load. It will happen inside initializer function for useState hook. The second part of the hook will be a handler function for storing data in local storage. This function will accept one parameter, the data to store. It will first take this value and store it inside the hook state.

Then, it will store the value in local storage. The name of the key for this data will be the name of the key passed to the hook during the call. The last part, returning something. This hook will return two things: current value of the state, data loaded from local storage, and handler function for storing data in local storage.

```JavaScript
// Import useState hook from 'react':
import { useState } from 'react'

export function useLocalStorage(keyName, initialValue) {
  // Create state for local storage:
  const [storedValue, setStoredValue] = useState(() => {
    try {
      // Check if local storage is available:
      if (typeof window === 'undefined') {
        return initialValue
      }

      // Check if item with the same name exists in local storage:
      const item = window.localStorage.getItem(keyName)

      // Return parsed data from storage or return the initialValue:
      return item !== null ? JSON.parse(item) : initialValue;
    } catch (error) {
      // Catch any errors and log them:
      console.log(error)

      // Return the initialValue:
      return initialValue
    }
  })

  // Create handler function for storing value in local storage:
  const setValue = (value) => {
    try {
      // Store the value in the state:
      setStoredValue(value)

      // Store the value in local storage:
      window.localStorage.setItem(keyName, JSON.stringify(value))
    } catch (error) {
      // Catch any errors and log them:
      console.log(error)
    }
  }

  // Return latest data and handler function for storing new data:
  return [storedValue, setValue]
}
```

The way to use this hook will be similar to using useState. When you call it, you pass in the name of the key and data for that key. The hook will return array with the data and handler function for storing new data. The data returned will be either the initial value or any data that are already stored in local storage for that key.

```jsx
// Import the useLocalStorage hook:
import { useLocalStorage } from './hook'

export default function App() {
  // Call the useLocalStorage hook and assign variables,
  // again, using destructuring assignment:
  const [value, setValue] = useLocalStorage('name', 'Joe')

  // Store data typed in the input in local storage
  // and also display them in the DOM:
  return (
    <div>
      <p>{value}</p>

      <input type="text" onChange={(e) => setValue(e.currentTarget.value)} />
    </div>
  )
}
```

## Conclusion: How to create your own React custom hooks

Official React hooks are very useful tools for every React developer. However, these official hooks can 't do everything you may want or need. Writing your own React custom hooks can help you solve this problem. I hope that this tutorial helped you learn what React custom hooks are, how they work and how to create your own.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->

[hooks]: https://reactjs.org/docs/hooks-intro.html
[react v16.8]: https://reactjs.org/blog/2019/02/06/react-v16.8.0.html
[javascript classes]: https://blog.alexdevero.com/get-started-with-javascript-classes/
[javascript functions]: https://blog.alexdevero.com/javascript-functions-pt1/
[usestate]: https://blog.alexdevero.com/react-usestate-hook-in-action/
[useeffect]: https://blog.alexdevero.com/react-useeffect-hook/
[rules of hooks]: https://reactjs.org/docs/hooks-rules.html
[destructuring assignment]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment

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
