# How to Build a Great [Style Guide] with React & styled-components Pt.2

Every design project should have a style guide. This is one of the best ways to ensure the design is consistent. There are many tools to create a style guide. However, building one by yourself can be beneficial. It gives you more options and freedom. This tutorial will show you how to build your own style guide from scratch using `React` and `styled-components`.

<!--
Table of Contents:
## Improving the main component
## Creating generic helper component
## Colors
## Typography
## Epilogue: How to Build UI Style Guide with React Pt.2
-->

How to Build a Great Style Guide with React & styled-components [part 1].

## Improving the main component

Let's start with something easy. Do you remember those variables for objects for `colors` and `sizes`? We defined these variables at the top of the `index.js`. This is not the best place where to put them. Why? W are going to use these variables in all components of this style guide. This puts on a crossroad where we can choose from two available solutions.

First, we can keep these variables where they are, in `index.js`. Then, we can pass them as props to every component. Second, we can take these variables, save them in another file and export them. Then, we can import these variables, or just one, any time we need inside specific component. For the purpose of keeping the code tidy, let's choose the second option-exported variables.

So, let's remove the `colors` and `sizes` variables from `index.js` and move them to new file `variables.js` in root directory. Then, let's add imports for both variables to those we already have in the top of `index.js`. Fortunately, we are using the same name for variables. This means that we don't need to change any references in components created with styled-components.

```
// ./variables.js

// Codes for color palette
export const colors = {
  disabled: 'hsl(212.3, 16.7%, 69.4%)',
  error: 'hsl(359.6, 82.1%, 62.7%)',
  errorActive: 'hsl(359.6, 82.1%, 42.7%)',
  errorHover: 'hsl(359.6, 82.1%, 65%)',
  primary: 'hsl(209.6, 100%, 55.9%)',
  primaryActive: 'hsl(209.6, 100%, 35.9%)',
  primaryHover: 'hsl(209.6, 100%, 65%)',
  secondary: 'hsl(29.4, 100%, 63.1%)',
  secondaryActive: 'hsl(29.4, 100%, 43.1%)',
  secondaryHover: 'hsl(29.4, 100%, 65%)',
  success: 'hsl(164, 75.6%, 46.7%)',
  successActive: 'hsl(164, 75.6%, 26.7%)',
  successHover: 'hsl(164, 75.6%, 60%)',
  text: 'hsl(223.8, 81.3%, 6.3%)'
}

// Sizes for typography scale
export const sizes = {
  xs: '12px',
  sm: '14px',
  base: '16px',
  lg: '18px',
  xl: '20px',
  xxl: '24px',
  xxxl: '30px',
  xxxxl: '36px'
}
```

Finally, we can remove the `colors` and `scale` props passed by the main component to sub-components. With this, we are ready to proceed further.

```
// ./index.js

// Import dependencies
import React from 'react'
import ReactDOM from 'react-dom'
import styled, { injectGlobal } from 'styled-components'

// Import colors and sizes variables
import { colors, sizes } from './variables'

// Import style guide components
import Buttons from './components/buttons'
import Colors from './components/colors'
import Forms from './components/forms'
import Typography from './components/typography'

// Global styles and resets
injectGlobal`
  html {
    box-sizing: border-box;
    font-size: ${sizes.base};
  }

  *,
  *::before,
  *::after {
    box-sizing: inherit;
  }

  body {
    padding: 0;
    margin: 0;
    font: 100% / 1.618 Roboto, Arial, sans-serif;
    color: ${colors.text};
  }
`

// Main container or wrapper
const AppContainer = styled.div`
  padding: 0 8px 60px;
  margin-left: auto;
  margin-right: auto;
  display: flex;
  flex-flow: column wrap;
  align-items: flex-start;
  max-width: 992px;
`

// H1 heading
const StyleguideHeading = styled.h1`
  position: relative;
  display: inline-block;
  font-weight: 500;

  &::before {
    position: absolute;
    bottom: 0;
    left: 0;
    content: '';
    width: 100%;
    height: 2px;
    background-color: ${colors.text};
  }
`

// H2 heading
const StyleguideSubheading = styled.h2`
  position: relative;
  display: inline-block;
  margin-bottom: 26px;
  font-weight: 400;
  text-align: left;

  &::before {
    position: absolute;
    bottom: 0;
    left: 0;
    content: '';
    width: 100%;
    height: 1.5px;
    background-color: ${colors.text};
  }

  div + & {
    margin-top: 60px;
  }
`

class App extends React.Component {
  render() {
    return (
      <AppContainer>
        <StyleguideHeading>UI Style guide</StyleguideHeading>

        <p>
          A short info about the company. Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec quam felis, ultricies nec, pellentesque eu, pretium quis, sem.
        </p>

        <StyleguideSubheading>Colors</StyleguideSubheading>

        <Colors />

        <StyleguideSubheading>Typography</StyleguideSubheading>

        <Typography />

        <StyleguideSubheading>Buttons</StyleguideSubheading>

        <Buttons />

        <StyleguideSubheading>Forms</StyleguideSubheading>

        <Forms />
      </AppContainer>
    )
  }
}

const rootElement = document.getElementById('root')

ReactDOM.render(<App />, rootElement)
```

## Creating generic helper component

There is another thing we will use in all components of our style guide. This will be a small component that will wrap the content of every section in our style guide. Let's create this component and save it in new file `generic-helpers.jsx` in `./components` directory. This will save us few lines. As the last step, don't forget to export the component.

```
// ./components/generic-helpers.jsx

import styled from 'styled-components'

export const Container = styled.div`
  display: flex;
  flex-flow: column wrap;
  align-items: flex-start;
  text-align: left;
  width: 100%;

  h5 {
    margin-top: 28px;
    margin-bottom: 12px;
  }
`
```

## Colors

Now, let's put together a sub-component that will represent the first section of our style guide. At the top of this component we will import `React` and `styled-component` dependencies. Next, we will import `colors` and `sizes` variables and then the `Container` component. When we are done with this, we can start working on components specific for this section of the style guide.

Colors section will contain six samples of colors that will compose the color palette. The structure of the colors section will be following. We will create `ColorBlock` component for every sample. It will contain a thumbnail to show how the color looks like. We will represent this thumbnail with `ColorBlockColor` component.

Every `ColorBlockColor` will have `theme` prop. We will use this prop to specify the color of the thumbnail. Next will be a label with the name of the color. For this information we will create `ColorBlockTitle` component. Finally, as the last component, we will create `ColorBlockCode`. This will be a wrapper for Hex, RGB, HSL and CMYK codes. Every code will be on separate line.

*Note: on the line 12 of the example below, you will notice `const ColorsContainer = styled(Container)`. This does not look like the usual way we previously defined component with `styled-components`. We used `styled.tagname`` `. What is the difference between using `styled()` and `styled.tagname`` `? The `styled-components` allows us to create components based on valid HTML tags.*

*The `styled()` allows us to take existing React component, use all its styles, and add new. This can be also handy when we want to override some styles. It is also useful when we have a generic component and want to create variants. For example, we can create `Button` and then use this component to create `ButtonPrimary` and `ButtonSecondary`. Think about prototype and instances.*

```
// ./components/colors.jsx

// Import dependencies
import React from 'react'
import styled from 'styled-components'

// Import colors and sizes variables
import { colors, sizes } from './../variables'

// Import Container component
import { Container } from './generic-helpers'

// Extending Container component
const ColorsContainer = styled(Container)`
  flex-flow: row wrap;

  @media (min-width: 1200px) {
    max-width: 1200px;
  }
`

// Container for one color sample
const ColorBlock = styled.div`
  display: flex;
  flex-flow: column wrap;
  width: calc(33.3333% - 18px);
  font-size: ${sizes.base};
  background-color: ${props => props.theme};

  & + div {
    margin-left: 18px;
  }

  @media (max-width: 767px) {
    & + div:nth-of-type(n + 4) {
      margin-top: 32px;
    }

    & + div:nth-of-type(4) {
      margin-left: 0;
      margin-right: 18px;
    }

    & + div:nth-of-type(5) {
      margin-left: 18px;
    }
  }

  @media (min-width: 768px) {
    width: calc(25% - 18px);

    & + div:nth-of-type(n + 4) {
      margin-left: 18px;
    }
  }

  @media (max-width: 991px) {
    & + div:nth-of-type(n + 5) {
      margin-top: 32px;
    }

    & + div:nth-of-type(5) {
      margin-left: 0;
    }
  }

  @media (min-width: 992px) {
    width: calc(20% - 18px);

    & + div:nth-of-type(5) {
      margin-left: 18px;
    }

    & + div:nth-of-type(6) {
      margin-top: 32px;
      margin-left: 0;
    }
  }

  @media (min-width: 1200px) {
    width: calc(16.66667% - 18px);

    & + div:nth-of-type(6) {
      margin-left: 18px;
    }

    & + div:nth-of-type(6) {
      margin-top: 0;
      margin-left: 18px;
    }
  }
`

// Color thumbnail
const ColorBlockColor = styled.div`
  margin-bottom: 10px;
  width: 100%;
  height: 86px;
  background-color: ${props => props.theme};
`

// Color label
const ColorBlockTitle = styled.span`
  margin-bottom: 6px;
  font-size: ${sizes.sm};
  font-weight: 700;
  color: hsl(0, 0%, 55%);
`

// Color codes
const ColorBlockCode = styled.span`
  font-size: ${sizes.xs};
  color: hsl(0, 0%, 7%);

  & + & {
    margin-top: 2px;
  }
`

const Colors = () => {
  return (
    <ColorsContainer>
      {/* Color sample 1 */}
      <ColorBlock>
        <ColorBlockColor theme={colors.primary} />

        <ColorBlockTitle>Blue</ColorBlockTitle>

        <ColorBlockCode>
          <strong>Hex:</strong> #1e90ff
        </ColorBlockCode>

        <ColorBlockCode>
          <strong>RGB:</strong> 30, 144, 255
        </ColorBlockCode>

        <ColorBlockCode>
          <strong>HSL:</strong> 209.6, 100%, 55.9%
        </ColorBlockCode>

        <ColorBlockCode>
          <strong>CMYK:</strong> 88, 44, 0, 0
        </ColorBlockCode>
      </ColorBlock>

      {/* Color sample 2 */}
      <ColorBlock>
        <ColorBlockColor theme={colors.secondary} />

        <ColorBlockTitle>Orange</ColorBlockTitle>

        <ColorBlockCode>
          <strong>Hex:</strong> #ff9f43
        </ColorBlockCode>

        <ColorBlockCode>
          <strong>RGB:</strong> 255, 159, 67
        </ColorBlockCode>

        <ColorBlockCode>
          <strong>HSL:</strong> 29.4, 100%, 63.1%
        </ColorBlockCode>

        <ColorBlockCode>
          <strong>CMYK:</strong> 0, 38, 74, 0
        </ColorBlockCode>
      </ColorBlock>

      {/* Color sample 3 */}
      <ColorBlock>
        <ColorBlockColor theme={colors.disabled} />

        <ColorBlockTitle>Gray</ColorBlockTitle>

        <ColorBlockCode>
          <strong>Hex:</strong> #a4b0be
        </ColorBlockCode>

        <ColorBlockCode>
          <strong>RGB:</strong> 164, 176, 190
        </ColorBlockCode>

        <ColorBlockCode>
          <strong>HSL:</strong> 212.3, 16.7%, 69.4%
        </ColorBlockCode>

        <ColorBlockCode>
          <strong>CMYK:</strong> 14, 7, 0, 25
        </ColorBlockCode>
      </ColorBlock>

      {/* Color sample 4 */}
      <ColorBlock>
        <ColorBlockColor theme={colors.error} />

        <ColorBlockTitle>Red</ColorBlockTitle>

        <ColorBlockCode>
          <strong>Hex:</strong> #ee5253
        </ColorBlockCode>

        <ColorBlockCode>
          <strong>RGB:</strong> 238, 82, 83
        </ColorBlockCode>

        <ColorBlockCode>
          <strong>HSL:</strong> 359.6, 82.1%, 62.7%
        </ColorBlockCode>

        <ColorBlockCode>
          <strong>CMYK:</strong> 0, 66, 65, 7
        </ColorBlockCode>
      </ColorBlock>

      {/* Color sample 5 */}
      <ColorBlock>
        <ColorBlockColor theme={colors.success} />

        <ColorBlockTitle>Green</ColorBlockTitle>

        <ColorBlockCode>
          <strong>Hex:</strong> #1dd1a1
        </ColorBlockCode>

        <ColorBlockCode>
          <strong>RGB:</strong> 29, 209, 161
        </ColorBlockCode>

        <ColorBlockCode>
          <strong>HSL:</strong> 164, 75.6%, 46.7%
        </ColorBlockCode>

        <ColorBlockCode>
          <strong>CMYK:</strong> 86, 0, 23, 18
        </ColorBlockCode>
      </ColorBlock>

      {/* Color sample 6 */}
      <ColorBlock>
        <ColorBlockColor theme={colors.text} />

        <ColorBlockTitle>Dark blue</ColorBlockTitle>

        <ColorBlockCode>
          <strong>Hex:</strong> #030a1d
        </ColorBlockCode>

        <ColorBlockCode>
          <strong>RGB:</strong> 3, 10, 29
        </ColorBlockCode>

        <ColorBlockCode>
          <strong>HSL:</strong> 223.8, 81.3%, 6.3%
        </ColorBlockCode>

        <ColorBlockCode>
          <strong>CMYK:</strong> 90, 66, 0, 89
        </ColorBlockCode>
      </ColorBlock>
    </ColorsContainer>
  )
}

export default Colors
```

## Typography

The second section of our style guide will be dedicated to typography. As with colors, we will start be adding necessary imports. We will also need to extend the `Container` component with `styled()` to reset `margin-top` property applied to all `h5` headings by default. After that, let's define one variable, `HeadingStyle`, with styles we will apply to all headings.

Next, we will define components for each headline, from h1 to h6. Then, we will create components for body, small, bold, highlighted, italicized, underlined text. The last component will be for links. Unlike the previous typography components this one will be bigger. We will use `active`, `hover`, `visited` and `disabled` props to indicate different states and interactivity.

We will then use these props to show how every state of the link looks like. This will give us four link pseudo-variants that we can present in our style guide. With this, we will have a set of the most common and used elements a good style guide should contain.

*Note: we could include only the default and disabled variant and just add styles for `:hover`, `:active` and `:visited` states as this could be easier. However, it is always better to present all these states explicitly. Why? Imagine that you will present your style guide in the form of a pdf or as an image. How will you trigger `:hover`, `:active` and `:visited` states so you can show how will these states look? The answer is you can't.*

*Well, maybe this is doable with pdf. However, it is not doable with one image. You would need to have four copies of the images showing all possible states. The lesson? Always include variants for all possible states. You never know in what form will someone use the style guide. Including all variants will make your style guide close to bulletproof.*

```
// ./components/typography.jsx

// Import dependencies
import React from 'react'
import styled, { css } from 'styled-components'

// Import colors and sizes variables
import { colors, sizes } from './../variables'

// Import Container component
import { Container } from './generic-helpers'

// Extending Container component
const ColorsContainer = styled(Container)`
  h5 {
    margin-top: 0;
  }
`

// Styles for all headings
const HeadingStyle = css`
  margin-top: 0;
  margin-bottom: 16px;
`

// Heading h1
export const H1 = styled.h1`
  ${HeadingStyle};
  font-size: ${props => props.size};
`

// Heading h2
export const H2 = styled.h2`
  ${HeadingStyle};
  font-size: ${props => props.size};
`

// Heading h3
export const H3 = styled.h3`
  ${HeadingStyle};
  font-size: ${props => props.size};
`

// Heading h4
export const H4 = styled.h4`
  ${HeadingStyle};
  font-size: ${props => props.size};
`

// Heading h5
export const H5 = styled.h5`
  ${HeadingStyle};
  font-size: ${props => props.size};
`

// Heading h6
export const H6 = styled.h6`
  ${HeadingStyle};
  font-size: ${props => props.size};
`

// Body text
export const Text = styled.p`
  ${HeadingStyle};
  font-size: ${props => props.size};
`

// Small text (<small>)
export const Small = styled.small`
  font-size: ${props => props.size};
`

// Bold text
export const Strong = styled.strong`
  font-weight: bold;
`

// Highlighted text
export const Highlight = styled.mark`
    background-color: hsl(209.6,100%,85%);
`

// Italicized text
export const Italic = styled.em`
  font-style: italic;
`

// Underlined text
export const Underline = styled.u`
  text-decoration: underline;
`

// Links
export const Link = styled.a`
  margin-top: 12px;
  display: inline-block;
  font-size: ${props => props.size};
  text-decoration: underline;
  color: ${props => colors.primary};
  cursor: ${props => (props.disabled ? 'not-allowed' : 'pointer')};

  ${props =>
    props.active &&
    css`
      color: ${props => colors.primaryActive};
  `}

  ${props =>
    props.hover &&
    css`
      color: ${props => colors.primaryHover};
  `}

  ${props =>
    props.visited &&
    css`
      color:hsl(209.6,100%,15.9%);
      text-decoration: underline;
  `}

  ${props =>
    props.disabled &&
    css`
      color: ${props => colors.disabled};
  `}
`

const Typography = () => {
  return (
    <ColorsContainer>
      <H1 size={sizes.xxxxl}>Heading 1</H1>

      <H2 size={sizes.xxxl}>Heading 2</H2>

      <H3 size={sizes.xxl}>Heading 3</H3>

      <H4 size={sizes.xl}>Heading 4</H4>

      <H5 size={sizes.lg}>Heading 5</H5>

      <H6 size={sizes.base}>Heading 6</H6>

      <Text size={sizes.base}>
        This is a body text. Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec quam felis, ultricies nec, pellentesque eu, pretium quis, sem.
      </Text>

      <Text>
        <Small size={sizes.sm}>Small text</Small>
      </Text>

      <Text>
        <Strong>Bold text</Strong>
      </Text>

      <Text>
        <Highlight>Highlighted text</Highlight>
      </Text>

      <Text>
        <Italic>Italicized text</Italic>
      </Text>

      <Text>
        <Underline>Underlined text</Underline>
      </Text>

      <Link size={sizes.base}>Link default</Link>

      <Link hover size={sizes.base}>
        Link hover
      </Link>

      <Link active size={sizes.base}>
        Link active
      </Link>

      <Link visited size={sizes.base}>
        Link visited
      </Link>

      <Link disabled size={sizes.base}>
        Link disabled
      </Link>
    </ColorsContainer>
  )
}

export default Typography
```

## Epilogue: How to Build UI Style Guide with React Pt.2

Congratulations! You've just finished the second part of this mini series. Today, you've created the first two sections for your style guide, colors and typography. Now, you can go to `index.js` and uncomment the imports for these two components. Then, do the same with inside the `App` class. When you load the style guide on dev server, you will see colors and typography sections.

What can you expect in the next part? We will take a look at other sections for our style guide. These sections will buttons and forms. Until then, practice your skills and play with `React` and `styled-components`. Remember that diligent practice is the key to mastery. So, go and practice and then some more. With that, I look forward to seeing you here again the next week. Have a great day!

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[part 1]: https://blog.alexdevero.com/style-guide-react-pt1/

<!--
#### Meta:
-
-->

<!--
#### Inspiration:
-
-->
