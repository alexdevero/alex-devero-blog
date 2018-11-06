# Introduction to [React Hooks] - How to Get Started

Have you heard about this new feature called React hooks? A lot of people in React community are talking about them. Some people even call this feature a game changer. This brings a few questions. What are React Hooks? Why are they so hot? And, finally, how can we use them? This article will give you answers to all these questions!

<!--
Table of Contents:
## What are React hooks?
## Functional components on steroids and more freedom
## Custom React hooks allowed
## A game changer
## From theory to practice
### useState
### useEffect
### useContext
## Epilogue: Introduction to React Hooks
-->

## What are React hooks?

You probably know that when you work with React class components you can use features such as [state]. In the end, that is why these components are also called stateful. You also probably know that every class component have [lifecycle methods] you can use. For example, `componentWillUnmount()`, `componentDidMount()`, `componentWillUnmount()`, etc.

None of this applies to functional or stateless components. Stateless components can't use their own `state` and don't have lifecycle methods. This is also why we can't use functional components in every situation. Sometimes, we just have to use class component, or `PureComponent`, because functional component is not equipped to do the job.

This is no longer the truth with the introduction of React hooks. Put simply, React hooks allows us to take a React functional component and add `state` and lifecycle methods to it. Well, we are actually not adding a `state` to it. More precise will be saying that we are "hooking" the component into `state` and lifecycle methods.

## Functional components on steroids and more freedom

Yes, that's correct. Hooks allows functional components to use lifecycle methods, the features that were available only for class-based components. This means that we are no longer limited by the functionality of components. So, if you prefer to use functional components, the need to work with a `state` or lifecycle methods will prevent you from doing so.

Let's say that we decide to use a functional component. A few days later we find out that it has to handle `state` or use some lifecycle methods. This is not a problem. We don't have to rewrite our component into a class. All we need is to use a React hook. React hooks will give us access to both no matter if the component we are currently working with.

Yes, we can work with stateful or stateless components and use `state` and lifecycle methods as we wish. When you think about it, React hooks will help us transform what was previously a stateless component into stateful. All we need is to choose, import and use specific hook.

## Custom React hooks allowed

What if we can't find one that suits our current needs? This can happen. Especially since there are currently three basic hooks-`useState()`, `useEffect()` and `useContext()`. Aside to these, there also a few additional hooks-`useReducer()`, `useCallback()`, `useMemo()`, `useRef()`, `useImperativeMethods()`, `useMutationEffect()` and `useLayoutEffect()`. Still, what if none of these hooks is the right fit?

In that case, we can write our own custom hook! This means that we have even more freedom in our work. Not only that we are not limited by functionality of individual components. We are also not limited by the range of available React hooks. It seems that React ecosystem is slowly but surely becoming more and more liberal and open.

## A game changer

By now, it is probably clear why many people think React hooks are a game changer. The option to use `state` and lifecycle methods no matter what component are we currently working with is really game-changing. What's more, this basically allows to make `state` and lifecycle methods shareable between components. Finally, there is the option to write our own React hooks.

This brings me to another, less visible, benefit. We no longer have to use HOC (high order components) or wrappers in order to "extend" some components. Unless we really want to do that. The result of all this is that we have to write even less code that is also cleaner. And, thanks to that, we can increase the performance of our apps. A game changer.

_Side note: please keep in mind that React hooks are experimental feature, at the time of writing this post. So, you will need to use at least React version "16.7.0-alpha.0" or higher in order to use them._

## From theory to practice

By now, you understand what are React hooks. You also know how hooks can benefit your work and development of your projects. There is only one thing we have to resolve. How to get started with React hooks? How can we implement hooks in our projects? Let's answer these two questions by taking a look at a few simple examples of React hooks.

There are three basic React hooks available, aside to the additional. So, let's take a look at how can we use the `useState()`, `useEffect()` and `useContext()` hooks. It is time to move from theory to practice.

### useState

Let's start with the first basic React hook `useState()`. As the name of the hook implies, this hook allows us to use `state`. Imagine we have a counter. I know, timer? Let's keep it simple. So, we have a timer component. This component needs two things. First, it needs to store number of counts, somewhere. Second, it needs to change the number of counts, somehow.

One quick solution is a `state` and one method. In the past, this would also mean that we would have to use class component because it has a `state`. Now, we know that this is no longer the truth. We can use functional components combined with React hooks. This will "supplement" the missing `state`. Let's take a look at example of both.

Example of a class component:
```
// Import React
import React from 'react'

// A simple counter as a class component
class Counter extends React.Component {
  constructor(props) {
    super(props)

    // State storing count
    this.state = {
      counter: 0
    }

    this.handleCounter = this.handleCounter.bind(this)

  // Handler for increasing count
  handleCounter(value) {
    this.setState({
      count: value
    })
  }

  render() {
    return (
      <React.Fragment>
        <h1>{this.state.count}</h1>

        <button onClick={this.handleCounter((this.state.counter - 1))}>Increase count by 1</button>

        <button onClick={this.handleCounter((this.state.counter - 1))}>Decrease count by 1</button>
      </React.Fragment>
    )
  }
}
```

Example of a functional component and React hook:
```
// Import React and useState hook
import React, { useState } from 'react'

// A simple counter as a functional component
function Counter() {
  // Create new variable 'count' and 'handleCounter' function and store them in state using 'useState' hook.
  // The argument of 'useState' hook, the '0', is initial value for 'count' that will returned from state
  const [count, handleCounter] = useState(0)

  return (
    <React.Fragment>
        <h1>{count}</h1>

        {/* Click on the button will trigger 'handleCounter' function and increase current value of 'count' variable stored in the state by 1. */}
        <button onClick={() => handleCounter(count + 1)}>Increase count by 1</button>

        <button onClick={() => handleCounter(count - 1)}>Decrease count by 1</button>
    </React.Fragment>
  )
}
```

### useEffect

The second React hook is `useEffect()`. When we use `useEffect()` we basically gain access to `componentDidMount()`, `componentDidUpdate()` and `componentWillUnmount()` methods. `useEffect()` is a combination of these two lifecycle methods and works in the same way. This means that anything we create using `useEffect()` will run after every render. And, this also includes the first one.

Imagine we have a website and we want to change some data inside the DOM. For example, we may want to change the title of the page. Another good use cases for `useEffect()` you could encounter could be subscriptions and fetching some data. Now, let's take a look at how to achieve the title change this using both, class and functional component.

Example of a class component:
```
// Import React
import React from 'react'

// A simple page as a class component
class Page extends React.Component {
  componentDidMount() {
    console.log('Page component just mounted.')

    // Change the page title
    document.title = 'Your page is ready!'
  }

  componentDidUpdate() {
    console.log('Your page is ready!')

    // Change the page title
    document.title = 'Your page is ready!'
  }

  render() {
    return <div>
      <h1>This is your website</h1>

      <p>Some content of the page.</p>
    </div>
  }
}
```

Example of a functional component and React hook:
```
// Import React and useEffect hook
import React, { useEffect } from 'react'

// A simple page as a functional component
function Page() {
  // Replace 'componentDidMount()' with 'useEffect()' and then use the rest of previous code
  useEffect(() => {
    console.log('Page component just mounted.')

    // Change the page title
    document.title = 'Your page is ready!'
  })

  return <div>
      <h1>This is your website</h1>

      <p>Some content of the page.</p>
    </div>
}
```

We can also use the `useEffect()` with the previous example of a counter component.

```
// Import React, useState and useEffect hooks
import React, { useState, useEffect } from 'react'

// A simple counter as a functional component
function Counter() {
  // Use 'useState' hook.
  const [count, handleCounter] = useState(0)

  // Add 'useEffect()' hook
  useEffect(() => {
    console.log('Page component just mounted.')

    // Change the page title
    document.title = `The value of count is ${count}`
  })

  return (
    <React.Fragment>
        <h1>{count}</h1>

        {/* Click on the button will trigger 'handleCounter' function and increase current value of 'count' variable stored in the state by 1. */}
        <button onClick={() => handleCounter(count + 1)}>Increase count by 1</button>

        <button onClick={() => handleCounter(count - 1)}>Decrease count by 1</button>
    </React.Fragment>
  )
}
```

As you remember, I mentioned that `useEffect()` is a combination of `componentDidMount()`, `componentDidUpdate()` and `componentWillUnmount()` methods. This brings one interesting question. What if we want to use specifically `componentDidUpdate()`? Then, all we have to do is specify what value has to change in order to trigger `useEffect()` and "use" the `componentDidUpdate()`.

Let's say that we want to use the `componentDidUpdate()`, or fire `useEffect()`, when the value of `count` changes. We can do this by adding `count` as a second argument to `useEffect()`. It doesn't matter how many values we want to "watch". The only thing is that this second argument has to be always in the form of an `array`, with value(s) inside it.

```
// Import React, useState and useEffect hooks
import React, { useState, useEffect } from 'react'

// A simple counter as a functional component
function Counter() {
  // Use 'useState' hook.
  const [count, handleCounter] = useState(0)

  // Use 'useEffect()'
  useEffect(
    () => {
      console.log('Page component just mounted.')

      // Change the page title
      document.title = `The value of count is ${count}`
    }
    , [count] // Trigger 'useEffect' only when the value of 'count' changes - fire the 'componentDidUpdate()' method.
  )

  return (
    <React.Fragment>
        <h1>{count}</h1>

        {/* Click on the button will trigger 'handleCounter' function and increase current value of 'count' variable stored in the state by 1. */}
        <button onClick={() => handleCounter(count + 1)}>Increase count by 1</button>

        <button onClick={() => handleCounter(count - 1)}>Decrease count by 1</button>
    </React.Fragment>
  )
}
```

Okay, and what about the `componentWillUnmount()`? This will again be very simple. All we need is to return a function from `useEffect()`.

```
// Import React, useState and useEffect hooks
import React, { useState, useEffect } from 'react'

// A simple counter as a functional component
function Counter() {
  // Use 'useState' hook.
  const [count, handleCounter] = useState(0)

  // Use 'useEffect()'
  useEffect(
    () => {
      console.log('Page component just mounted.')

      // Change the page title
      document.title = `The value of count is ${count}`

      // Fire the 'componentWillUnmount()' method.
      return () => {
        console.log('Page component will unmount now.')

        document.title = 'See you soon!'
      }
    }
  )

  return (
    <React.Fragment>...</React.Fragment>
  )
}
```

One last thing. What if we want to trigger `useEffect` only when component either mounts or unmounts and ignore updates? Meaning, what if we are interested only in using `componentDidMount()` and `componentWillUnmount()` methods, but not `componentDidUpdate()`? Then, we will again use the `array` as a second argument for `useEffect`. But now, we will leave it empty.

```
// Import React, useState and useEffect hooks
import React, { useState, useEffect } from 'react'

// A simple counter as a functional component
function Counter() {
  // Use 'useState' hook.
  const [count, handleCounter] = useState(0)

  // Use 'useEffect()'
  useEffect(
    () => {
      console.log('Page component just mounted.')

      // Change the page title
      document.title = `The value of count is ${count}`
    }
    , [] // Trigger 'useEffect' only on mount and unmount - fire only 'componentDidMount()' and 'componentWillUnmount()' methods.
  )

  return (
    <React.Fragment>...</React.Fragment>
  )
}
```

### useContext

Finally, there is the `useContext` hook. Imagine we have a project that uses `Context` API to share information about current theme. Sounds simple, right? So, let's take a look at how we can make this information shareable using both approaches, with `Context` and with `useContext`.

Example of a class component:
```
// Import React
import React from 'react'

// Create a Context
const AppContext = React.createContext()

const App = () => {
  // Use the 'Provider' to make the theme available for all children and grandchildren components
  return (
    <AppContext.Provider theme="blue">
      <div>
        <Screen />
      </div>
    </AppContext.Provider>
  )
}

const Screen = () => {
  // Use the 'Consumer' to access the theme in context
  return (
    <AppContext.Consumer>
      {theme => <div>Current theme color is {theme}.</div>}
    </AppContext.Consumer>
  )
}
```

Example of a functional component and React hooks:
```
// Import React
import React from 'react'

// Create a Context
const AppContext = React.createContext()

const App = () => {
  // Again, use the 'Provider' to make the theme available for all children and grandchildren components
  return (
    <AppContext.Provider theme="blue">
      <div>
        <Screen />
      </div>
    </AppContext.Provider>
  )
}

const Screen = () => {
  const theme = useContext(AppContext)

  // Look ma, no Consumer!
  return <div>Current theme color is {theme}.</div>
}
```

## Epilogue: Introduction to React Hooks

That's it! Congratulations! You've just finished this quick introduction and learned about React hooks. You know what React Hooks are, why they are so hot and useful and also how to use them. React hooks can help you make your code much cleaner, simpler and easier to understand. Now, it is up to you play with them and maybe start implementing them in your projects.

Do you want to know more about hooks? There are two good places where you should go. The first place is [official documentation]. Here, you will learn all you need to know about both, basic and additional, React hooks. There are also code examples for each hook. This will help you go immediately from theory to practice.

The second place is [awesome-react-hooks]. This is a GitHub repo full of tutorials, tools and custom-made React hooks available on npm. In addition, there are two good talks from React Conf 2018 focused on React hooks. One is [90% Cleaner React With Hooks]. The second is [React Today and Tomorrow]. You can take a look at them in your spare time. With that, thank you for your time and have a great day.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[state]: https://reactjs.org/docs/state-and-lifecycle.html
[lifecycle methods]: https://reactjs.org/docs/react-component.html#the-component-lifecycle
[official documentation]: https://reactjs.org/docs/hooks-reference.html
[90% Cleaner React With Hooks]: https://www.youtube.com/watch?v=wXLf18DsV-I&feature=youtu.be
[React Today and Tomorrow]: https://www.youtube.com/watch?v=V-QO-KO90iQ&feature=youtu.be
[awesome-react-hooks]: https://github.com/rehooks/awesome-react-hooks

<!--
#### Inspiration:
- https://scotch.io/tutorials/getting-started-with-react-hooks
- https://daveceddia.com/usestate-hook-examples/
- https://medium.com/@JhonnyMichel/global-state-management-with-react-hooks-5e453468c5bf
- https://medium.com/@dispix/from-react-component-to-hooks-b50241334365
- https://daveceddia.com/usecontext-hook/
-->

<!--
#### Keyword:
- React hooks
-->

<!--
#### Meta:
-
-->
