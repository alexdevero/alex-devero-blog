# How to Build a Website with [React], React Router & Styled-Components Pt.2

Have you ever though about building a website with React, React-router and styled-components? Then, this tutorial is right for you. In this second, we will start by creating responsive navigation, playing with React `state`, and creating a few more React components. We will also use some handy helpers from styled-components. And, at the very end, we will create the first page for our React website. So, dust off your knowledge of React and styled-components and get ready. Our adventure into the world of React continues.

<!--
Table of Contents:
## Before we begin
## Styled-components + React Pt.2
### Navigation, state and our first component
### Adding a few more components
### Creating our first page, the homepage
## Closing thoughts on building a website with React, React Router & styled-components
How to Build a Website with React, React Router & Styled-Components [part 1].
-->

## Before we begin

In this part of this tutorial to build a React website we will make a heavy use of `styled-components`. So, if you are not familiar with this library you may take a look at [A Simple Introduction to Styled-components] and [Styled-Components – Mastering the Fundamentals Through Practice]. Also, if you find any piece of code you are not sure about or don't understand, take a look at the official [documentation], especially API Reference section can be handy. Now, let's continue.

## Styled-components + React Pt.2

What is a better way to start the second part of this React website tutorial than resetting some default browser styles, such as those for `margin`, `padding` applied to `body` element and `box-sizing` applied to `html` and, well, everything. After that, we can also add our own custom styles. For example, we can again select `body` element and change some typography styles for our React website, such as `font-size`, `line-height` and `font-family`.

In order to do this, we will need to import [injectGlobal] helper from 'styled-components'. Then, we can use `injectGlobal` to apply all the styles we want to apply to global elements such as `html` and `body`. Thanks to this method, we can add any styles directly to the stylesheet, instead of having to create custom "styled" components. However, do not over-use this helper. `injectGlobal` helper should be used as little as possible like for styling `html` and `body`. And, it should be used only once, if possible.

This will be all we really need for now. We can take care about the rest directly inside each component. One thing, I should mention that we don't have to do any other work with styles we want to apply via `injectGlobal`. We just need to use `injectGlobal` helper and say what styles we want. That's all. `styled-components` will do the rest, the heavy lifting, for us. We can also add styles for `#app` and `.wrapper`, `height` and `min-height`, so we can make some pages full-height.

code:
```
// index.js
import React from 'react'
import ReactDOM from 'react-dom'
import { BrowserRouter } from 'react-router-dom'

// import injectGlobal helper
import { injectGlobal } from 'styled-components'

import Main from './App/Main'

// Global style
injectGlobal`
  html,
  body,
  #app,
  .wrapper {
    min-height: 100vh;
    height: 100%;
  }

  html {
    box-sizing: border-box;
    font-size: 100%;
  }

  * {
    &,
    &::after,
    &::before {
      box-sizing: inherit;
    }
  }

  body {
    padding: 0;
    margin: 0;
    font: 1rem / 1.414 arial, sans-serif;
  }
`

const wrapper = document.getElementById('app')

const App = () => (
  <BrowserRouter>
    <Main />
  </BrowserRouter>
)

ReactDOM.render(<App />, wrapper)
```

### Navigation, state and our first component

At this moment, we have the whole code for our navigation right inside in the `Main.js` file. This is not really necessary, and it even creates a clutter and increases complexity a bit. What we can do instead is create a new directory, in `App` directory, called `components`. Inside this directory, let's create a new file called `Nav.js`. We will stick to this naming convention through this tutorial, all files for both, pages and components, will always start with capital letter, and use camel case.

Next, let's take the code for our navigation we have in `main.js` and move it to this new file `Nav.js`. We have to keep in mind that we need to move just the HTML structure for our navigation. We don't have to, or even should, move the imports we defined for `Route` and all our future pages. This code will stay in `Main.js`. And, the same applies to the `Route` components we created for every page before the closing tag for the wrapper `div`. This will leave us with cleaner `Main.js` file. The result will look like the code below.

code:
```
import React from 'react'
import { Route } from 'react-router-dom'

// Import pages
import About from './pages/About'
import Contact from './pages/Contact'
import Home from './pages/Home'
import Portfolio from './pages/Portfolio'

export default class Main extends React.Component {
  render () {
    return (
      <div className="wrapper">
        <Route exact={true} path="/" component={Home}/>
        <Route path="/about" component={About}/>
        <Route path="/contact" component={Contact}/>
        <Route path="/portfolio" component={Portfolio}/>
      </div>
    )
  }
}
```

As the next step, let's turn our attention to the `Nav.js` file. Now we should add some basic styles for our navigation, but before we can do that we need to import `styled` from `styled-components` library. This will allow us to use `styled-components` to style our React website. And, let's also import `css` helper from `styled-components` library because this will be handy. Now, we can use `styled-components`, create components for navigation, list and navigation links and add some simple styling.

So far, so good. However, styling the navigation is not enough. We also have to keep in mind people who may visit our website on their mobile devices. In other words, we should make our navigation responsive. There are many different ways to achieve this. The way we will choose is using JavaScript `class` for our nav component along with React `state`. Meaning, we will create `state` with one key-value pair. This key can be `show`, for example, and its initial value will be `false`. We will do this in `constructor` method.

Then, we will create a very simple function called `toggleMenu`. This function will use `setState` to change the value of `show` key to its opposite. Next, we can create a `button`, above the navigation list, and use this function to open and close our navigation on small screens and mobile devices. The next step to make our responsive navigation is creating a `prop` on the `nav` element and set it to the value of the `show` key inside `state`. The `prop` will exist only if the value of `show` is `true`.

The final step is using `styled-components` to create necessary styles for our mobile navigation. We will use combo of `height` set to `auto` and `max-height` set to `0`. When navigation should be open, we will change the `max-height` to `1000px`. With this, we have responsive and working navigation. I will skip the rest of the styling and give you the complete code for the `Nav` component. Take this is an example and use the styles you want.

code:
```
// Nav.js
import React from 'react'
import styled, { css } from 'styled-components'

const Header = styled.header`
  position: fixed;
  top: 0;
  left: 0;
  z-index: 999;
  width: 100%;
`

const NavWrapper = styled.nav`
  padding: 16px;
  display: flex;
  justify-content: flex-end;

  @media (max-width: 479px) {
    flex-direction: column;
    align-items: flex-end;

    /* If navigation is open (show is true) */
    ${props => props.isOpen && css`
      ul {
        position: absolute;
        top: 64px;
        max-height: 1000px;
      }
    `}
  }
`

const NavList = styled.ul`
  margin: 0;
  display: flex;
  overflow: hidden;
  flex-direction: column;
  justify-content: flex-end;
  list-style-type: none;
  height: auto;
  max-height: 0;

  @media (min-width: 480px) {
    flex-direction: row;
    justify-content: flex-end;
    max-height: 1000px;
  }
`

const NavItem = styled.li`
  & + & {
    margin-top: 12px;
  }

  @media (min-width: 480px) {
    & + & {
      margin-top: 0;
      margin-left: 32px;
    }
  }

  a {
    font-size: 16px;
    font-weight: bold;
    text-decoration: none;
    color: #fff;
    transition: color .25s ease-in-out;

    &:hover {
      color: #888;
    }
  }
`

const NavButton = styled.button`
  padding: 8px 12px;
  font-size: 16px;
  font-weight: 700;
  text-decoration: none;
  text-transform: uppercase;
  color: #fff;
  background: transparent;
  border: 2px solid;
  cursor: pointer;
  transition: color .25s ease-in-out;

  &:hover {
    color: #888;
  }

  @media (min-width: 479px) {
    display: none;
  }
`

export default class Nav extends React.Component {
  constructor(props) {
    super(props)

    this.state = {
      show: false
    }

    this.toggleMenu = this.toggleMenu.bind(this)
  }

  toggleMenu() {
    this.setState({
      show: !this.state.show
    })
  }

  render () {
    return (
      <Header>
        <NavWrapper isOpen={this.state.show}>
          <NavButton onClick={this.toggleMenu}>Menu</NavButton>

          <NavList>
            <NavItem>
              <a href="/">Home</a>
            </NavItem>

            <NavItem>
              <a href="/about">About</a>
            </NavItem>

            <NavItem>
              <a href="/portfolio">Portfolio</a>
            </NavItem>

            <NavItem>
              <a href="/contact">Contact</a>
            </NavItem>
          </NavList>
        </NavWrapper>
      </Header>
    )
  }
}
```

Now, since we have a fully working and ready to use `Nav` component, we can go back the `Main.js` file and import it there, as the first child component of the wrapper `div`.

code:
```
// Main.js
import React from 'react'
import { Route } from 'react-router-dom'

// Import pages
import About from './pages/About'
import Contact from './pages/Contact'
import Home from './pages/Home'
import Portfolio from './pages/Portfolio'

// Import nav component
import Nav from './components/Nav'

export default class Main extends React.Component {
  render () {
    return (
      <div className="wrapper">
        <Nav />

        <Route exact={true} path="/" component={Home}/>
        <Route path="/about" component={About}/>
        <Route path="/contact" component={Contact}/>
        <Route path="/portfolio" component={Portfolio}/>
      </div>
    )
  }
}
```

_Something to think about: If you want to re-use any React component, such as the button we created in `Nav.js`, create a new file for it and export it from there. Then, import and use that component inside `Nav.js`, or on any other location. When you plan to work with some piece of code more than once, it is a good practice to create new React component so you don't write the same code over and over again. Let's take a look at how this might look._

code:
```
// Button.js
import styled from 'styled-components'

const Button = styled.button`
  padding: 8px 12px;
  font-size: 16px;
  font-weight: 700;
  text-decoration: none;
  text-transform: uppercase;
  color: #fff;
  background: transparent;
  border: 2px solid;
  cursor: pointer;
  transition: color .25s ease-in-out;

  &:hover {
    color: #888;
  }
`

export default Button
```

code:
```
// Nav.js
import React from 'react'
import styled, { css } from 'styled-components'

// Import Button component
import Button from './Button'

... styles for navigation

const NavButton = styled(Button)`
  @media (min-width: 479px) {
    display: none;
  }
`

export default class Nav extends React.Component {
  constructor(props) {
    super(props)

    this.state = {
      show: false
    }

    this.toggleMenu = this.toggleMenu.bind(this)
  }

  toggleMenu() {
    this.setState({
      show: !this.state.show
    })
  }

  render () {
    return (
      <header>
        <NavWrapper isOpen={this.state.show}>
          <NavButton onClick={this.toggleMenu}>Menu</NavButton>

          <NavList>
            <NavItem>
              <a href="/">Home</a>
            </NavItem>

            <NavItem>
              <a href="/about">About</a>
            </NavItem>

            <NavItem>
              <a href="/portfolio">Portfolio</a>
            </NavItem>

            <NavItem>
              <a href="/contact">Contact</a>
            </NavItem>
          </NavList>
        </NavWrapper>
      </header>
    )
  }
}
```

### Adding a few more components

We have a working version of navigation. As the next step, we can take care about the first page for our React website, the homepage. Before we do that, it will be useful to create one component we will use on all pages. This component will be for grid container. In order to make this React tutorial shorter, we will create only container. However, if you want the whole grid system, you can find the code you need in this [tutorial] on Create Flipping Card & Responsive Grid with Styled-components & React.

Our component for container will be very simple. We will need only few styles and four breakpoints to change the `max-width` of the container component. And, since we are creating general React components let's also create a couple of components for our typography elements. To keep our React website project tidy, we can put all components for typography into one file. Let's call this file `Typography.js` and put inside `components` directory, right next to the `Container.js` with container component.

code:
```
// Container.js
import styled from 'styled-components'

const Container = styled.div`
  padding-right: 15px;
  padding-left: 15px;
  margin-right: auto;
  margin-left: auto;
  width: 100%;

  /* Breakpoint for tablets */
  @media (min-width: 576px) {
    max-width: 540px;
  }

  /* Breakpoint for small desktops */
  @media (min-width: 768px) {
    max-width: 720px;
  }

  /* Breakpoint for medium desktops */
  @media (min-width: 992px) {
    max-width: 960px;
  }

  /* Breakpoint for large desktops and HD devices */
  @media (min-width: 1200px) {
    max-width: 1140px;
  }
`

export default Container
```

code:
```
// Typography.js
import styled from 'styled-components'

export const Heading = styled.h1`
  margin-top: 0;
  margin-bottom: 0;
  font-size: 36px;
  font-weight: bold;

  @media (min-width: 480px) {
    font-size: 48px;
  }

  @media (min-width: 768px) {
    font-size: 72px;
  }

  & + ${Subheading} {
    margin-top: 32px;
  }
`

export const Subheading = styled.h2`
  margin-top: 0;
  margin-bottom: 0;
  font-size: 24px;
  font-weight: bold;

  @media (min-width: 480px) {
    font-size: 36px;
  }

  @media (min-width: 768px) {
    font-size: 48px;
  }
`
```

### Creating our first page, the homepage

Now, we can create our homepage. This will be a very simple homepage. Our homepage will use photo as a background with light dark overlay. We will create this overlay with `::before` pseudo-element. In the terms of the content, there will be one primary heading and one secondary heading. We will import and use the `Heading` and `Subheading` components we created previously. Below the secondary heading will be a `button` leading to Portfolio page. And, this is where we will end today.

code:
```
import React from 'react'
import styled from 'styled-components'
import { Link } from 'react-router';

// Import Container component
import Button from './../components/Button'
import Container from './../components/Container'

// Import Typography components
import { Heading, Subheading } from './../components/Typography'

const HomeWrapper = styled.section`
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100%;
  background-image: url(https://source.unsplash.com/t3zrEm88ehc/480x800);
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;

  @media (min-width: 480px) {
    background-image: url(https://source.unsplash.com/t3zrEm88ehc/768x1024);
  }

  @media (min-width: 768px) {
    background-image: url(https://source.unsplash.com/t3zrEm88ehc/1280x800);
  }

  @media (min-width: 1280px) {
    background-image: url(https://source.unsplash.com/t3zrEm88ehc/1600x900);
  }

  @media (min-width: 1600px) {
    background-image: url(https://source.unsplash.com/t3zrEm88ehc/1920x1080);
  }

  &::before {
    position: absolute;
    top: 0;
    left: 0;
    z-index: 1;
    content: '';
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, .4);
  }

  ${Container} {
    position: relative;
    z-index: 2;
    color: #fff;
  }

  ${Subheading} {
    margin-bottom: 32px;
  }
`

// Using Button component but changing the element to 'a'
const HomeButton = Button.withComponent('a')

export default class Home extends React.Component {
  render () {
    return (
      <HomeWrapper>
        <Container>
          <Heading>Thomas Paine</Heading>

          <Subheading>Designer & developer</Subheading>

          <HomeButton href="/portfolio">My work</HomeButton>
        </Container>
      </HomeWrapper>
    )
  }
}
```

## Closing thoughts on building a website with React, React Router & styled-components

Congratulations! You just finished the second part of this tutorial on how to build a website with React, React Router and styled-components. Let's do a quick recap. Today, we started by learning how to use `injectGlobal`. After that, we created our first smaller component for main navigation. Then, we used `state` to add some functionality and make it responsive. Next, we created a few more components for `Button`, `Container` and some typography elements.

When we finished our work on these components, we put together the first page for our React website, the homepage. Our homepage is very simple and contains only a small amount of content. However, as Robert Browning wrote in his poem "Andrea del Sarto", less is more. Also, the goal of this React tutorial is to show you how to use React to build your own website. What content, and how much of it, will it contain is completely and only up to you.

I hope you enjoyed this second part, had fun and learned something new. In the next and last part, we will take care about the rest of our React website and create Portfolio, About and Contact pages. With that, we will build a simple React website you can customize and use as you want. Until then, work on your knowledge of React and styled-components and remember that deliberate practice is important for learning. Have a great day.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[part 1]: https://blog.alexdevero.com/build-website-react-pt1/
[A Simple Introduction to Styled-components]: https://blog.alexdevero.com/introduction-styled-components/
[Styled-Components – Mastering the Fundamentals Through Practice]: https://blog.alexdevero.com/styled-components-mastering-fundamentals/
[documentation]: https://www.styled-components.com/docs
[injectGlobal]: https://www.styled-components.com/docs/api#injectglobal
[tutorial]: https://blog.alexdevero.com/flipping-card-grid-styled-components-react/

<!-- ### Inspiration
-
 -->
