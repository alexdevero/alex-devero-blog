# 5 Most Popular Ways to Style React Components Pt.1
There are many ways to style React components. Some are better than others. This can make choosing the right one hard. In this article, we will review the first three most popular ways to style React components. We will also take a look at how to implement each, so you can find the one you like the most.
<!--more-->
<!--
Table of Contents:
## No.1: Inline CSS
### Using `style` attribute
### Using JavaScript object
### Mistake to avoid when using inline CSS
### The downside of styling React Components with inline CSS styles
### When to use inline CSS styles
## No.2: External CSS stylesheets
### How to use external CSS stylesheets
### Upsides and downsides
### Implementation
### Minifying CSS files made automatic
## No.3: CSS post-processors and pre-processors
### Using PostCSS
### Using Sass with CRA
### Using Sass with custom webpack config
### Using Less with overrides
### Using Less with custom webpack config
## Epilogue: Most Popular Ways to Style React Components

5 Most Popular Ways to Style React Components [Part 2].
-->

## No.1: Inline CSS

Using inline CSS is one of the easiest ways to style React components. It doesn't require any vast knowledge of CSS or even React. In addition, there is no need to use any 3rd party plugin or library. You already have everything you need to make this work. This makes it is very easy to use for beginners.

### Using `style` attribute

There are two ways to use inline CSS to style React components. The first one is passing the CSS styles through the `style` attribute right to the element. When you choose this way of styling your React components you pass your CSS styles in the form of an object. This way gives you two options to write your CSS styles.

The first option is to write all your CSS styles as you would in CSS stylesheet, or as inlined in HTML, wrapping individual CSS properties with quotes, i.e. `'font-size'` or `'max-width'`. The second option is to write your CSS styles using camelCase notation. Here, you don't have to use quotes. There is camelCase equivalent for every CSS property.

If CSS property consists only from one word, i.e. `display`, `margin`, `border`, you can omit the quotes as well. Specifying values also works in two ways. Numerical CSS values don't require quotes. If some value contains pixel unit, you can omit the `px`. React will add `px` units automatically.

So, instead of `'font-size': '32px'` you can write `'font-size': 32`, or `fontSize: 32`. If you include units, along with numbers, you have to wrap the value with quotes. For non-numerical units quotes are necessary. So, setting `font-weight` to `normal` without quotes will not work. You will have to use quotes-`'normal'`.

The other option is to use number `400`. Since, numerical unitless values don't require quotes, this will allow you to omit quotes also here and use `400` without quotes to set `font-weight`. Notice, and remember, that when you specify CSS styles through the `style` attribute, you have to use double curly brackets `{{}}`.

The first pair of curly brackets, the outer, creates an expression in JSX. This allows you to pass any JavaScript expression, variable or object to the attribute. The second pair, the inner, specifies that you are using JavaScript object.

```
// Create simple App React component
function App() {
  return (
    {/* Use inline styles to style wrapper div */}
    <div
      className="App"
      style={{
        'display': 'flex',
        'flex-flow': 'column nowrap'
      }}
    >
      {/* Use inline styles to style primary heading */}
      {/* We use CSS properties wrapped in quotes and values with units. */}
      <h1
        style={{
          'margin-top': '21px',
          'font-size': '21px',
          'line-height': 1.2,
          'font-weight': 600,
          'color': '#fff'
        }}
      >

      {/* Use inline styles to style secondary heading */}
      {/* We use CSS properties without quotes, using camelCase notation, and values without units. */}
      <h2
        style={{
          marginTop: 21,
          fontSize: 21,
          fontWeight: 600,
          lineHeight: 1.2,
          color: '#fff'
        }}
      >
        This is greeting from React.
      </h2>
    </div>
  )
}
```

### Using JavaScript object

The second way to use inline CSS to style React components is by creating new variable and assigning JavaScript object with your CSS to it. Then, you pass the name of this variable to the `style` attribute. The benefit of this approach is that it can help you keep your React components cleaner.

Instead of cluttering the `render` method of your React components with CSS, you can declare your styles outside it. Then, you can just reference those variables, using specific variable name. What's more, this also allows you to use inline styles more than once. This would not be possible if you passed CSS straight to the `style` attribute.

The same rules we discussed for the direct approach using `style` attribute applies here as well. In the end, we are doing the same. We are still passing JavaScript object containing CSS styles in the form of key/value pairs. So, `px` units and quotes for one-word properties, or properties written using camelCase notation, are not necessary.

Notice, on the example below, that when you pass the variable name to the `style` attribute you use only one pair of curly brackets `{}`. You use two only if you pass your CSS styles directly. When you use variables, you only need to specify that you want to use expression in JSX, you want to use a variable. The second pair is included in the object, you are referencing by the variable name.

```
// Declare CSS styles for wrapper div
const divWrapperStyles = {
  'display': 'flex',
  'flex-flow': 'column nowrap'
}

// Declare CSS styles for primary heading
const headingStyles = {
  'font-size': '21px',
  'line-height': 1.2,
  'color': '#fff'
}

// Create simple App React component
function App() {
  return (
    {/* Style wrapper div referencing the 'divWrapperStyles' variable containing CSS styles */}
    <div className="App" style={divWrapperStyles}>
      {/* Style primary heading referencing the 'headingStyles' variable containing CSS styles */}
      <h1 style={headingStyles}>
        Hello World!
      </h1>
    </div>
  )
}
```

### Mistake to avoid when using inline CSS

One important thing to remember about using inline CSS is that, now, you are specifying your CSS in the form of an JavaScript object. This means that you don't use semicolons (`;`) to separate individual CSS property/value pairs. Semicolons inside object would break JavaScript code, and your React components.

Instead of using semicolons, as you would in CSS stylesheet of HTML, you separate CSS property/value pair with commas (`,`). Remember, you are working with JavaScript objects and key/value pairs not CSS stylesheet. Key/value pairs in objects are separated by commas (`,`). One more thing. Whether you also add dangling comma is up to you.

```
///
// WRONG: What not to do
function App() {
  return (
    <div className="App">
      <h1
        style={{
          'font-size': 21; // ! Don't use semicolons here
          'line-height': 1.2; // ! Don't use semicolons here
          'color': '#fff; // ! Don't use semicolons here
        }}
      >
        Hello World!
      </h1>
    </div>
  )
}

const rootElement = document.getElementById('root')
render(<App />, rootElement)


///
// Correct: What to do
function App() {
  return (
    <div className="App">
      <h1
        style={{
          'font-size': 21, // Use only commas here
          'line-height': 1.2, // Use only commas here
          'color': '#fff // Trailing comma is optional
        }}
      >
        Hello World!
      </h1>
    </div>
  )
}

const rootElement = document.getElementById('root')
render(<App />, rootElement)
```

### The downside of styling React Components with inline CSS styles

There are few major downsides coming with inline CSS styles. The first big problem is that you can't use CSS pseudo-classes, such as `:hover`, `:active`, `:focus`, `:visited`, `::before`, `::after`, etc. This puts serious limits on how you can style React components. Another issues us that you can't use media queries.

If you want to build responsive React components you will not like inline CSS styles. There is no way to use media queries. This also used to be a big problem with CSS-in-JS, another way to style React components we will discuss later. The last big issue used to be inability to use vendor prefixes. Fortunately, this one has been solved.

Vendor prefixes are pain in the butt. They clutter your CSS and make it larger than necessary. Unfortunately, there are necessary, at least if you want to keep the number of browser that can view your React app at a reasonable level. When you want to support older browsers, you need to use slightly modified version of CSS properties.

CSS styles in React you want to have prefixed need to 1) start with the vendor prefix and 2) use camelCase. For example, prefixed `transition` property would be `WebkitTransition` for `-webkit-transition`, `msTransition` for `-ms-transition`, `MozTransform` for `-moz-` and `OTransition` for `-o-transition`.

Notice that properties with `-ms-` prefix start with lowercase "m". No, that is not a typo. Prefixes with `-ms-` do start with lowercase letters. This is one exception when it comes to prefixed CSS styles in React. The rest of vendor prefixes, prefixed properties, always starts with capital letter.

```
///
// JavaScript object with prefixed CSS styles
const wrapperStyles = {
  WebkitTransform: 'rotate(30deg)',
  msTransform: 'rotate(30deg)',
  transform: 'rotate(30deg)',
  WebkitFilter: 'grayscale(50%)',
  filter: 'grayscale(50%)'
}

function App() {
  return (
    <div className="App" style={wrapperStyles}>
      <h1>Hello world!</h1>
    </div>
  )
}


///
// Prefixes with 'style' attribute
function App() {
  return (
    <div className="App" style={{
      WebkitTransform: 'rotate(30deg)',
      msTransform: 'rotate(30deg)',
      transform: 'rotate(30deg)',
      WebkitFilter: 'grayscale(50%)',
      filter: 'grayscale(50%)'
    }}>
      <h1>Hello world!</h1>
    </div>
  )
}
```

On the good note, inline CSS styles at least allows to re-use your CSS styles. If you create your styles as objects and assign them to variables you can then reference (use) these variables as often as you want. You don't have to write all the CSS styles over and over again.

```
// JavaScript object with prefixed CSS styles
const headingSecondaryStyles = {
  'font-size': '21px',
  'font-weight': 700,
  'text-transform': 'capitalize',
  color: '#11'
}

function App() {
  return (
    <div className="App">
      <h1>Hello world!</h1>

      {/* Using previously defined styles to style h2 heading */}
      <h2 style={headingSecondaryStyles}>Hello world!</h2>

      {/* Using previously defined styles to style h2 heading */}
      <h2 style={headingSecondaryStyles}>Hello world!</h2>
    </div>
  )
}
```

### When to use inline CSS styles

There are two use cases we have to consider. These are React web apps and React apps built with either React, [React native] or [electron]. In case of apps build for web, inline styles are good if you want to make some small, quick corrections. However, that is about it. I would not recommend using inline styles on a larger scale.

Inline styles are hard to maintain, even if you use JavaScript objects. It would also be a pain to prefix many properties to have wider browser support. This is the main reason against using inline styles in React-based web apps. If you build for web, it is better to use stylesheets and let React take care of prefixing.

What about desktop and mobile apps, built with either React, React native or electron? In this case, it is a matter of personal preference. The majority of, or at least a big chunk, mobile apps do use inline styles as the main way to style React components. For example, React native apps use almost exclusively inline styles.

This is understandable. When you build an app, either for mobile or desktop, you are not as limited by the platform, as you are on the web. You don't have to care much about prefixes. Also, you may not need CSS pseudo-classes. Instead, you can use other JavaScript-based solution. Or, you can use some package that solves all this.

So, let's do a short summary for use of inline styles. They are good on the web for small and quick improvements, corrections and fixes. Otherwise, I would not recommend them. In mobile and desktop apps, good option for the default and main way to style React components.

## No.2: External CSS stylesheets

The second way to style React components is using external CSS stylesheets. This is one of the most popular ways to style React components, along with inline CSS styles. Especially people coming from web development like it. It is no wonder. In web development, CSS stylesheets are the main way to style websites.

What's more, many web developers have a healthy reluctance to use inline CSS styles. For many, this is considered a bad practice. Just try to tell someone you are use inline styles to style websites. Then, watch their Reaction.This could be one of the reasons [create-react-app] supports CSS stylesheets out of the box.

It is also what makes it easier for web developers to try React and start using it. Think about it. You setup new CRA (create-react-app). After that, you don't have to add or configure anything. You just create new CSS stylesheet and import it, and start writing first CSS styles. Or, you use the main stylesheet provided by CRA.

This makes developing React app simple, fast and similar to web development. So, even if you switch only temporarily, you don't have to change your workflow as much. You don't have to learn many new tricks just to get started. Instead, you can focus on the work and use your favorite CSS stylesheet to style React components.

### How to use external CSS stylesheets

As I mentioned, adding new CSS stylesheet and using it to style React components is very simple. Create new CSS stylesheet. Next, import it in your React app. If you are using create-react-app, if you use [react-scripts], that's all you have to do. Now you can start writing CSS and style React components. If not?

If you are using custom configuration you will need to add necessary plugin(s) that will allow to use CSS stylesheets. For webpack for example, you will need to add `style-loader` and `css-loader`. Next, add rules for CSS files to your webpack config that will test for `css` files and tell webpack to use `style-loader` and `css-loader` plugins.

Update your webpack config:

```
// webpack.dev.config.js

const path = require('path')

module.exports = {
  entry: './src/index.tsx',
  output: {
    path: path.resolve('dist'),
    filename: 'index_bundle.js'
  },
  module: {
    rules: [
      ///
      // ! Add rules for handling CSS files
      // with 'style-loader' and 'css-loader' plugins
      ///
      { test: /\.css$/,
        use: [
          { loader: 'style-loader' },
          { loader: 'css-loader' }
        ]
      },
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: 'babel-loader'
      },
      {
        test: /\.jsx?$/,
        exclude: /node_modules/,
        use: 'babel-loader'
      },
      {
        test: /\.ts?$/,
        exclude: /node_modules/,
        use: [{ loader: 'babel-loader' }, { loader: 'ts-loader' }]
      },
      {
        test: /\.tsx?$/,
        exclude: /node_modules/,
        use: [{ loader: 'babel-loader' }, { loader: 'ts-loader' }]
      }
    ]
  }
}
```

Import new CSS stylesheet:

```
// Import React and React DOM libraries
import * as React from 'react'
import { render } from 'react-dom'

// Import your CSS stylesheet
import './styles/styles.css'

function App() {
  return (
    <div className="App">
      <h1>Hello world!</h1>
    </div>
  )
}

// Cache root div element
const rootElement = document.getElementById('root')

// Render React app in the DOM
render(<App />, rootElement)
```

### Upsides and downsides

One potential downside is that you will spread your code base across higher number of files. Many React developers prefer to have code on one place. No external CSS stylesheets. CSS styles to style React components are in the same file as the React component. This is also why CSS-in-JS got such a traction (more about this later).

One the other hand, some developers prefer the opposite. They like to have JavaScript, or React, code separated from CSS. So, this is rather a matter of personal preference. Aside to that, I don't think there are any real downsides to using external CSS stylesheets as your main way to style React component.

### Implementation

If you use are using create-react-app or react-scripts you don't have to worry about vendor prefixes. CRA implements [autoprefixer] out of the box. You specify the target browsers through the `browserslist` key in your `package.json`. If you use custom configuration, you can again add necessary plugins for adding vendor prefixes and other tasks.

### Minifying CSS files made automatic

CRA also automatically minifies your CSS files. So, you don't have to worry about optimization of CSS files either. This makes it easier for your to focus on build your React app instead of those painful tasks related to maintenance.

Fortunately, if you are using your own custom config there are plugins that will take care of this for you. For webpack, a good plugin for CSS minification is [optimize-css-assets-webpack-plugin]. Implementing this plugin in webpack is simple.

```
// webpack.build.config.js

const OptimizeCssAssetsPlugin = require('optimize-css-assets-webpack-plugin')

...

plugins: [
  // Add to Webpack plugins OptimizeCssAssetsPlugin
  new OptimizeCssAssetsPlugin({
    assetNameRegExp: /\.optimize\.css$/g,
    cssProcessor: require('cssnano'),
    cssProcessorPluginOptions: {
      preset: ['default', { discardComments: { removeAll: true } }],
    },
    canPrint: true
  })
]
...
```

## No.3: CSS post-processors and pre-processors

So far we discussed the simplest ways to style React components with plain CSS. However, what if you want something else? What if you are used to working with other tools such as post-processors and pre-pocessors? For example, what if you want to use PostCSS or Sass?

### Using PostCSS

Unfortunately, CRA doesn't support PostCSS. If you want to add it to your React app you will have to choose from two options. First you can use some available workarounds and hacks. One Popular option is [react-app-rewired] along with [react-app-rewire-postcss]. The second option is to create your own custom webpack config and set up npm scripts.

Let's start with the first option, using `react-app-rewired`. You will need to add `react-app-rewired` and `react-app-rewire-postcss` packages to your React app. Next, you will need to create `config-overrides.js` and create override for PostCSS. You can use this file to configure PostCSS plugins. Or, you can use `postcss.config.js`.

```
// config-overrides.js

module.exports = config => {
  require('react-app-rewire-postcss')(config, {
     plugins: loader => [
      // Plugins go here
    ]
  })

  return config
};
```

The next step is to update your npm scripts in `package.json`. This means replacing `react-scripts` with `react-app-rewired`. After this, you are ready to use Less to style React components.

```
// package.json

"scripts": {
  "start": "react-app-rewired start",
  "build": "react-app-rewired build",
  "test": "react-app-rewired test --env=jsdom",
  "eject": "react-scripts eject"
}
```

Now, let's take a look at the second option, using custom configuration with webpack. First, you need to add `postcss-loader` to your project. Next, add your favorite PostCSS plugins. When you are done with that, add the `postcss-loader` to your webpack config. This will tell webpack to use PostCSS.

When you update your webpack config, remember one thing. Add the `postcss-loader` loader as the last loader for CSS files. Add it at the end of the array with loaders, after `style-loader` and `css-loader` plugins.

```
// webpack.dev.config.js

const webpack = require('webpack')
const path = require('path')

const config = {
  entry: './src/index.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        use: 'babel-loader',
        exclude: /node_modules/
      },
      {
        test: /\.css$/,
        use: [
          'style-loader',
          {
            loader: 'css-loader',
            options: {
              importLoaders: 1
            }
          },
          'postcss-loader'
        ]
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

module.exports = config
```

When you are done with updating webpack config(s) there is one more step you need to make. You need to create `.postcss.config.js` file, config for PostCSS. You then use this file to configure your PostCSS plugins. For example, you can start with adding `postcss-cssnext`, replacement for autoprefixer, and specify browsers for vendor prefixes.

```
// .postcss.config.js

module.exports = {
  plugins: {
    'postcss-cssnext': {
      browsers: [
        'Firefox >= 58',
        'Chrome >= 62',
        'ie >= 10',
        'last 4 versions',
        'Safari >= 9'
      ]
    }
  }
}
```

After you finish updating configs for webpack and PostCSS, there is one last step you have to make. You have to update npm scripts in `package.json`. Instead of using `react-scripts`, you will now use your custom webpack configs.

```
// package.json

"scripts": {
  "clean": "rm dist/bundle.js",
  "build-dev": "webpack -d --mode development",
  "build-prod": "webpack -p --mode production",
  "start": "webpack-dev-server --hot --mode development"
}
```

### Using Sass with CRA

Fortunately, implementing Sass to default CRA app is much easier than adding PostCSS. If you are using CRA v2.0 or higher, or `react-scripts` v2.0.0 or higher, you need to do only one thing. Add `node-sass` to your React app. That's all. Now, you can rename all `.css` files to `.scss` (newer Sass). You can also import new `.scss` files.

```
// Import your Sass stylesheet
import './styles/styles.scss'

function App() {
  return (
    <div className="App">
      <h1>Hello world!</h1>
    </div>
  )
}
```

### Using Sass with custom webpack config

Implementing Sass in CRA is easy. But what if you use custom configuration for your React app? Let's take a look at how to implement Sass in React app using webpack. In this case, you will need to add `sass-loader` and also the `node-sass`. After that, you will need to add rules for `.scss` files and `sass-loader` to your webpack config.

```
const webpack = require('webpack')
const path = require('path')

const config = {
  entry: './src/index.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        use: 'babel-loader',
        exclude: /node_modules/
      },
      {
        // Add rule for scss files with sass-loader
        test: /\.scss$/,
        use: [
          'style-loader',
          'css-loader',
          'sass-loader'
        ]
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

module.exports = config
```

After you update your webpack config you are ready to go, and use Sass to style React components. Well, you may also need to update npm scripts. You can use the ones you saw in the example with PostCSS.

```
// package.json

"scripts": {
  "clean": "rm dist/bundle.js",
  "build-dev": "webpack -d --mode development",
  "build-prod": "webpack -p --mode production",
  "start": "webpack-dev-server --hot --mode development"
},
```

### Using Less with overrides

Similarly to PostCSS, there is no support for Less in CRA either. So, if you like this pre-processor there are two options. First, you can use [react-app-rewired] along with [react-app-rewire-less]. Add these two packages to your React app. Then, create `config-overrides.js` and create override for Less.

```
// config-overrides.js

const rewireLess = require('react-app-rewire-less');

module.exports = function override(config, env) {
  config = rewireLess(config, env)

  return config
}
```

Next, update your npm scripts in `package.json`, i.e. replace `react-scripts` with `react-app-rewired`. With that, you are ready to go, and use Less to style React components.

```
// package.json

"scripts": {
  "start": "react-app-rewired start",
  "build": "react-app-rewired build",
  "test": "react-app-rewired test --env=jsdom",
  "eject": "react-scripts eject"
}
```

### Using Less with custom webpack config

Setting up Less with custom webpack is very similar to setting up Sass. It is almost the same. The only difference is that you will need to add  config`less-loader` instead of `sass-loader` and `less` instead of `node-sass`. Then, you will need to add rule for `.less` files to your webpack config. Remember to add `less-loader` as the last one.

```
const webpack = require('webpack')
const path = require('path')

const config = {
  entry: './src/index.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        use: 'babel-loader',
        exclude: /node_modules/
      },
      {
        // Add rule for less files with less-loader
        test: /\.less$/,
        use: [
          'style-loader',
          'css-loader',
          'less-loader'
        ]
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

module.exports = config
```

As usually, you will need to update your npm scripts, replace `react-scripts` with custom scrpits for webpack.

```
// package.json

"scripts": {
  "clean": "rm dist/bundle.js",
  "build-dev": "webpack -d --mode development",
  "build-prod": "webpack -p --mode production",
  "start": "webpack-dev-server --hot --mode development"
},
```

## Epilogue: Most Popular Ways to Style React Components

These were the first three most popular ways to style React components, inline styles, external CSS stylesheets, post-processors and pre-processors. First two require no configuration. The last one are relatively easy to implement. If you are just switching to React, these three ways to style React components are very good ways to start.

This is especially true if you have experience in web development. If you are used to working with CSS stylesheets it might be better to stick to them, at least in the beginning. This will make the transition to React easier for you. It will also give you more time and space to focus on learning about more important parts of React.

So, for now, try those three ways we discussed today and see which one you like. If you find that none of them is a good fit, don't worry. These are not the only ways to style React components. In the next part, we will discuss another three. Who knows, you might find one of these to be exactly what you are looking for. Until then, have a great day.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
<!-- [Part 2]: -->
[React native]: https://facebook.github.io/React-native/
[electron]: https://electronjs.org/
[create-react-app]: https://create-react-app.dev/
[react-scripts]: https://www.npmjs.com/package/react-scripts
[optimize-css-assets-webpack-plugin]: https://github.com/NMFR/optimize-css-assets-webpack-plugin
[react-app-rewired]: https://github.com/timarney/react-app-rewired
[react-app-rewire-postcss]: https://github.com/csstools/react-app-rewire-postcss

<!--
### Meta:
- There are many ways to style React components. In this article, we will review the first three most popular ways and how to implement each in your React app.
-->

<!--
#### Resources:
- https://blog.bitsrc.io/5-ways-to-style-React-components-in-2019-30f1ccc2b5b
- https://codeburst.io/4-four-ways-to-style-React-components-ac6f323da822
- https://css-tricks.com/css-modules-part-3-React/
- https://www.agiratech.com/5-best-way-to-style-React-components/
-->
