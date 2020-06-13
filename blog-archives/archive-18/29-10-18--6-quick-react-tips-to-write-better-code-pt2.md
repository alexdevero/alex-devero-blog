# 6 Quick React Tips to Write A Better Code Pt.2

Learning new quick React tips is always good. A handful of tips can help you improve your code and results of your work. In this article, you will learn about another three quick React tips to write cleaner and more efficient code. You will learn about things such as pure components, conditional loading and `propTypes` and also two bonus tips. Take your React code to another level!

<!--
Table of Contents:
## Use pure components
## Use inline conditional loading
## Use propTypes and defaultProps
## Bonus 1: Stay on the edge
## Bonus 2: Get better in JavaScript
## Epilogue: 6 Quick React Tips to Write A Better Code Pt.1
-->

6 Quick React Tips to Write A Better Code [Part 1].

## Use pure components

In the [previous part] of React tips, we talked a lot about keeping our components small. With relation to that, we then discussed stateless, or functional, components. Let's take this one step farther. Aside to classical, statefull `Component`, React also offer something called `PureComponent`. So, What is the difference between `PureComponent` and `Component`?

These two are very similar. The main difference is that the `shouldComponentUpdate()` method is not implemented in `PureComponent`. Instead,  there is only comparison of the `props` and `state` of the `PureComponent`. This means that when component's `props` or `state` doesn't change, the component will not re-render.

This can be very useful in case in which you have an interface containing multiple small components inside one main component. Let's say that all these small components are created via the classical `Component` API. Then, every time there is some change in the main component, that change will trigger re-rendering of all these small components as well.

On the hand, let's say that you created your small components via `PureComponent`. In that case, change in the main component will not necessarily trigger re-rendering of all those smaller components. React will compare the `props` and `state` of these small components first. Only if `props` or `state` is different from the previous it will re-render them.

This can result in significant performance improvements. This is especially true if your UI contains a lot of smaller components that don't need to be updated. When you use create these components via `PureComponent` API, as discussed, you will tell React to re-render these component only when there is a change in `props` or `state` of a specific component.

```
// Example of stateful component
// This will re-render when parent component changes
// Import React
import * as React from 'react'

export default class Article extends React.Component {
  handleClick = (e) => {}

  render() {
    return(
      <article>
        <h1 className="article__heading">{props.heading}</h1>

        <span className="article__date">Published on {props.published}</span>

        <div className="article__slug">
          <p>{props.slug}</p>
        </div>

        <a className="article__link" onClick={this.handleClick}>Read more</a>
      </article>
    )
  }
}

// Example of stateless component
// This will re-render when parent component changes
import * as React from 'react'

export const Article = (props) => (
  <article>
    <h1 className="article__heading">{props.heading}</h1>

    <span className="article__date">Published on {props.published}</span>

    <div className="article__slug">
      <p>{props.slug}</p>
    </div>

    <a className="article__link" onClick={props.handleClick}>Read more</a>
  </article>
)


// Example of pure component
// This will not re-render when parent component changes.
// It will re-render only if props or state of this component changes.
// Import React
import * as React from 'react'

export default class Article extends React.PureComponent {
  handleClick = (e) => {}

  render() {
    return(
      <article>
        <h1 className="article__heading">{props.heading}</h1>

        <span className="article__date">Published on {props.published}</span>

        <div className="article__slug">
          <p>{props.slug}</p>
        </div>

        <a className="article__link" onClick={this.handleClick}>Read more</a>
      </article>
    )
  }
}
```

## Use inline conditional loading

Another tip from the stack of React tips is to use load components only when necessary by using conditional statements. And, we can take this even farther by using inline conditional statements. This can help us write code that is cleaner, simpler and easier to understand. We don't have to write `if (x ... y) { ... }`. Instead, we can simply use `x && ...`.

When we use this operator, we are telling React to do something if specific condition evaluates to `true`. Let's say that you have an article. When user lands on the page, he will see only a short part, or slug, of the article. He can view the full text if he wants by clicking on a button under the slug.

When user clicks the button, he will trigger change that will result in removing the slug and showing the full text. In this example, we can use the condition to either manipulate only with the text or whole components.

```
// Article component with text manipulation
// Import React
import * as React from 'react'

export default class Article extends React.Component {
  constructor(props) {
    super(props)

    this.handleClick = this.handleClick.bind(this)

    this.state = {
      isFullTextVisible: false
    }
  }

  handleClick() {
    this.setState({
      isFullTextVisible: true
    })
  }

  render() {
    return(
      <article>
        <h1 className="article__heading">{this.props.heading}</h1>

        <span className="article__date">Published on {this.props.published}</span>

        {!this.state.isFullTextVisible && <div className="article__slug">
          <p>{this.props.slug}</p>}
        </div>}

        {this.state.isFullTextVisible && <div className="article__text">
          <p>{this.props.text}</p>}
        </div>}

        <a className="article__link" onClick={this.handleClick}>View full text</a>
      </article>
    )
  }
}

// Article component with component manipulation
// Import React
import * as React from 'react'

export default class Article extends React.Component {
  constructor(props) {
    super(props)

    this.handleClick = this.handleClick.bind(this)

    this.state = {
      isFullTextVisible: false
    }
  }

  handleClick() {
    this.setState({
      isFullTextVisible: true
    })
  }

  render() {
    return(
      <article>
        <h1 className="article__heading">{this.props.heading}</h1>

        <span className="article__date">Published on {this.props.published}</span>

        {!this.state.isFullTextVisible && <ArticleSlug slug={this.props.slug} />}

        {this.state.isFullTextVisible && <ArticleText text={this.props.text} />}

        <a className="article__link" onClick={this.handleClick}>View full text</a>
      </article>
    )
  }
}
```

## Use propTypes and defaultProps

This is one of React tips I started using heavily recently, after I started using TypeScript. One benefit of TypeScript, and also reason it became so popular, is allows to define types for variables, function, props in React, etc. It then runs a type-check during every code compilation. This helps us make sure we always use correct type of data and prevent many potential issues.

Let's think about the example with article above. There are some specific props that are necessary for the article component to work. The `heading`, `published`, `slug`, `text` for example. The problem is that mere existence of these props is not enough. Meaning, if we want the article component to work, we need to provide these props. And, we must provide them in correct type or format.

Imagine that the `published` prop accepts only number. For example, unformatted date. What would happen if we provide the component with string? It will probably not work correctly. It may either render nothing, no publishing date, or it may not render at all. This can happen. What if there was some check that would warn us that we used string instead of number?

This is where types in TypeScript come into the play. Fortunately, we don't have to use TypeScript to enjoy this feature. Instead, we can use [propTypes] package. Then, we can specify the type of data that is acceptable. For example, we can say that `published` has to be a number and that `slug` has to be a string. So, if we, or someone else, try to use different type we will immediately see a warning that we used wrong type and also where we used it.

What's more, [propTypes], and also TypeScript, allows us to specify if certain props is necessary or just optional. If we want to specify that some prop is necessary, we can use `isRequired`.

Let's take a look at how the example of article could look like using `propTypes`. We will make the `heading`, `published`, `slug` and `text` required props. We will also add `subheading` and `author` as optional props. Since the `author` may be in most cases us, we can also specify a default value for this prop to make sure something is always passed.

```
// Import React
import * as React from 'react'

// Import PropTypes
import PropTypes from 'prop-types'

export default class Article extends React.Component {
  constructor(props) {
    super(props)

    this.handleClick = this.handleClick.bind(this)

    this.state = {
      isFullTextVisible: false
    }
  }

  handleClick() {
    this.setState({
      isFullTextVisible: true
    })
  }

  render() {
    return(
      <article>
        <h1 className="article__heading">{this.props.heading}</h1>

        {this.props.subheading && <ArticleSubHeading subheading={this.props.subheading} />}

        {this.props.author && <ArticleAuthor author={this.props.author} />}

        <span className="article__date">Published on {this.props.published}</span>

        {!this.state.isFullTextVisible && <ArticleSlug slug={this.props.slug} />}

        {this.state.isFullTextVisible && <ArticleText text={this.props.text} />}

        <a className="article__link" onClick={this.handleClick}>View full text</a>
      </article>
    )
  }
}

// Define types and mark all as required
Article.propTypes = {
  author: 'Anthony Logan', // Optional prop with default value
  heading: PropTypes.string.isRequired,
  published: PropTypes.number.isRequired,
  slug: PropTypes.string.isRequired,
  subheading: PropTypes.string, // optional prop
  text: PropTypes.string.isRequired
}
```

Do you want to learn more about how to use `propTypes` in your projects? There is a very good tutorial on [Fullstack React]. This tutorial shows very well how to use `propTypes` on various examples. You will learn all you need.

## Bonus 1: Stay on the edge

With that, we are done with the main batch of React tips. Now you know six quick React tips that will help you write better code. Still, there are some other more general useful React tips that will help you improve your skills. This first, let's say a bonus, tip is about keeping up with the pace of React development and staying on the edge.

React is a very lively project. There is some minor release almost every week and major almost every month. This means two things. First, React is not going to fade away any time soon. There is a large community of passionate developers, fans and evangelists working on React and contributing to it in various ways. Second, React is continuously getting better and better.

There are bugs fixed, improvements made and new features implemented with every release. This means that it is not an option to learn something and then don't check the news about React the next year. It is necessary for every developer who wants to work with React to stay relevant. It is crucial to watch, and/or be part of, the community and know about releases.

It also means that there might be some improvement in every release that can help you write better code. In the end, almost all the React tips we talked about in this mini series were once new features. Aside to that, team behind the React is working hard on making React cleaner and more efficient. So, it is not just new features how staying on the edge can improve your code.

This means that your projects might become faster and more efficient with time even if you don't change anything. This improvement will be simply a result of the work team behind the React did. So, if you are looking for some free benefits in the form of better performance you don't have to work for, this is a good place to start. Add [React blog] to your bookmarks or RSS reader.

## Bonus 2: Get better in JavaScript

This is one of the React tips I wish I knew sooner. It would help me avoid many mistakes and slips. When I started with React I treated it like jQuery. This is a well-known fact among developers. You don't need to know a lot about JavaScript in order to use jQuery. In the end, this is one of the reasons jQuery became so popular in such a short time.

Before jQuery, every developer has to learn how JavaScript works and how to use its, back then often difficult, syntax in the proper way. After jQuery entered the scene, almost anyone could write a simple script to get the job done. We still see the consequences today. The problem is that many developers are following the same or similar approach with React.

Why should one learn the nuts and bolts of JavaScript? Watching few videos and look at few tutorials will help to get into React much faster. You can always "hack" your way and get the job done. Well, this doesn't work. At least not if one of your goals is writing a code you will not regret later, code that is clean. I know this from my own experience.

This, skipping a proper JavaScript learning path, is not the approach worth following. It may save you some time now, but it will also lead to many headaches and much more time wasted in the future. So, if you are not sure about your current knowledge of JavaScript, don't proceed any further with React. Work on your JavaScript knowledge first. Fix all gaps and remove any uncertainty.

Only when you get your JavaScript knowledge to advanced level you should proceed to React. This may sound uncomfortable, as a waste of time. It is not. It is a very good investment that will have very positive returns in the future. There are two resources I would recommend to anyone and any time. First is [Eloquent JavaScript]. Second is You Don't Know JS [book series].

Reading these books will teach you everything you need to master JavaScript. Well, it will basically teach you everything there is about JavaScript. Yes, it will take time to get through all this material. Just remember that it is one of the best ways to invest your time. And, the sooner you start the sooner you finish. So, stop wasting any second and start learning now.

One more thing. The You Don't Know JS book series is available for free to read online. Eloquent JavaScript is not only available for free to read online, it is also available in the form of pdf, epub and mobi, the latest edition. So, there is no excuse to delay this. Start reading, start learning. React is waiting.

## Epilogue: 6 Quick React Tips to Write A Better Code Pt.2

Congratulations! You've just reached the end of this React tips mini series. By now, you know a handful of tips that will help you write better and cleaner code. What's more, these React tips will also lead to better and more enjoyable work. In the end, what is better than seeing the results of your work, especially when your code clean as snow?

Next steps? Don't stop with reading about these six quick React tips, we talked about throughout this mini series. Now, it is time to take what you've learned and apply it. This is the only way to really start writing cleaner and better code. Reading alone will not do the job. Only diligent application and practice will.

So, apply what you've read about and take your React code to another level. And, remember those two bonus tips. Stay on the edge and if you think you have some gaps in your JavaScript knowledge fix them first. JavaScript is the foundation of React. Make it strong, solid, resilient, anti-fragile. With that, thank you for your time and have a great day.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Part 1]: https://blog.alexdevero.com/quick-react-tips-pt1/
[previous part]: https://blog.alexdevero.com/quick-react-tips-pt1/
[propTypes]: https://www.npmjs.com/package/prop-types
[Fullstack React]: https://www.fullstackreact.com/30-days-of-react/day-8/
[React blog]: https://reactjs.org/blog/
[Eloquent JavaScript]: https://eloquentjavascript.net
[book series]: https://github.com/getify/You-Dont-Know-JS

<!--
#### Resources:
- https://logrocket-blog.ghost.io/death-by-a-thousand-cuts-a-checklist-for-eliminating-common-react-performance-issues/?utm_source=reactdigest
- https://blog.usejournal.com/how-to-apply-solid-principles-in-react-applications-6c964091a982
- https://vasanthk.gitbooks.io/react-bits/
- https://camjackson.net/post/9-things-every-reactjs-beginner-should-know
- https://blog.risingstack.com/8-tips-to-build-better-react-apps-in-2018/
- https://medium.freecodecamp.org/the-beginners-collection-of-powerful-tips-and-tricks-for-react-f2e3833c6f12
- https://react.christmas/23
- https://www.toptal.com/react/tips-and-practices
- http://aeflash.com/2015-02/react-tips-and-best-practices.html
- https://blog.lavrton.com/how-to-optimise-rendering-of-a-set-of-elements-in-react-ad01f5b161ae
- https://firstdoit.com/how-to-write-a-react-stateless-functional-component-in-typescript-5d150419bbbc
- https://hackernoon.com/react-stateless-functional-components-nine-wins-you-might-have-overlooked-997b0d933dbc
- https://medium.freecodecamp.org/functional-setstate-is-the-future-of-react-374f30401b6b
-->
