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

## Creating state with initial value

The useState hook allows you set an initial value for every state you create. You can set this initial value by passing it as an argument to the useState hook when you declared it. This initial value can be any valid [data type] in JavaScript. You can also leave the argument empty and create state without any initial value.

```jsx
// Create function component:
function App() {
  // Declare new state without initial value:
  const [count, setCount] = useState()

  // Declare new state with string as initial value:
  const [count, setCount] = useState('Hello!')

  // Declare new state with number as initial value:
  const [count, setCount] = useState(0)

  // Declare new state with array as initial value:
  const [count, setCount] = useState([0, 1, 2, 3])

  // Declare new state with object as initial value:
  const [count, setCount] = useState({
    name: 'Joe Doe',
    email: 'joe@doe.com'
  })

  return (
    <div>
      {/* ... */}
    </div>
  )
}
```

## Reading the state

When you want to read the state, access its value, you use the variable the hook returned. Remember to use the state variable. Don't try to use the update function to do this. On the same token, don't try to update the state by modifying the variable. Instead, use the update function for that specific state.

```jsx
// Create function component:
function App() {
  // Declare states for name and age:
  const [name, setName] = useState({
    firstName: 'Jack',
    lastName: 'Doer'
  })
  const [age, setAge] = useState(33)

  return (
    <div>
      {/* Read from the "name" state. */}
      <p>Hello, my name is: {name.firstName} {name.lastName}</p>

      {/* Read from the "age" state. */}
      <p>My age is: {age}</p>
    </div>
  )
}
```

## Updating state with update function

The simplest way to update existing state is by using update function returned for that state. This is important to remember. If you have multiple states, update specific state only with function associated with that state. Don't try to use different functions for updating different states.

```jsx
// Create function component:
function App() {
  // Declare state for name:
  const [name, setName] = useState('')

  return (
    <div>
      {/* Read from the "name" state. */}
      <p>Hello, my name is: {name}</p>

      {/*
        * Set "name" state is input value
        * and update the state on input change.
      */}
      <input
        value={name}
        onChange={(event) => setName(event.target.value)}
      />
    </div>
  )
}


// Alternative:
function App() {
  // Declare state for name:
  const [name, setName] = useState('')

  // Create input handler that will update the state:
  const onInputChange = (event) {
    setName(event.target.value)
  }

  return (
    <div>
      {/* Read from the "name" state. */}
      <p>Hello, my name is: {name}</p>

      {/*
        * Set attach the input handler that updates "name" state:
      */}
      <input
        value={name}
        onChange={onInputChange}
      />
    </div>
  )
}
```

## Some limitations

Hooks are great. Nonetheless, there are two important things to remember. The first one is that you can't use hooks in class components. Hooks work only with function components. If you try to use hook in a class component React will complain. This makes sense. Hooks bring functionality available to classes to function components.

Why bring this functionality back to classes if it is already there? To make your life, and development, easier use hooks only in function component. The second thing is that hooks can be declared only in the root of your function component. You can't declare them inside another functions that are inside your components.

That said, the variables you declared for hooks are not restricted in scope. You can use them anywhere in the component. This also includes any inner functions of your function components. You can read about this, and other, "rules of hooks" in official React [documentation].

```jsx
// This will work:
function App() {
  // Hook is declared in the root of function component.
  const [count, setCount] = useState(0)

  return (
    <div>
      {/* ... */}
    </div>
  )
}


// This will not work:
function App() {
  function onButtonClick = () => {
    // Hook must be declared in the root of function component.
    // It must be declared outside this function.
    // Then, the "count" and "setCount" can be used here.
    const [count, setCount] = useState(0)
  }

  return (
    <div>
      {/* ... */}
    </div>
  )
}
```

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
