# React useEffect Hook Demystified: What You Need to Know

The React useEffect Hook helps you manage side-effects in functional React components. It also makes this task much easier than it used to be. In this tutorial you will learn about what useEffect hook is and how it works. You will also learn how to use it in your React applications.<!--more-->

## Introduction to React useEffect hook

If you are familiar with React class components you know there are lifecycle methods available to use. You can use these methods to execute code at a specific moment you need. You can execute your code only when on component's initial render. You can also execute it on very re-render of the component, or if only some data change.

These lifecycle methods, along with other features of class components, don't work with functions. These methods doesn't exist in their scope or environment. React hooks made it possible to bring many of these features from classes to functional components so you can use them here as well.

The React useEffect hook is a hook that brings the functionality of lifecycle methods to functional components. To make this easier, you can think about the useEffect hook as `componentDidMount`, `componentDidUpdate` and `componentWillUnmount` lifecycle methods in one package.

That said, there are some differences between useEffect hook and lifecycle method. One difference is that useEffect hook runs after render. It runs after the first render, and also after every next update. It doesn't run before it. This makes it easy to execute any code right after a component is rendered.

Another difference is that, by default, useEffect hook runs after every render. Fortunately, there is a way to prevent this behavior. When you use the useEffect hook, there is an option you can use to say when you want the useEffect hook to run. The hook will than run only under correct conditions and ignore others.

Another useful feature of useEffect hook is that it can also clean up after itself. This cleanup happens automatically before the hook is executed again. One example when cleanup can be handy is removing attached event listeners when you "change" page in your React application.

### A word on side-effects

The name useEffect is based on the idea of [side-effects]. Put simply, side-effects are changes made by a function to anything other than inputs provided to that function. This usually means changes made to the outside world. Some examples of side-effects can be fetch requests and direct manipulation with DOM.

Another example can be using timer functions like `setTimeout()` and `setTimeout()`. One problem can be synchronizing the rendering of a component with side-effect you want to make. These two things happen independently and component rendering is outside of your control. This is one thing the React useEffect hook is trying solve.

The useEffect hook allows you to extract side-effects into a function that is proved and managed by React itself. All you have to do is to say what is the side-effect you want and when it should be executed. React will take care of the rest. This function provided and managed by React is the useEffect hook.

## The syntax

The useEffect hook accepts two arguments. The first argument is a callback function. This callback function contains the code you want to execute. This is the side-effect you want to make. The useEffect hook executes this callback function after the component is rendered. The second argument is for array of dependencies.

This argument is optional. Whether you use it or not will depend on when you want the useEffect hook to execute the callback function. Above, I mentioned that there is an option to specify when the useEffect hook should run. This array of dependencies is this option. By working with it you change how the useEffect hook behaves.

```JavaScript
// Syntax of useEffect hook:
useEffect(callback, [dependencies]);


// Simple example:
// Import useEffect hook from React.
import { useEffect } from 'react'

function App() {
  // Use useEffect hook:
  useEffect(() => {
    // Execute some code.
  }, [])
  // ...
}
```

## Dependencies

The dependencies array is an optional argument. Nonetheless, it is a very powerful feature. By providing different values, or omitting it, you can fundamentally change when the useEffect hook will run. Dependencies give you three options for when the useEffect hook should run.

### No.1: Run after every render

THe first option is to run the useEffect hook after every render of your component. For this, omit the dependencies array and provide only the callback function. From now, every time React renders your component, it will also run the useEffect hook and execute the code inside it.

```JavaScript
// Import useEffect hook from React.
import { useEffect } from 'react'

function App() {
  // Use useEffect hook:
  useEffect(() => {
    // Run something after every render.
  }) // <= Omit the dependencies argument.
}
```

### No.2: Run after initial render

Another option is to run the useEffect hook only once, after the initial render. This is the very first render of the component. From now, if React re-renders the component, the useEffect hook will not run again.

```JavaScript
// Import useEffect hook from React.
import { useEffect } from 'react'

function App() {
  // Use useEffect hook:
  useEffect(() => {
    // Run something only after initial render.
  }, []) // <= Pass [] as dependencies argument.
}
```

### No.3: Run when specific value changes

The third and last option is to watch specific value and run the useEffect hook when this value changes. This value can be almost anything. It can be all component props or just one specific prop. It can be some variable. It can also be a state created with [useState hook].

When you know what value you want to watch, you pass that value into the dependencies array. What if you want to watch more than one value? No problem. You can pass as many values to the dependencies array as you want. Then, when just one of these values changes, the useEffect hook will run.

```JavaScript
// Import useEffect and useState hooks from React.
import { useEffect, useState } from 'react'

function App(props) {
  // Create states:
  const [name, setName] = useState('')
  const [age, setAge] = useState(0)

  // Use useEffect hook:
  useEffect(() => {
    // Run something only when props.isLoading prop,
    // name state or age state changes.
  }, [props.isLoading, name, age]) // <= Pass props.isLoading, name, age as dependencies argument.
}
```

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
