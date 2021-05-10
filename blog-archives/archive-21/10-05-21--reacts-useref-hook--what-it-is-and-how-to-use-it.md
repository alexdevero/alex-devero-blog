# Reacts useRef Hook: What It Is and How to Use It

React useRef hook can be helpful when you need to create mutable variables in your components without causing these components to re-render. For example, store references to elements or some other values. In this tutorial, you will learn about what React useRef hook is, how it works and how to use it.<!--more-->
<!--
Table of Contents:
## React useRef hook briefly
## Using the useRef hook
### Storing references to nodes and elements
### useRef hook and storing values
### Storing previous state values with React useRef hook
## Updating values, re-renders and updating UI
## A word of caution
## Conclusion: Reacts useRef Hook
-->

## React useRef hook briefly

The useRef hook may not be as popular as other hooks such as [useState], [useEffect] and [useReducer]. Due to this, it may not be clear what is the purpose of this hook. Nonetheless, useRef hook can be very useful in certain situations. The ref, in useRef, is a shorthand for "reference".

What this hook does is it allows you to store data, and persist them across renders. What's even more interesting and important, this hook does this without causing the component to re-render. This means that when you update the value stored by useRef, React will not re-render your component.

The most common use case for the useRef hook is to store references to DOM nodes and React components. This then allows you to access these nodes directly and work with them as you need. This is similar to using JavaScript `querySelector()` method to find DOM node and storing the node in a variable.

## Using the useRef hook

Using the useRef hook requires few steps. The first step is about initializing the hook. You initialize the useRef hook by calling it and storing it in a variable. You can also pass some value to the hook as an argument. React will use this value as the initial value for the hook.

When the useRef is used to store references to DOM nodes or React components, developers usually set the initial value to `null`. When you initialize the hook, it will return an object. This object contains property called `current`. The initial value you used for the hook will become the value of this property.

```jsx
// Import useRef hook from React:
import { useRef } from 'react'

// Create function component:
const App = () => {
  // Initialize the useRef hook
  // with null as initial value:
  const myRef = React.useRef(null)
  // Note:
  // The value of myRef now: { current: null }

  return (
    <div className="app">
      <div className="app-wrapper">
        <p>Hello from the metaverse!</p>
      </div>
    </div>
  )
}
```

### Storing references to nodes and elements

The next steps depend on what you want to do. You use the hook to store references to DOM node or React element. To do this, you find the node or element and add `ref` attribute. The value for this attribute will be the initialized useRef hook. You will pass the variable name to this attribute.

When you do this, the value of `current` property returned by the ref object will be the element. From now, you will be able to access the element by using this `current` property on the ref.

```jsx
// Import useRef hook from React:
import { useRef } from 'react'

// Create function component:
const App = () => {
  // Initialize the useRef hook:
  const inputRef = useRef(null)

  // Create button click handler:
  const onButtonClick = () => {
    // Log the value of input:
    console.log(inputRef.current.value)
  }

  return (
    <div className="app">
      <div className="app-wrapper">
        <p>What's your name?</p>

        {/*
          Add ref "attribute" to the input
          and pass in the created ref as a value:
        */}
        <input ref={inputRef} />

        {/* Create button */}
        <button onClick={onButtonClick}>Load text</button>
      </div>
    </div>
  )
}
```

### useRef hook and storing values

Just as useRef can store references to nodes and elements it can also store values. This can be handy when you want to store values without triggering re-render. You can't do this with useState hook. Every update of a state value will cause re-render. That said, this is a feature, not a bug.

You want to keep your component in sync with state. This is one thing useState was created to do. Using useRef hook allows you to bypass this by directly manipulating with the value of `current` property. This property is not read-only. You can change its value manually. This allows you to use useRef to store anything you want.

When you want to use useRef to store values and update them remember that these updates are side effects. As such, you should do these updates in the "layout" or "commit" phase. This is a phase when React applies any changes. To make updates to ref vales during this phase you can use `useLayoutEffect` or `useEffect` hooks.

Aside to these two, another option for these updates are handler functions. You can create function to handle specific actions. Then, you can update ref values inside these functions. Whatever option you choose, avoid updating ref in the root of your React components.

```jsx
// Import useEffect and useRef hooks from React:
import { useEffect, useRef } from 'react'

// Create function component:
const App = () => {
  // Initialize the useRef hook with 1 as initial value:
  const renderCount = useRef(1)

  // Don't do this - update values in root:
  renderCount.current += 1

  useEffect(() => {
    // Use useEffect to update "current" value
    // on every render of the component:
    renderCount.current += 1
  }, [])

  // Using handler function:
  const onIncrementRenderCount = () => {
    // Update "current" value manually:
    renderCount.current += 1
  }

  // NOTE: this log will not show up if you update
  // the value by clicking on the "Increment count" button.
  // useRef doesn't cause re-renders.
  console.log('Rendered!')

  return (
    <div className="app">
      <div className="app-wrapper">
        {/* Show the number of renders: */}
        <p>Number of renders: {renderCount.current}</p>

        {/* Add button to ref's current value: */}
        <button onClick={onIncrementRenderCount}>Increment count</button>
      </div>
    </div>
  )
}
```

### Storing previous state values with React useRef hook

One interesting use case for useRef hook is storing previous state values. The useRef hook persists values between renders. With the help of `useEffect` hook, you can store value of state in a ref before the value changes. This will make the old value available in the next render, through the ref.

```jsx
// Import useEffect, useRef and useState hooks from React:
import { useEffect, useRef, useState } from 'react'

// Create function component:
const App = () => {
  // Add state for name:
  const [name, setName] = useState('')

  // Use useRef hook to store reference to input:
  const inputRef = useRef('')

  // Use useRef hook to store previous name:
  const oldNameRef = useRef('')

  useEffect(() => {
    // On re-render, store the old name in ref:
    oldNameRef.current = name
  }, [name])

  const onSaveNameButtonClick = () => {
    // Update the value of name state,
    // and trigger re-render:
    setName(inputRef.current.value);

    // This will also trigger the useEffect which
    // will update the ref's value with the previous
    // value of "name" state.
  }

  return (
    <div className="app">
      <div className="app-wrapper">
        <input defaultValue={name} ref={inputRef} />

        <p>New name: {name}</p>
        <p>Previous name: {oldNameRef.current}</p>

        <div>
          {/* Add button to save name: */}
          <button onClick={onSaveNameButtonClick}>Save name</button>
        </div>
      </div>
    </div>
  )
}
```

## Updating values, re-renders and updating UI

One thing to keep in mind. In the example with updating values manually, click on the button will update the value. However, change of the value will not cause re-render. So, you will still see the same value until something causes the component to re-render and the UI to update itself with the latest value.

You can test that the ref value is really updated by triggering re-render manually. For example, you can add new state. When you update the state with new value it will also trigger re-render. The re-render will update the UI. After this update the UI will also show the latest value of ref.

```jsx
// Import useEffect, useRef and useState hooks from React:
import { useEffect, useRef, useState } from 'react'

// Create function component:
const App = () => {
  // Initialize the useRef hook:
  const renderCount = useRef(1)

  // Add state to trigger re-render:
  const [count, setCount] = useState(1)

  useEffect(() => {
    // Use useEffect to update "current" value
    // on every render of the component:
    renderCount.current += 1
  }, []);

  const onIncrementRenderCount = () => {
    // Update "current" value manually:
    renderCount.current += 1
  };

  const onIncrementCount = () => {
    // Update state value:
    setCount((prevCount) => (prevCount += 1))
    // Note: this will trigger re-render.
  }

  return (
    <div className="app">
      <div className="app-wrapper">
        {/* Show the number of renders: */}
        <p>Number of renders: {renderCount.current}</p>

        {/* Add button to ref's current value: */}
        <button onClick={onIncrementRenderCount}>Increment count</button>

        {/* Add button to increase state value (trigger re-render): */}
        <button onClick={onIncrementCount}>Increment state</button>
      </div>
    </div>
  )
}
```

## A word of caution

The useRef hook makes it very easy to work with DOM nodes and React components. This can make it tempting to use it every time you want to communicate with your components or between them. This is generally not a good idea. It is usually better to create these communication bridges by using props and passing data through them.

This is one of the things the system of props was designed for. It is also probably the most reliable way to establish this communication between components. So, use useRef when you really need to, when you need to work with components and props are not capable of doing the job.

## Conclusion: Reacts useRef Hook

The React useRef hook can be handy. It allows you to store data between renders and update this data without causing a re-renders. You can also use it to store references to DOM nodes and React components so you can work with them directly. I hope that this tutorial helped you understand what the useRef hook is and how to use it.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[useState]: https://blog.alexdevero.com/react-usestate-hook-in-action/
[useEffect]: https://blog.alexdevero.com/react-useeffect-hook/
[useReducer]: https://reactjs.org/docs/hooks-reference.html#usereducer

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
