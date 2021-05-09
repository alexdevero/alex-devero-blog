# Reacts useRef Hook: What It Is and How to Use It

React useRef hook can be helpful when you need to store references to elements. It can be also useful when you want to store values without causing your components to re-render. In this tutorial, you will learn about what React useRef hook is, how it works and how to use it.

<!--more-->
<!--
Table of Contents:
## h2
### h3
### h3
## h2
## Conclusion: [...] ...
-->

## React useRef hook briefly

The useRef hook may not be as popular as other hooks such as [useState], [useEffect] and [useReducer]. Due to this, it may not be clear what is the purpose of this hook. Nonetheless, useRef hook can be very useful in certain situations. The ref, in useRef, is a shorthand for "reference".

What this hook does is it allows you to store data, and persist them across renders. What's even more interesting and important, this hook does this without causing the component to re-render. This means that when you update the value stored by useRef, React will not re-render your component.

The most common use case for the useRef hook is to store references to DOM nodes and React elements. This then allows you to access these nodes directly and work with them as you need. This is similar to using JavaScript `querySelector()` method to find DOM node and storing the node in a variable.

## Using the useRef hook

Using the useRef hook requires few steps. The first step is about initializing the hook. You initialize the useRef hook by calling it and storing it in a variable. You can also pass some value to the hook as an argument. React will use this value as the initial value for the hook.

When the useRef is used to store references to DOM nodes or React elements, developers usually set the initial value to `null`. When you initialize the hook, it will return an object. This object contains property called `current`. The initial value you used for the hook will become the value of this property.

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
