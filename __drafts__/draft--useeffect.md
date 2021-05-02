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
// Import useEffect hook from React:
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
// Import useEffect hook from React:
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
// Import useEffect hook from React:
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
// Import useEffect and useState hooks from React:
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

## Simple useEffect and fetch example

In the beginning, when we talked about side effects, I mentioned fetch requests. Fetching data is one thing that is done frequently. It is also one example where useEffect hook can be very handy. Let's create a simple component that will use the React useEffect hook to perform a simple fetching.

We will use an [async function] to fetch Reddit posts from specific reddit. Then, we will extract some information from received data and store them in its state. When all this is done and the data are ready, we will render al posts with authors in a simple list. Below is one example of how to do this.

In this example, we will fetch the posts only on initial render. In a real app, you could add some value to dependencies array that you want to watch. For example, you could provide a way to change reddit from which to fetch posts. Then, you could watch for this and run the useEffect to fetch new posts, with modified URL to fetch.

```jsx
// Import useEffect and useState hooks from React:
import { useEffect, useState } from 'react'

export default function App() {
  // Create state for Reddit feed:
  const [feed, setFeed] = useState([])

  // Use useEffect hook:
  useEffect(() => {
    // Create async function to fetch Reactjs posts from Reddit:
    async function fetchRedditFeed() {
      // Make a request to fetch Reactjs posts from Reddit:
      const redditResponse = await fetch('https://www.reddit.com/r/reactjs.json')

      // Check if data are available (response code is 200-299):
      if (redditResponse.ok) {
        // Translate received response (promise) to JSON:
        const redditJSON = await redditResponse.json()

        // Extract title, author and post id:
        const posts = redditJSON.data.children.map(post => {
          return {
            title: post.data.title,
            author: post.data.author,
            id: post.data.id
          }
        })

        // Save posts to feed state:
        setFeed(posts)
      }
    }

    // Invoke the fetchRedditFeed function:
    fetchRedditFeed()
  }, []) // <= Run only on initial render.

  // Render a list of posts
  return (
    <div className="App">
      <ul>
        {feed.map(feedItem => {
          return <li key={feedItem.id}>{feedItem.title} by {feedItem.author}</li>
        })}
      </ul>
    </div>
  )
}
```

*Note 1: You don't have to put the whole fetching function to useEffect hook. You can just as well put it outside it, and then only call it from the useEffect hook.*

*Note 2: You can't use promises and async with useEffect hook directly (`(async () => ...)`). This is not supported and React will warn you if you try it. The reason is that useEffect callbacks are synchronous to prevent [race conditions]. If you want to make an async call inside an useEffect hook you still can.*

*What you can do is to use the async function inside the useEffect hook and call it. This is why we created another function, now async, inside the useEffect hook callback function and used it to make the fetch request. So, remember that the useEffect callback itself must be always synchronous ... but the content doesn't.*

## Cleaning up side-effects

One interesting feature of the useEffect hook is automatic cleanup. This cleanup allows you to execute code right before the next useEffect run or before the component unmounts. Some scenarios where this can be useful are removing attached event listeners, clearing timers and closing external subscriptions and connections.

This cleanup is specified by a function and this function must be returned from the useEffect hook. This function can be a regular function, arrow function, and/or unnamed function. The only thing that is important is that it must be returned from the hook. Inside this function is a code you want to execute during the cleanup.

```jsx
// Syntax:
function App(props) {
  // Use useEffect hook:
  useEffect(() => {
    // Do something on every render

    // Specify returned cleanup function:
    return function() {
      // Do something during cleanup procedure.
      // Clean up will happen before next run
      // of this hook and before component unmounts.
    }
  }) // <= Run on every render.
}


// Example with event listener:
// Import useEffect hook from React:
import { useEffect } from 'react'

export default function App() {
  // Use useEffect hook:
  useEffect(() => {
    // Create function to invoke when window resizes:
    function handleResize() {
      // Log message when window is resized:
      console.log('Resize! New width is: ', window.innerWidth)
    }

    // Attach event listener for "resize" event to window:
    window.addEventListener('resize', handleResize)

    // Add cleanup function:
    return function() {
      // Remove event listener from window
      // when component unmounts:
      window.removeEventListener(handleResize)
    }
  }, []) // <= Run only on initial render

  // ...
}
```

## Conclusion: React useEffect Hook Made Simple

The React useEffect hook provides a friendly way to work with side-effects in your React components. It also makes it easier to manage these side-effects and keep them synchronized with the component itself. I hope that this tutorial helped you understand what useEffect hook is, how it works and how to use it.

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
