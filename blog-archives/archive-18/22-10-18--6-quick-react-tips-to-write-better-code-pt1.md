# 6 Quick React Tips to Write A Better Code Pt.1

Have you ever wanted to know some quick React tips to help you write a better code? You are on the right place. This two-part series will give you six of these React tips. These tips will cover a variety of topics. However, all will share the same goal, to help you write a better code and make your work easier and more enjoyable. Let's begin.

<!--
Table of Contents:
## Keep your components small
## Use stateless components
## Choose one approach for styling and stick with it
## Epilogue: 6 Quick React Tips to Write A Better Code Pt.1
-->

## Keep your components small

Take a look at some of your React components. How big are they? How much code do they contain? Is it easy for someone new who never worked with your components before to understand the code? There is usually some chance that at least some of your components will be quite big. This is especially true if you are a beginner without more prior experience with React or programming.

You don't have to feel bad if this is your case, if your current practice results in quite big components. Almost everyone does in the beginning. You should see some of the code I wrote when I started working with React. Back then my code was a disaster. Well, there is still a lot of polishing to do. However, I am working on it and making a decent progress.

Many of us have some experience with bloated code and big React components. This is not the ideal state one should aim for, rather the opposite. Your React components should be small. Don't be afraid that this practice will result to having "too" many files. This is something I was worried about when I started with [Atomic Design]. Yes, you will end up with more files.

On the other hand, it will be much easier for you to work with and maintain your code, as well as whole projects. This is one of the easiest React tips you can learn about. It is also one of those React tips you can implement almost immediately and often with relative ease.

Let's take a look at a simple example of a landing page. This page will contain header, hero, a number of small sections and footer. In the first version we will put everything in one file.

Before:
```
// Import React and ReactDOM
import React from 'react'
import { render } from 'react-dom'

// The main component for our landing page
class LandingPage extends React.Component {
  render() {
    return (
      <div className="wrapper">
        <header>
          <nav>
            <ul>
              <li><a href="#who">Who we are</a></li>
              <li><a href="#work">How we work</a></li>
              <li><a href="#gallery">Gallery</a></li>
              <li><a href="#clients">Our clients</a></li>
              <li><a href="#contact">Contact</a></li>
            </ul>
          </nav>
        </header>

        <section>
          <h1>Change the way you develop apps</h1>

          <h2>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</h2>

          <a href="work.html">See how we can help</a>
        </section>

        <section id="who">
          <div className="container">
            <h1>Who we are</h1>

            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</p>
          </div>
        </section>

        <section id="work">
          <div className="container">
            <h1>How we work</h1>

            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
          </div>
        </section>

        <section id="gallery">
          <div className="container">
            <h1>Gallery</h1>

            <div class="row">
              <div class="col-md-6 col-lg-4">
                <a href="">
                  <img src="images/img-00" alt="Artwork 00">
                </a>
              </div>

              <div class="col-md-6 col-lg-4">
                <a href="">
                  <img src="images/img-01" alt="Artwork 01">
                </a>
              </div>

              <div class="col-md-6 col-lg-4">
                <a href="">
                  <img src="images/img-02" alt="Artwork 02">
                </a>
              </div>
            </div>

            <div class="row">
              <div class="col-md-6 col-lg-4">
                <a href="">
                  <img src="images/img-03" alt="Artwork 03">
                </a>
              </div>

              <div class="col-md-6 col-lg-4">
                <a href="">
                  <img src="images/img-04" alt="Artwork 04">
                </a>
              </div>

              <div class="col-md-6 col-lg-4">
                <a href="">
                  <img src="images/img-05" alt="Artwork 05">
                </a>
              </div>
            </div>
          </div>
        </section>

        <section id="clients">
          <div className="container">
            <h1>Clients</h1>

            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>

            <div class="row">
              <div class="col-md-6 col-lg-4">
                <a href="">
                  <img src="images/logos/logo-tesla.svg" alt="Tesla logo">
                </a>
              </div>

              <div class="col-md-6 col-lg-4">
                <a href="">
                  <img src="images/logos/logo-spacex.svg" alt="Spacex logo">
                </a>
              </div>

              <div class="col-md-6 col-lg-4">
                <a href="">
                  <img src="images/logos/logo-microsoft.svg" alt="Microsoft logo">
                </a>
              </div>
            </div>

            <div class="row">
              <div class="col-md-6 col-lg-4">
                <a href="">
                  <img src="images/logos/logo-uber.svg" alt="Uber logo">
                </a>
              </div>

              <div class="col-md-6 col-lg-4">
                <a href="">
                  <img src="images/logos/logo-intel.svg" alt="Intel logo">
                </a>
              </div>

              <div class="col-md-6 col-lg-4">
                <a href="">
                  <img src="images/logos/logo-adobe.svg" alt="Adobe logo">
                </a>
              </div>
            </div>
          </div>
        </section>

        <section id="contact">
          <div className="container">
            <h1>Get in touch with us</h1>

            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>

            <a href="mailto:example@email.com">example@email.com</a>
          </div>
        </section>

        <footer>
          <ul>
            <li>
                <a href="" rel="noopener"><span className="fab fa-slack" /></a>
            </li>

            <li>
                <a href="o" rel="noopener"><span className="fab fa-github" /></a>
            </li>

            <li>
                <a href="" rel="noopener"><span className="fab fa-twitter" /></a>
            </li>

            <li>
                <a href="" rel="noopener"><span className="fab fa-facebook-f" /></a>
            </li>
          </ul>
        </footer>
      </div>
    )
  }
}

// Render the LandingPage in the DOM
render(<LandingPage />, document.getElementById('root'))
```

Now, let's take a look at what we can do with our landing page and code. Let's say that we decide to split the whole landing page into smaller pieces and files. Then, we will import all those pieces and use them to replace the previous markup. The result can be following.

After:
```
// Import React and ReactDOM
import React from 'react'
import { render } from 'react-dom'

// Import page components
import { Header } from 'Components/Header'
import { SectionHero } from 'Components/SectionHero'
import { SectionWho } from 'Components/SectionWho'
import { SectionWork } from 'Components/SectionWork'
import { SectionGallery } from 'Components/SectionGallery'
import { SectionClients } from 'Components/SectionClients'
import { SectionContact } from 'Components/SectionContact'
import { Footer } from 'Components/Footer'

// The main component for our landing page
class LandingPage extends React.Component {
  render() {
    return (
      <div className="wrapper">
        <Header />

        <SectionHero />

        <SectionWho />

        <SectionWork />

        <SectionGallery />

        <SectionClients />

        <SectionContact />

        <Footer />
      </div>
    )
  }
}

// Render the LandingPage in the DOM
render(<LandingPage />, document.getElementById('root'))
```

As you can see, the code looks cleaner and is more readable. Well, at least in the case of our landing page. However, if we consider the HTML markup we replaced, our new components should look good as well.

## Use stateless components

This brings us to the second item on our list of React tips. You don't have to use JavaScript classes every time you create a new component. Instead, you can use stateless, or functional, components when you don't need state. The majority of components in the previous example doesn't need or require state. So, there is no reason, other than your aesthetic taste, to use classes.

And, if we need to pass some data from the `LandingPage`, we will probably use `props`. There is really no reason to use JavaScript `class`. Let's take a look at example of one of our components, the header for example. First, we will create it with JavaScript `class`, or stateful component. Then, we will create it with function, as a stateless or functional component.

Header as a stateful component:
```
// Import React and ReactDOM
import React from 'react'

// Stateful component for header
export class Header extends React.Component {
  render() {
    return (
      <header>
        <nav>
          <ul>
            <li><a href="#who">Who we are</a></li>
            <li><a href="#work">How we work</a></li>
            <li><a href="#gallery">Gallery</a></li>
            <li><a href="#clients">Our clients</a></li>
            <li><a href="#contact">Contact</a></li>
          </ul>
        </nav>
      </header>
    )
  }
}
```

Header as a stateless (functional) component:
```
// Import React and ReactDOM
import React from 'react'

// Stateless component for header
export const Header = props => {
  return (
    <header>
      <nav>
        <ul>
          <li><a href="#who">Who we are</a></li>
          <li><a href="#work">How we work</a></li>
          <li><a href="#gallery">Gallery</a></li>
          <li><a href="#clients">Our clients</a></li>
          <li><a href="#contact">Contact</a></li>
        </ul>
      </nav>
    </header>
  )
}
```

Both results look very similar. However, the second one with stateless or functional header component still contains less code than the first one. This is the first benefit of using stateless components. You write a little bit less code and, in turn, you code can be more readable. The second benefit is that it is easier to understand what a component does.

There are only props and HTML in stateless components. If something doesn't work, the problem is in one of these two. This also makes components easier to test. If you pass some data through props, you know that you should expect the component to return a specific markup. Props either work or they don't. You either get the result you desired or you don't.

If you don't get what you expected, you know where to look for issues. Or, at least where you should start. The third benefit is again that stateless components can help you improve the performance of your app, or project. Why? Stateless components are transpiled to less code than class components. So, the final bundle will be smaller. Sure, this difference will vary from case to case.

Another reason for expecting a better performance is that stateless components don't contain state or lifecycle methods. This means that it is not necessary to do as many comparisons, checks and memory allocation like in the case of stateful components. This has been even mentioned by people behind React. So, this might be one of the React tips with bright future.

Whether you use stateless, functional, components is up to you. Many developers like and prefer the `class` syntax. This is especially true for developers with experience with OOP. So, think about it and decide for yourself. And, even if you decide to stick with `class` syntax, consider using stateless components at least for those really small components. You can save a lot of code.

A small stateful component:
```
// Import React and ReactDOM
import React from 'react'

export class User extends React.Component {
  render() {
    const { firstName, lastName, role } = this.props

    return (
      <div>
        <p>Hi, I am {firstName} {lastName} and my job is {role}.</p>
      </div>
    )
  }
}
```

The same example, but as stateless component:
```
export const Info = ({firstName, lastName, role}) => <div><p>Hi, I am {firstName} {lastName} and my job is {role}.</p></div>
```

## Choose one approach for styling and stick with it

The third item on our list of React tips is all about styling. This is a never-ending debate. Should you keep CSS styles in separate CSS files or use [CSS modules]? Or, should you declare them right inside JavaScript. And, if so, should you use inline styles or some library such as styled-components, [Radium], [emotion], [aphrodite] or any other?

I think that the best answer is that it doesn't really matter so much. All these approaches have their pros and cons, their benefits and pains. And, from the performance view? Well, hard to say as this depends on how much code do you write. The most important factor is that you are comfortable with it. Forget any React tips and tricks. You are the one writing the code.

Anyway, when you make a decision and choose the approach you like, stick with it. One of the best ways to write cleaner code, going beyond these React Tips, is consistency. If you decide to style your components with imported CSS or CSS modules great. If you decide to use inline styles great. The same if you pick any of the [CSS-in-JS] libraries. Follow your taste. Just stick with it.

The worst thing you can do is following multiple approaches and mixing them together. That can lead to a disaster, especially if you work with a lot of code and large projects. Imagine the time debugging broken styles would take if you had to look at multiple places. All that just because you declared some styles as inline, some in CSS stylesheet and some with CSS-in-JS library.

Stay away from this practice, even in case where it looks like there is no other solution. It is often better to spend a little bit more time on thinking than a lot of time on debugging. Plus, it will lead to fewer headaches. Think about the issue at hand again. If you should remember only one of the React tips we discussed today, be it this one. Be consistent.

## Epilogue: 6 Quick React Tips to Write A Better Code Pt.1

This is all for this first part of this React tips mini series. I hope that you enjoyed reading this first batch of React tips to write a better code. I also hope that you've learned something that will really help you write a better code. Something that will help you do your work better and faster. These are some of the factors that can make a lot of difference.

These factors can make your work much more enjoyable. It can make it something you look forward to do. When this happens, be glad for it. Now, the last question. What can you expect in the second batch of React tips? We will take a look at what we can do with state, play with propTypes, explore presentational and container components and more.

When put together, these two batches of React tips will help you take your expertise to a whole new level. Now, it is up to you to take the React tips we discussed today and implement those you like. And, as always, practice writing code since this is the best way to learn it and get better at it. Thank you for your time. I look forward to seeing you here again the next week. Until then, have a great day!

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Atomic Design]: https://blog.alexdevero.com/atomic-design-scalable-modular-css-sass/
[CSS modules]: https://github.com/css-modules/css-modules
[styled-components]: https://www.styled-components.com/
[Radium]: https://formidable.com/open-source/radium/
[emotion]: https://github.com/emotion-js/emotion
[aphrodite]: https://github.com/Khan/aphrodite
[CSS-in-JS]: https://github.com/MicheleBertoli/css-in-js

<!--
#### Inspiration:
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
