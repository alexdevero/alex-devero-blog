# How to Build a Simple Website with [GatsbyJS] & PostCSS Pt.1

GatsbyJS is one of the most popular static website generators. This mini series will teach you all you need to use GatsbyJS to build your own website. We will start with a short info and what makes GatsbyJS a good choice. Next, we will install required dependencies and create GatsbyJS config. Finally, we will create a couple of simple components.

<!--
Table of Contents:
## What is GatsbyJS?
## Why GastbyJS?
## Project outline
## Getting started
## Configuring GatsbyJS-One config to rule them all
## Creating the layout
## Building a simple header component
## Building a simple footer component
## Epilogue: How to Build a Simple Website with GatsbyJS & PostCSS Pt.1
-->

## What is GatsbyJS?

First things first. What is GatsbyJS? The short version is that GatsbyJS is a static site generator. The longer version is that GatsbyJS is a static site generator on steroids, something very close to a Swiss Army knife. It is basically a ready-to-use complex solution you can use for building fast and optimized websites of any kind.

## Why GastbyJS?

The main benefit of GatsbyJS is that it is a complex solution. It comes packed with everything you need. This makes it incredibly to get started.  From this point of view, GatsbyJS is more than just a static site generator. It is more like a framework. Let's take a look at some concrete benefits so you know what can you expect.

First, GatsbyJS comes with both, ready-to-use front-end as well as back-end. There is basically no need to build or hack anything on your own. You can take it and use it right out of the box. Second, it is all written in JavaScript as a single programming language. GatsbyJS uses [React] component as a view layer on the front-end and [GraphQL] on the back-end.

This allows you to query and fetch data from anywhere. You no longer have to have all your data stored in local static Markdown files, or something similar. You can store your data on any database or storage you want. Then, you can leverage GraphQL to retrieve it and render as you wish. Third, it has great and thorough documentation with guides and recipes.

Then, there is also a very rich system of plugins that is constantly growing. If you like something and want to continue using it, chances are there is a plugin for it. For example, if you are moving from WordPress, there are [plugins] you can choose from and use. And, if you can't find what you are looking for, or hit some roadblock, there is also a large community of passionate developers and evangelists you can reach to for help.

Fourth, GatsbyJS comes with code and data splitting out-of-the-box. There is no one big package of code that takes eternity to load. Instead, you will get your code optimized and split into multiple files. This allows you to load first your critical HTML and CSS. When this is loaded, it prefetches resources for other pages. The result is that browsing your website feels, and is, so fast.

Fifth, when you build your website, you will end up with static files you can then easily deploy, using your favorite service. Almost as simple and easy as drag and drop. Sixth, minimum configuration. GatsbyJS requires only one config to get your website up and running. This is enough for the benefits. As you can see GatsbyJS is really great. Now, let's start building.

## Project outline

Before we begin, let's take a quick look at the outline of this project. The outline below is what you will have when we finish this first part. Keep in mind that `.cache` and `public` directories are generated automatically, by GatsbyJS. We will directly work only with the content of `src`, and `gatsby-config.js` and `package.json`. The rest will come in part 2.

```
gatsbyjs-website
├── .cache/
├── node_modules/
├── public/
├── src/
│   └── components/
│       └── footer.js
│       └── header.js
│       └── layout.js
│   └── images/
│   └── pages/
│   └── styles/
│       └── footer.css
│       └── header.css
├── gatsby-config.js
└── package.json
```

## Getting started

It is time to move from theory to practice. First, before you can start building your website with GatsbyJS, you will need to install few dependencies. There are some dependencies that are good to include in your project and skipping them is not a good idea. These are `gatsby`, `gatsby-plugin-manifest`, `gatsby-plugin-offline`, `gatsby-plugin-sharp`, `gatsby-source-filesystem`, `gatsby-transformer-sharp`, `react`, `react-dom` and `react-helmet`.

Aside to these, there are also there less or more "optional", namely `gatsby-plugin-react-helmet`, `gatsby-image` and `react-helmet`. `gatsby-image` is for optimizing image assets. `gatsby-plugin-react-helmet` and `react-helmet` adds support for customizing the content of the document head. It allows you to add additional title, metadata, stylesheets, scripts and so on.

Finally, since this tutorial will use PostCSS for processing CSS you will also need `gatsby-plugin-postcss`. This is all. After this, it is up to you to add additional PostCSS, or GatsbyJS, plugins you want to use. My favorite PostCSS plugins, I like to use on all projects, are `cssnano`, `postcss-extend`, `postcss-import`, `postcss-merge-rules`, `postcss-nesting`, `postcss-preset-env` and `postcss-pxtorem`.

Considering you want to use all the dependencies the final `package.json` will look something similar to the example below. The last step is adding npm scripts, at least `start` and `build`. These scripts use `gatsby develop` and `gatsby build` commands. With that, you can install all the dependencies with npm, yarn or any other package packager of your choice.

```
// package.json

{
  "name": "gatsbyjs-website",
  "description": "Your website built with GatsbyJS.",
  "version": "1.0.0",
  "author": "Your name",
  "license": "MIT",
  "keywords": [
    "gatsbyjs",
    "javascript",
    "postcss",
    "react",
    "reactjs",
    "website"
  ],
  "scripts": {
    "build": "gatsby build",
    "start": "gatsby develop"
  },
  "repository": {
    "type": "git",
    "url": "https://example.com"
  },
  "bugs": "https://example.com/bugs",
  "contributors": [],
  "dependencies": {
    "gatsby": "^2.0.50",
    "gatsby-image": "^2.0.20",
    "gatsby-plugin-manifest": "^2.0.9",
    "gatsby-plugin-offline": "^2.0.15",
    "gatsby-plugin-postcss": "^2.0.1",
    "gatsby-plugin-react-helmet": "^3.0.2",
    "gatsby-plugin-sharp": "^2.0.12",
    "gatsby-source-filesystem": "^2.0.8",
    "gatsby-transformer-sharp": "^2.1.8",
    "react": "^16.6.3",
    "react-dom": "^16.6.3",
    "react-helmet": "^5.2.0"
  },
  "devDependencies": {
    "cssnano": "^4.1.7",
    "postcss-extend": "^1.0.5",
    "postcss-import": "^12.0.1",
    "postcss-merge-rules": "^4.0.2",
    "postcss-nesting": "^7.0.0",
    "postcss-preset-env": "^6.4.0",
    "postcss-pxtorem": "^4.0.1"
  }
}
```

## Configuring GatsbyJS&ndash;One config to rule them all

Next on the line is config for GatsbyJS. This config is for setting some useful things such as website metadata, plugins, pollyfils and so on. We will use the first two to set the title for the website and configure plugins. The snippet below contains some comments for clarification. You can find more information about the config in [config API docs].

```
// gatsby-config.js

module.exports = {
  siteMetadata: {
    title: 'Your website built with Gatsby' // Set the title for the website
  },
  plugins: [
    'gatsby-plugin-react-helmet', // Implements Helmet plugin
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `images`,
        path: `${__dirname}/src/images` // path to dir with image assets
      }
    },
    {
      resolve: `gatsby-plugin-postcss`, // Implements PostCSS
      options: {
        postCssPlugins: [
          require('postcss-import')(), // Add support for sass-like '@import'
          require('postcss-extend')(), // Add support for sass-like '@extend'
          require('postcss-nesting')(), // Add support for sass-like nesting of rules
          require('postcss-pxtorem')({
            mediaQuery: false, // Ignore media queries
            minPixelValue: 0, // Minimal pixel value that will be processed
            propList: [], // List of CSS properties that can be changed from px to rem; empty array means that all CSS properties can change from px to rem
            replace: true, // Replace pixels with rems
            rootValue: 16, // Root font-size
            selectorBlackList: ['html'], // Ignore pixels used for html
            unitPrecision: 4 // Round rem units to 4 digits
          }),
          require('postcss-preset-env`)({
            stage: 3 // More info about stages: https://cssdb.org/#staging-process
          })
          require('cssnano')() // Minify CSS
        ]
      }
    },
    'gatsby-transformer-sharp', // Allows to process your images - resize, crop and create responsive images
    'gatsby-plugin-sharp', // Adds several image processing functions
    {
      resolve: `gatsby-plugin-manifest`, // Generates manifest.webmanifest to make your website a progressive web app
      options: {
        name: 'gatsby-starter-default',
        short_name: 'starter',
        start_url: '/',
        background_color: '#663399',
        theme_color: '#663399',
        display: 'minimal-ui',
        icon: 'src/images/website-icon.png' // This path is relative to the root of the site.
      }
    }
    // this (optional) plugin enables Progressive Web App + Offline functionality
    // To learn more, visit: https://gatsby.app/offline
    // 'gatsby-plugin-offline'
  ]
}
```

Aside to the main config, there are also three additional configs-browser, node and ssr. All these configs are optional and you don't have to use them or even create them. Meaning, your website will work like a charm without them. If you want to learn more about these configs and how to use them, the best place to take a look at are [official docs].

## Creating the layout

Now, it is time to build the first component. This component will be called "Layout". You will use this component as the main wrapper for the content of your website, content of the `body` HTML element. It will also implement `graphql` and `helmet` plugins. This will ensure your website has correct metadata and also all addition external resources.

Keep in mind that we will use this component as a main wrapper. If you want to add any additional resources, such as stylesheets, you want to use everywhere this is the best place where to put them. You insert them into `Helmet` component. We will add stylesheet for [Font Awesome] icon font. This will give us a variety of good-looking icons we can then use.

It is also this component where you will import components for header and footer. Since all pages will be wrapped inside this, layout, component as its children, footer and header will be rendered on all pages. To keep the layout simple, let's add one additional "page-content" `div` and one "container" `div` with React `children` element.

```
// src/components/layout.js

// Import dependencies
import React from 'react'
import PropTypes from 'prop-types'
import Helmet from 'react-helmet'
import { StaticQuery, graphql } from 'gatsby'

// Import Footer component
import Footer from './footer'

// Import Header component
import Header from './header'

import '../styles/styles.css'

// Layout component
const Layout = ({ children }) => (
  <StaticQuery
    query={graphql`
      query SiteTitleQuery {
        site {
          siteMetadata {
            title
          }
        }
      }
    `}
    render={data => (
      <>
        <Helmet
          title={data.site.siteMetadata.title}
          meta={[
            { name: 'description', content: 'Your website built with GatsbyJS.' }
          ]}
        >
          <html lang="en" />

          <!-- Font Awesome stylesheet for icons -->
          <link
            rel="stylesheet"
            href="https://use.fontawesome.com/releases/v5.5.0/css/all.css"
            integrity="sha384-B4dIYHKNBt8Bc12p+WXckhzcICo0wtJAoU8YZTY5qE0Id1GSseTk6S+L3BlXeVIU"
            crossorigin="anonymous"
          />
        </Helmet>

        <div className="page-wrapper">
          <Header siteTitle={data.site.siteMetadata.title} />

          <div className="page-content">
            <div className="container">{children}</div>
          </div>

          <Footer />
        </div>
      </>
    )}
  />
)

Layout.propTypes = {
  children: PropTypes.node.isRequired
}

export default Layout
```

## Building a simple header component

Every website that contains more than one page should have navigation. So, let's build a simple Header component. This component will contain `nav` element with two unordered lists. First list will contain three inbound links to About me, Portfolio and Blog. The second list will contain four links to profiles on social media.

We can link to Facebook, Twitter, Instagram and Linkedin. The first list will be aligned on the left side of the navigation while the second on the right side. Since we are talking about social media ... We will use icons provided by Font Awesome.

```
// src/components/header.js

// Import dependencies
import React from 'react'
import { Link } from 'gatsby'

// Header component
const Header = () => (
  <header className="header">
    <div className="container">
      <nav className="nav">
        <ul className="header__list-links">
          <li>
            <Link to="/about-me/">About me</Link>
          </li>

          <li>
            <Link to="/portfolio">Portfolio</Link>
          </li>

          <li>
            <Link to="/blog">Blog</Link>
          </li>
        </ul>

        <ul className="header__list-social">
          <li>
            <a href="/" target="_blank">
              <span className="fab fa-facebook-f" rel="noopener noreferrer" target="_blank" />
            </a>
          </li>

          <li>
            <a href="/" target="_blank">
              <span className="fab fa-twitter" rel="noopener noreferrer" target="_blank" />
            </a>
          </li>

          <li>
            <a href="/" target="_blank">
              <span className="fab fa-instagram" rel="noopener noreferrer" target="_blank" />
            </a>
          </li>

          <li>
            <a href="/" target="_blank">
              <span className="fab fa-linkedin" rel="noopener noreferrer" target="_blank" />
            </a>
          </li>
        </ul>
      </nav>
    </div>
  </header>
)

export default Header
```

Now, when we are done with the component, let's add some simple styling to make the header look good. We can make the header black, with white links and icons. Then, we can change the background of the links and color of icons on `:hover`, both with smooth transition. This will be just enough to do the job, at least for now.

```
// src/styles/_header.css

header {
  width: 100%;
  background: #333;
}

.nav,
.header ul {
  display: flex;
  flex-flow: row wrap;
}

.nav {
  align-items: center;
  justify-content: space-between;
}

.header ul {
  padding: 0;
  margin: 0;
  list-style-type: none;
}

.header__list-social {
  align-items: center;
}

.header__list-social li + li {
  margin-left: 18px;
}

.header a {
  display: block;
  text-decoration: none;
  color: #fff;
}

.header__list-links a {
  padding: 18px 14px;
  transition: background-color .25s ease-in-out;
}

.header__list-links a:hover {
  background-color: #e74c3c;
}

.header__list-social a {
  transition: color .25s ease-in-out;
}

.header__list-social a:hover {
  color: #e74c3c;
}

.header__list-social .fab {
  font-size: 22px;
}

.header__list-social .fa-facebook-f {
  font-size: 18px;
}
```

## Building a simple footer component

Next, let's build the footer component. It will follow the simplicity of `Header` component. It will again contain two lists, one for links and one for social media profiles. Now, both lists will be in centered. List with links will be first and list social media will be below it. Nothing complex, let's keep it simple.

```
// Imports
import React from 'react'
import { Link } from 'gatsby'

// Footer component
const Footer = () => (
  <footer className="footer">
    <div className="container">
      <ul className="footer__list-links">
        <li>
          <Link to="/about-me/">About me</Link>
        </li>

        <li>
          <Link to="/portfolio">Portfolio</Link>
        </li>

        <li>
          <Link to="/blog">Blog</Link>
        </li>
      </ul>

      <ul className="footer__list-social">
        <li>
          <a href="/" rel="noopener noreferrer" target="_blank">
            <span className="fab fa-facebook-f" />
          </a>
        </li>

        <li>
          <a href="/" rel="noopener noreferrer" target="_blank">
            <span className="fab fa-twitter" />
          </a>
        </li>

        <li>
          <a href="/" rel="noopener noreferrer" target="_blank">
            <span className="fab fa-instagram" />
          </a>
        </li>

        <li>
          <a href="/" rel="noopener noreferrer" target="_blank">
            <span className="fab fa-linkedin" />
          </a>
        </li>
      </ul>
    </div>
  </footer>
)

export default Footer
```

Just like with header, we should add some styles also for elements inside footer. Let's make the footer more eye-popping. Say, orange, with white links and icons. For `:hover`, we will change the color of links and icons to darker shade of orange, again with smooth transition.

```
footer {
  padding-top: 32px;
  padding-bottom: 32px;
  width: 100%;
  background: #e74c3c;
}

.footer__list-links,
.footer__list-social {
  display: flex;
  flex-flow: row wrap;
  align-items: center;
  justify-content: center;
  padding: 0;
  margin: 0;
  list-style-type: none;
}

.footer__list-links li + li,
.footer__list-social li + li {
  margin-left: 21px;
}

.footer__list-social {
  margin-top: 32px;
}

.footer__list-social .fab {
  font-size: 28px;
}

.footer__list-social .fa-facebook-f {
  font-size: 23px;
}

.footer a {
  text-decoration: none;
  color: #fff;
  transition: color .25s ease-in-out;
}

.footer a:hover {
  color: #c0392b;
}
```

## Epilogue: How to Build a Simple Website with GatsbyJS & PostCSS Pt.1

This is all we will do today. I hope you had fun and learned a lot. Let's do a quick recap. We started with a brief introduction to GatsbyJS, especially its benefits. Next, we installed required dependencies. Then, we created a simple GatsbyJS config. And, when we finished this work, we created three simple components for your website-layout, header and footer.

In case of header and footer, we also added some basic styling to make these components look good. This is where we finished the work for this, first, part. What is coming in the second part? We will start with PostCSS and adding some global styles. We will also implement a simple grid that will help us create a structure the layout.

After that, we will dive into the best part of this tutorial-build all pages for your website. This means creating a homepage, about page, portfolio, blog and also 404. When we finish this, you will have a great fully working starting template you can use for your website, and other future projects. With that, I look forward to seeing you here again the next week. Until then, have a great day!

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[React]: https://reactjs.org
[GraphQL]: https://graphql.org/learn/
[plugins]: https://www.gatsbyjs.org/plugins/?=wordpress
[config API docs]: https://www.gatsbyjs.org/docs/gatsby-config/
[official docs]: https://www.gatsbyjs.org/docs/
[Font Awesome]: https://fontawesome.com

<!--
#### Meta:
-
-->
