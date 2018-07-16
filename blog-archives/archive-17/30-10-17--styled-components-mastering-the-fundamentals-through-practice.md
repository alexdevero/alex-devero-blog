# [Styled-components] - Mastering the fundamentals through practice

Styled-components is becoming more and more popular. Many projects built with React.js use this library. This is no surprise. Styled-components make working with CSS easy and fun, even in JavaScript. However, everything requires practices, especially when what you want is mastery. This is the goal of this article. Let's go back to the fundamentals of styled-components and practice.

<!--
Table of Contents:
## Briefing
### Note to the reader
## Workspace and HTML
## JavaScript, React.js and Styled-components
### Bringing in more modularity
### Extending styled-components
### Adaptive styled-components and using props
## Closing thoughts on starting a business
-->

## Briefing

As usually, let's start with a brief introduction and setting up some goals for today's practice. So, what will we be working on? This article will be all about practicing with styled-components. We will use this library to create a number of various examples. And, in order to make it a bit easier, we will start with simple examples. Then, we will gradually move to more difficult.

This article, or tutorial, doesn't require any previous knowledge of styled-components or React.js. I will try to explain those parts that may cause you some troubles. So, even if you don't know anything about styled-components or React.js, you will be able to follow it. That being said, if you have some knowledge it will be easier for you to understand the code, how it works and why.

If you want to learn more about styled-components, there are two resources you should definitely take a look at. The first one is [website] and documentation for styled-components. The second is [introduction to styled-components] published on this blog. You can take a look at both now, or you can do it later, after you get some experience of what it is like to work with styled-components.

### Note to the reader

There is one more thing I want to say. If you don't like the idea of having CSS code mixed with JavaScript, right inside the React component, don't leave. Give styled-components a chance. I know how you feel. I was on the same boat. I disliked this idea a lot. However, I tried styled-components on a few examples and then on couple projects. And, this experience changed my mind.

Getting started with styled-components was very easy and working with it felt natural, like working with vanilla CSS, Sass or PostCSS. I have to say that styled-components took modularity of my code to the next level, literally. This will sound like a no-brainer, but having all code for the component, CSS and JavaScript/React.js, in one place is much clearer and allows work faster.

So, take a look at the examples we will work on today. Play and experiment with the code. Check out the docs and introduction to styled-components. And see it for yourself, whether you like this approach or not. There is a chance that you will change your mind. Well, maybe. And, if not, what is the worst thing that can happen? You will learn something new and return to the approach you like.

## Workspace and HTML

Okay, enough of talking and let's get to work. First, we need to set up our workspace. Aside, to styled-components, we will need to use two additional libraries. We will use CDN to get both of them, as well as the library for [styled-components]. These libraries are [React.js] and [React-DOM]. We will use CDN to get both. Let's also use [babel] transpiler. It will make working with React.js easier.

The second thing we need is prepare the HTML document where we will render our React.js components. This will be quick and simple since the rest of our code will be in JavaScript/React.js. All we need is one _div_ element. As I said, we will use this element as a "placeholder" to render our React components. Let's give it a class "container". And, that's it for HTML.

Code:

```
<div class="container"></div>
```

## JavaScript, React.js and Styled-components

Now, when all is set and ready, we can finally start playing with styled-components. As I mentioned in the beginning, we will start with the basic stuff. Well, there is actually nothing really so difficult about styled-components, or CSS for that matter. Anyway, let's start with the basics and create a few typography styles for headings and body text, using _font-weight_ and _font-size_.

Code:

```
// Import React.js and styled-components
import React from 'react'
import styled from 'styled-components'

const container = document.querySelector('.container')

// Define typography styles
const H1 = styled.h1`
  font-size: 54px;
  font-weight: bold;
`

const H2 = styled.h2`
  font-size: 36px;
  font-weight: bold;
`

const H3 = styled.h3`
  font-size: 24px;
  font-weight: bold;
`

const H4 = styled.h4`
  font-size: 16px;
  font-weight: bold;
`

const H5 = styled.h5`
  font-size: 14px;
  font-weight: bold;
`

const H6 = styled.h6`
  font-size: 12px;
  font-weight: bold;
`

const Text = styled.p`
  font-size: 16px;
`

const Small = styled.small`
  font-size: 80%;
`

// Use our styles
const WrapperContainer = () => (
  <div>
    <H1>Heading h1</H1>

    <H2>Heading h2</H2>

    <H3>Heading h3</H3>

    <H4>Heading h4</H4>

    <H5>Heading h5</H5>

    <H6>Heading h6</H6>

    <Text>Body text</Text>

    <Small>Small text</Small>
  </div>
)

ReactDOM.render(
  <WrapperContainer />,
  container
)
```

### Bringing in more modularity

As you can see on the example above, working with styled-components is like working with vanilla CSS. You may need a bit of time to remember a different way to define styles, such as with _const_, like in our example. However, it is still far from a rocket science. Now, back to our example. Have you noticed something on it? Yes, we are using the same _font-weight_ multiple times.

This is not such an issue, when our code is very short, like in this case. However, we can write our code in a better and more modular way than that. What if we define a new _const_, set its _font-weight_ to "bold" and then use that variable in each heading style? Then, if something happens we will decide to change that _font-weight_, we have to change it on just one place.

This change will be easy and fast. However, we will need to import one additional method from styled-components library. This method is defined and exported from styled-component library as _css_. Let's change the second line with styled-components import and include the _css_ method. Remember, "css" is written in lower case. Next, we can define that reusable _const_ with bold style.

After that, we can use this new _const_ whenever and wherever we want. All we will have to do is use the _${}_ syntax, with name of a specific _const_ between the curly brackets.

Code:

```
// Import React.js, styled-components and css
import React from 'react'
import styled, { css } from 'styled-components'

const container = document.querySelector('.container')

// Define new const with bold style
const headingStyle = css`
  font-weight: bold;
`

// Define typography styles
const H1 = styled.h1`
  font-size: 54px;

  // Using headingStyle const
  ${headingStyle}
`

const H2 = styled.h2`
  font-size: 36px;

  // Using headingStyle const
  ${headingStyle}
`

const H3 = styled.h3`
  font-size: 24px;

  // Using headingStyle const
  ${headingStyle}
`

const H4 = styled.h4`
  font-size: 16px;

  // Using headingStyle const
  ${headingStyle}
`

const H5 = styled.h5`
  font-size: 14px;

  // Using headingStyle const
  ${headingStyle}
`

const H6 = styled.h6`
  font-size: 12px;

  // Using headingStyle const
  ${headingStyle}
`

const Text = styled.p`
  font-size: 16px;
`

const Small = styled.small`
  font-size: 80%;
`

// Use our styles
const WrapperContainer = () => (
  <div>
    <H1>Heading h1</H1>

    <H2>Heading h2</H2>

    <H3>Heading h3</H3>

    <H4>Heading h4</H4>

    <H5>Heading h5</H5>

    <H6>Heading h6</H6>

    <Text>Body text</Text>

    <Small>Small text</Small>
  </div>
)

ReactDOM.render(
  <WrapperContainer />,
  container
)
```

There is one thing we need to keep in mind. If we define that _const_ in a different file, and we will want to use it elsewhere, we will need to export it from the original file and then import it where we want to use it.

Code:

```
// File foo.js
// Import React.js, styled-components and css
import React from 'react'
import styled, { css } from 'styled-components'

// Define and export new const with bold style
export const headingStyle = css`
  font-weight: bold;
`

// File bar.js
// Import React.js, styled-components and css
import React from 'react'
import styled, { css } from 'styled-components'

// Import our const
import { headingStyle } from './styles/foo'

const container = document.querySelector('.container')

// Define typography styles
const H1 = styled.h1`
  font-size: 54px;

  // Using headingStyle const
  ${headingStyle}
`

// Use our styles
const WrapperContainer = () => (
  <div>
    <H1>Heading h1</H1>
  </div>
)

ReactDOM.render(
  <WrapperContainer />,
  container
)
```

Again, it is important to remember that we have to export any and every _const_ variable we would like to use like in the example above, and then import it where we want to use it. That being said, if we have only one variable, function, method or classes we want to export from file, we can export it as "default". Then, we will not need to use the curly brackets ("{}") when we import it.

Code:

```
// File foo.js
// Import React.js, styled-components and css
import React from 'react'
import styled, { css } from 'styled-components'

// Define new const with bold style
const headingStyle = css`
  font-weight: bold;
`

// Export our const as default
export default headingStyle

// File bar.js
// Import React.js and styled-components
import React from 'react'
import styled from 'styled-components'

// Import our const - without curly brackets
import headingStyle from './styles/foo'

const container = document.querySelector('.container')

// Define typography styles
const H1 = styled.h1`
  font-size: 54px;

  // Using headingStyle const
  ${headingStyle}
`

// Use our styles
const WrapperContainer = () => (
  <div>
    <H1>Heading h1</H1>
  </div>
)

ReactDOM.render(
  <WrapperContainer />,
  container
)
```

Having said that, we can use default _export_ along with named _export_ so we can _export_ multiple variables, functions, methods or classes. However, we need to keep in mind which _export_ did we use for which variable, function, method or class. Remember, default _export_ doesn't require curly brackets, named does.

Code:

```
// File foo.js
// Import React.js, styled-components and css
import React from 'react'
import styled, { css } from 'styled-components'

// Define and export some consts
const firstVariable = css`
  font-size: 21px;
  text-decoration: none;
`

const secondVariable = css`
  text-align: center;
  color: #black;
`

const thirdVariable = css`
  padding: 4px;
  border: 1px solid gray;
`

// Export our first const as default ad the rest as named
export { firstVariable as default, secondVariable, thirdVariable }

// File bar.js
// Import React.js and styled-components
import React from 'react'
import styled from 'styled-components'

// Import our const - default without curly brackets, named with curly brackets
import firstVariable, { secondVariable, thirdVariable } from './styles/foo'

// Or, we can import our const this way:
// default without curly brackets, named by using "*"
import firstVariable, * from './styles/foo'
```

Does _import_ and _export_ statements sound interesting to you? If you want to learn more about them, I suggest taking a look at the MDN documentation, for [export] as well as for [import]. There are many examples that will help you understand the nuts and bolts of these statements and how to use them in the right way. I hope I did.

### Extending styled-components

Okay. Now we know how to create new components with specific styles through variables using styled-components. What if we want to have one variable with specific styles and use it for both, component and also for extending styles of other components, like we did with "headingStyle" and "H1"? We can do just that, extend the component, I mean almost literally. We can use _extend_.

What we need to do is define a new variable for some component, say a button. Then, we will add some styles to make this button look better. After that, we will create another variable, or another button that will inherit the styles of the first one while having its own. Instead of using _const * = styled.*`_ syntax we used for the first button, we will use  _const * = Button.extend`_.

One more thing, we don't have to import any additional method from styled-components library, like we had to in the case of _css_. We need to import just styled-components and use _extend_ as we want. Notice that we are importing the default _export_ because we don't have to surround the "styled" import with curly brackets.

Code:

```
// Import React.js and styled-components
import React from 'react'
import styled from 'styled-components'

const container = document.querySelector('.container')

const Button = styled.button`
  padding: 12px 24px;
  font-size: 16px;
  color: #fff;
  border: 0;
  border-radius: 35px;
  box-shadow: 0 10px 20px rgba(0,0,0,0.19), 0 6px 6px rgba(0,0,0,0.23);
  cursor: pointer;
`

// Using extend to create a red variant of the button
const ButtonRed = Button.extend`
  background-color: #e74c3c;
`

// Using extend to create a green variant of the button
const ButtonGreen = Button.extend`
  background-color: #2ecc71;
`

// Use our styles
const WrapperContainer = () => (
  <div>
    <Button>Defaul button</Button>

    <ButtonRed>Red button</ButtonRed>

    <ButtonGreen>Green button</ButtonGreen>
  </div>
)

ReactDOM.render(
  <WrapperContainer />,
  container
)
```

### Adaptive styled-components and using props

So far we created new components with specific styles through variables. Then, we also practiced how to define reusable variables and how to use _extend_. The problem is that the code in previous example is still too long. We can make it shorter and more concise. To do that, we will use _props_. Note: we will again need to import "css" from styled-components library.

Next, we can use _props_ to define variants of our variable or component without having to create new ones. We can do this by using _${props => props.componentProp && css` ...some styles... `}_ syntax where "componentProp" is the property we will attach to the variant of our default component.

Code:
```
// Import React.js, styled-components and css
import React from 'react'
import styled, { css } from 'styled-components'

const container = document.querySelector('.container')

const Button = styled.button`
  padding: 12px 24px;
  font-size: 16px;
  border: 0;
  border-radius: 35px;
  box-shadow: 0 10px 20px rgba(0,0,0,0.19), 0 6px 6px rgba(0,0,0,0.23);
  cursor: pointer;

  // Using props to create a gray variant of the button
  ${props => props.gray && css`
    background-color: #95a5a6;
  `}

  // Using props to create a green variant of the button
  ${props => props.green && css`
    background-color: #2ecc71;
  `}

  // Using props to create a red variant of the button
  ${props => props.red && css`
    background-color: #e74c3c;
  `}

  // We can also use a ternary operator for "binary" changes
  // if button has prop "gray", the color will be "#2c3e50" otherwise it will be "#fff"
  color: ${props => props.gray ? '#2c3e50' : '#fff'};
`

const WrapperContainer = () => (
  <div>
    <Button>Defaul button</Button>

    {/* Button with prop "red" */}
    <Button red>Red button</Button>

    {/* Button with prop "green" */}
    <Button green>Green button</Button>
  </div>
)

ReactDOM.render(
  <WrapperContainer />,
  container
)
```

## Closing thoughts on styled-components

So, did styled-components convince you to change your mind about mixing CSS in JavaScript? If you are used to working with vanilla CSS, Sass or PostCSS, like me, it can be weird. If you are still not fully convinced, maybe give it a little bit of time. Then, you can take a look at the examples we created today later with fresh eyes and clear mind. Or, go back to what you like.

There is one last thing I want to say. Today, we focused on the fundamentals of styled-components. And, maybe too much. As a result, maybe you found this article to be too basic. And, you are right. It was basic, very basic. However, mastering the basics is necessary before we can move further and practice more advanced topics. We will focus on the advanced topics in the next article.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[website]: https://www.styled-components.com/
[introduction to styled-components]: https://blog.alexdevero.com/introduction-styled-components/
[React.js]: https://cdnjs.com/libraries/react
[React-DOM]: https://cdnjs.com/libraries/react-dom
[styled-components]: https://cdnjs.com/libraries/styled-components
[babel]: https://babeljs.io/
[export]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export
[import]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import
