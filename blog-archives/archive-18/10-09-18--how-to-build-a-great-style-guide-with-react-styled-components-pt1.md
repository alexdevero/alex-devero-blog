# How to Build a Great Style Guide with React & styled-components Pt.1

How hard could it be to create a style guide for your website, app, or any other project? And, what if you want to build it with React and styled-components? So, will you accept this challenge? Great! This tutorial will take you through the whole process and show you how you, too, can build a great style guide from scratch! Now, let's start and have some fun!

<!--
Table of Contents:
## Project setup
## Project structure
## Index 1.0
## Index 2.0
### Consts and styles
### Composing the main component
## Epilogue: How to Build UI [Style Guide] with React Pt.1
-->

## Project setup

Let's start with the first step. This step is about putting together the dependencies we will need to develop our style guide. We will need to install four of them-`react`, `react-dom`, `react-scripts` and `styled-components`. `react`, `react-dom` probably need no explanation. `react-scripts` is a bundle of scripts and configuration used and provided by [Create React App] project.

We will use these scripts and configs to make our work faster an easier. We will not have to deal with any bundler such as Webpack or Parcel. This all will be taken care of by `react-scripts`. Finally, we will use `styled-components` to take care about styling. We will not work with any CSS or Sass files. All styling will be done in JavaScript.

If this is the first time you will be using `styled-components`, you may want to take a look at its documentation. Then, you can also go through two tutorials focused on this library. First is [A Simple Introduction to Styled-components]. Second is [Styled-Components – Mastering the Fundamentals Through Practice]. This will help you understand how `styled-components` works.

Next, we will create scripts to run the style guide on dev server and also to build it when we are done. As I mentioned, we will use scripts from Create React App project. Now, the only thing we need to do is to "wire" together specific scripts with npm scripts. We will create four scripts-`start`, `build`, `test` and `eject`. However, today, we will only use the first two. And, that is all. This is how our `package.json` looks like.

_Note: you will need either npm or yarn package managers installed on your computer in order to install dependencies and work on this style guide. Npm is distributed with node. You can get the installer for your system on [nodejs website]. If you prefer yarn, that is actually really much better option, you can download the installer [here]._

```
// package.json

{
  "name": "ui-style-guide",
  "version": "1.0.0",
  "description": "",
  "keywords": [
    "design",
    "react",
    "reactjs",
    "styled-components",
    "style guide",
    "web design"
  ],
  "main": "src/index.js",
  "dependencies": {
    "react": "16.4.2",
    "react-dom": "16.4.2",
    "react-scripts": "1.1.4",
    "styled-components": "3.4.5"
  },
  "devDependencies": {},
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test --env=jsdom",
    "eject": "react-scripts eject"
  }
}
```

## Project structure

As the second step, let's outline the structure for this project. This will help us orient ourselves in the project. This will be quick. There will be two main directories in our style guide project, aside from `node_modules`. These directories will be `public` and `src`.

`public` will contain only one file-`index.html`. This is the file where we will render our style guide. `src` will contain directory called `components` and one file called `index.js`. `index.js` will be the main file where we will import all components for our style guide.

The `components` directory will contain all components, or parts, for our style guide. We will create all these components as [stateless functional components]. The only stateful component will be `App` in `index.js` which will be the main component for our style guide. This is the final representation of the structure of this project.

```
ui-style-guide
├── node_modules/
├── public/
│   └── index.html
├── src/
│   └── components/
│       └── component.jsx
│   └── index.js
├── package.json
└── yarn.lock
```

## Index 1.0

The `index.html` in `public` will be very simple. We will use a template used and provided by Create React App project. `head` will contain only the most necessary tags. There will be only two small changes-title and custom typeface [Roboto] loaded over Google Fonts CDN. Feel free to add additional [useful tags] if you want.

`body` will contain only two things. One will be notification message wrapped inside `noscript` saying that JavaScript is necessary to view the style guide. The second thing will be `div` where we will render the style guide. And, that is all. The final version of `index.html` looks like this:

```
<!-- index.html -->

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <meta name="theme-color" content="#000000">

    <!--
        manifest.json provides metadata used when your web app is added to the
        homescreen on Android. See https://developers.google.com/web/fundamentals/engage-and-retain/web-app-manifest/
      -->
    <link rel="manifest" href="%PUBLIC_URL%/manifest.json">
    <link rel="shortcut icon" href="%PUBLIC_URL%/favicon.ico">
    <!--
        Notice the use of %PUBLIC_URL% in the tags above.
        It will be replaced with the URL of the `public` folder during the build.
        Only files inside the `public` folder can be referenced from the HTML.

        Unlike "/favicon.ico" or "favicon.ico", "%PUBLIC_URL%/favicon.ico" will
        work correctly both with client-side routing and a non-root public URL.
        Learn how to configure a non-root public URL by running `npm run build`.
      -->

    <title>UI Style Guide</title>

    <!-- Roboto typeface -->
    <link href="https://fonts.googleapis.com/css?family=Roboto:300,400,500,700" rel="stylesheet">
  </head>

  <body>
    <noscript>
      You need to enable JavaScript to run this app.
    </noscript>

    <div id="root"></div>

    <!--
      This HTML file is a template.
      If you open it directly in the browser, you will see an empty page.

      You can add webfonts, meta tags, or analytics to this file.
      The build step will place the bundled scripts into the <body> tag.

      To begin the development, run `npm start` or `yarn start`.
      To create a production bundle, use `npm run build` or `yarn build`.
      -->
  </body>
</html>
```

## Index 2.0

Okay, let's finally dive into React! Our next goal is to create the `index.js` inside `src` directory. We will start by adding imports for all dependencies we will use inside this file. These dependencies are `react`, `react-dom` and `styled-components`. Next, we can add imports for all components we will create in the future. Let's comment them out for now so we can run the project.

_A note about `styled-components` and `injectGlobal`: throughout this tutorial we will use `styled-components` version "3.4.5". This is the latest. Aside to this version, there is also version 4 that is in beta. Feel free to use the beta version if you want. Just make sure to replace `injectGlobal` with `createGlobalStyle` ([info]). `injectGlobal` will not be available in version 4 and newer._

### Consts and styles

Next, let's create two variables, `colors` and `typography`. We will define both as `const`. And, they both will contain objects. `colors` will contain the main colors for the style guide color palette. `typography` will contain sizes in pixels for typography scale. After that, we will use the `injectGlobal` helper from by `styled-components` to add some default styling. If you decided to use `styled-components` version 4, use `createGlobalStyle`.

These styles will be about changing `box-sizing` for `html` and all elements. Then, we will add resets for `body` for `padding` and `margin`. Next, we will change the settings for main typeface, `font-family`, `line-height` and `font-size`. We will do this in one fell swoop by using CSS `font` property with shorthand. Finally, we can also change text color.

Now, we can play with `styled-components` and see how to use it to create some simple "styled" components. Let's create three components-`AppContainer`, `StyleguideHeading` and `StyleguideSubheading`. We will use these components only here, in `index.js`, to add some styling for our style guide. Meaning, these components will not be part of the style guide itself.

The `AppContainer` container will be div and we will use it is a main container, or "wrapper", for all content in our style guide. The `StyleguideHeading` and `StyleguideSubheading` will be for primary (h1) and secondary (h2) headings. There is one thing worth mentioning. Both headings will use CSS `::before` pseudo-class for creating underline.

What is the reason for creating the underline this way, rather than using just `text-decoration`, or `border`? Using `::before` will allow us much greater customization. We will have much more space to style the underline as we want, including its length. And, this is all for styling.

### Composing the main component

Now, there is one last thing we need to do, create the main stateful component for style guide-`App`, JavaScript class. As I mentioned in the begging, `App` will be the only stateful component we will create throughout this tutorial. Nonetheless, this component will be very simple. The only method this class will contain will be `render`. No `state`, at least for now.

`render` will return the `AppContainer`, as the top "wrapper". This wrapper will contain one top heading. Here, we will use the `StyleguideHeading` component. Next we will be some short text. This can be an introduction about the company website, app, or any other product, briefly describing what this style guide actually presents.

After that will come individual parts or components of our style guide. We will use the `StyleguideSubheading` component to create h2 headings that will differentiate these parts. For now, we will comment out all components since none of them exists now. Otherwise, we could not run launch the style guide and work on it on dev server.

Last but not least, we will query the DOM, find the `div` with id "root" in `index.html` and store it inside const variable. Finally, we will use this variable along with `render` method from `react-dom` and render the main, `App`, component in the DOM. With this, you should be able to launch the project and open the style guide on dev server. You can do so by using `yarn start` or `npm run start` command.

_Note: The default port is `3000`. If you want to change the default port, you can do so by changing npm scripts in `package.json`. Find the `start` script and change it to `"set PORT=xxxx && react-scripts start"` for Windows or `"PORT=xxxx && react-scripts start"` for Linux and MacOS. Some Linux distributions will require `"export PORT=xxxx && react-scripts start"`. The "xxxx" is for the port you want to use, such as 3001, 1999 or whatever._

```
// index.js

// Import dependencies
import React from 'react'
import ReactDOM from 'react-dom'
import styled, { injectGlobal } from 'styled-components'

// Import style guide components
// import Buttons from './components/buttons'
// import Colors from './components/colors'
// import Forms from './components/forms'
// import Typography from './components/typography'

// Codes for color palette
const colors = {
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
const typography = {
  xs: '12px',
  sm: '14px',
  base: '16px',
  lg: '18px',
  xl: '20px',
  xxl: '24px',
  xxxl: '30px',
  xxxxl: '36px'
}

// Global styles and resets
injectGlobal`
  html {
    box-sizing: border-box;
    font-size: ${typography.base};
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

  // Customizable underline
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

  // Customizable underline
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

        {/*<Colors colors={colors} />*/}

        <StyleguideSubheading>Typography</StyleguideSubheading>

        {/*<Typography colors={colors} scale={typography} />*/}

        <StyleguideSubheading>Buttons</StyleguideSubheading>

        {/*<Buttons colors={colors} />*/}

        <StyleguideSubheading>Forms</StyleguideSubheading>

        {/*<Forms colors={colors} scale={typography} />*/}
      </AppContainer>
    )
  }
}

const rootElement = document.getElementById('root')

ReactDOM.render(<App />, rootElement)
```

## Epilogue: How to Build UI Style Guide with React Pt.1

This is all for today and the first part of this tutorial. I hope you enjoyed it and learn something new, something useful. Let's do a quick recap. We started by putting together all dependencies, setting up the workflow and discussing the structure of this project. Then, we created the main `index.html` file which is also the only non-JavaScript file in this project, aside to files with configuration.

As the last step, we moved to JavaScript, or rather React. We created the `index.js`. Here, we used `styled-components` to style the style guide and created a couple of very simple "styled" components, used purely for presentation. After that, we created the main component, the `App`, and finished our today's work by rendered the `App` into DOM.

What is next? In the next part we will work on individual components, or parts, for our style guide. These components will include colors, typography, buttons and forms. We will work a lot with `styled-components`. So, you may want to set aside some time and explore this library to prepare yourself. With that, I look forward to seeing you here again the next week. Have a great day!

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Create React App]: https://github.com/facebook/create-react-app
[documentation]: https://www.styled-components.com/docs
[A Simple Introduction to Styled-components]: https://blog.alexdevero.com/introduction-styled-components/
[Styled-Components – Mastering the Fundamentals Through Practice]: https://blog.alexdevero.com/styled-components-mastering-fundamentals/
[stateless functional components]: https://code.tutsplus.com/tutorials/stateful-vs-stateless-functional-components-in-react--cms-29541
[useful tags]: https://github.com/joshbuchea/HEAD
[Roboto]: https://fonts.google.com/specimen/Roboto
[info]: https://www.styled-components.com/docs/api#createglobalstyle
[nodejs website]: https://nodejs.org/en/download/
[here]: https://yarnpkg.com/en/docs/install#windows-stable

<!--
#### Meta:
-
-->

<!--
#### Inspiration:
- https://codesandbox.io/s/29xv0n51y
- https://designmodo.com/create-style-guides/
- https://www.kickstarter.com/help/brand_assets
- https://webstyleguide.com/
-->
