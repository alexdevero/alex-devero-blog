# Create Flipping Card & Responsive Grid with Styled-components & React

Have you ever thought about using styled-components to create a simple flipping card and responsive grid layout? In this tutorial, you will get a chance to do both! First, we will use styled-components to create flexbox-based responsive grid system. Then, we will create a component for a very simple flipping card. I hope you will enjoy this very easy tutorial on styled-components and React and find it useful. And, with that, let's begin.

<!--
Table of Contents:
## Assets and prerequisites
## HTML
## Styled-components + React
### Building responsive grid with styled-components
### Creating a flipping card with styled-components
## Closing thoughts on flipping card, grid and styled-components
-->

Demo on [Codepen].

## Assets and prerequisites

As always, we have to make sure we have all prerequisites and assets in place before we begin. Going through this step first will also help us avoid potential problems with some piece of code either not working as it should or at all. So, what assets will we need to successfully finish this tutorial with working code? For this tutorial we will need to include three JavaScript libraries. In order to make it easier, we will use versions hosted on [CDN] (Content Delivery Network). Then, you will not need to have this any of these libraries on your computer.

The first two libraries are [React] and [React-DOM]. Keep in mind that we need to use both. At the time of writing this article, the latest version of React, and React-DOM, is 16.1.1. In this tutorial, we will use this version, the UMD (Universal Module Definition). Are you curious about UMD, AMD and CJS (CommonJS)? In that case, take a look at this [quick explanation] to understand the differences between these module specs by David Calhoun. Another very good article for learning more modules is [JavaScript Modules: A Beginner’s Guide] by Preethi Kasireddy.

The third and last library we will need to include to make this tutorial work is [styled-components]. The latest version of styled-components library is currently 2.2.3. We will this. Yes, always on the cutting-edge. There is one more thing. We will also use [Babel] transpiler. This tool will transform the JavaScript code we will write into syntax that is supported by older browsers. In other words, it will help us increase the range of browsers able to read and run our JavaScript code. Well, [browser support] is a subject for itself. With this, we can move to step number two.

_A quick side note: versions of React and React-DOM libraries should always be the same. These two libraries are developed together. When one gets updated, the other gets updated as well. So, when you work on some project that uses React and React-DOM, make sure to use identical versions. Otherwise, you will probably run into a number of "unexpected" problems._

## HTML

The second step is putting together all that is necessary in the terms of HTML. Since this tutorial is focused on styled-components and React, our work in HTML will be very quick and simple. All we need, aside to default content such as head and including our libraries, is just one element. We will use this element as a place where we will later render our grid with flipping cards built with React and styled-components. Since this element will have no semantic meaning, we can use the good old `div`. And, that is all we need.

Code:
```
<div class="container"></div>
```

## Styled-components + React

Now, it is time for the third, and the biggest, step. In this part, we will first use styled-components to create a simple, responsive and flex-based grid. Then, we will use styled-components again and create the flipping card we will then use to populate the grid. So, let's get right into it and build our grid.

### Building responsive grid with styled-components

The first thing we will need is to use styled-components to build a responsive grid. This grid will have three parts, or components, created with styled-components. These parts are "GridContainer", "GridRow" and "GridColumn". All these components are borrowed from grid used in [Bootstrap framework] and work in the same way. The only difference is that we will only use a different syntax. We will use "GridContainer" to set maximum width of the layout. "GridRow" will be a wrapper for columns. "GridColumn" components will help us split the layout into columns, or blocks.

Keep in mind that when you will want to use the grid, you must place your content either within the "GridColumn" component or within the "GridContainer" component. Don't place your content directly within the "GridRow", as its immediate children. You can do that only with "GridColumn" component and place your content within that. We will use four main breakpoints to make our grid responsive and flexible: 576px, 768px, 992px and 1200px. These breakpoints will be defined as "xs", "sm", "md", "lg" and "xl".

In order to make this easier, we will create two helper _functions_, "getWidth" and "getFlex". These functions will help us automate calculation of values for `flex` and `width` properties. Both will accept value as a parameter, divide this value by 12, multiply it by 100 and return the fraction of layout a column should take in the form of _style_ declaration. We will use these functions in "GridColumn" for each breakpoint to generate components for all 12 columns.

In the terms of "GridColumn" component, there is probably one thing I should explain. For each breakpoint, we will look for corresponding `prop` and, if it is present and has some value, we will take that value and pass it to our "getFlex" and "getWidth" helper _functions_. As we discussed above, these functions will return proper style declaration we will then use with styled-components. All grid components will use `div` elements. This is all we need to create our simple and responsive grid with styled-components. One more thing.

We need to import the styled-components library before we can start working with it. We can do this either with `import` statement or `const`. I used the later in order to make this code work on Codepen. Otherwise, I suggest using the version with `import`. We will also need to import `css` _method_ from styled-components. This will allow us create styles without the need to define specific element. You can learn more about how the `css` _method_, and styled-components, work in this [fundamentals of styled-components] tutorial, or in [docs].

_A quick side note: I like to use rem units in the majority of situations. However, converting pixels to rems manually all the time is quite slow. So, let's make this easier by creating additional simple helper function called remy. This function will accept numeric value as a parameter, divide it by 16, add 'rem' string and return it._

Code:
```
// Import styled-components library - "import" version
import styled as sc from styled-components
import { css } from styled-components

// Import styled-components library - "const" version
const sc = styled.default
const { css } = styled

// Save container div inside const
const container = document.querySelector('.container')

// Helper function to convert pixels to rems (remy)
const remy = px => `${px / 16}rem`

// Function for calculating value for width
const getWidth = (value) => {
  if (!value) return

  let width = value / 12 * 100
  return `width: ${width}%;`
}

// Function for calculating value for flex
const getFlex = (value) => {
  if (!value) return

  let flex = value / 12 * 100
  return `flex: 0 0 ${flex}%;`
}

// Grid container
const GridContainer = sc.div`
  padding-right: ${remy(15)};
  padding-left: ${remy(15)};
  margin-right: auto;
  margin-left: auto;
  width: 100%;

  // Breakpoint for tablets
  @media (min-width: 576px) {
    max-width: ${remy(540)};
  }

  // Breakpoint for small desktops
  @media (min-width: 768px) {
    max-width: ${remy(720)};
  }

  // Breakpoint for medium desktops
  @media (min-width: 992px) {
    max-width: ${remy(9600)};
  }

  // Breakpoint for large desktops and HD devices
  @media (min-width: 1200px) {
    max-width: ${remy(1140)};
  }
`

// Grid row
const GridRow = sc.div`
  margin-right: ${remy(-15)};
  margin-left: ${remy(-15)};
  display: flex;
  flex-wrap: wrap;
`

// Grid columns
const GridColumn = sc.div`
  padding-right: ${remy(15)};
  padding-left: ${remy(15)};

  // Columns for mobile
  ${({ xs }) => (xs ? getFlex(xs) : 'flex: 0 0 100%')};
  ${({ xs }) => (xs ? getWidth(xs) : 'width: 100%')};

  // Columns for tablets
  @media (min-width: 576px) {
    ${({ sm }) => sm && getFlex(sm)};
    ${({ sm }) => sm && getWidth(sm)};
  }

  // Columns for small desktops
  @media (min-width: 768px) {
    ${({ md }) => md && getFlex(md)};
    ${({ md }) => md && getWidth(md)};
  }

  // Columns for medium desktops
  @media (min-width: 992px) {
    ${({ lg }) => lg && getFlex(lg)};
    ${({ lg }) => lg && getWidth(lg)};
  }

  // Columns for large desktops and HD devices
  @media (min-width: 1200px) {
    ${({ xl }) => xl && getFlex(xl)};
    ${({ xl }) => xl && getWidth(xl)};
  }
`
```

### Creating a flipping card with styled-components

Our grid is finished and ready to use. Now, our job is to use styled-components and create the flipping card. This card will have four main components: Card, "CardSide", "CardFront", "CardBack". Then, there will be additional three components for styling the content of the card: "CardNumber", "CardTitle", "CardDescription". These additional components are neither essential nor necessary to make our card work. So, feel free to omit them. They are here just for presentation, to make the textual content our cards look a bit better.

The theory behind the flipping card, and the mechanism of how it works, is quite simple. We will use styled-components to create one component called "Card". This component will be the main wrapper that contain two additional child component, one for frontside ("CardFront") and one for backside ("CardBack") of the card. Let's tackle the "Card" component first. "Card" will need two important CSS properties in order to work properly. First, we will need to set its `position` to "relative" and `perspective` to "1000px".

Next, both sides of the card, "CardFront" and "CardBack", will need two CSS properties that will be the same for both. The first one will be `position` set to "absolute" and the second one will be `backface-visibility` set to "hidden". Thanks to this, both sides will be stacked on each other and only one will be visible. Aside to these shared properties and values, "Cardback" will also need to have `transform` property set to "rotateY(-180deg)". Again, the rest of the styles is just for presentation and making our card a bit more pretty.

The last missing piece is the flipping mechanism. When the card is flipped, we will attach new _class_ "flipped" to the "Card" component. Then, we will use `transform` property along with `rotateY()` _method_ to rotate both sides of the card. Each side will require a different value. In case of the frontside, the value will be "-180deg". For the backside, it will be "0deg". We will also use `perspective()` _method_ with value of "1000px" and apply it to both cards. We can use `transition`, and declare inside the "CardSide" component, to make the flipping effect smoother.

Code:
```
// Flipping card
const Card = sc.article`
  position: relative;
  width: 100%;
  min-height: ${remy(380)};
  cursor: pointer;
  perspective: 1000px;
  transition: all .25s ease-in-out;

  &:focus,
  &:hover {
    box-shadow: 0 0 ${remy(40)} rgba(0,0,0,.15);
  }

  &.flipped {
    & > div:first-of-type { // frontside of the card
      transform: perspective(1000px) rotateY(-180deg);
    }

    & > div:last-of-type { // backside of the card
      transform: perspective(1000px) rotateY(0deg);
    }
  }
`

// Card sides
const CardSide = css`
  position: absolute;
  top: 0;
  left: 0;
  overflow: hidden;
  padding: ${remy(24)};
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  transition: all .25s ease-in-out;
`

// Card side - front
const CardFront = sc.div`
  ${CardSide};

  font-weight: bold;
  text-align: center;
`

// Card side - back
const CardBack = sc.div`
  ${CardSide};

  transform: rotateY(-180deg);
`

// Card content
const CardNumber = sc.span`
  display: block;
  font-size: ${remy(24)};
`

const CardTitle = sc.h2`
  font-size: ${remy(21)};
`

const CardDescription = sc.span`
  font-size: ${remy(16)};
`
```

### Building a simple layout

So, what we have done so far. We used styled-components to create responsive grid system. Then, we created a simple flipping card. However, we still have only styles. There is no layout we can render in our HTML container. Also, we don't have the function to attach the "flipped" _class_ to the "Card" component. Let's fix both these issues. We will do so by using all the components we previously created with styled-components to build a simple grid-based layout with one row containing four flipping cards.

Let's create a new `class` called "Layout". This class will contain one _method_ called "flipCard". This method will use `event` object, `currentTarget` and `classList` properties and `toggle` _method_ to add /remove _class_ "flipped" to/from the "Card" component. We will then attach this function, "flipCard", to every card and use it as a handler for `onClick` _event_. Now, to the grid. We will use two cards per row on resolutions bigger than 576 pixels ("sm" `prop` will be equal to'6') and 3 cards per row on resolutions bigger than 992 pixels ("lg" `prop` will be equal to'4').

Keep in mind that, as we discussed above, "GridColumn" components must be nested inside the "GridRow" component. And the "GridRow" components inside the "GridContainer". Another way is nesting our cards right inside the "GridContainer". Just don't put any card right into "GridRow". Ever. Otherwise, the layout will not work properly.

Code:
```
// Create layout component
class Layout extends React.Component {
  flipCard(event) {
    event.currentTarget.classList.toggle('flipped')
  }

  render() {
    return (
      <LayoutWrapper>
        <GridContainer>
          <GridRow>
            <GridColumn sm='6' lg='4'>
              <Card onClick={this.flipCard.bind(this)}>
                <CardFront>
                  <CardNumber>1.</CardNumber>

                  <CardTitle>Card</CardTitle>
                </CardFront>

                <CardBack>
                  <CardDescription>Rand's stated goal for writing the novel was "to show how desperately the world needs prime movers and how viciously it treats them" and to portray "what happens to the world without them".</CardDescription>
                </CardBack>
              </Card>
            </GridColumn>

            <GridColumn sm='6' lg='4'>
              <Card onClick={this.flipCard.bind(this)}>
                <CardFront>
                  <CardNumber>2.</CardNumber>

                  <CardTitle>Card</CardTitle>
                </CardFront>

                <CardBack>
                  <CardDescription>The core idea for the book came to her after a 1943 telephone conversation with a friend, who asserted that Rand owed it to her readers to write fiction about her philosophy.</CardDescription>
                </CardBack>
              </Card>
            </GridColumn>

            <GridColumn sm='6' lg='4'>
              <Card onClick={this.flipCard.bind(this)}>
                <CardFront>
                  <CardNumber>3.</CardNumber>

                  <CardTitle>Card</CardTitle>
                </CardFront>

                <CardBack>
                  <CardDescription>To produce Atlas Shrugged, Rand conducted research on the American railroad industry. Her previous work on a proposed (but never realized) screenplay.</CardDescription>
                </CardBack>
              </Card>
            </GridColumn>

            <GridColumn sm='6' lg='4'>
              <Card onClick={this.flipCard.bind(this)}>
                <CardFront>
                  <CardNumber>4.</CardNumber>

                  <CardTitle>Card</CardTitle>
                </CardFront>

                <CardBack>
                  <CardDescription>Atlas Shrugged is set in a dystopian United States at an unspecified time, in which the country has a "National Legislature" instead of Congress and a "Head of State" instead of a President.</CardDescription>
                </CardBack>
              </Card>
            </GridColumn>
          </GridRow>
        </GridContainer>
      </LayoutWrapper>
    )
  }
}

// Render Layout React element into the DOM
ReactDOM.render(
  <Layout />,
  container
)
```

## Closing thoughts on flipping card, grid and styled-components

That's it! You just finished this tutorial on styled-components and React. If everything went well, and you managed to follow this tutorial, you now have a responsive grid system with four simple flipping cards. I hope you had fun while working on this tutorial and learned something new about styled-components and maybe even React. If something went wrong, don't worry or beat yourself up. This too is part of the learning process. Give it a time and try to find out where is the problem and what caused it. Just don't give up.

However, if you it is too difficult to find the problem or how to fix it, please post a comment or contact me directly, over social media or email. I will do my best to help you solve it. Aside to that, if you want to learn more about styled-components, take a look at this [A Simple Introduction to Styled-components], [this article] about mastering styled-components fundamentals and also [official documentation].

What do you think about styled-components and React? Do you like this way of working with CSS in React? If so, what do you like the most? If not, do is your preferred way of using CSS in React?

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[CDN]: https://en.wikipedia.org/wiki/Content_delivery_network
[React]: https://cdnjs.com/libraries/react
[React-DOM]: https://cdnjs.com/libraries/react-dom
[styled-components]: https://cdnjs.com/libraries/styled-components
[quick explanation]: https://www.davidbcalhoun.com/2014/what-is-amd-commonjs-and-umd/
[JavaScript Modules: A Beginner’s Guide]: https://medium.freecodecamp.org/javascript-modules-a-beginner-s-guide-783f7d7a5fcc
[Babel]: https://babeljs.io/
[browser support]: https://blog.alexdevero.com/talk-browser-support/
[Bootstrap framework]: http://getbootstrap.com/
[fundamentals of styled-components]: https://blog.alexdevero.com/styled-components-mastering-fundamentals/
[docs]: https://www.styled-components.com/
[Codepen]: https://codepen.io/alexdevero/pen/EbpJro?editors=1010
[A Simple Introduction to Styled-components]: https://blog.alexdevero.com/introduction-styled-components/
[this article]: https://blog.alexdevero.com/styled-components-mastering-fundamentals/
[official documentation]: https://www.styled-components.com/

<!-- ### Inspiration
-
 -->
