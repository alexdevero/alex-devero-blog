# Build a Simple Website with [GatsbyJS] and PostCSS Pt.1

Building a website with GatsbyJS is incredibly simple. This tutorial will teach you how to use this static website generator to build your own website. You will learn about creating and linking pages, handling 404, managing static files and more. Learn what you need to know about GatsbyJS and build your own website. It is easier than you think.

<!--
Table of Contents:
## Project outline
## Adding default styles
## Adding a simple grid
## Everything starts with index
## Pages and links
## Creating additional pages
## What if ... 404
## Contact page and static files
## Epilogue: How to Build a Simple Website with GatsbyJS & PostCSS Pt.2
-->

How to Build a Simple Website with GatsbyJS & PostCSS [Part 2].

## Project outline

Before we begin, let's again take a quick look at the outline for this tutorial. The outline below is what you get when you finish this second part, and also use the code from the part 1. Jut to remind you, the `.cache` and `public` directories are generated by GatsbyJS. They are not created by you.

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
│       └── gatsby-icon.png
│   └── pages/
│       └── 404.js
│       └── about-me.js
│       └── contact.js
│       └── index.js
│   └── styles/
│       └── _base.css
│       └── _footer.css
│       └── _grid.css
│       └── _header.css
│       └── styles.css
├── static
│       └── sendEmail.php
├── gatsby-config.js
└── package.json
```

## Adding default styles

Let's start with something easier, such as PostCSS and adding some basic styles to make your GatsbyJS website nicer. These styles will be mostly resets applied to `html`, `body` and general elements you will see in this tutorial. This will help ensure browsers will render your website as you want. So, let's create a new stylesheet in `src/styles`. It can be called `_base.css`.

```
/* src/styles/_base.css */

html {
	box-sizing: border-box;
  font-size: 16px;
  line-height: 1.15;
	-webkit-text-size-adjust: 100%;
}

*,
*::before,
*::after {
	box-sizing: inherit;
}

:root {
	-moz-tab-size: 4;
	tab-size: 4;
}

body {
  margin: 0;
  font: 1rem / 1.616 georgia, serif;
  -moz-font-feature-settings: 'kern', 'liga', 'clig', 'calt';
  -ms-font-feature-settings: 'kern', 'liga', 'clig', 'calt';
  -webkit-font-feature-settings: 'kern', 'liga', 'clig', 'calt';
  font-feature-settings: 'kern', 'liga', 'clig', 'calt';
  font-kerning: normal;
  font-weight: 400;
  word-wrap: break-word;
  color: hsla(0, 0%, 0%, .8);
}

b,
strong {
	font-weight: bolder;
}

button,
input,
textarea {
	font-family: inherit;
	font-size: 100%;
	line-height: 1.15;
	margin: 0;
}

button,
select {
	text-transform: none;
}

button,
[type='button'],
[type='submit'] {
	-webkit-appearance: button;
}

button::-moz-focus-inner,
[type='button']::-moz-focus-inner,
[type='submit']::-moz-focus-inner {
	border-style: none;
	padding: 0;
}

button:-moz-focusring,
[type='button']:-moz-focusring,
[type='submit']:-moz-focusring {
	outline: 1px dotted ButtonText;
}

fieldset {
	padding: 0;
  border: 0;
}

.page-wrapper {
  display: flex;
  flex-flow: column wrap;
  min-height: 100vh;
}

.page-content {
  flex: 1; /* Make sure footer is always on the bottom. */
}
```

These styles are the bare minimum. However, it is still a good starting point for building your website with GatsbyJS. Next, still in the `src/styles` directory, let's create another file called `styles.css`. We will use this file as the main point for PostCSS and for importing all other stylesheets you will create.

Now, you can add imports for `_base.css` stylesheet. You can also add imports for stylesheets you created for `Footer` and `Header` components in the [previous part]. Finally, let's also add one more import. This will be a import for stylesheet with grid you will create next.

```
/* src/styles/styles.css */

/* Import base styles */
@import '_base.css';

/* Import grid */
@import '_grid.css';

/* Import components */
@import '_header.css';
@import '_footer.css';
```

## Adding a simple grid

When it comes to grid, we don't need anything overly complex. So, for the sake of simplicity, let's just take the grid from [Bootstrap 4] framework and customize it a little bit. Meaning, we can remove all CSS helper classes and leave just classes for grid. That will be just enough to build a simple website powered by GatsbyJS.

```
/* src/styles/_grid.css */

.container {
  margin: auto;
  width: 100%;
  padding-right: 15px;
  padding-left: 15px;
}

@media (min-width: 576px) {
  .container {
    max-width: 540px;
  }
}

@media (min-width: 768px) {
  .container {
    max-width: 720px;
  }
}

@media (min-width: 992px) {
  .container {
    max-width: 960px;
  }
}

@media (min-width: 1200px) {
  .container {
    max-width: 1140px;
  }
}

.container-fluid {
  width: 100%;
  padding-right: 15px;
  padding-left: 15px;
}

.row {
  display: flex;
  flex-wrap: wrap;
  margin-right: -15px;
  margin-left: -15px;
}

.col-1,
.col-2,
.col-3,
.col-4,
.col-5,
.col-6,
.col-7,
.col-8,
.col-9,
.col-10,
.col-11,
.col-12,
.col,
.col-sm-1,
.col-sm-2,
.col-sm-3,
.col-sm-4,
.col-sm-5,
.col-sm-6,
.col-sm-7,
.col-sm-8,
.col-sm-9,
.col-sm-10,
.col-sm-11,
.col-sm-12,
.col-sm,
.col-md-1,
.col-md-2,
.col-md-3,
.col-md-4,
.col-md-5,
.col-md-6,
.col-md-7,
.col-md-8,
.col-md-9,
.col-md-10,
.col-md-11,
.col-md-12,
.col-md,
.col-lg-1,
.col-lg-2,
.col-lg-3,
.col-lg-4,
.col-lg-5,
.col-lg-6,
.col-lg-7,
.col-lg-8,
.col-lg-9,
.col-lg-10,
.col-lg-11,
.col-lg-12,
.col-lg,
.col-xl-1,
.col-xl-2,
.col-xl-3,
.col-xl-4,
.col-xl-5,
.col-xl-6,
.col-xl-7,
.col-xl-8,
.col-xl-9,
.col-xl-10,
.col-xl-11,
.col-xl-12,
.col-xl {
  position: relative;
  width: 100%;
  min-height: 1px;
  padding-right: 15px;
  padding-left: 15px;
}

.col {
  flex-basis: 0;
  flex-grow: 1;
  max-width: 100%;
}

.col-1 {
  flex: 0 0 8.333333%;
  max-width: 8.333333%;
}

.col-2 {
  flex: 0 0 16.666667%;
  max-width: 16.666667%;
}

.col-3 {
  flex: 0 0 25%;
  max-width: 25%;
}

.col-4 {
  flex: 0 0 33.333333%;
  max-width: 33.333333%;
}

.col-5 {
  flex: 0 0 41.666667%;
  max-width: 41.666667%;
}

.col-6 {
  flex: 0 0 50%;
  max-width: 50%;
}

.col-7 {
  flex: 0 0 58.333333%;
  max-width: 58.333333%;
}

.col-8 {
  flex: 0 0 66.666667%;
  max-width: 66.666667%;
}

.col-9 {
  flex: 0 0 75%;
  max-width: 75%;
}

.col-10 {
  flex: 0 0 83.333333%;
  max-width: 83.333333%;
}

.col-11 {
  flex: 0 0 91.666667%;
  max-width: 91.666667%;
}

.col-12 {
  flex: 0 0 100%;
  max-width: 100%;
}

@media (min-width: 576px) {
  .col-sm {
    flex-basis: 0;
    flex-grow: 1;
    max-width: 100%;
  }

  .col-sm-1 {
    flex: 0 0 8.333333%;
    max-width: 8.333333%;
  }

  .col-sm-2 {
    flex: 0 0 16.666667%;
    max-width: 16.666667%;
  }

  .col-sm-3 {
    flex: 0 0 25%;
    max-width: 25%;
  }

  .col-sm-4 {
    flex: 0 0 33.333333%;
    max-width: 33.333333%;
  }

  .col-sm-5 {
    flex: 0 0 41.666667%;
    max-width: 41.666667%;
  }

  .col-sm-6 {
    flex: 0 0 50%;
    max-width: 50%;
  }

  .col-sm-7 {
    flex: 0 0 58.333333%;
    max-width: 58.333333%;
  }

  .col-sm-8 {
    flex: 0 0 66.666667%;
    max-width: 66.666667%;
  }

  .col-sm-9 {
    flex: 0 0 75%;
    max-width: 75%;
  }

  .col-sm-10 {
    flex: 0 0 83.333333%;
    max-width: 83.333333%;
  }

  .col-sm-11 {
    flex: 0 0 91.666667%;
    max-width: 91.666667%;
  }

  .col-sm-12 {
    flex: 0 0 100%;
    max-width: 100%;
  }
}

@media (min-width: 768px) {
  .col-md {
    flex-basis: 0;
    flex-grow: 1;
    max-width: 100%;
  }

  .col-md-1 {
    flex: 0 0 8.333333%;
    max-width: 8.333333%;
  }

  .col-md-2 {
    flex: 0 0 16.666667%;
    max-width: 16.666667%;
  }

  .col-md-3 {
    flex: 0 0 25%;
    max-width: 25%;
  }

  .col-md-4 {
    flex: 0 0 33.333333%;
    max-width: 33.333333%;
  }

  .col-md-5 {
    flex: 0 0 41.666667%;
    max-width: 41.666667%;
  }

  .col-md-6 {
    flex: 0 0 50%;
    max-width: 50%;
  }

  .col-md-7 {
    flex: 0 0 58.333333%;
    max-width: 58.333333%;
  }

  .col-md-8 {
    flex: 0 0 66.666667%;
    max-width: 66.666667%;
  }

  .col-md-9 {
    flex: 0 0 75%;
    max-width: 75%;
  }

  .col-md-10 {
    flex: 0 0 83.333333%;
    max-width: 83.333333%;
  }

  .col-md-11 {
    flex: 0 0 91.666667%;
    max-width: 91.666667%;
  }

  .col-md-12 {
    flex: 0 0 100%;
    max-width: 100%;
  }
}

@media (min-width: 992px) {
  .col-lg {
    flex-basis: 0;
    flex-grow: 1;
    max-width: 100%;
  }

  .col-lg-1 {
    flex: 0 0 8.333333%;
    max-width: 8.333333%;
  }

  .col-lg-2 {
    flex: 0 0 16.666667%;
    max-width: 16.666667%;
  }

  .col-lg-3 {
    flex: 0 0 25%;
    max-width: 25%;
  }

  .col-lg-4 {
    flex: 0 0 33.333333%;
    max-width: 33.333333%;
  }

  .col-lg-5 {
    flex: 0 0 41.666667%;
    max-width: 41.666667%;
  }

  .col-lg-6 {
    flex: 0 0 50%;
    max-width: 50%;
  }

  .col-lg-7 {
    flex: 0 0 58.333333%;
    max-width: 58.333333%;
  }

  .col-lg-8 {
    flex: 0 0 66.666667%;
    max-width: 66.666667%;
  }

  .col-lg-9 {
    flex: 0 0 75%;
    max-width: 75%;
  }

  .col-lg-10 {
    flex: 0 0 83.333333%;
    max-width: 83.333333%;
  }

  .col-lg-11 {
    flex: 0 0 91.666667%;
    max-width: 91.666667%;
  }

  .col-lg-12 {
    flex: 0 0 100%;
    max-width: 100%;
  }
}

@media (min-width: 1200px) {
  .col-xl {
    flex-basis: 0;
    flex-grow: 1;
    max-width: 100%;
  }

  .col-xl-1 {
    flex: 0 0 8.333333%;
    max-width: 8.333333%;
  }

  .col-xl-2 {
    flex: 0 0 16.666667%;
    max-width: 16.666667%;
  }

  .col-xl-3 {
    flex: 0 0 25%;
    max-width: 25%;
  }

  .col-xl-4 {
    flex: 0 0 33.333333%;
    max-width: 33.333333%;
  }

  .col-xl-5 {
    flex: 0 0 41.666667%;
    max-width: 41.666667%;
  }

  .col-xl-6 {
    flex: 0 0 50%;
    max-width: 50%;
  }

  .col-xl-7 {
    flex: 0 0 58.333333%;
    max-width: 58.333333%;
  }

  .col-xl-8 {
    flex: 0 0 66.666667%;
    max-width: 66.666667%;
  }

  .col-xl-9 {
    flex: 0 0 75%;
    max-width: 75%;
  }

  .col-xl-10 {
    flex: 0 0 83.333333%;
    max-width: 83.333333%;
  }

  .col-xl-11 {
    flex: 0 0 91.666667%;
    max-width: 91.666667%;
  }

  .col-xl-12 {
    flex: 0 0 100%;
    max-width: 100%;
  }
}
```

## Everything starts with index

it is time to taste the simplicity GatsbyJS as to offer. Let's create your first page. This will be the homepage for your website powered by GatsbyJS. Navigate into the `src` directory and create new folder called `pages`. Inside this folder create new file called `index.js`. Now, you can open this file and add some content.

The first thing to do is to add import for `React` library. Next, let's also add import for the `layout` component from `src/components/`, you also created in the [previous part]. As we discussed, we will use the `layout` component as the main container for the content. Finally, we will need to export the component for homepage. And, that's all we have to do.

```
// src/pages/index.js

// Imports
import React from 'react'

// Import layout component
import Layout from '../components/layout'

// Component for homepage
const IndexPage = () => (
  <Layout>
    <h1>Hello world!</h1>

    <p>This is your website build with GatsbyJS. You have everything you need to get started. Now, it is your turn to take this website and make it awesome!</p>
  </Layout>
)

export default IndexPage
```

No, this is not a joke. This is really all you have to do to create a new page with GatsbyJS. When you want to create new page, you create a new file in `page` directory, filename being the URL for the page. Here, you will create new component for your page. Then, you export that component. You don't need to create a route for that page or import it anywhere. GatsbyJS will do all this for you automatically. This is how you create all pages for your website.

_Important note 1: It doesn't matter how you name your page component. In the example above, we called the component `IndexPage`. However, we could as well use `FooBar`, `LoremIpsum` or `YetAnotherPage`. The result will be always the same, as long as you export the component. The only thing that matters for GatsbyJS is the name of the file, or `index.js` for homepage and `some-name.js` for any other page._

_Important note 2: There is another way to create new pages with GatsbyJS. You can also create a folder with a specific name and then create `index.js` there. For example, let's say you want to create "About me" page. Then, you create `about-me` folder with `index.js` inside it. GatsbyJS will correctly render the `index.js` as "About me" page._

Creating pages using filenames:

```
│   └── pages/
│       └── index.js // this is homepage ("/")
│       └── about-me.js // this is About me page ("/about-me/")
│       └── portfolio.js // this is Portfolio page ("/portfolio/")
```

Creating pages using folders:

```
│   └── pages/
│       └── about-me/
│           └── index.js // this is About me page ("/about-me/")
│       └── portfolio/
│           └── index.js // this is Portfolio page ("/portfolio/")
│       └── index.js // this is homepage ("/")
```

## Pages and links

Okay, but what if you want to connect some of your pages? For example, you may want to link from one page to another. With GatsbyJS, this is very easy and fast as well. When you want to link to your new page, you use the name of the file, where you exported the component for that page, as the URL for link. GatsbyJS will do the rest.

As you may remember, this is what you already done in the [previous part], when you build components for header and footer. There, you used `Link` module imported from `gatsby` and passed the page filename to `to` prop. In case of homepage it would be `to="/"`. What if you have an About page and file called `about-me.js`? Then, it will be `to="/about-me/"`.

Let's take a look at the `Header` component again so you can see it. And, since we are there, we can also add a link to homepage. This is one thing we previously forgot. And, since it is good to give people come way to go back to homepage let's fix it now.

```
// Imports
import React from 'react'

// Import 'Link' module from GatsbyJS
import { Link } from 'gatsby'

// Header component
const Header = () => (
  <header className="header">
    <div className="container">
      <nav className="nav">
        <ul className="header__list-links">
          <li>
            {/* file: index.js */}
            <Link to="/">Home</Link>
          </li>

          <li>
            {/* file: about-me.js */}
            <Link to="/about-me/">About me</Link>
          </li>

          <li>
            {/* file: portfolio.js */}
            <Link to="/portfolio/">Portfolio</Link>
          </li>

          <li>
            {/* file: blog.js */}
            <Link to="/blog/">Blog</Link>
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

## Creating additional pages

Now, you know how to add new pages. You also how to use `Link` module provided by GatsbyJS to connect them. Knowing this, you can know create any page you want, using one of those approaches we discussed. For example, let's say you want to create "About me" page. First, in `pages` directory, you create a new file. It can be called `about-me.js` or `about.js`. Choose any name you want. Just remember that the filename will then work as a URL.

Second, inside this file you create a new component for your page. You create a layout using the grid you created and populate the component with some content. Then, you export the component. As we discussed, it doesn't matter what is the name of the component. Just make sure to export it. GatsbyJS will then use that export with the filename and wire the page correctly.

This was the first way. The second way is using `index.js` and "unique" folder. It is almost like turning the first approach upside down. Again you must go to `pages` folder. Here, you create a new folder using the name you want to use as a URL. Following the first way, the folder name can be `about-me` or `about`. Inside this folder, you create new file called `index.js`.

From here, the procedure is the same as the one you followed the first way. You create component for your About me page, with some name of your choice, and export it. Then, you can navigate to that page, again using the folder name as the URL. So, if you used `about-me` as the name of the file/folder, the URL will be `/about-me`.

```
// either src/pages/about.js or src/pages/about/index.js

// Imports
import React from 'react'

// Import layout
import Layout from '../components/layout'

// Component for your About me page
const AboutPage = () => (
  <Layout>
    <h1>I am John Doe</h1>

    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Eum perferendis quidem quae iste molestias, vitae in quaerat labore natus aliquid eveniet veniam obcaecati quis deleniti ad aut quam voluptate assumenda!</p>
  </Layout>
)

// Export the page component
export default AboutPage
```

## What if ... 404

Although GatsbyJS is great there are still some limitations to what it can do. 404 page is one of those limitations. Meaning, when it comes to 404 GatsbyJS looks for specific name. GatsbyJS uses regex pattern that has to match `404`. The file extension doesn't matter. GatsbyJS will find the page whether it is `js`, `jsx` or `tsx`. Well, if you add necessary GatsbyJS plugin. Just make sure the filename for your 404 is `404`.

One more thing. When you are running your website on dev GatsbyJS adds default 404 page. This page will override your custom 404 page. So, don't be surprised if you navigate to a non-existing page and you will not see your custom 404 page. You can preview your 404 page by clicking on the "Preview custom 404 page" link. Below is an example of a simple 404 page.

```
// src/pages/404.js

// Imports
import React from 'react'
import { Link } from 'gatsby'

import Layout from '../components/layout'

const NotFoundPage = () => (
  <Layout>
    <h1>404</h1>

    <p>You just hit a route that doesn&#39;t exist yet.</p>

    <Link to="/">Go home.</Link>
  </Layout>
)

export default NotFoundPage
```

## Contact page and static files

There is one last thing you should know. When you want to use other types of files in your code you have to edit main GatsbyJS config. For example, let's say that you want to build a Contact page with a simple contact form, so people can contact you directly through your website. You decided that you will use AJAX and php file to send the form data.

In this case, referencing the php file in your code would lead to error during compilation. The way to solve this is by adding `pathPrefix: '/'` to GatsbyJS config, the `gatsby-config.js` file in root. Then, you also have to create new folder called `static` in the root. After that, you put your php file for the form inside this folder.

```
module.exports = {
  siteMetadata: {
    title: 'Your website built with GatsbyJS'
  },
  pathPrefix: '/', // Adding path for static files
  plugins: [
    'gatsby-plugin-react-helmet',
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `images`,
        path: `${__dirname}/src/images`
      }
    },
    {
      resolve: `gatsby-plugin-postcss`,
      options: {
        postCssPlugins: [
          require(`postcss-import`)(),
          require(`postcss-extend`)(),
          require(`postcss-nesting`)(),
          require('postcss-pxtorem')({
            mediaQuery: false,
            minPixelValue: 0,
            propWhiteList: [],
            replace: true,
            rootValue: 16,
            selectorBlackList: ['html'],
            unitPrecision: 4
          }),
          require(`postcss-preset-env`)({
            stage: 3 // https://cssdb.org/#staging-process
          }),
          require(`cssnano`)()
        ]
      }
    },
    'gatsby-transformer-sharp',
    'gatsby-plugin-sharp',
    {
      resolve: `gatsby-plugin-manifest`,
      options: {
        name: 'gatsby-starter-default',
        short_name: 'starter',
        start_url: '/',
        background_color: '#663399',
        theme_color: '#663399',
        display: 'minimal-ui',
        icon: 'src/images/gatsby-icon.png' // This path is relative to the root of the site.
      }
    }
    // this (optional) plugin enables Progressive Web App + Offline functionality
    // To learn more, visit: https://gatsby.app/offline
    // 'gatsby-plugin-offline',
  ]
}
```

Finally, when you want to use that file, or any other inside `static`, you use `withPrefix` method imported from `gatsby`. Let's take a quick at an example of Contact page that uses jQuery and AJAX request to send form data. Pay attention especially to two lines. The first is `import { withPrefix } from 'gatsby'` at the top. Here, we import `withPrefix` method from `gatsby`.

The second line is somewhere around the middle, inside `handleFormSubmit` method, where we make AJAX request. It is the `url: withPrefix('/sendEmail.php')` line. As you can see, we are using the `withPrefix` method to reference the php file for the form. This tells GatsbyJS to include this file in build, but not process it. That would lead to an error during compilation, caused by php syntax.

GatsbyJS will two things. First, it will take that file from `static` folder and copy it to the `public` folder. `public` is where you find your website after running build script. It is content of this folder that you deploy on your server. Second, GatsbyJS will correctly link to that file in `contact.js`. As a result, your, form will work as it should.

When you think about it, using `withPrefix` method is similar to using `require`, or `import`. GatsbyJS will include the file you want to use in build and then link to correct destination so your code will work.

```
// src/pages/contact.js

// Imports
import React from 'react'

// Import jQuery for handling AJAX request
import $ from 'jquery'

// Import 'withPrefix' module from 'gatsby'
import { withPrefix } from 'gatsby'

import Layout from '../components/layout'

class ContactPage extends React.Component {
  // Prepare state for storing form data
  state = {
    email: '',
    message: '',
    name: ''
  }

  // Method to handle inputs
  handleInputChange = event => {
    // Check if name input contains text.
    // Don't test email, yet.
    if (event.target.value.length > 0 && event.target.name !== 'email') {
      this.setState({
        [event.target.name]: event.target.value
      })
    }

    // Run a simple test to validate email address
    if (event.target.name === 'email') {
      var re = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/

      if (re.test(String(event.target.value).toLowerCase())) {
        this.setState({
          [event.target.name]: event.target.value
        })
      }
    }
  }

  // Method to handle form submission
  handleFormSubmit = event => {
    event.preventDefault()

    // Test required fields - email and name
    if (this.state.email.length > 0 && this.state.name.length > 0) {
      // Send the data with Ajax and jQuery
      $.ajax({
        data: this.state,
        type: 'POST',
        url: withPrefix('/sendEmail.php'), // use 'withPrefix' module from 'gatsby' to reference 'sendEmail.php' in 'static' folder.
        success: function(data) {
          console.info(data)
        },
        error: function(xhr, status, err) {
          console.error(status, err.toString())
        }
      })
    }
  }

  render() {
    return (
      <Layout>
        <section>
          <h1>Let's get in touch</h1>

          <form action="">
            <fieldset>
              <label htmlFor="name">Full name</label>

              <input onChange={this.handleInputChange} type="text" name="name" id="name" required={true} />
            </fieldset>

            <fieldset>
              <label htmlFor="email">Email address</label>

              <input onChange={this.handleInputChange} type="email" name="email" id="email" required={true} />
            </fieldset>

            <h2>Your message</h2>

            <textarea onChange={this.handleInputChange} name="message" id="message" />

            <fieldset>
              <button onClick={this.handleFormSubmit}>Send</button>
            </fieldset>
          </form>
        </section>
      </Layout>
    )
  }
}

export default ContactPage
```

## Epilogue: How to Build a Simple Website with GatsbyJS & PostCSS Pt.2

This is where we will end this second part as well as this mini series. You learned a lot about GatsbyJS. Now you know how to use this great static website generator to build your own website. What's more, you also have a starting template you can use immediately. Now, it is only up to you to take the next step.

Use the code from this tutorial, and what you know about GatsbyJS, and start building your own website. In the end, it is practice what is the best way to really learn anything and understand it. So, get your hands dirty and write some code. In other words, `yarn start`. And, when you are done, `yarn build` With that, thank you for your time and have a great day!

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Part 1]: https://blog.alexdevero.com/website-gatsbyjs-postcss-pt1/
[previous part]: https://blog.alexdevero.com/website-gatsbyjs-postcss-pt1/
[Bootstrap 4]: http://getbootstrap.com

<!--
#### Meta:
-
-->