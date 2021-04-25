# React useState Hook in Action: What You Need to Know

The React useState hook is one of the most popular hooks in React. This hook makes it easy to manage state within your function components. It is also very simple to use. In this tutorial you will learn what useState hook is and how to use it in your React applications.<!--more-->
<!--
Table of Contents:
-->

## A brief introduction to React hooks

React hooks are feature introduced in React 16.8. Under the hood, hooks are functions. These functions allow you to work with component state and lifecycle. Both these things were previously possible only with classes. The introduction of hooks changed this, and made functional components much more powerful.

## A quick introduction to React useState hook

One of these hooks that come with React is also the useState hook. This hook focuses on one specific thing. It allows you to add state to your function components. This means that you no longer have to work with class components. You also no longer have to convert function components to classes just so you can use state.

## Getting started with React useState

The first step to use useState hook is to declare it in your function component. Well, after you import it in your file where you want to use it. When you declare it, useState will return an array with two values. The first value is the actual state. Value allows you to read the current state.

The second value is a function. This function allows you to update the state, or its value. Since it returns an array, there are two ways to declare this hook. First, you can use array indices. Second, you can use [array destructuring]. The second approach is much more popular and you will see it very often.

```jsx
// Create function component:
function App() {
  // Declare useState hook with destructuring:
  // count: the current state (its value).
  // setCount: function that allows update the state.
  const [count, setCount] = useState()

  return (
    <div>
      {/* ... */}
    </div>
  )
}

// Create function component:
function App() {
  // Declare useState hook with array indices:
  const countArray = useState()
  const count = countArray[0] // The state.
  const setCount = countArray[1] // The update function.

  return (
    <div>
      {/* ... */}
    </div>
  )
}
```

You can use any name for the state and the update function you want. The only rule to remember is that it must be [valid variable name]. It is a good practice to start the name for the update function with "set". This is not a rule, and you don't have to follow it. However, it is a preferred naming convention and you will see it very often.


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
