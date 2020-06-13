# 5 Most Popular Ways to Style [React Components] Pt.2
Choosing the right way to style React components is hard. There are too many choices. In this article, we will take a look at the last two most popular ways to style React components. In order to help you find the right fit for you, we will also try each of these ways on a very simple example.<!--more-->
<!--
Table of Contents:
## No.4: CSS modules
### How to use CSS modules to style React Components
### How to implement CSS modules in create-react-app
### How to implement CSS modules with custom webpack config
### CSS modules with Sass
### How to implement CSS modules with Sass with CRA
### How to implement CSS modules with Sass with custom webpack config
## No.5: CSS-in-JS
### How to choose CS-in-JS library
## The most popular CSS-in-JS libraries
### Styled-components
### Emotion
### JSS
### Radium
### Aphrodite
### Styletron
### Fela
## Epilogue: Most Popular Ways to Style React Components
-->

5 Most Popular Ways to Style React Components [Part 1].

## No.4: CSS modules

[CSS modules] are the last option to style React components with good old CSS stylesheets. CSS modules allows you to keep your CSS styles in external CSS files. A lot of developers like this because it helps them keep their project structure clean and organized. On the other hand, other developers prefer to have both, JS and CSS, in the same file.

### How to use CSS modules to style React Components

Using CSS modules is simple. When you want to use specific styles, or stylesheet, you import it. You an import it in two ways. First, you can import it as a regular stylesheet, i.e. `import '.some-stylesheet.css'`. Or, second, you can stay true to the name and important your styles as a modul.

This means using named import, i.e. `import buttonStyles from './button.module.css'`. There are few things that deserve closer examination. First, the 'buttonStyles' name can be anything you want. You will use this name later when you will want to reference this stylesheet, when you will want to apply the styles in this stylesheet.

The second thing is the '.module.css' part. This is a naming convention for using CSS modules. This is recommended as a good practice to follow it. It is good to follow it to make sure everything works as it should. You know, things can break. That was about importing stylesheets. Now, how can you use individual classes defined in those stylesheets?

This is where comes the name you chose for the import. To import a specific style, defined inside a class, you use the name of the import followed by dot (`.`) followed by the class name. So, if the `button.module.css` contains styles for `.btnPrimary` the syntax will be `buttonStyles.btnPrimary`.

You will pass this syntax in the `className` attribute on the React component. It is very similar to using inline styles with JavaScript object, we discussed in the [first part]. Let's take a look at more concrete example. First, you will create `button.module.css` file and put CSS styles you want to use to style React components here.

One thing that CSS modules allow, and CSS not, is extending one CSS class with another. In other words, you can let one class inherit styles from another. As a result, you don't have to write the same chunk of CSS multiple times. Instead, you can create a "base" class with all default styles.

Then, you can let other class inherit, and use, those styles. You can do this using `composes` property. Remember that this property has to be at the top, before any other CSS rules.

```
/* button.module.css */
/* Create base button class*/
.btn {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 8px 16px;
  font-size: 15px;
  font-weight: 700;
  color: #fff;
  border: 0;
  border-radius: 3px;
}

/* Create variants of button styles */
.btnPrimary {
  composes: btn; /* extends btnPrimary with styles from btn */

  background-color: #3498db;
}

.btnSecondary {
  composes: btn; /* extends btnPrimary with styles from btn */

  background-color: #1abc9c;
}

.btnDanger {
  composes: btn; /* extends btnPrimary with styles from btn */

  background-color: #e74c3c;
}
```

Next step, when you are have the CSS to style React components ready, is to import the stylesheet in your React component. Remember the syntax for importing your stylesheet, i.e. `import someStyles from 'someStyles.module.css'`. And, remember to pass the import name with specific class to the `className` attribute, i.e. `style={buttonStyles.btnSecondary}`.

```
// button.jsx

// Import react
import * as React from 'react'

// Import styles for button component
import buttonStyles from 'button.module.css'

// Create react Button component
const ButtonExample = () => {
  return (
    <>
      {/* Use 'btnPrimary' class from 'buttonStyles' to style the button */}
      <button className={buttonStyles.btnPrimary}>Primary button</button>

      {/* Use 'btnSecondary' class from 'buttonStyles' to style the button */}
      <button className={buttonStyles.btnSecondary}>Secondary button</button>

      {/* Use 'btnDanger' class from 'buttonStyles' to style the button */}
      <button className={buttonStyles.btnDanger}>Danger button</button>
    </>
  )
}
```

### How to implement CSS modules in create-react-app

If you are using [create-react-app], or at least react-scripts, you don't have to worry about anything. CRA supports CSS right from the start, since version 2.0.0. All you have to do is create your first CSS module, add some styles, import it in your app and start using these styles to style React components.

### How to implement CSS modules with custom webpack config

What if you are not using CRA? Implementing CSS modules, with webpack for example, is quite easy. First, you will need to install `css-loader` and `style-loader` plugins for webpack. Next, you will need to add rules for CSS files, and implement these loaders.

In options you will need to enable CSS modules setting `modules` to `true`. You will also need to set `importLoaders` to `1`, or higher if you are using other loaders than `css-loader`. This will be also in settings for `css-loader` plugin.

```
// webpack.config.js

const webpack = require('webpack');
const path = require('path');

const config = {
  entry: './src/index.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  },
  module: {
    rules: [
      {
        test: /\.css$/, // Add rules for css files
        use: [
          'style-loader',
          {
            loader: 'css-loader',
            options: {
              importLoaders: 1,
              modules: true // Enable CSS modules
            }
          }
        ]
      },
      {
        test: /\.(js|jsx)$/,
        use: 'babel-loader',
        exclude: /node_modules/
      }
    ]
  },
  resolve: {
    extensions: [
      '.js',
      '.jsx'
    ]
  },
  devServer: {
    contentBase: './dist'
  }
}

module.exports = config;
```

Lastly, if you already have npm scripts prepared you are good to go. If not, you can use npm scripts from the example `package.json` below.

```
{
  "name": "empty-project",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "keywords": [],
  "author": "",
  "license": "ISC",
  "scripts": {
    "clean": "rm dist/bundle.js",
    "build-dev": "webpack -d --mode development",
    "build-prod": "webpack -p --mode production",
    "start": "webpack-dev-server --hot --mode development"
  },
  "dependencies": {
    "react": "^16.9.0",
    "react-dom": "^16.9.0",
    "react-hot-loader": "^4.12.13"
  },
  "devDependencies": {
    "@babel/core": "^7.6.0",
    "@babel/preset-env": "^7.6.0",
    "@babel/preset-react": "^7.0.0",
    "babel-loader": "^8.0.6",
    "css-loader": "^3.2.0",
    "style-loader": "^1.0.0",
    "webpack-cli": "^3.3.8",
    "webpack-dev-server": "^3.8.0"
    "webpack": "^4.40.2",
  }
}
```

### CSS modules with Sass

Another good thing on CSS modules is that they also support pre-processors such as [Sass]. We talked about Sass, and how to use it to style React components, in the [previous part] as an alternative to CSS stylesheet. However, you can also use Sass stylesheets as CSS modules. So, if Sass is your favorite you can use it with CSS modules.

The syntax for import and usage is the same as with CSS modules. The naming convention is also almost the same, except you use `.scss` or `.sass` instead of `.css` file extension. So, something like `foo.module.scss` or `foo.module.sass`.

### How to implement CSS modules with Sass with CRA

Another good news for those using CRA. As you know from the [previous part], Sass is supported by CRA from the start. And, as you now know CSS modules are supported as well. And, yes, you can use them together. You will need to install `css-loader` and `style-loader` plugins for webpack so webpack can work with CSS files, and CSS modules.

Next, you will also need to install and `node-sass`. This will allow webpack work with Sass files, both `.scss` and `.sass`. And, that's it. You are ready to start using Sass and CSS modules to style React components in your project. Just add new `.scss` or `.sass` module, add some styles, import it and apply the styles via `className` attribute.

```
// button.module.scss
/* Create base button class*/
.btn {
  .. some styles ...
}

.btnPrimary {
  composes: btn; /* extends btnPrimary with styles from btn */

  background-color: #3498db;
}
```

Remember to import your stylesheets as `.scss` or `.sass`.

```
// button.jsx

// Import react
import * as React from 'react'

// Import styles for button component
import buttonStyles from 'button.module.scss'

// Create react Button component
const ButtonExample = () => {
  return (
    <>
      {/* Use 'btnPrimary' class from 'buttonStyles' to style the button */}
      <button className={buttonStyles.btnPrimary}>Primary button</button>
    </>
  )
}
```

### How to implement CSS modules with Sass with custom webpack config

Implementing Sass with CSS modules is almost the same as implementing CSS modules. The difference is that you will need to install `sass-loader` and `node-sass`. After that, you will need to add rules for Sass files and implement `sass-loader` in your webpack config.

```
// webpack.config.js

const webpack = require('webpack');
const path = require('path');

const config = {
  entry: './src/index.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  },
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          'style-loader',
          {
            loader: 'css-loader',
            options: {
              importLoaders: 1,
              modules: true // Enable CSS modules
            }
          }
        ]
      },
      {
        //  Add rules for scss files
        test: /\.(scss|sass)$/,
        use: [
          'style-loader',
          'css-loader',
          'sass-loader'
        ]
      },
      {
        test: /\.(js|jsx)$/,
        use: 'babel-loader',
        exclude: /node_modules/
      }
    ]
  },
  resolve: {
    extensions: [
      '.js',
      '.jsx'
    ]
  },
  devServer: {
    contentBase: './dist'
  }
}

module.exports = config;
```

## No.5: CSS-in-JS

Enough of CSS. It is time to take a look at "native" JavaScript solutions to style React components. These are usually referred to as CSS-in-JS. There are [many libraries] belonging into this category. There are some CSS-in-JS libraries that look very similar to inline CSS. The syntax is almost indistinguishable and it works in the same way.

Then, there are libraries that take CSS to another level. These libraries have their own API and offer additional features and more flexibility. On big difference between inline CSS and CSS-in-JS is that CSS-in-JS injects a `<style>` HTML tag on top of the DOM, the HEAD section. Inline styles attaches CSS properties to the DOM node.

This is why when you use some CSS-in-JS library to style React components you will see many `<style>` HTML tag pop up from nowhere. Don't worry. This is completely normal. It could be a problem when there were no `<style>` tags at all.

### How to choose CS-in-JS library

When it comes to choosing which library to use there are criteria you can use. For example, does the library support pseudo-classes? Right now, the majority of CS-in-JS libraries supports pseudo-classes. However, there are still some exceptions that don't. So, pay attention and read the docs before you make your decision.

Another thing to look for is support of media queries. This used to be an issue as well, like in the case of pseudo-class. Now, the majority of CS-in-JS libraries supports media queries. Next, you can look for libraries that support automatic vendor prefixing. This will help you narrow your selection since not all libraries have this feature.

If you like to have your CSS in separate files, you can also look for libraries that support extracting CSS to files. This will help you narrow your selection of CS-in-JS libraries to style React components even more. However, consider if this is really what you want, using external CSS files, instead of injected `<style>` tags.

Lastly, when you are about to choose one of the CS-in-JS libraries consider the non-technical things. Pay attention to how maintained the library is. You should avoid libraries that are no longer in development. Another thing to look for is active community, its size and also support.

You should always prefer libraries that are in active development with big, active and supportive community. In other words, check releases and their dates, number of issues and PRs, number of stars and forks and even public chat channels. This will help you narrow your selection to only few options.

Next, you can take this selection and try one option after another to see which one suits you and your style the best. Okay, let's take a look at the most popular CSS-in-JS libraries.

## A Quick Introduction to the most popular CSS-in-JS libraries

The most popular, and still maintained, CSS-in-JS libraries at this moment are [styled-components], [radium], [emotion], [jss], [aphrodite], [styletron] and [fela]. Another popular library is [glamor]. However, this one was not updated since 2017. It looks like it is no longer in development. So, let's stick with those seven, and let's take a look at one quick example and how to implement it with these libraries.

### Styled-components

Let's start with [styled-components] this is probably the most popular CSS-in-JS library, and way to style React component, right now. This is also my favorite way to style React components. With styled-components you create custom React components that styled-components then renders as a specific, valid, HTML element.

A simple example of how to use styled-components:

```
// Import React
import React from 'react'

// Import styled components
import styled from 'styled-components'

// Create custom Container component that will render as 'main' HTML element
const Container = styled.main`
  display: flex;
 	align-items: center;
  flex-direction: column;
  min-height: 100%;
  width: 100%;
  background-color: #fff;
`;

// Create custom Button component that will render as 'button' HTML element
const Button = styled.button`
  display: flex;
 	align-items: center;
  justify-content: center;
  width: 150px;
  height: 45px;
  background: #3498db;
  border: 0;
	color: #fff;

	&:hover {
    background: #2980b9;
  }
`;

// Create main React component
export default Example = () => {
  return (
    {/* Use custom Container component */}
    <Container>
      {/* Use custom Button component */}
      <Button>Click me</Button>
    </Container>
  )
}
```

If you like this approach check out these two tutorials that will help you learn how to use styled-component. The first one is [A Simple Introduction to Styled-components]. The second one is [Styled-Components – Mastering the Fundamentals Through Practice].

### Emotion

[Emotion] is another very popular CSS-in-JS library. It is probably right after styled-components. It is also very easy to use. And, as you can see, it actually looks and works in a similar way to styled-components. You use it to create custom React components and emotion then renders these components as regular HTML elements.

A simple example of how to use emotion:

```
// Import React
import React from 'react'

// Import emotion
import styled from 'react-emotion'

// Create custom Container component
const Container = styled('main')`
  display: flex;
 	align-items: center;
  flex-direction: column;
  min-height: 100%;
  width: 100%;
  background-color: #fff;
`;

// Create custom Button component
const Button = styled('button')`
  display: flex;
 	align-items: center;
  justify-content: center;
  width: 150px;
  height: 45px;
  background: #3498db;
  border: 0;
	color: #fff;

	&:hover {
    background: #2980b9;
  }
`;

// Create main React component
export default function Example() {
  return (
    {/* Use custom Container component */}
    <Container>
      {/* Use custom Button component */}
      <Button>Click me</Button>
    </Container>
  )
}
```

### JSS

Next, the [JSS]. With JSS, you create CSS in the form of a JavaScript object. Individual CSS classes are keys and values are objects with CSS styles. Before you can use these styles, you have to do a one-time setup to load presets with `setup()` method. Then, you need to compile your styles, apply presets and create stylesheet.

You do this with `createStyleSheet()` and `attach()` methods. After this, you are ready to use the CSS you created to style React components through `className` attribute.

A simple example of how to use JSS:

```
///
// JSS example
// Import React
import React, { Component } from 'react'

// Import JSS and default preset
import jss from 'jss'
import preset from 'jss-preset-default'

// One-time setup with default plugins and settings.
jss.setup(preset());

// Create JS object with CSS styles
const styles = {
  container: {
    display: 'flex',
    alignItems: 'center',
    flexDirection: 'column',
    width: '100%',
    minHeight: '100%',
    backgroundColor: '#fff'
  },
  button: {
    display: 'flex',
    alignItems: 'center',
    justifyContent: 'center',
    width: 150,
    height: 45,
    background: '#3498db',
    border: 0
    ':hover': {
      backgroundColor: '#2980b9'
    }
  }
}

// Compile styles and apply plugins.
const { classes } = jss.createStyleSheet(styles).attach();

// Create main React component
export default function Example() {
  return (
    {/* Apply styles for container */}
    <main className={classes.container}>
      {/* Apply styles for button */}
      <button className={classes.button}>Click me</button>
    </main>
  )
}
```

### Radium

Then comes the [Radium]. In the case of Radium, the setup is easier. You import the Radium library, define your CSS styles, also in the form of a JavaScript object. Then, you can apply these styles using the variable name and the CSS class, key inside the object with styles. As the last step, you activate Radium by wrapping your component with it.

A simple example of how to use Radium:

```
// Import React
import React, { Component } from 'react'

// Import radium
import Radium from 'radium'

// Create JS object with CSS styles
const styles = {
  container: {
    display: 'flex',
    alignItems: 'center',
    flexDirection: 'column',
    width: '100%',
    minHeight: '100%',
    backgroundColor: '#fff'
  },
  button: {
    display: 'flex',
    alignItems: 'center',
    justifyContent: 'center',
    width: 150,
    height: 45,
    background: '#3498db',
    border: 0
  }
}

// Create React component
function Example() {
  return (
    {/* Apply styles for container */}
    <div style={styles.container}>
      {/* Apply styles for button */}
      <button style={styles.button}>Click me</button>
    </div>
  )
}

// Activate Radium by wrapping your component
export default Radium(Example)
```

### Aphrodite

Aphrodite looks similar to JSS. Like JSS, you also create styles in the form of an object. And, you also create a stylesheet, with `StyleSheet` and `create()`. However, you don't have to set up or attach anything. You only need to use aphrodite's `css` function to apply specific class (key) from the object that contains your CSS styles.

A simple example of how to use aphrodite:

```
// Import React
import React from 'react'

// Import aphrodite
import { StyleSheet, css } from 'aphrodite'

// Create main React component
function Example() {
  return (
    {/* Apply styles for container */}
    <div className={css(styles.container)}>
      {/* Apply styles for button */}
      <button className={css(styles.button)}>Click me</button>
    </div>
  )
}

// Use aphrodite to create CSS stylesheet
const styles = StyleSheet.create({
	container: {
    display: 'flex',
    alignItems: 'center',
    flexDirection: 'column',
    width: '100%',
    minHeight: '100%',
    backgroundColor: '#fff'
  },
  button: {
    display: 'flex',
    alignItems: 'center',
    justifyContent: 'center',
    width: 150,
    height: 45,
    background: '#3498db',
    border: 0,
    ':hover': {
      backgroundColor: '#2980b9'
    }
  }
})

export default Example
```

### Styletron

[Styletron] is very similar to emotion and styled-components. It is also based on creating custom React component that styletron renders as usual HTML elements. Just like styled-components and emotion, it also injects CSS style to DOM via `<style>` HTML tag. However, the setup requires one more step.

When you want to use custom components created with styletron you need to provide an instance of styletron engine, i.e. use `StyletronProvider` as a wrapper for your main React component. Aside to this difference, work with styletron is almost the same as with emotion and styled-components.

A simple example of how to use styletron:

```
// Import React
import React from 'react'

// Import styletron
import Styletron from 'styletron'
import { styled, StyletronProvider } from 'styletron-react'

// Create custom Container component
const Container = styled('main', {
  display: 'flex',
  alignItems: 'center',
  flexDirection: 'column',
  width: '100%',
  minHeight: '100%',
  backgroundColor: '#fff'
})

// Create custom Container component
const Button = styled('button', {
  display: 'flex',
 	alignItems: 'center',
  justifyContent: 'center',
  width: 150,
  height: 45,
  background: '#3498db',
  border: 0,
  ':hover': {
    backgroundColor: '#2980b9'
  }
})

// Create main React component
export default function Example() {
  return (
    {/* Create StyletronProvider */}
    <StyletronProvider styletron={new Styletron()}>
      {/* Use Container component */}
      <Container>
        {/* Use Button component */}
        <Button>Click me</Button>
      </Container>
    </StyletronProvider>
  )
}
```

### Fela

[Fela] will be the last CSS-in-JS library you can use to style React components we will take a look at. By the syntax, fela is somewhat similar to styletron. The setup requires a few more steps than in the case of styled-components or emotion. You need to create a Fela renderer, using `createRenderer`, that will render your CSS styles.

When you create the renderer, you can also configure any plugins and presets you want to use. This is similar to JSS. Then, you can create your custom React component that will render as HTML elements, using `createComponent()` method. This is similar to styled-components and emotion, and the `styled()` method. However, this is not all yet.

Before you can render your React components in the DOM, you also need to wrap your main React component with `Provider` component, provided by `react-fela`. After this, you can render your components.

A simple example of how to use Fela:

```
// Import React
import React from 'react'

// Import Fela
import { Provider, createComponent } from 'react-fela'
import { createRenderer } from 'fela'
import webPreset from 'fela-preset-web'

// Create a Fela renderer to render CSS styles
// and configure plugins to process CSS styles
const renderer = createRenderer({
  plugins: [...webPreset]
})

// Create custom Container component
const Container = createComponent(() => ({
  display: 'flex',
  alignItems: 'center',
  flexDirection: 'column',
  width: '100%',
  minHeight: '100%',
  backgroundColor: '#fff'
}))

// Create custom Button component
const Button = createComponent(() => ({
  display: 'flex',
 	alignItems: 'center',
  justifyContent: 'center',
  width: '150px',
  height: '45px',
  background: '#3498db',
  border: 0,
  ':hover': {
    backgroundColor: '#2980b9'
  }
}))

// Create main React component.
export default () => (
  // Creates a Fela provider
  <Provider renderer={renderer}>
    {/* Use Container component */}
    <Container>
      {/* Use Button component */}
      <Button>Click me</Button>
    </Container>
  </Provider>
)
```

## Epilogue: Most Popular Ways to Style React Components

There you have it. These were the last two most popular ways to style React components. Next step? Take a look at all five ways to style React components we discussed in this and the [previous part]. Try each of these ways. This will give you a better understanding of how they work. You will also see which one feels more comfortable to you.

In the end, it doesn't matter how popular some library is. Or, how many stars it has on GitHub. What matters is if you like working with it. So, set aside a few minutes and create a small side project. Use this side project to experiment with various options to style React components you find interesting.

When you find one, stick to it. Learn how to use it and how it works. Then, master it. If you find something better, something you like more, sure, go for it and try it. However, don't "change your mind" every week or month. Remember, it is better to truly master one library or framework than to barely know a handful.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Part 1]: https://blog.alexdevero.com/style-react-components-pt1/
[CSS modules]: https://github.com/css-modules/css-modules
[first part]: https://blog.alexdevero.com/style-react-components-pt1/#using-javascript-object
[create-react-app]: https://github.com/facebook/create-react-app
[react-scripts]: https://www.npmjs.com/package/react-scripts
[Sass]: https://sass-lang.com/
[previous part]: https://blog.alexdevero.com/style-react-components-pt1/#no3-css-post-processors-and-pre-processors
[many libraries]: https://michelebertoli.github.io/css-in-js/
[styled-components]: https://www.styled-components.com/
[radium]: https://github.com/FormidableLabs/radium
[Radium]: https://github.com/FormidableLabs/radium
[emotion]: https://github.com/emotion-js/emotion
[Emotion]: https://emotion.sh/docs/introduction
[jss]: https://github.com/cssinjs/jss
[aphrodite]: https://github.com/Khan/aphrodite
[styletron]: https://github.com/styletron/styletron
[Styletron]: https://www.styletron.org/react/
[fela]: https://github.com/robinweser/fela
[Fela]: http://fela.js.org/
[glamor]: https://github.com/threepointone/glamor
[JSS docs]: https://cssinjs.org/
[A Simple Introduction to Styled-components]: https://blog.alexdevero.com/introduction-styled-components/
[Styled-Components – Mastering the Fundamentals Through Practice]: https://blog.alexdevero.com/styled-components-mastering-fundamentals/

<!--
### Meta:
- Choosing the right way to style React components is hard. There are too many options to choose from. This article will help you make this choice easier.
-->

<!--
#### Resources:
- https://blog.bitsrc.io/5-ways-to-style-react-components-in-2019-30f1ccc2b5b
- https://codeburst.io/4-four-ways-to-style-react-components-ac6f323da822
- https://css-tricks.com/css-modules-part-3-react/
- https://www.agiratech.com/5-best-way-to-style-react-components/
-->
