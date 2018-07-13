# How to Build a Website with [React], React Router & Styled-Components Pt.3

React gained a lot of popularity. We can say that it became probably the most popular JavaScript library for building user interfaces. Its flexibility allows us to create anything we want, from apps, to websites. This tutorial is about the second. Its goal is to show you how to use React, react-router and styled-components to build your own simple website. In this part, we will create the rest of the pages and finish our React website. Let's begin!

<!--
Table of Contents:
## Styled-components + React Pt.3
## About page and additional components
### Bringing in modularity
### Putting together the About page
## Portfolio page and a simple grid
## Contact page and Font Awesome
## Closing thoughts on building a website with React, React Router & styled-components
How to Build a Website with React, React Router & Styled-Components [part 1].
How to Build a Website with React, React Router & Styled-Components [part 2].
-->

## Styled-components + React Pt.3

Welcome back. This is the third and final part of this tutorial focused on building a simple website with React, react-router and styled-Components. We did a lot of work in the previous part. The last thing we managed to do was creating and styling a simple homepage. As I mentioned above, today, our goal will be about finishing our website. We will start with creating About page. After that, we will build another page, now it will be for our Portfolio. Finally, we will put together the Contact page.

## About page and additional components

The first page we will take a look at, at this part, will be About page. The structure for this page will be very simple. This page will contain one primary heading, one secondary heading, two paragraphs of text and CTA in the form of a simple link with email contact. Since this page will not contain as much content, we can use the same layout we used on our homepage. In other words, we can use flexbox and, when the screen is large enough, center the content vertically.

### Bringing in modularity

This leaves us with two choices. First, we can simply copy and paste some parts of the code we wrote for homepage. This is a very fast way to replicate the layout. However, it is also a very bad practice, at least this is what I think. Copying and pasting code over and over again will quickly start to backfire. This practice will make our code bigger, more complex and harder to maintain. What we should do instead is embrace [modularity] and abstract the code into new React component.

Let's create one new file inside the `components` directory called `Section.js`. Next, we can grab some part of the code we wrote for our homepage and put it here. And, as the final step, we will import and use this component on homepage and remove the, now redundant, code. A couple of things. It is necessary to add import for `styled-components`, with `css` helper, and also for `Container` component. With this, we will be able to create custom component and also add some styles for Container inside the Section.

_Note: Section component will be centered vertically only if it has `centered` props. Otherwise, styles for centering will not be applied._

Code:
```
// Section.js
import styled, { css } from 'styled-components'

// Import Container component
import Container from './Container'

const Section = styled.section`
  ${props => props.centered && css`
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100%;
  `}

  ${Container} {
    position: relative;
    z-index: 2;
  }
`

export default Section
```

Code:
```
// Home.js
import React from 'react'
import styled from 'styled-components'
import { Link } from 'react-router';

// Import Button component
import Button from './../components/Button'

// Import Container component
import Container from './../components/Container'

// Import Section component
import Section from './../components/Section'

// Import typography components
import { Heading, Subheading } from './../components/Typography'

const HomeWrapper = styled(Section)`
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
      <HomeWrapper centered>
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

### Putting together the About page

Now, we can go back and build the About page. Keep in mind that, at the top of the page, we need to import `react` and `styled-components`. We will import these two libraries on every page. Next, we will also need to import `Container`, `Section` as well as all our typography components. When we are talking about typography components ... Let's quickly visit the `Typography.js` file and create new component for text, and some additional styles for space management between primary and secondary heading and text.

Code:
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

  // Styles for handling spacing between typography elements
  & + h1,
  & + h2,
  & + p {
    margin-top: 21px;
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

  // Styles for handling spacing between typography elements
  & + h1,
  & + h2,
  & + p {
    margin-top: 21px;
  }
`

export const Text = styled.p`
  margin-top: 0;
  font-size: 16px;

  @media (min-width: 768px) {
    font-size: 18px;
  }

  @media (min-width: 992px) {
    font-size: 21px;
  }

  & + & {
    margin-top: 32px;
  }
`
```

Now, we can add the `Text` component to the imports for typography components. One more thing. Why not to use the link with email not only on this page, but on others as well? You know what I am talking about. We should prepare for the future and quickly create another small component, now for the link. Styling for the link will be simple. We will remove the underline, change color and make the text bolder. When we are done with that, we add import for `Link` component on our About page.

Code:
```
// Link.js
import styled from 'styled-components'

const Link = styled.a`
  font-weight: bold;
  text-decoration: none;
  color: #7f8c8d;
  transition: color .25s ease-in-out;

  &:focus,
  &:hover {
    color: #95a5a6;
  }
`

export default Link
```

For the About page itself, all we need to do now is to add some content. Simple primary heading and secondary heading, two paragraphs and link with email contact I mentioned will do the job, at least for this tutorial. For your own React, choose the content you want and that reflects you. Remember, the best person you can be is yourself. So, describe yourself with honesty. Just make sure to focus mainly on information that will be useful and interesting for the people you want to attract (clients, employers, etc.).

Code:
```
// About.js
import React from 'react'
import styled from 'styled-components'

// Import Container component
import Container from './../components/Container'

// Import Link component
import Link from './../components/Link'

// Import Section component
import Section from './../components/Section'

// Import typography components
import { Heading, Subheading, Text } from './../components/Typography'

export default class About extends React.Component {
  render () {
    return (
      <Section centered>
        <Container>
          <Subheading>Thomas Paine</Subheading>

          <Heading>About Me</Heading>

          <Text>I am a digital designer and developer originally from London and based in New York with over 10 years of experience in the industry. I am a passionate creative that always leads by example and likes to get his hands dirty. I believe that design is only as powerful as the message it is able to carry. I constantly seek to inspire, and build the best work possible. I am a critical thinker and problem solver that pursues a holistic approach. I always make sure every aspect gets produced at the highest quality.</Text>

          <Text>Now I am working full time freelance as a designer and developer, building interactive digital products for clients from around the World. If you are interested in a new project, collaboration, or just to chat, feel free to contact me:</Text>

          <a href="mailto:email@example.com">email@example.com</a>
        </Container>
      </Section>
    )
  }
}
```

## Portfolio page and a simple grid

Portfolio will be the next page we will create for our React website. This page will follow the simplicity of our website. There will be one primary heading, one secondary heading, a number of examples of work and CTA link with email at the bottom. These examples will be `img` elements wrapped inside `a` elements. For this tutorial, we are going to use some royalty-free photos provided by [Unsplash]. For your own web, use the best examples of your work. Focus on quality, not quantity. In this case, less is often more.

The only one a little bit more difficult thing on the portfolio page will be layout of columns inside a grid we will use to present the examples of our work. For this tutorial, we will use a grid with one example per line on mobile, two examples on tablets and three examples on desktops and big screens. Instead of creating a full grid system, we will create a container called `PortfolioGrid` and apply `flexbox` to it. Then, we will change the `width` of the individual `a` elements, or `PortfolioItem`.

Code:
```
// Portfolio.js
import React from 'react'
import styled from 'styled-components'

// Import Container component
import Container from './../components/Container'

// Import Link component
import Link from './../components/Link'

// Import Section component
import Section from './../components/Section'

// Import typography components
import { Heading, Subheading, Text } from './../components/Typography'

const PortfolioWrapper = styled(Section)`
  padding-top: 120px;
  padding-bottom: 80px;
`
const PortfolioGrid = styled.div`
  padding-bottom: 32px;
  display: flex;
  flex-wrap: wrap;
`

const PortfolioItem = styled.a`
  display: block;
  cursor: pointer;
  width: 100%;
  transition: opacity .25s ease-in-out;

  &:focus,
  &:hover {
    opacity: .5;
  }

  @media (max-width: 767px) {
    &:nth-child(n+2) {
      margin-top: 16px;
    }
  }

  @media (min-width: 768px) and (max-width: 991px) {
    width: calc(50% - 32px);

    &:nth-child(odd) {
      margin-right: 32px;
    }

    &:nth-child(even) {
      margin-left: 32px;
    }

    &:nth-child(n+3) {
      margin-top: 48px;
    }
  }

  @media (min-width: 992px) {
    width: calc(33.33333% - 32px);

    &:first-child,
    &:nth-child(4),
    &:nth-child(7) {
      margin-right: 32px;
    }

    &:nth-child(2),
    &:nth-child(4),
    &:nth-child(8), {
      margin-left: 16px;
      margin-right: 16px;
    }

    &:nth-child(3),
    &:nth-child(6),
    &:last-child {
      margin-left: 32px;
    }

    &:nth-child(n+4) {
      margin-top: 24px;
    }
  }
`

const PortfolioItemThumbnail = styled.img`
  max-width: 100%;
  object-fit: contain;
`

export default class Portfolio extends React.Component {
  render () {
    return (
      <PortfolioWrapper>
        <Container>
          <Subheading>Thomas Paine</Subheading>

          <Heading>My work</Heading>

          <Text>Selected examples of my work. If you want to see more, drop me an email.</Text>

          <PortfolioGrid>
            <PortfolioItem href="">
              <PortfolioItemThumbnail src="https://source.unsplash.com/z4CAuzwaXrM/600x600" srcSet="https://source.unsplash.com/z4CAuzwaXrM/600x600 1x, https://source.unsplash.com/z4CAuzwaXrM/1200x1200 2x" alt="Example of work" />
            </PortfolioItem>

            <PortfolioItem href="">
              <PortfolioItemThumbnail src="https://source.unsplash.com/-aDl1z8_nGY/600x600" srcSet="https://source.unsplash.com/-aDl1z8_nGY/600x600 1x, https://source.unsplash.com/-aDl1z8_nGY/1200x1200 2x" alt="Example of work" />
            </PortfolioItem>

            <PortfolioItem href="">
              <PortfolioItemThumbnail src="https://source.unsplash.com/qvEwMfUX_DM/600x600" srcSet="https://source.unsplash.com/qvEwMfUX_DM/600x600 1x, https://source.unsplash.com/qvEwMfUX_DM/1200x1200 2x" alt="Example of work" />
            </PortfolioItem>

            <PortfolioItem href="">
              <PortfolioItemThumbnail src="https://source.unsplash.com/9QjbejABFn8/600x600" srcSet="https://source.unsplash.com/9QjbejABFn8/600x600 1x, https://source.unsplash.com/9QjbejABFn8/1200x1200 2x" alt="Example of work" />
            </PortfolioItem>

            <PortfolioItem href="">
              <PortfolioItemThumbnail src="https://source.unsplash.com/cDD83wV627U/600x600" srcSet="https://source.unsplash.com/cDD83wV627U/600x600 1x, https://source.unsplash.com/cDD83wV627U/1200x1200 2x" alt="Example of work" />
            </PortfolioItem>

            <PortfolioItem href="">
              <PortfolioItemThumbnail src="https://source.unsplash.com/KDYcgCEoFcY/600x600" srcSet="https://source.unsplash.com/KDYcgCEoFcY/600x600 1x, https://source.unsplash.com/KDYcgCEoFcY/1200x1200 2x" alt="Example of work" />
            </PortfolioItem>

            <PortfolioItem href="">
              <PortfolioItemThumbnail src="https://source.unsplash.com/oKfCxcKnCo8/600x600" srcSet="https://source.unsplash.com/oKfCxcKnCo8/600x600 1x, https://source.unsplash.com/oKfCxcKnCo8/1200x1200 2x" alt="Example of work" />
            </PortfolioItem>

            <PortfolioItem href="">
              <PortfolioItemThumbnail src="https://source.unsplash.com/dClHqW-EfS8/600x600" srcSet="https://source.unsplash.com/dClHqW-EfS8/600x600 1x, https://source.unsplash.com/dClHqW-EfS8/1200x1200 2x" alt="Example of work" />
            </PortfolioItem>

            <PortfolioItem href="">
              <PortfolioItemThumbnail src="https://source.unsplash.com/74elF-XSsPg/600x600" srcSet="https://source.unsplash.com/74elF-XSsPg/600x600 1x, https://source.unsplash.com/74elF-XSsPg/1200x1200 2x" alt="Example of work" />
            </PortfolioItem>
          </PortfolioGrid>

          <Text>Let's get in touch:</Text>

          <Link href="mailto:email@example.com">email@example.com</Link>
        </Container>
      </PortfolioWrapper>
    )
  }
}
```

## Contact page and Font Awesome

We are the final chapter of this tutorial. There is only one page we need to create in order to finish our React website, the Contact page. This page will be very simple as well. Its content will be one primary heading, some text, CTA link with email and list with a couple of useful links to social media profiles and profiles on other websites. We will use [Font Awesome] to render these links. This gives us two tasks. First, we need to add link to Font Awesome. Second, we can create small React component for icons.

Let's start with the first task, adding link to Font Awesome. We can use either local version of the font, or we can use version hosted on CDN. For now, let's choose the version hosted on CDN. So, open the `index.html` file and add link to Font Awesome to the `head`.

Code:
```
<!DOCTYPE html>
<html lang="en">
<head>
  ... some code ...

  <!-- Font Awesome - icon font -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
</head>

<body>
  <!-- Main React component -->
  <div id="app"></div>

  <script src='./index.js'></script>
</body>
</html>
```

Now, we can take care about the second task and create new React component for icons. We will create this component as a [stateless function] with one parameter, type of the icon we want to render. Returned element will be a `span` with `className` set to "fa" and type of icon we want prefixed with "fa-". We will use [template literals] and placeholder to make this simpler. Let's save this component as `AwesomeIcon.js`.

```
import React from 'react'

const AwesomeIcon = ({ icon }) => (
	<span className={`fa fa-${icon}`}></span>
)

export default AwesomeIcon
```

Now, can create new file, `Contact.js`, inside `pages` directory, add necessary imports and put together the Contact page for our React website. With that, our new website is finally complete!

Code:
```
// Contact.js
import React from 'react'
import styled from 'styled-components'

// Import AwesomeIcon
import AwesomeIcon from './../components/AwesomeIcon'

// Import Container component
import Container from './../components/Container'

// Import Link component
import Link from './../components/Link'

// Import Section component
import Section from './../components/Section'

// Import typography components
import { Heading, Text } from './../components/Typography'

const ContactLink = styled(Link)`
  margin-bottom: 32px;
  display: inline-block;
  font-size: 16px;

  @media (min-width: 768px) {
    font-size: 18px;
  }
`

const SocialMediaList = styled.ul`
  padding: 0;
  margin: 0;

  li {
    display: inline-block;
    list-style-type: none;

    &:not(:last-child) {
      margin-right: 16px;
    }
  }


  a {
    font-size: 18px;

    @media (min-width: 480px) {
      font-size: 24px;
    }
  }
`

export default class Contact extends React.Component {
  render () {
    return (
      <Section centered>
        <Container>
          <Heading>Say hello</Heading>

          <Text>I'm available for freelance work. If you are interested in a new project, collaboration, or just to chat, feel free to contact me.</Text>

          <ContactLink href="mailto:email@example.com">email@example.com</ContactLink>

          <Text>Follow me on the web:</Text>

          <SocialMediaList>
            <li>
              <Link href="">
                <AwesomeIcon icon="twitter" />
              </Link>
            </li>

            <li>
              <Link href="">
                <AwesomeIcon icon="linkedin" />
              </Link>
            </li>

            <li>
              <Link href="">
                <AwesomeIcon icon="behance" />
              </Link>
            </li>

            <li>
              <Link href="">
                <AwesomeIcon icon="dribbble" />
              </Link>
            </li>

            <li>
              <Link href="">
                <AwesomeIcon icon="github" />
              </Link>
            </li>

            <li>
              <Link href="">
                <AwesomeIcon icon="codepen" />
              </Link>
            </li>
          </SocialMediaList>
        </Container>
      </Section>
    )
  }
}
```

## Closing thoughts on building a website with React, react-router & styled-components

You made it! Congratulations! You used the power of React, react-router and styled-components and created your own React website. We wrote a lot of code through this mini series and I hope that you enjoyed it and had fun. I also hope that this tutorial helped you learn something new, or that it helped you get better in something you already know. In the end, it is the deliberate, purposeful practice that is usually the best and fastest way to learn something.

This may sound stupid. When I was planning this tutorial, there was one thing I was constantly thinking about. I wasn't exactly sure about how much code should I use for this tutorial. I wanted to help you learn how to build website using React. The idea was to keep it simple and uncluttered and to give you something you can customize as much as you can. Something like a boilerplate. As a result, the design of the example page is very simple and austere.

So, now it is your turn. Take this boilerplate customize it to your liking and build an amazing React website.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[part 1]: https://blog.alexdevero.com/build-website-react-pt1/
[part 2]: https://blog.alexdevero.com/build-website-react-pt2/
[modularity]: https://blog.alexdevero.com/write-clean-css-10-simple-steps-pt1/
[Unsplash]: https://unsplash.com/
[Font Awesome]: http://fontawesome.io/
[stateless function]: https://hackernoon.com/react-stateless-functional-components-nine-wins-you-might-have-overlooked-997b0d933dbc
[template literals]: https://developer.mozilla.org/cs/docs/Web/JavaScript/Reference/Template_literals

<!-- ### Inspiration
-
 -->
