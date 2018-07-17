# A Simple Introduction to Styled-components - Modular CSS and Reactjs

Have you ever heard about styled-components? Chances are that you did, at least if you have some experience with app development, or Reactjs. This is a very interesting take on modular CSS. What is this styled-components thing about? As its website says, its goal is to help developers style their apps without any stress. Let's take a look at what it is and how we can use it.

<!--
Table of Contents:
The past
Before styled-components
The world of styled-components
How it works
Getting started with styled-components
Standing on the shoulders of giants
Styled-components and CSS animations
Styled-components and props
Closing thoughts on styled-components
-->

## The past

There are many approaches to how to create modular CSS. Currently the most popular ones are probably [Atomic CSS], [SMACSS],  [OOCSS] and [ITCSS]. All these approaches have at least one thing in common, web developers are usually using them either with [Sass], [Less] or [PostCSS]. Well, there are some developers who use one of these approaches with good old vanilla CSS as well. However, that is a relatively rare to see.

I think that there could be at least two main causes. First, good old CSS was not built for modularity. CSS originated in times when no one was even thinking about splitting CSS stylesheet into multiple files, something like modules. Having just one stylesheet was enough to get the job done. Also, imagine linking multiple stylesheet or using imports. Neither of those things are considered the best practices.

Finally, websites were often less complex than they are today. Well, there are always some edge cases and outliers. However, I think that the average website was still rather simple. When you have a CSS that is still relatively easy to maintain, there is nothing that nudges you to think about making a change. You just keep doing what you always did and that was sufficient. Well, this is just my theory.

Then, there is a second reason why it is so rare to see someone to use modular approach with vanilla CSS. For many developers, it is often part of the learning path to learn how to use one or more preprocessors. When a beginner learns the basic and advanced topics of CSS, he will usually get some advice to try this or that preprocessor. And, after he learns how to use one, why would he ever want to look back?

## Before styled-components

Nowadays, a large part of the world of web development moved to a web app development. This different world may require different tools. This is where styled-components enter the scene. So, how different is it is to work with styled-components? If you are used to using stylesheets, a lot. With styled-component, stylesheets are no longer necessary. You write all your CSS right in JavaScript files.

As a result, you may end up with a smaller amount of files. This can help you keep your app more maintainable. And, this is just one thing. Another is that there is no longer a reason to use CSS classes. Well, at least not in the usual fashion. In the past, when you wanted to add some styles to an element, you would do it by using a CSS class, or selector, and then attach this class to that element.

Before styled-components, you would usually use one of four approaches. One, you could define these styles in an external CSS stylesheet and then use this class as needed. Two, you could again use external stylesheet but now you would import the styles, you wanted to use, in specific component. Three, you could style your components using inline styles. Or, four, you could use [CSS modules].

Example one - external CSS + classes:
```
/* in _card.css */
.card__wrapper {
  padding: 16px;
	width: 320px;
  border: 1px solid #eee;
}

.card__header {
  font-size: 21px;
  font-weight: bold;
  text-align: center;
  color: #212121;
}


// In react component
import React from 'react'

const Card = () => (
  <div className="card__wrapper">
    <header className="card__header">This changes everything!</p>
  </div>
)

export default Card
```

Example two - external CSS + classes + imports:
```
/* in _card.css */
.card__wrapper {
  padding: 16px;
	width: 320px;
  border: 1px solid #eee;
}

.card__header {
  font-size: 21px;
  font-weight: bold;
  text-align: center;
  color: #212121;
}

// In react component
import React from 'react'

import './styles/_card.css'

const Card = () => (
  <div className="card__wrapper">
    <header className="card__header">This changes everything!</p>
  </div>
)

export default Card
```

Example three - inline styles:
```
// In react component
import React from 'react'

const cardWrapper = {
  padding: '16px';
	width: '320px';
  border: '1px solid #eee';
}

const cardHeader = {
  fontSize: '21px';
  fontWeight: 'bold';
  textAlign: 'center';
  color: '#212121';
}

const Card = () => (
  <div style={cardWrapper>
    <header style={cardHeader}>This changes everything!</p>
  </div>
)

export default Card
```

Example four - CSS modules:
```
/* in _card.css */
.cardWrapper {
  padding: 16px;
	width: 320px;
  border: 1px solid #eee;
}

.cardHeader {
  font-size: 21px;
  font-weight: bold;
  text-align: center;
  color: #212121;
}

// In react component
import React from 'react'

import './styles/Card.css'

const Card = () => (
  <div className={styles.cardWrapper}>
    <header className={styles.cardHeader}>This changes everything!</p>
  </div>
)

export default Card
```

## The world of styled-components

Now, what if we take the approach demonstrated in the example number three, inline styles, and take it one step further. Meaning, why should we use the _style_ attribute? Why can't we just change the name of the component wrapper? Then, we can use that name to style it as we wish. Wouldn't it be easier to create this custom component? Very simply said, this is what styled-components do.

### How it works

When you want to style some component, you define a class with a set of some styles as a variable, in a way that is similar to classical inline styles. However, there is a difference. You are not working with object whose key has to be camelCased (_fontSize_, _fontWeight_, etc.) And, when you want to use this class/variable you will use it as a name of the component wrapper. Here is an example.

Example:
```
import React from 'react'
import styled from 'styled-components'

// Define a div for card wrapper
const CardWrapper = styled.div`
  padding: 16px;
	width: 320px;
  border: 1px solid #eee;
`

// Define a header for card wrapper
const CardHeader = styled.header`
  font-size: 21px;
  font-weight: bold;
  text-align: center;
  color: #212121;
`

const Card = () => (
  <CardWrapper>
    <CardHeader>This changes everything!</CardHeader>
  </CardWrapper>
)

export default Card
```

As you can see on the example above, styled-component allow us to define what type of element do we want to create right at the moment we are creating variables for our styles. Then, when we use one of these variables, styled-components will do two things. First, styled-components will "replace" our custom components with correct elements. So, rendered code will contain _header_ inside a _div_.

And, as the second step, styled-components will take the names we used for variables and generate a unique CSS class for every name, each will keep its styling. Then, these classes will be attached to all elements as regular CSS classes. As a result, we will end up with a _div_ with class like "etSVuJ" and a _header_ with class like "cFSwty". Also, all CSS rules are automatically prefixed.

### Getting started with styled-components

As you can see on the card example, learning to work with styled-components is easy. It is definitely no rocket science. Since the best way to learn something is by doing, let's practice working with styled-components on a few more examples. And, since we already started working on a card, we should also finish it. Let's create some additional components to make sure our card is complete.

Let's create styles for _h1_ heading that will be inside the header of the card, and maybe styles for _h2_ that will work as a subheading. Then, we can create styles for _div_ that will work as card's body. We can also create styles for the text inside the body. Finally, we can create a _footer_. We can then use it as a container for a good old _button_ element. Finally, we may change the wrapper element from _div_ to _article_, for a better semantic.

Example:
```
import React from 'react'
import styled from 'styled-components'

// Define an article for card wrapper
const CardWrapper = styled.article`
  padding: 16px;
	width: 320px;
  font-family: Arial, sans-serif;
  border: 1px solid #eee;
  box-shadow: 0 0 20px rgba(0, 0, 0, .05), 0 0px 40px rgba(0, 0, 0, .08);
`

// Define a header for card wrapper
const CardHeader = styled.header`
  padding-bottom: 18px;
  font-weight: bold;
  text-align: center;
  color: #212121;
`

// Define h1 for card heading
const CardHeading = styled.h1`
  margin-top: 0;
  margin-bottom: 12px;
  font-size: 21px;
`

// Define h2 for card subheading
const CardSubheading = styled.h2`
  margin-top: 0;
  margin-bottom: 0;
  font-size: 18px;
`

// Define div for card body
const CardBody = styled.div`
  padding-top: 24px;
  padding-bottom: 24px;
  border-top: 1px solid #eee;
  border-bottom: 1px solid #eee;
`

// Define a div for card body text
const CardBodyText = styled.p`
  margin: 0;
  font-size: 16px;
  color: #333;
`

// Define a footer for card footer
const CardFooter = styled.footer`
  padding-top: 24px;
  padding-bottom: 24px;
  text-align: center;
`

// Define a button for card button
const CardButton = styled.a`
  padding: 12px 24px;
  display: inline-block;
  font-family: inherit;
  font-size: 14px;
  font-weight: 700;
  text-decoration: none;
  color: #fff;
  background-color: #e5195f;
  border: 0;
  border-radius: 35px;
  box-shadow: 0 10px 10px rgba(0, 0, 0, .08);
  cursor: pointer;
  transition: all .25s cubic-bezier(.02, .01, .47, 1);

  &:hover {
    box-shadow: 0 15px 15px rgba(0, 0, 0, .16);
    transform: translate(0, -5px);
  }
`

class Card extends React.Component {
  render () {
    return (
      <CardWrapper>
        <CardHeader>
          <CardHeading>This changes everything!</CardHeading>

          <CardSubheading>Do you like styled-components?</CardSubheading>
        </CardHeader>

        <CardBody>
          <CardBodyText>Call it extreme if you like, but I propose we hit it hard and hit it fast with a major - and I mean major - leaflet campaign.</CardBodyText>
        </CardBody>

        <CardFooter>
          <CardButton>Read more ></CardButton>
        </CardFooter>
      </CardWrapper>
    )
  }
}
```

### Standing on the shoulders of giants

After a few minutes, working with styled-components feels like a second nature. When you think about it, it is almost like working with good old CSS. We are only working with a slightly different syntax and in a different type of files. Besides that, is there a real difference? All this is great. However, there is one thing we didn't discuss yet. What about pseudo-classes and pseudo-elements?

Through your work, you will probably also want to add styles for states such as _hover_, _focus_, _visited_, _active_ and so on. Or, you may want to use pseudo-classes such as _:first-child_, _:last-child_, _:nth-child()_, _:first-of-type_, _:last-of-type_, _:nth-of-type()_ and so on. So, how can we use these pseudo-classes in styled-components. Fortunately, it is very easy.

It is safe to say that styled-components are standing on the shoulders of giants. Why? Not only do they allow you to use CSS in a way that makes your syntax more readable, by creating custom components. Styled-components also borrowed some of the best tricks from established preprocessors. For example, nesting and ampersand character (&). You can see this on the previous example. Hint: the button.

So, let's say that you want to add some styles for _hover_ or _focus_ states, are any other pseudo-class. In that case, you can group these styles together and "nest" them inside the element, with the use of ampersand (&). If you know Sass or Less, you already know how the ampersand character works. If not, it is simple. It is like a variable that always represents the parent selector.

Example:
```
// Nesting with styled-components
const Link = styled.a`
  font-size: 16px;
  text-decoration: none;
  color: #4c8ee8;

  &:active,
  &:focus,  
  &:hover {
    cursor: pointer;
  }

  &:focus,  
  &:hover {
    color: #a6c7f4;
  }
`

/* Is similar to this in vanilla CSS */
.Link {
  font-size: 16px;
  text-decoration: none;
  color: #4c8ee8;
}

.Link:active,
.Link:focus,
.Link:hover {
  cursor: pointer;
}

.Link:focus,
.Link:hover {
  color: #a6c7f4;
}

```

As you can see, if you have some previous experience with preprocessor such as Sass or Less, moving to styled-components will be very smooth. You will basically just switch from .scss or .sass file to .js or .jsx. You can use many of the things you've learned and used before in also styled-components.

### Styled-components and CSS animations

Sounds good so far? Okay, what about CSS animation? Meaning, how do you create keyframes when you work with styled-components? When you want to create a keyframes, you will use procedure similar to creating styles for your components. You will define a variable for every keyframe. Then, you continue just like you would if you were working with plain CSS or any preprocessor.

Then, when you want to use this animation, you will use its name using the _${}_ syntax. There is one thing you have to keep in mind. When you want to work with keyframes, remember that you need to import 'keyframes' from styled-components library.

Example:
```
import React from 'react'

// Import styled and keyframes
import styled, { keyframes } from 'styled-components'

// Define new keyframes
const animationName = keyframes`
  0% {
    opacity: 0;
  }

  100% {
    opacity: 1;
  }
`

const Slide = styled.div`
  animation: ${animationName} 0.25s 0s both;
`
```

### Styled-components and props

One of the great things on styled-components is that they allow you to change styles of your components according to its props. Imagine that you want to create a new variant of a button, say large. Then, you don't have to create a new variable for a new button. Instead, you attach a new prop to the button component and use it to apply different styles-like `props => props.large && css`.

Just like in the case of keyframes, remember that you need to import 'css' from styled-components library.

Example:
```
import React from 'react'

// Import styled and css
import styled, { css } from 'styled-components'

const Button = styled.button`
  padding: 8px 12px;
  display: inline-block
  font-size: 15px;
  text-decoration: none;
  color: #4c8ee8;

  &:focus,  
  &:hover {
    color: #a6c7f4;
  }

  // a large button
  ${props => props.large && css`
    padding: 16px 24px;
    font-size: 16px;
  `}

  // a small button
  ${props => props.small && css`
    padding: 4px 8px;
    font-size: 14px;
  `}
`

const CardButton = () => (
  <Button>Default Button</Button>
)

const CardButtonLarge = () => (
  <Button large>Large Button</Button>
)

const CardButtonSmall = () => (
  <Button small>Small Button</Button>
)
```

If you want to make a simple, binary, change you can also use a much shorter version, using a ternary operator. In other words, when the component has the prop, condition is equal to true, styled-components will use one style. If the component doesn't have that prop, condition is false, styled-components will use different style. All with just a single line.

Example:
```
import React from 'react'

// Import styled and css
import styled, { css } from 'styled-components'

const Button = styled.button`
  display: inline-block
  font-size: 15px;
  text-decoration: none;
  
  // a large button or default
  padding: ${props => props.large ? '16px 24px' : '8px 12px'}
  
  // an active or disabled button
  color: ${props => props.disabled ? '#95a5a6' : '#3498db'}
`

const CardButton = () => (
  <Button>Active Button</Button>
)

const CardButtonLarge = () => (
  <Button large>Large Button</Button>
)

const CardButtonDisabled = () => (
  <Button disabled>Disabled Button</Button>
)
```

## Closing thoughts on styled-components

So, what do you think about styled-components? Do you like this approach to modular CSS? I have to admit that I wasn't very excited the first time when I heard about styled-components. Leaving Sass and PostCSS? And, mixing CSS with JavaScript? I liked to use these preprocessors. And, I also liked to keep CSS and JavaScript separate. Is this really necessary? Are you sure?

Then, I decided to give styled-components a chance. After a while, I changed my mind and started to like styled-components. One of the things I like the most is how readable it can make the syntax. Well, you still have to use good names for components. However, it is no longer necessary to look for that _className_ attribute that is sometimes hidden in a jungle of other attributes.

With styled-components, it is clear what element are you looking at. From someone who disliked just the idea of mixing CSS and JavaScript to someone who is using styled-components as often as possible. What a change. Now, what about you? Will you give styled-components a try? What is the worst thing that can happen? You will go back to what you used before. You have nothing to lose.

If styled-components caught your attention, take a look at the [documentation]. There is much more you can learn about styled-components and then use to enhance your workflow. This is the best place to start.

[xyz-ihs snippet="thank-you-message"]

### links:
[Atomic CSS]: https://blog.alexdevero.com/atomic-design-scalable-modular-css-sass/
[SMACSS]: https://smacss.com/
[OOCSS]: http://oocss.org/
[ITCSS]: https://www.xfive.co/blog/itcss-scalable-maintainable-css-architecture/
[Sass]: http://sass-lang.com/
[Less]: http://lesscss.org/
[PostCSS]: http://postcss.org/
[CSS modules]: https://medium.com/@pioul/modular-css-with-react-61638ae9ea3e
[documentation]: https://www.styled-components.com/