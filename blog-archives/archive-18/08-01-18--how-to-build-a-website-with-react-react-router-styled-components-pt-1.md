# How to Build a Website with [React], React Router & Styled-Components Pt.1

How fast can you build a simple website with react, react-router and styled-components? The question is not whether it is doable. Everything is. The real and more important question is, how hard it is? Well, it is actually very easy. You can do this in just a few minutes, even with only a very basic knowledge! In this easy tutorial we will take a look at all the steps that are necessary to do it. So, let's use the power of react, react-router and styled-component and build a simple website completely from scratch!

<!--
Table of Contents:
## Assets and prerequisites
### Installing dependencies
### Installing devDependencies
### Creating scripts and putting together package.json
### Setting up Babel
## Project structure and HTML
### A brief journey to the world of HTML
## Styled-components + React
### Setting up routes
## Closing thoughts on building a website with React, React Router & styled-components
-->

## Assets and prerequisites

As usually, there are some things we have to do before we jump right into working on our React website. First, we need to make sure we have all the prerequisites and assets in a place. Otherwise, we might run into some problems during the development phase. And, that is not the best time to solve these kinds of problems. There are more important things to do than solving some missing library or plugin. So, let's prevent this problem from happening and make the development phase smoother and faster.

### Installing dependencies

So, what assets will we need to finish this tutorial? I decided to make the setup as simple as possible, without any redundant dependencies. Let's start with dependencies. We will need four dependencies to build our React website. These dependencies are [react], [react-dom], [react-router-dom] and, the fourth one, [styled-components]. There are two options how to get these dependencies. First, we can use versions hosted on CDN. Second, we can install them locally via yarn, npm or pnpm. Let's choose the second.

```
yarn add react react-dom react-router-dom styled-components
```
or
```
npm install react react-dom react-router-dom styled-components
```
or
```
pnpm install react react-dom react-router-dom styled-components
```

### Installing devDependencies

Now, we have all dependencies we need. Make sure to install these packages as dependencies and not devDependencies. Some people may think that this is just a minor detail. However, these are the details that eventually create the whole. In other words, details matter a lot. Call me perfectionist if you want, but let's keep our `package.json` tidy. Next on the list are devDependencies. We will need again need four. These devDependencies are [babel-core], [babel-preset-env], [babel-preset-react] and [parcel-bundler].

```
yarn add --dev babel-core babel-preset-env babel-preset-react parcel-bundler
```
or
```
npm install --save-dev babel-core babel-preset-env babel-preset-react parcel-bundler
```
or
```
pnpm install --save-dev babel-core babel-preset-env babel-preset-react parcel-bundler
```

### Creating scripts and putting together package.json

With this, we have all prerequisites we need. There is one last thing we have to do before we can start building our React website. We need to create npm scripts to use Parcel to compile our website and run a server. These scripts will be very easy. This script will use command `start` and it will start our website on localhost, on port `1337`. Change the number after `-p` to use a different port. Then, we will add another one that will build our React website when we are done. This script will use command `build`.

```
{
  "scripts": {
    "build": "parcel build ./src/index.html",
    "start": "parcel ./src/index.html -p 1337"
  }
}
```

There are also some additional keys we should add, such as name, version, description, engines, keywords, main, author and maybe license. The complete version of our `package.json` file will probably look something like the example below. Now, we are ready to start.
```
{
  "name": "react-website",
  "version": "1.0.0",
  "description": "A simple website build with react.",
  "engines": {
    "node": ">=9.x",
    "npm": ">=5.x",
    "yarn": ">=1.x.x"
  },
  "keywords": [
    "react",
    "reactjs",
    "styled-components",
    "website"
  ],
  "main": "./src/index.js",
  "scripts": {
    "build": "parcel build ./src/index.html",
    "start": "parcel ./src/index.html -p 1337"
  },
  "author": "Your name",
  "license": "MIT",
  "dependencies": {
    "react": "^16.2.0",
    "react-dom": "^16.2.0",
    "react-router-dom": "^4.2.2",
    "styled-components": "^2.4.0"
  },
  "devDependencies": {
    "babel-core": "6.26.0",
    "babel-preset-env": "^1.6.1",
    "babel-preset-react": "^6.24.1",
    "parcel-bundler": "^1.4.1"
  }
}
```

_Quick note no.1: I decided to use Parcel as our bundler of choice for this project. There were two main reasons. First, using Parcel is incredibly easy. It doesn't need or require any putting together any config. This will save us some time in the beginning. Second, any other option would increase the amount of knowledge necessary to work with this tutorial. This is something I want to avoid. Anyone, or almost anyone, should be able to finish this tutorial without having to read documentation for some bundler._

_Quick note no.2: At the time of writing this tutorial, the latest version of react and react-dom was "16.2.0". For react-router-dom it was "4.2.2" and "2.4.0" for styled-components. We will use these versions. If you encounter some issues, please, make sure you are using these versions first. Sometimes, doing this solves a lot of issues and headaches. And, if  something is still not working properly, let me know and we will fix it together._

### Setting up Babel

Before we start working on this project, we need to create a config file for Babel. This file is called `.babelrc` and it will be in the root of our project, next to the files such as `package.json`. Put simply, without this config file Parcel would not work properly because it would not know how to treat our JavaScript code. Through `.babelrc` we will specify two things. First, we are working with React. And, we need to use `babel-preset-react`. Second, we want to transform our code with `babel-preset-env`.

```
{
  "presets": [
    "env",
    "react"
  ]
}
```

## Project structure and HTML

As you may have noticed when we created our scripts, the default directory for the development phase will be `src` where we will store all our files. Inside this directory we will have one directory called `app` (or website) and two files, `index.html` and `index.js`. The first mentioned, `index.html`, will be our main and also only HTML file. We will use this file to render our React website. The second one, `index.js`, will be our main file for React. Here, we will use `render` method to render our website (or app).

Inside the `app` directory will be another two directories, `components` and `pages`, and one file, `Main.js`. The first directory, `pages`, will contain the home page as well as all subpages for our website. The second directory, `components`, will contain all React components we will create and use in this project. Finally, the `Main.js` file, will contain the main "wrapper" `div` for our React website, main navigation with navigation links and routes to the home page and subpages. The structure will look like the example below.

```
react-website
├── .babelrc
├── node_modules
├── package.json
├── yarn.lock
├── src
│   └── app
│       └── components
│       └── pages
│       └── Main.js
└────── index.html
└────── index.js
```

### A brief journey to the world of HTML

The workflow for development is ready and we also know the folder structure for our React website. Now, let's create the main HTML file for our website, the `index.html`. As you can see on the structure outline above, this file will be right inside the `src` directory. And, if you remember the `start` and `build` scripts in `package.json`, we will also use this HTML file for Parcel for both, running the server during the development phase as well as building our React website in the end. So, what will be inside this file?

The `head` will contain title along with a couple of commonly used meta tags. We will also include meta tags for social media such as Facebook, Google+ and Twitter. Meta tags for Facbook and Google+ will be the same (OpenGraph). We will also add necessary link and meta tags for website's favicon. However, I will comment these out for now because I don't have any favicon to use and without it Parcel would throw an error. That is all for the `head`. The `body` will contain one `div` and one `script` element.

The `div` element will be a container where will render our React website, or app. And, the `script` element? That will load the code from our main React file, `index.js`. That's it for the `body` and also for the `index.html`. When we put all these pieces together, we will get a structure that looks like the code below.

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">

  <title>A simple website built with React</title>

  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <meta name="handheldFriendly" content="true">
  <meta name="description" content="Description for your website">
  <meta name="subject" content="Name of the website">
  <meta name="language" content="Enlish">
  <meta name="robots" content="index,follow">
  <meta name="googlebot" content="index,follow">
  <meta name="classification" content="">
  <meta name="url" content="https://www.website-url.com">
  <meta name="identifier-URL" content="https://www.website-url.com">
  <meta name="coverage" content="Worldwide">
  <meta name="rating" content="General">

  <!-- Favicons
  <link rel="apple-touch-icon" sizes="180x180" href="/images/favicon/apple-touch-icon.png">
  <link rel="icon" type="image/png" href="/images/favicon/favicon-32x32.png" sizes="32x32">
  <link rel="icon" type="image/png" href="/images/favicon/favicon-16x16.png" sizes="16x16">
  <link rel="manifest" href="/images/favicon/manifest.json">
  <link rel="mask-icon" href="/images/favicon/safari-pinned-tab.svg" color="#5bbad5">
  <link rel="shortcut icon" href="/images/favicon/favicon.ico">
  <meta name="msapplication-config" content="/images/favicon/browserconfig.xml">
  <meta name="theme-color" content="#ffffff">
  -->

  <!-- Facebook & Google+ OpenGraph tags -->
  <meta property="og:title" content="Name of the website">
  <meta property="og:type" content="website">
  <meta property="og:description" content="Description for your website">
  <meta property="og:image" content="https://www.website-url.com/images/facebook-card-image.jpg"><!-- photo -->
  <meta property="og:url" content="https://www.website-url.com">
  <meta property="og:locale" content="en_US">
  <meta property="og:site_name" content="Name of the website">
  <meta property="article:author" content="Your name">

  <!-- Twitter cards tags -->
  <meta name="twitter:card" content="summary">
  <meta name="twitter:creator" content="@username">
  <meta name="twitter:url" content="https://www.website-url.com">
  <meta name="twitter:title" content="Name of the website">
  <meta name="twitter:description" content="Description for your website">
  <meta name="twitter:image" content="https://www.website-url.com/images/twitter-summary-card-image.jpg" />

  <script type="application/ld+json">
   {
     "@context": "http://schema.org/",
     "name": "Website name",
     "url": "https://www.website-url.com",
     "logo": "https://www.website-url.com/images/website-logo.png",
     "contactPoint": {
       "@type":"ContactPoint",
       "contactType":"customer service",
       "areaServed":"Worldwide",
       "availableLanguage":"English",
       "email":"info@email.com"
     }
   }
 </script>
</head>

<body>
  <!-- Container for React -->
  <div id="app"></div>

  <script src='./index.js'></script>
</body>
</html>
```

<!-- To let's start the Parcel server by using `npm run start`. -->

## Styled-components + React

We took care about the HTML part of this project. Now, we can finally start working on the most interesting part, React, React Router and styled-components. There is no better place to start then the already mentioned `index.js` placed right inside the `src` directory. Inside this file, we start by importing three things, `React` from `react`, `ReactDOM` from `react-dom` and `BrowserRouter` from `react-router-dom`. First two are necessary if we want to work with React itself. The fourth will allow us to create routes for our website, navigate through it.

Next, we will add another import, now for `Main.js` file. We will create this file in a minute right inside the `App` directory. After that, let's save the `div` container for our React website into a `const` "container". As a next step, it is time to create our first React component. We can call this component "App". I know that we are working on a website, but it is almost a general convention to talk about React in the terms of "Apps". So, let's stick with that name even though we are building a website.

This component will be stateless because, well, we don't need to work with React `state` at this moment, and in the context of this component. Inside it will be two elements, `BrowserRouter` (we imported from `react-router-dom`) and `Main`, the `Main` nested inside the `BrowserRouter`. And, finally, we will use `ReactDOM` (we imported from `react-dom`) and its `render` method to take our small `App` component and render it inside the container `div` (the "container" `const`).

```
import React from 'react'
import ReactDOM from 'react-dom'
import { BrowserRouter } from 'react-router-dom'

import Main from './App/Main'

const container = document.querySelector('#app')

const App = () => (
  <BrowserRouter>
    <Main />
  </BrowserRouter>
)

ReactDOM.render(<App />, container)
```

### Setting up routes

Now, let's create the `Main.js` file we already mentioned above. This will be the last thing we will do today, in this first part. This file will be very important. It will contain the routes for every page as well as a `header` with navigation for our website. In the beginning of this file, we will need to import `React` from `react` again. Then, we will need to import `Route` from 'react-router-dom'. Next, we can prepare imports for pages we will create in the future, "About", "Contact", "Home" and "Portfolio". Let's commented them out for now.

Next, we will create new component that will contain the navigation with links as well as necessary routes. Unlike the previous component for `App`, this one will not be stateless. We will use JavaScript `class` to create this component. The reason for using `class` is that we can later use `state` to create a simple logic for opening and closing collapsed navigation on small screens. However, we don't need to create the `state` at this moment. Instead, let's create `render` method with `return` statement inside it.

This `return` statement will contain a single `div`. Inside this `div` will be `header` with `nav`, `ul` and a couple of `li` elements with links, one for every page. Below the `header` will be four routes, one for every page. Each `Route` will have two `props`, `path` and `component`. `path` will specify the pathname of a location, basically the URL. `component` will specify what component should be rendered when the `path` matches the pathname of a location.

So, for example, let's say we have an "About" page. In that case, we want the `path` to match "/about" (`http://www.website.com/about`) and the `component` to be `About` or `AboutPage`. Then, when the pathname of a location matches the "/about", it will render the content of `About` component, or "About" page. Let's prepare routes for Home page, About, Contact and Portfolio.

One more thing. `route` for home page will have one additional `props`, `exact` and it will be set to `˛true`. The reason is that we will use "/" to match the pathname of a location for home page. Since, "/about" and other `paths` also contain "/", router would always want to render home page as well. By using `exact`, we say that we want to match just and only "/", no other characters in the pathname of a location are allowed. That will be all for our `Main` component. Let's comment out this routes for now.

```
import React from 'react'
import { Route } from 'react-router-dom'

// import About from './pages/About'
// import Contact from './pages/Contact'
// import Home from './pages/Home'
// import Portfolio from './pages/Portfolio'

export default class Main extends React.Component {
  render () {
    return (
      <div className="wrapper">
        <header>
          <nav>
            <ul>
              <li>
                <a href="/">Home</a>
              </li>

              <li>
                <a href="/about">About</a>
              </li>

              <li>
                <a href="/portfolio">Portfolio</a>
              </li>

              <li>
                <a href="/contact">Contact</a>
              </li>
            </ul>
          </nav>
        </header>

        {/* <Route exact={true} path="/" component={Home}/> */}
        {/* <Route path="/about" component={About}/> */}
        {/* <Route path="/contact" component={Contact}/> */}
        {/* <Route path="/portfolio" component={Portfolio}/> */}
      </div>
    )
  }
}
```

## Closing thoughts on building a website with React, React Router & styled-components

This is all for the first part of this tutorial on how to build a website with React, React Router and styled-components. I hope you enjoyed this article, even though we mostly worked on the workflow and setup for development and touched React only at the very end. The upside of taking care about this maybe less interesting work is that we can focus solely on React in the next part. So, for now, brush up your knowledge of React and get ready for the second part of this tutorial. It will be a wild ride!

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[react]: https://www.npmjs.com/package/react
[react-dom]: https://www.npmjs.com/package/react-dom
[react-router-dom]: https://www.npmjs.com/package/react-router
[styled-components]: https://www.npmjs.com/package/styled-components
[babel-core]: https://www.npmjs.com/package/babel-core
[babel-preset-env]: https://www.npmjs.com/package/babel-preset-env
[babel-preset-react]: https://www.npmjs.com/package/babel-preset-react
[parcel-bundler]: https://www.npmjs.com/package/parcel-bundler

<!-- ### Inspiration
-
 -->
