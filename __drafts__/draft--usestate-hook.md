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

You can use any name for the state and the update function you want. In other words, the "count" and "setCount" can be anything you want. The only rule to remember is that it must be [valid variable name]. It is a good practice to start the name for the update function with "set". This is a preferred naming convention and you will see it very often.

## Creating state with initial value

The useState hook allows you set an initial value for every state you create. You can set this initial value by passing it as an argument to the useState hook when you declared it. This initial value can be any valid [data type] in JavaScript. You can also leave the argument empty and create state without any initial value.

```jsx
// Create function component:
function App() {
  // Declare new state without initial value:
  const [count, setCount] = useState()

  // Declare new state with string as initial value:
  const [word, setWord] = useState('Hello!')

  // Declare new state with number as initial value:
  const [num, setNum] = useState(0)

  // Declare new state with array as initial value:
  const [series, setSeries] = useState([0, 1, 2, 3])

  // Declare new state with object as initial value:
  const [person, setPerson] = useState({
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

### Lazy initialization

There might be situations where you will need to perform some expensive operation and use the result as a state value. That said, you may need to perform this operation only once, on the initial render. You can do this with the useState hook. As you know, when you declare new state, you can provide it with some initial value.

There another option. You can also pass in a function as an argument to useState hook. The useState hook will execute this function, but only on the initial render, to get the initial state. If you component re-renders, the function will not be executed again.

```jsx
// Some expensive operation:
function generateNumber() {
  return Math.floor(Math.random() * 1024)
}

// Create function component:
function App() {
  // Declare new state with lazy initialization:
  const [state, setState] = useState(() => generateNumber())

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
        * Attach the input handler that updates "name" state:
      */}
      <input
        value={name}
        onChange={onInputChange}
      />
    </div>
  )
}
```

## Updating state with previous state

This can be handy. The update function accepts a callback function as an argument. The update function also passes the previous state an argument to this callback. This allows you to work with the latest state when you want to update it. So, if you need to know previous state, pass a callback function instead of a value.

Then, inside this callback function you can use the previous state to do whatever you want. This previous state will be passed into the callback by the update function. You just have to specify it as an argument.

```jsx
// Create function component:
function App() {
  // Declare state for clicks:
  const [clicks, setClicks] = useState(0)

  // Create button handler that will update the state:
  const onButtonClick = () {
    // Use callback function and previous state
    // to update the state.
    // Make sure to specify the argument
    // for the previous state ("prevState" for example).
    setName(prevState => prevState + 1)
  }

  return (
    <div>
      {/* Read from the "name" state. */}
      <p>You clicked: {clicks}</p>

      {/*
        * Attach the button handler that updates "clicks" state:
      */}
      <button
        type="button"
        onChange={onButtonClick}
      >Click</button>
    </div>
  )
}


// Alternative:
function App() {
  // Declare state for clicks:
  const [clicks, setClicks] = useState(0)

  return (
    <div>
      {/* Read from the "name" state. */}
      <p>You clicked: {clicks}</p>

      {/*
        * Attach the button handler that updates "clicks" state:
      */}
      <button
        type="button"
        onChange={() => setName(prevState => prevState + 1)}
      >Click</button>
    </div>
  )
}
```

### Previous state and handling objects and arrays

Working with previous state in update function can be especially useful in two cases. The first one is if your state is an array. Second one is if your state is an object. In both cases, setting new state will overwrite the whole state. In other words, if you try to change one object property, it will rewrite the whole object.

Similar thing will happen with arrays. Trying to add new item to an array will result in rewriting the whole array. Sure, you can use the variable for current state. However, this doesn't guarantee that state will be the latest. It can happen that state variable will be old due to how state works.

Previous state passed into the callback helps you avoid this because it will always know the latest state. With state in the form of an object, you can update individual properties and their values with the help of previous state and [spread]. Spread will also help you insert new items to an array without rewriting.

```jsx
// Updating state with an array:
// Create function component:
function App() {
  // Declare state for clicks:
  const [names, setNames] = useState(['Andrew', 'Jill'])

  // Create handler that will update the "names" state:
  const addNameToState = (name) {
    // New name will be passed as an argument.
    // We will insert the name, along with current content
    // of "names" state array, and set it as a new state.
    setNames(prevState => [name, ...prevState])

    // Hypothetical result:
    // ['some new name will be here', 'Andrew', 'Jill']
  }

  return (
    <div>{/* ... */}</div>
  )
}


// Updating state with an object:
// Create function component:
function App() {
  // Declare state for clicks:
  const [person, setPerson] = useState({
    name: 'Joshua Pink',
    email: 'joshua@pink.com',
    age: 37,
  })

  // Create handler that will update the "person" state:
  const addNameToState = (prop, value) {
    // The property to update, and new value,
    // will be passed as an argument.
    // We will insert the name, after the current content
    // of "person" state object.
    // To ensure only new key-value pair will be updated,
    // use spread with previous state first.
    // This will add all existing properties
    // and the new one on top.
    setNames(prevState => {
      ...prevState, // Spread the previous state.
      [prop]: value // Update only the relevant property.
    })

    // Hypothetical result:
    // setNames(prevState => {
    //   ...prevState,
    //   age: 42
    // })

    // {
    //   name: 'Joshua Pink',
    //   email: 'joshua@pink.com',
    //   age: 42,
    // }
  }

  return (
    <div>{/* ... */}</div>
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

## Conclusion: React useState Hook in Action

The React useState hook can be very useful for managing state of component and even the whole application. It makes state management simple with only a small amount of code. I hope that this tutorial helped you understand what the useState hook is about and how to use it in your React projects.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[documentation]: https://reactjs.org/docs/hooks-rules.html
[array destructuring]: https://blog.alexdevero.com/destructuring-assignment-javascript/#destructuring-arrays
[data type]: https://blog.alexdevero.com/javascript-basics-data-types-pt1/
[valid variable name]: https://blog.alexdevero.com/javascript-variables-introduction/#naming-variables
[spread]: https://blog.alexdevero.com/javascript-spread-operator/

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
