# React Best Practices & Tips Every React Developer Should Know Pt.2
Writing clean React code is hard and it takes time. Use these React best practices to make your code better and your work easier and faster. Learn how to initialize state faster, use `key` props the right way, deal with asynchronous nature of the setState and how to use propTypes and defaultProps.
<!--more-->
<!--
Table of Contents:
## 6. Initialize component state without class constructor
## 7. Don't use indexes as a key prop
### The role of key
### The problem with using index as a key
### Simple rules for better keys
## 8. Never rely on setState always being synchronous
## 9. Use defaultProps and prop-types
### Where JavaScript falls short
### Getting started with defaultProps
### Getting started with prop-types
## Epilogue: React Best Practices & Tips Every React Developer Should Know Pt.2
-->

React Best Practices & Tips Every React Developer Should Know [Part 1].

<!-- React Best Practices & Tips Every React Developer Should Know [Part 3]. -->

## 6. Initialize component state without class constructor

This used to be one of the React best practices, to always initialize component `state` in class constructor, assuming you were dealing with stateful component. Well, it was at least a common thing to do. Nowadays, thanks to [class fields], also called class properties, proposal, this practice is not really necessary, or required.

It is true that class fields, or properties, are not official part of JavaScript, yet. However, that doesn't mean you should avoid them. In a fact, you are pretty much safe using them in your JavaScript, and React, projects. If you use [Babel] transpiler or [TypeScript] you can use class field. Both, Babel and TypeScript support them.

Why should you consider initializing `state` with class fields as one of the React best practices to follow? There are two reasons for doing so. First, it can help you improve performance of your React app. The problem with initializing `state` inside the constructor is that it comes with an overhead of calling super, and remembering about props.

The second reason is that it will help you reduce noise in your code. Consider how many lines of code you have to add in order to initialize `state` inside a constructor. Also, you have to remember to pass `props` as argument when you call the `constructor()` and `super()` methods. How much of this code is really necessary just to initializing `state`?

The answer is very short. None of that. Well, except the statement for initializing the `state`. Everything else is redundant. It is a noise cluttering your code, slowing your React app. Skip the nonessential, the `constructor()` and `super()`. If you need only the `state = { key: value }` use just that. Compare the examples below. Which one do you like more?

Before:

```
// Import React library
import React from 'react'

// Create React component
class MyComponent extends React.Component {
  constructor(props) {
    super(props)

    // Initialize component State
    this.state = {
      counter: 0
    }
  }

  ...
}
```

After:

```
// Import React library
import React from 'react'

// Create React component
class MyComponent extends React.Component {
  // Initialize component State
  state = {
    counter: 0
  }

  ...
}
```

## 7. Don't use indexes as a key prop

Never use `index` as a value for `key` prop. This is one of those React best practices I wish I knew sooner. For a long time, when I used `map()` or some other iterator or loop, `index` was my go-to option when I needed something as a value for `key` prop. Another one was `random()` method provided by JavaScript `Math` object. Sounds familiar?

I saw many React developers repeat the same mistake. Why is this a mistake? Why this must be one of the React best practices you follow? In React, `key` is not a nice-to-have. Nor is it yet another annoying thing you have to remember when you work with React. `Key` is actually important prop when you iterate over a collection of elements, such as an array.

### The role of key

React uses `key` props to determine what needs to be rendered or re-rendered. In other words, the `key` prop is used for identification. React doesn't want to waste time rendering duplicates. So, if you have two elements and those two elements have the same keys, React sees them as the same and this can cause some elements to be omitted.

Next, React also re-renders elements whose `key` has changed for a specific element's contents, even if the content itself hasn't changed. This is the main reason why using `index` as a value for `key` prop is such a bad idea. Imagine you want to render some collection as a list. For example, it can be a collection of book you are reading right now.

What you can do is create an array with objects, one object for each book. This object can contain two key/value pairs, the name of the book and its author. The easiest way to render these books is probably by using `map()` to iterate over it and return `li` element for each book, or object in the array. The `key` prop? Nah, let's just use index.

```
// Import React library
import React from 'react'

// Add new book at the beginning of the list
let bookListData = [
  {
    title: 'The Hard Things About Hard Things',
    author: 'Ben Horowitz'
  }, {
    title: 'Only the Paranoid Survive',
    author: 'Andrew S. Grove'
  }, {
    title: 'Lean Startup',
    author: 'Eric Ries'
  }, {
    title: 'Fullstack React',
    author: 'Anthony Accomazzo'
  }
]

// Create component that will return the book list
const BookList = () => {
  return(
    <ul>
      {
        bookListData.map((book, index) => <li key={index}>{book.title} by {book.author}</li>)
      }
    </ul>
  )
}
```

### The problem with using index as a key

Now, what will happen if you change the array with books. Let's say that you decide to add new book, at the beginning. Sure, React will re-render the list and update the DOM structure. The question is, how many elements, or books, will React re-create from scratch and how many will it use from the previous version of DOM structure?

```
// Add new book at the beginning of the list
bookListData.unshift({
  title: 'Elon Musk',
  author: 'Ashlee Vance'
})
```

The answer is ... All of them! It doesn't matter that you added only one book and the previous four are the same. React doesn't know that. All React knows is that there were four elements with specific `keys`, and ALL those keys have changed. Remember, you used indexes as a `keys`. So, the first book had index "0" as `key`, the second "1", the third "2" and the fourth "3".

Why is this a problem? When you added new book at the beginning of the array, you've also changed indexes of all subsequent books. You increased indexes of those books by 1. The first book is now second and has index "1" as `key`. The second is now third and its `key`, or index, is "2". The third is now fourth and its `key` is "3" and the fourth is fifth and its `key` is "4".

Do you remember what we talked about above about re-rendering? React re-renders elements whose `key` has changed for a specific element's contents, even if the content itself hasn't changed. When you added new book, you also changed indexes for the rest of the books. This caused change of `key` props. This triggered re-render. Was all this necessary?

The answer is no. React didn't have to re-render all books. React could simply use the previous DOM structure and just add one new element, that one new book. Unfortunately, when you've changed the indexes you've also changed the only identifier React could use to determine if it is necessary to re-render the whole DOM structure, the `key`.

Do you now see the problem with using `index` as a `key`? Similar problem arises when you use `Math` and `random()`. When you add new book, it will cause re-render. New render will also trigger the `random()` method which will then generate new keys. And we are where we were before. New keys, confused React, re-rendering all books.

### Simple rules for better keys

So how can you avoid all those issues we discussed? How can you implement this as one of the React best practices? How can you create better keys? Here are some simple rules for better keys. First, `key` of an element should be always unique. It doesn't have to be unique in the global scope, or the scope of the project.

It has to be unique just among its siblings. Second, it has to be stable. The key for the same element should not change with time, refreshing the page or re-ordering of elements. This was the problem you saw in the example with indexes. They were not stable. You changed the source array and that action consequently also changed the indexes.

Something like this should never happen. The key has to be immutable, a constant. The third and last rule is predictability. The `key` should never be generated randomly. Any time you render the element you should always get the same `key`. Remember these simple rules and add this to your list of React best practices. Start writing better React code.

After:

```
// Import React library
import React from 'react'

// Add new book at the beginning of the list
let bookListData = [
  {
    title: 'The Hard Things About Hard Things',
    author: 'Ben Horowitz',
    isbn: '978-0547265452'
  }, {
    title: 'Only the Paranoid Survive',
    author: 'Andrew S. Grove',
    isbn: '978-0385483827'
  }, {
    title: 'Lean Startup',
    author: 'Eric Ries',
    isbn: '978-0307887894'
  }, {
    title: 'Fullstack React',
    author: 'Anthony Accomazzo',
    isbn: '978-0991344628'
  }
]

// Add new book at the beginning of the list
bookListData.unshift({
  title: 'Elon Musk',
  author: 'Ashlee Vance',
  isbn: '978-0062301239'
})

// Create component that will return the book list
const BookList = () => {
  return(
    <ul>
      {
        bookListData.map(book => <li key={book.isbn}>{book.title} by {book.author}</li>)
      }
    </ul>
  )
}

```

## 8. Never rely on setState always being synchronous

Guess what. `setState` is asynchronous. This is one of the things I wish I knew when I started using React. It could save me a lot of headaches, and time spent debugging. It is also why I believe that never relying on `setState` always being synchronous should also be among React best practices every React developer should at least know about.

The result of `setState` being asynchronous, and sometimes cause of headaches, is that it returns before actually setting the `state`. Put simply, If you have a function that calls `setState`, any code you add right after changing the `state` using `setState` method may actually execute faster.

It doesn't matter that the subsequent code follows after the `setState`. The reason for this is that the execution of `setState` is waiting in the event loop until that function finishes execution. It is for this reason the code following `setState` is very likely to work with the old `state`. This theory is easy to test.

Imagine you have component with `state` and a button. The `state` is initialized with `count` variable set to `0`. When you click the button it will increase the value of `count` by one. Then, it will log the value of `count` to the console. Then, it will wait for 2 second and log the value of `count`  again. What do you think will happen?

```
// Import React library
import React from 'react'

// Create simple counter component
class MyComponent extends React.Component {
  state = {
    count: 0
  }

  handleCountChange = () => {
    // Update count in state
    this.setState({
      count: this.state.count + 1
    })

    // Log the value of "count"
    console.log(`Immediate log: ${this.state.count}`)

    // Wait for 2 seconds and log the value of "count" again
    setTimeout(() => {
      console.log(`Delayed log: ${this.state.count}`)
    }, 2000)
  }

  render() {
    return(
      <>
        <button onClick={this.handleCountChange}>Click</button>
      </>
    )
  }
}

// Result of the first click:
// Immediate log: 0
// Delayed log: 1

// Result of the second click:
// Immediate log: 1
// Delayed log: 2
```

As you can see, the first `console.log()` statement, following after the the `setState`, logs different value than the next `console.log()` that is delayed by `setTimeout()`. The "immediate" log is executed before the execution of `setState` while the "delayed" log is executed after the execution of `setState`. What the solution?

Fortunately, React provides a simple and easy way to solve this issue. All you have to do is to pass a callback function as a second argument to the `setState`. This function will be executed after the `setState` method. Any code you put inside it will have access to the latest version of the `state`.

As you can see on the updated example, the `console.log()` inside the callback function always logs the correct value. So, if you have some function or method that uses `setState` and then executes some other code. This might be one of those React best practices that can be useful. Use callback function to ensure you work with the latest `state`.

```
// Import React library
import React from 'react'

// Create simple counter component
class MyComponent extends React.Component {
  state = {
    count: 0
  }

  handleCountChange = () => {
    // Update count in state
    this.setState({
      count: this.state.count + 1
    }, () => {
      // !
      // Add callback function that logs the value of "count"
      console.log(`Callback log: ${this.state.count}`)
    })

    // Log the value of "count"
    console.log(`Immediate log: ${this.state.count}`)

    // Wait for 2 seconds and log the value of "count" again
    setTimeout(() => {
      console.log(`Delayed log: ${this.state.count}`)
    }, 2000)
  }

  render() {
    return(
      <>
        <button onClick={this.handleCountChange}>Click</button>
      </>
    )
  }
}

// Result of the first click:
// Immediate log: 0
// Callback log: 1
// Delayed log: 1

// Result of the second click:
// Immediate log: 1
// Callback log: 2
// Delayed log: 2
```

## 9. Use defaultProps and prop-types

This is one of those React best practices that can make a significant difference in the quality of your code. It can also make your code much safer and easier to debug. As you know, JavaScript is [dynamically and weakly] typed programming language. This basically means that it doesn't enforce correct typing and type of variable can be changed.

### Where JavaScript falls short

Why is this important? Or, why can this be a problem? In one word, unpredictability. There is no way in JavaScript to set variables and parameters to specific type. As a result, it is very easy to use wrong type here and there. For example, to accidentally pass a string to a function that actually requires integer or boolean.

Another problem is that JavaScript doesn't allow to specify default properties for objects, or components in React. Nor does it allow to specify which properties are required and which are optional. This can lead to problems when you accidentally forget to add property to some React component that is necessary, i.e., required.

Imagine there was something that could allow all the above. Also, imagine it would also warn you when something is wrong, i.e., wrong type or missing property. Okay, one more. Imagine you could specify the default props, i.e., something like a fallback if you forget or simply don't provide the necessary props.

### Getting started with defaultProps

Luckily, there is this "something". It is called `defaultProps` and `prop-types`. With the help of `defaultProps` you can specify default props for your components. Then, if you omit these props, or one of them, when you render the component React will automatically render the default values you've set, the `defaultProps`, for those missing props.

The best thing? In the case of `defaultProps`, you don't have to install any additional dependencies. This means that you can start using `defaultProps` right away. The use of `defaultProps` is easy. You define it as an object, one key/value pair per prop. Then, you use `props` as usually.

Remember, you have to use `defaultProps` only in the beginning, when you define the default props. Then, it is just `props`. So, no `{this.defaultProps.someProp}` (class component) or `{defaultProps.someProp}` (functional component). Just `{this.props.someProp}` (class component) or `{props.someProp}` (functional component).

_One important thing you need to remember. When you define `defaultProps` outside the component you have to define them after you create the component itself. Component must always come first. If you switch the order, React will display error saying that the component is not defined, which ... is actually true._

```
// Import React and ReactDOM
import React from 'react'
import ReactDOM from 'react-dom'

///
// Example no.1: defaultProps with functional, stateless, component
const MyFunctionalComponent = (props) => <div>{props.name}</div>

// Define default props for MyFunctionalComponent
// ! Always define defaultProps only after you create the component
MyFunctionalComponent.defaultProps = {
  name: 'Tonny'
}


///
// Example no.2: defaultProps with class, stateful, component - defaultProps defined as static property
class MyClassComponentOne extends React.PureComponent {
  // Define default props for MyClassComponentOne
  static defaultProps = {
    someDefaultProp: 'MyClassComponentOne',
  }

  render() {
    return(
      <div>
        {/* Render value of someDefaultProp */}
        {this.props.someDefaultProp}
      </div>
    )
  }
}



///
// Example no.3: defaultProps with class, stateful, component - defaultProps defined outside the class
class MyClassComponentTwo extends React.PureComponent {
  render() {
    return(
      <div>
        {/* Render value of someDefaultProp */}
        {this.props.someDefaultProp}
      </div>
    )
  }
}

// Define default props for MyClassComponentTwo
// ! Again, define defaultProps only after you create the component
MyClassComponentTwo.defaultProps = {
  someDefaultProp: 'MyClassComponentTwo',
}

// Create main component that renders all previously created components
const App = () => {
  return (
    <div className='App'>
      {/* Render MyClassComponentOne without someDefaultProp prop */}
      {/* Renders div with 'MyClassComponentOne' text inside */}
      <MyClassComponentOne />

      {/* Render MyClassComponentOne with someDefaultProp prop */}
      {/* Renders div with 'foo' text inside */}
      <MyClassComponentOne someDefaultProp="foo" />

      {/* Render MyClassComponentTwo without someDefaultProp prop */}
      {/* Renders div with 'MyClassComponentTwo' text inside */}
      <MyClassComponentTwo />

      {/* Render MyClassComponentTwo with someDefaultProp prop */}
      {/* Renders div with 'bazzy' text inside */}
      <MyClassComponentTwo someDefaultProp="bazzy" />

      {/* Render MyFunctionalComponent without title prop */}
      {/* Renders div with 'Tonny' text inside */}
      <MyFunctionalComponent />

      {/* Render MyFunctionalComponent with title prop */}
      {/* Renders div with 'Joyce' text inside */}
      <MyFunctionalComponent name="Joyce" />
    </div>
  )
}

// Render App in DOM
const rootElement = document.getElementById('root')
ReactDOM.render(<App />, rootElement)
```

### Getting started with prop-types

Now you probably understand why `defaultProps` why should definitely be on your list of React best practices. However, there is still that potential issue with unpredictability, now smaller, and using incorrect types. The good news is that there is are multiple ways to solve this problem. One of these ways is [prop-types].

The bad news? `prop-types` are not part of React library, like `defaultProps`. Well, they were, but that changed with React v15. Anyway, adding one additional dependency will not be such a problem when you consider the significant impact this dependency can have on your code quality and stability, and also your productivity.

Using `prop-types` is very similar to using `defaultProps`. It is almost the same. There are two differences. First, you are defining props the component should or must have. You mark props as required with `isRequired` property (see the example below). The second difference is that you don't specify the exact value.

Instead, you specify the type of the value. For example, you specify if prop accepts types such as `integer`, `string`, `boolean`, `object`, etc. The shape is the same as in `defaultProps`, object with key/value pairs. `Key` is the property and `value` is the type. As usually, there is one more thing.

How do you know you used incorrect type or omitted required prop? React will show warning message. This message will tell you where you made a mistake and why. This is why `prop-types` can significantly improve code quality and stability, and also your productivity. It is also why they should be on your list of React best practices as well.

```
// Import React and ReactDom
import React from 'react'
import ReactDOM from 'react-dom'

// Import prop-types
import { PropTypes } from 'prop-types'

// Create functional, stateless, component
const MyFunctionalComponent = (props) => (
  <div>{props.name} ({props.age}){props.isPremium && ', is premium'}</div>
)

// Define prop-types for MyFunctionalComponent
// ! Similarly to defaultProps, define prop-types only after you create the component
MyFunctionalComponent.propTypes = {
  name: PropTypes.string.isRequired, // marks required prop
  age: PropTypes.number,
  isPremium: PropTypes.bool
}


///
// Example no.2: prop-types with class, stateful, component - prop-types defined as static property
class MyClassComponentOne extends React.PureComponent {
  // Define prop-types for MyClassComponentOne
  static propTypes = {
    name: PropTypes.string,
    age: PropTypes.number.isRequired,  // marks required prop
    isPremium: PropTypes.bool
  }

  render() {
    return(
      <div>
        {/* Render values of props */}
        {this.props.name} ({this.props.age}){this.props.isPremium && ', is premium'}
      </div>
    )
  }
}

///
// Example no.3: prop-types with class, stateful, component - prop-types defined outside the class
class MyClassComponentTwo extends React.PureComponent {
  render() {
    return(
      <div>
        {/* Render values of props */}
        {this.props.name} ({this.props.age}){this.props.isPremium && ', is premium'}
      </div>
    )
  }
}

// Define prop-types for MyClassComponentTwo
// ! Similarly to defaultProps, define prop-types only after you create the component
MyClassComponentTwo.propTypes = {
  name: PropTypes.string,
  age: PropTypes.number,
  isPremium: PropTypes.bool
}

// Create main component that renders all previously created components
const App = () => {
  return (
    <div className='App'>
      {/* Render MyClassComponentOne */}
      <MyClassComponentOne
        name="Tony Stark"
        age={38}
        isPremium={true}
      />

      {/* Render MyClassComponentTwo */}
      <MyClassComponentTwo
        name="Bruce Banner"
        age={36}
        isPremium={false}
      />

      {/* Render MyFunctionalComponent */}
      <MyFunctionalComponent
        name="Joyce Strand"
        age={false} // Warning: Failed prop type: Invalid prop `age` of type `boolean` supplied to `MyFunctionalComponent`, expected `number`.
        isPremium="no" // Warning: Failed prop type: Invalid prop `isPremium` of type `string` supplied to `MyFunctionalComponent`, expected `boolean`.
      />
    </div>
  )
}

// Render App in DOM
const rootElement = document.getElementById('root')
ReactDOM.render(<App />, rootElement)
```

## Epilogue: React Best Practices & Tips Every React Developer Should Know Pt.2

Congratulations! You've just finished the second part of this mini series focused on React best practices. In a recap, you've learned how to initialize component state with less code and why you should never use indexes as a key prop. After that, you've also learned how to handle asynchronous nature of setState method.

As the last thing, you've learned about `defaultProps` and `prop-types`, and how these two can help you write more stable, predictable and safer React code. Now, it is up to you to choose which of the React best practices we discussed will you implement. So, go ahead. Pick your favorites, implement them, and improve your React code.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Part 1]: https://blog.alexdevero.com/react-best-practices-pt1/
[class fields]: https://www.sitepoint.com/javascript-private-class-fields/
[Babel]: https://babeljs.io/
[TypeScript]: https://www.typescriptlang.org/
[dynamically and weakly]: https://stackoverflow.com/questions/964910/is-javascript-an-untyped-language
[prop-types]: https://www.npmjs.com/package/prop-types
<!-- [Part 3]: https://blog.alexdevero.com/react-best-practices-pt3/ -->

<!--
### Meta:
-
-->
