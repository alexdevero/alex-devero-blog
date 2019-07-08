# React Best Practices & Tips Every React Developer Should Know Pt.1
React is one of the most popular libraries for building interactive user interfaces. In this post, I will show you a handful of React best practices that will help you become a better React developer. Learn these practices so you can start writing a better React code.<!--more-->
<!--
Table of Contents:
## 1. Keep your components small
## 2. Avoid component hell
## 3. Reduce the use of stateful components
## 4. Use functional component with hooks, and memo, instead of classes
## 5. Don't use props in initial state
## Epilogue: React Best Practices & Tips You Should Know Pt.1
-->

## 1. Keep your components small

Keeping your components small is one of the React best practices that can make wonders. Implementing just this one seemingly simple practice can help you write cleaner and more maintainable. Not to mention it can help you keep your sanity, or at least what's left. The most important question you may ask now, how big is too big?

There is one good rule of thumb you can use. Take a look at your render method. If it has more than 10 lines your component is probably too big, and a good candidate for refactoring and splitting to multiple smaller components. Remember that one of the ideas for using React, or part of its philosophy, is re-usability of the code.

The goal is to create pieces of code you write once and then re-use ever time you need. From this point of view, it doesn't make any sense to put all your into one massive component, one file. And, even if you don't really care about re-usable code, think about this. How easy to maintain will component with hundreds lines of code be?

Such a component will be difficult to maintain, debug and update. This also means that any work with that component will also take much more time. In other words, your overall productivity will suffer. And, sooner or later, it will drive you insane. Or, it will drive insane your teammates and colleagues and they will start to drive insane you.

Whatever you choose, you will soon lose your sanity, and probably make a few enemies. This is not worth it. Keep your components small. Save your friendships, sanity of yours and your teammates, your time and productivity. Make your code easier to debug, update and maintain. Let's take a look at one example.

Before

```
///
// file: index.jsx
import React from 'react'

const books = [
  {
    category: 'Business',
    price: '$20.00',
    name: 'Private Empires',
    author: 'Steve Coll'
  },
  {
    category: 'Philosophy',
    price: '$25.00',
    name: 'The Daily Stoic',
    author: 'Ryan Holiday'
  },
  {
    category: 'Sport',
    price: '$15.95',
    name: 'Moneyball',
    author: 'Michael Lewis'
  },
  {
    category: 'Biography',
    price: '$21.00',
    name: 'Titan',
    author: 'Ron Chernow'
  },
  {
    category: 'Business',
    price: '$29.99',
    name: 'The Hard Thing About Hard Things',
    author: 'Ben Horowitz'
  '},
  {
    category: 'Fiction',
    price: '$4.81',
    name: 'Limitless: A Novel',
    author: 'Alan Glynn'
  '}
]

class Bookshelf extends React.Component {
  render() {
    const tableRows = []

    this.props.books.forEach((book) => {
      tableRows.push(
        <tr>
          <td>{book.name}</td>
          <td>{book.author}</td>
          <td>{book.price}</td>
          <td>{book.category}</td>
        </tr>
      )
    })

    return (
      <div>
        <form>
          <input type="text" placeholder="Search..." />

          <button>Search</button>
        </form>

        <table>
          <thead>
            <tr>
              <th>Name</th>
              <th>Author</th>
              <th>Price</th>
              <th>Category</th>
            </tr>
          </thead>

          <tbody>{tableRows}</tbody>
        </table>
      </div>
    )
  }
}

// Render Bookshelf component
ReactDOM.render(<Bookshelf books={booksData} />, document.getElementById('container'))
```

After

```
///
// file: books-data.js
const books = [
  {
    category: 'Business',
    price: '$20.00',
    name: 'Private Empires',
    author: 'Steve Coll'
  },
  {
    category: 'Philosophy',
    price: '$25.00',
    name: 'The Daily Stoic',
    author: 'Ryan Holiday'
  },
  {
    category: 'Sport',
    price: '$15.95',
    name: 'Moneyball',
    author: 'Michael Lewis'
  },
  {
    category: 'Biography',
    price: '$21.00',
    name: 'Titan',
    author: 'Ron Chernow'
  },
  {
    category: 'Business',
    price: '$29.99',
    name: 'The Hard Thing About Hard Things',
    author: 'Ben Horowitz'
  '},
  {
    category: 'Fiction',
    price: '$4.81',
    name: 'Limitless: A Novel',
    author: 'Alan Glynn'
  '}
]

export default booksData

///
// file: components/books-table.jsx
import React from 'react'

class BooksTable extends React.Component {
  render() {
    const tableRows = []

    this.props.books.forEach((book) => {
      tableRows.push(
        <tr>
          <td>{book.name}</td>
          <td>{book.author}</td>
          <td>{book.price}</td>
          <td>{book.category}</td>
        </tr>
      )
    })

    return (
      <table>
        <thead>
          <tr>
            <th>Name</th>
            <th>Author</th>
            <th>Price</th>
            <th>Category</th>
          </tr>
        </thead>

        <tbody>{tableRows}</tbody>
      </table>
    )
  }
}

export default BooksTable

///
// file: components/search-bar.jsx
import React from 'react'

class SearchBar extends React.Component {
  render() {
    return (
      <form>
        <input type="text" placeholder="Search..." />

        <button>Search</button>
      </form>
    )
  }
}

export default SearchBar

///
// file: components/bookshelf.jsx
import React from 'react'

// Import components
import BooksTable from './components/books-table'
import SearchBar from './components/search-bar'

class Bookshelf extends React.Component {
  render() {
    return (
      <div>
        <SearchBar />

        <BooksTable books={this.props.books} />
      </div>
    )
  }
}

export default Bookshelf

///
// file: index.jsx
import React from 'react'

// Import components
import Bookshelf from './components/bookshelf

// Import data
import booksData from './books-data'

// Render Bookshelf component
ReactDOM.render(<Bookshelf books={booksData} />, document.getElementById('container'))
```

## 2. Avoid component hell

Every rule and practice has to be applied with caution. This is also true about these React best practices, especially the previous one. When it comes to components, it is very easy to overdo it and write even the tiniest snippets of code as components. Don't do this. There is no point in making every paragraph, span or div a component.

Think before you start splitting every component into smaller pieces. You can think of a component as a mix of "HTML" elements that does only do one thing, is independent, and the user perceives it as one. So, from this point of view, does it make sense to make this piece of code a component? If not, keep that code together. Otherwise, split it.

Let's take a look at some examples to illustrate this definition of a component. One example is a modal dialog. This component can be composed of many smaller elements, such as `div` containers, headings, paragraphs of text, buttons, etc. In theory, you could extract all these elements into small components.

In practice, it doesn't make sense. Yes, some of these elements can exist independently. However, is it really beneficial to create component that is composed of just one paragraph, or one heading? What's coming next? Component for label, input or even a span? This approach is not sustainable.

Fortunately, there is another way to look at it. You can use the [atomic design] methodology as a guide here. In atomic design, everything is split into six categories: atoms, molecules, organisms, templates, pages and utilities. You start with the smallest elements, such as buttons, links, labels, inputs, etc. These are atoms.

Then, you combine atoms and create molecules. Examples of molecules can be modal dialog, form, popup, dropdown, navigation, etc. Next, you can combine one molecule with another, or with atom, and create an organism. Example of an organism can be header, product listing or shopping cart. Templates, pages and utilities are not important now.

How can you combine atomic design with these two React best practices about components? Let's keep it simple. A component can be anything bigger than atom, i.e.: molecule, organism or even template or a page, if taken to the extreme. In this sense, label, heading, paragraph are not components because these are atoms.

However, modal dialogs, forms, popups, dropdowns, etc. are components because they all belong to either molecules or organism category. There are still some elements that are questionable, such as button. Yes, from the perspective of atomic design it is an atom. However, it can exist independently, in many variations, and still work.

In these cases, I suggest not overthinking these React best practices and instead just going with your gut. In the end, you are the one who will work with the code. The important thing is what feels comfortable to you. So don't just blindly follow some list of React best practices. And, if you work in a team? Share your thoughts about this with your colleagues.

## 3. Reduce the use of stateful components

This is one of the React best practices that have been around for a while. However, this practice became more popular especially with the introduction of React 16.8.0 and [React hooks]. Before this, when you wanted to use `state`, or any [lifecycle method], you also had to use stateful component. There was no other way around this.

Hooks changed this. After they were officially introduced, React developers were no longer limited to stateful components because they needed to use `state`. Thanks to hooks, React developers could now write stateless, or functional, components while using `state` and even lifecycle methods as the wish.

Why is this important? Stateless, or functional, components are generally better than stateful components when it comes to performance. The reason is that there is no `state` and no lifecycle method. In other words, less code to be executed and also transpiled. Sure this difference can be very small, almost invisible, if you work on some very small project.

However, these small differences can add up as your project grows. Also, think about how many lines of code stateful component requires in comparison to functional. Functional are also shorter and often easier to read. Let's take a look at a button component defined as stateful and functional component. Which one do you like more?

```
// Button defined as a stateful component
class Button extends React.Component {
  handleClick = () => {
    // Do something
  }

  render() {
    return(
      <button type="button" onClick={this.handleClick}>Click me</button>
    )
  }
}

// Button defined as a functional component
const Button = () => {
  const handleClick = () => {
    // Do something
  }

  return(
    <button type="button" onClick={handleClick}>Click me</button>
  )
}
```

## 4. Use functional component with hooks, and memo, instead of classes

As we already discussed, you no longer have to use stateful components just to use `state`. What's more, some React developers also believe that React will start to move away from classes in the future. Whether this is true is not important now. What is important is that, one functional component can now use `state` thanks to hooks.

And, two, there are [benefits] to using functional components. TLDR? No class, extends and the constructor. No `this` keyword. Enforced React best practices. High signal-to-noise ratio. Bloated components and poor data structures are easier to spot. Code is easier to understand and test. And, again, performance is better.

One more thing. Many React developers used to argue against functional components. One problem is that you as a React developer have no control over re-rendering process when you use functional component. When something changes, React will re-render functional component, no matter if the component itself has changed.

In the past, the solution was to use [pure component]. Pure component allows shallow prop and state comparison. Meaning, React can "test" if the content of the component, props, or the component itself has changed. If so, it will re-render it. Otherwise, it will skip re-rendering and reuse the last rendered result instead. Fewer re-renders equals better performance.

With the release of React 16.6.0, this is no longer a problem, and the argument against functional components no longer valid. What changed the game was [memo]. Memo brought shallow prop comparison to functional component, the ability to "test" if the content of the component, props, or the component itself has changed.

Then, again, based on this comparison, React will either re-render the component or reuse the last rendered result. In short, memo allows you to create "pure" functional components. There is no reason to use stateful components, or pure components, anymore. At least not if you don't need to handle complex state.

In that case, you should consider using something more scalable and manageable such as [MobX], [Redux] or [Flux] instead of component `state`. Another option could potentially be using [context]. Anyway, thanks to hooks and memo, functional components are definitely one of the React best practices worth thinking about.

## 5. Don't use props in initial state

This is one of the React best practices I wish I knew when I got to React. Back then, I didn't know that it was a very bad idea it was to use props in initial `state`. Why is this a bad idea? The problem is that the constructor is called only once, at the time when the component is created.

This means that when you make some change to the props next time, component state will not be updated. It will still retain its previous value. Back then, I, incorrectly, assumed that props are in sync with the state. So, when some props change the state will change as well in order to reflect that change. Unfortunately, this is not true.

This may not be a problem if you want the `state` to get values from props only once, during the initial render, and you will manage the state inside the component. Otherwise, you can fix this problem using `componentDidUpdate`. As the name says, this lifecycle method allows you to update the component when something changed, such as props.

If you decide to use this method, remember one thing. It will not be invoked on the initial render, only on the following. So, make sure to initialize component `state` with necessary values, probably fetched from props. Then, use `componentDidUpdate` to update those values, and the component, as you need.

## Epilogue: React Best Practices & Tips You Should Know Pt.1

Congratulations! You've just finished the first part of this mini series focused on React best practices. Today, you've learned about five practices you can use to make your React code shorter, simpler, better, faster and easier to read and maintain. Now, it is up to you to implement those practice you agree with and start using them.

In the next part, you will learn about another set of React best practices, and tips, that will help you improve your React code, as well as your coding skills. Until then, take what you've learned today and invest some of your time in practice.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[atomic design]: https://blog.alexdevero.com/atomic-design-scalable-modular-css-sass/
[React hooks]: https://reactjs.org/docs/hooks-intro.html
[lifecycle method]: https://reactjs.org/docs/react-component.html#the-component-lifecycle
[benefits]: https://hackernoon.com/react-stateless-functional-components-nine-wins-you-might-have-overlooked-997b0d933dbc
[pure component]: https://reactjs.org/docs/react-api.html#reactpurecomponent
[memo]: https://reactjs.org/docs/react-api.html#reactmemo
[MobX]: https://mobx.js.org
[Redux]: https://redux.js.org
[Flux]: https://facebook.github.io/flux/docs/overview.html
[context]: https://reactjs.org/docs/context.html

<!--
#### Meta:
-
-->

<!--
#### Inspiration:
- https://reactpatterns.com
- https://medium.com/@User3141592/react-gotchas-and-best-practices-2d47fd67dd22
- https://codeburst.io/how-to-not-react-common-anti-patterns-and-gotchas-in-react-40141fe0dcd
-->
