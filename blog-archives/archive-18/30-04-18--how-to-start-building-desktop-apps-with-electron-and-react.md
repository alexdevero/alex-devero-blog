# How to Start Building [Desktop Apps] with Electron and React

Imagine you could build desktop apps only with HTML, CSS and JavaScript. This is possible and easy with library called Electron. This tutorial will show you how to start building your first desktop apps with Electron and React. We will take a look at what dependencies are necessary. Then, we will set up Webpack. Finally, we will create a starting template for your electron app.

<!--
Table of Contents:
## Starting with the basics
## Setting up Webpack, Babel and PostCSS
## Setting up electron
## Creating the starting app
### Adding React
### Adding styles
## Final structure
## Closing thoughts on building desktop apps with Election and React
-->

## Starting with the basics

The first thing we will do is taking care about dependencies. These packages will help us start building our desktop apps. As we touched upon in the intro, we will use Electron and React. So, we will need to install `electron`, `react` and `react-dom` packages from npm. I also mentioned Webpack. This means that we will also need `html-webpack-plugin`, `file-loader`, `webpack`, `webpack-cli`, `webpack-dev-server`.

If we want to build desktop apps with React and ES6 syntax, we will need to add `babel-core`, `babel-loader` and `babel-preset-react`. And, we can also add `babili-webpack-plugin`. This is Webpack plugin for minifying based on Babel. Since we will want to use CSS let's also add `css-loader`, `style-loader` and `mini-css-extract-plugin` to our stack. When it comes to CSS, we have a couple of options.

We can either use a plain CSS or we can use some preprocessor. Or, we can another tool to transform our CSS such as PostCSS. Since PostCSS is incredibly extensible and still very similar to pure CSS, let's choose that. This will mean that that we will need a few more packages. These packages will depend on what PostCSS plugins will you want to use.

One that will be necessary is `postcss-loader`. This will help Webpack process CSS "written" in PostCSS. Some handy PostCSS plugins are `postcss-cssnext`, `postcss-import`, `postcss-nested` and `postcss-pxtorem`. First will take care about prefixes. Second will allow us to use imports and third to nest selectors, like in Sass or Less. The last will convert pixels to rems.

The last dependency we will need to add will be either `electron-packager` or `electron-builder`. These dependencies will help us build our desktops apps so we can use them as normal apps. Meaning, it will generate folder with executable files and anything our app needs in order to run. For now, let's choose the first one. Available options for packager are on [GitHub].

Now, to the `package.json`. The absolute minimum amount of information required are just two, `name` and `version`. I like to create more descriptive info. Decide how much information do you want to include for your project. About the scripts, we will use four, `prod`, `start`, `build`, `package` and `postpackage`.

The `build` and `prod` scripts will use Webpack configs for "build" or production. The `start` script will use config for "dev". The same applies to webpack modes. The `build` and `prod` scripts will use production mode while `start` will use development mode. The `prod` script will use webpack in production mode with electron so we can preview our app. The `package` will build our code and use electron to generate the app.

A more descriptive version of `package.json` can look something like this:

```
// package.json

{
  "name": "my-electron-react-app",
  "version": "1.0.0",
  "description": "My Electron app built with React, PostCSS and Webpack.",
  "license": "unlicensed",
  "private": true,
  "repository": {
    "type": "git",
    "url": "https://url.com/repository.git"
  },
  "homepage": "",
  "bugs": {
    "url": "https://url.com/issues"
  },
  "author": {
    "name": "Your Name",
    "email": "your@name.com",
    "url": "https://url.com"
  },
  "keywords": [
    "app",
    "css",
    "desktop",
    "electron",
    "postcss",
    "react",
    "reactjs",
    "webpack"
  ],
  "main": "main.js",
  "scripts": {
    "prod": "webpack --mode production --config webpack.build.config.js && electron --noDevServer .",
    "start": "webpack-dev-server --hot --host 0.0.0.0 --config=./webpack.dev.config.js --mode development",
    "build": "webpack --config webpack.build.config.js --mode production",
    "package": "npm run build && electron-packager ./ --out=./builds --platform=all"
  },
  "dependencies": {
    "electron": "^1.8.6",
    "react": "^16.3.2",
    "react-dom": "^16.3.2"
  },
  "devDependencies": {
    "babel-core": "^6.26.3",
    "babel-loader": "^7.1.4",
    "babel-preset-react": "^6.24.1",
    "babili-webpack-plugin": "^0.1.2",
    "css-loader": "^0.28.11",
    "electron": "^1.8.6",
    "electron-packager": "^12.0.1",
    "file-loader": "^1.1.11",
    "html-webpack-plugin": "^3.2.0",
    "mini-css-extract-plugin": "^0.4.0",
    "postcss-cssnext": "^3.1.0",
    "postcss-import": "^11.1.0",
    "postcss-loader": "^2.1.4",
    "postcss-nested": "^3.0.0",
    "postcss-pxtorem": "^4.0.1",
    "style-loader": "^0.21.0",
    "webpack": "^4.6.0",
    "webpack-cli": "^2.0.15",
    "webpack-dev-server": "^3.1.3"
  }
}
```

Now, when we have completed the `package.json`, with all dependencies, we can now run  `npm install` or `yarn`. This will download all dependencies specified in `package.json` from npm.

When we work on our desktop apps, there might be some files we don't want to include in git. For this reason, we should also add some `.gitignore`. Below is a more universal `.gitignore` that will take care about a lot of files that you may not want to include in git. It will work well with most projects. For now, the first three sections (build, development and logs) will be very useful. Other than that, use whatever you want.

```
// .gitignore

# Build folder and files #
##########################
builds/

# Development folders and files #
#################################
dist/
node_modules/

# Log files & folders #
#######################
logs/
*.log
npm-debug.log*
.npm

# Packages #
############
# it's better to unpack these files and commit the raw source
# git has its own built in compression methods
*.7z
*.dmg
*.gz
*.iso
*.jar
*.rar
*.tar
*.zip

# Photoshop & Illustrator files #
#################################
*.ai
*.eps
*.psd

# Windows & Mac file caches #
#############################
.DS_Store
Thumbs.db
ehthumbs.db

# Windows shortcuts #
#####################
*.lnk
```

## Setting up Webpack, Babel and PostCSS

Next, let's take care about config files for Webpack. We will create two. We will use one config while developing our desktop apps. The second config will be used when we decide to build our desktop apps and package them for production. These configs we look very similar. One difference is that, unlike config for production, config for development will use `devtool` and `devServer`. Second, config for production will use `BabiliPlugin` plugin.

Aside to these, we will also need to specify `rules`, `target` and `plugins`. `Plugins` will tell Webpack what plugins do we want to use. `target` will specify that we want to compile our desktop apps for Electron, for renderer process more specifically. `Rules` will tell Webpack what files to watch and how to handle them, what loader should it use to process them.

If you are curios about additional options or the inner working of Webpack, take a look at [Webpack documentation]. Another good place to learn about Webpack is [Webpack Academy]. Below are examples of configs that will help us set up Webpack so we can start working on our desktop apps.

*Side note: I included rules for images and custom fonts. If you don't want to use any images or fonts in your desktops apps, hosted locally, feel free to remove these rules. Also, if you decide that you don't want to use both, you can also remove `file-loader` from `package.json`. This package will no longer have any use.*

Webpack config for development environment:

```
// webpack.dev.config.js

const webpack = require('webpack')
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')
const { spawn } = require('child_process')

// Any directories you will be adding code/files into, need to be added to this array so webpack will pick them up
const defaultInclude = path.resolve(__dirname, 'src')

module.exports = {
  module: {
    rules: [
      {
        test: /\.css$/, // loader CSS
        use: [{ loader: 'style-loader' }, { loader: 'css-loader' }, { loader: 'postcss-loader' }],
        include: defaultInclude
      },
      {
        test: /\.jsx?$/, // loader for react
        use: [{ loader: 'babel-loader' }],
        include: defaultInclude
      },
      {
        test: /\.(jpe?g|png|gif)$/, // loader for images
        use: [{ loader: 'file-loader?name=img/[name]__[hash:base64:5].[ext]' }],
        include: defaultInclude
      },
      {
        test: /\.(eot|svg|ttf|woff|woff2)$/, // loader for custom fonts
        use: [{ loader: 'file-loader?name=font/[name]__[hash:base64:5].[ext]' }],
        include: defaultInclude
      }
    ]
  },
  target: 'electron-renderer',
  plugins: [
    new HtmlWebpackPlugin({
      template: 'public/index.html'
    }),
    new webpack.DefinePlugin({
      'process.env.NODE_ENV': JSON.stringify('development')
    })
  ],
  devtool: 'cheap-source-map',
  devServer: {
    contentBase: path.resolve(__dirname, 'dist'),
    stats: {
      colors: true,
      chunks: false,
      children: false
    },
    before() {
      spawn(
        'electron',
        ['.'],
        { shell: true, env: process.env, stdio: 'inherit' }
      )
      .on('close', code => process.exit(0))
      .on('error', spawnError => console.error(spawnError))
    }
  }
}
```

Webpack config for production environment:

```
// webpack.build.config.js

const webpack = require('webpack')
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')
const BabiliPlugin = require('babili-webpack-plugin')
const MiniCssExtractPlugin = require('mini-css-extract-plugin')

// Any directories you will be adding code/files into, need to be added to this array so webpack will pick them up
const defaultInclude = path.resolve(__dirname, 'src')

module.exports = {
  module: {
    rules: [
      {
        test: /\.css$/, // loader CSS
        use: [ MiniCssExtractPlugin.loader, 'css-loader', 'postcss-loader'],
        include: defaultInclude
      },
      {
        test: /\.jsx?$/, // loader for react
        use: [{ loader: 'babel-loader' }],
        include: defaultInclude
      },
      {
        test: /\.(jpe?g|png|gif)$/, // loader for images
        use: [{ loader: 'file-loader?name=img/[name]__[hash:base64:5].[ext]' }],
        include: defaultInclude
      },
      {
        test: /\.(eot|svg|ttf|woff|woff2)$/, // loader for custom fonts
        use: [{ loader: 'file-loader?name=font/[name]__[hash:base64:5].[ext]' }],
        include: defaultInclude
      }
    ]
  },
  target: 'electron-renderer',
  plugins: [
    new HtmlWebpackPlugin({
      template: 'public/index.html'
    }),
    new MiniCssExtractPlugin({ filename: 'bundle.css' }),
    new webpack.DefinePlugin({
      'process.env.NODE_ENV': JSON.stringify('production')
    }),
    new BabiliPlugin()
  ],
  stats: {
    colors: true,
    children: false,
    chunks: false,
    modules: false
  }
}
```

*Side note: `HtmlWebpackPlugin` can generate default template (index.html file) for use. However, you may want to add additional assets or tags, and you may not want to do it through the plugin itself. So, for this reason we will use custom template specified by `template` inside `HtmlWebpackPlugin` in `plugins` section of both configs. If you want to use generated template, remove the `template` part from `HtmlWebpackPlugin` configuration.*

When we are done with Webpack we still need to do one thing. We need to set up configs babel and PostCSS Webpack will use. This will be very fast. We will need to create `.babelrc` and `postcss.config.js`. For babel, we will specify what preset we want to use. This will be "react. For PostCSS, we will define what plugins we want to use. We can also add some custom configuration, such as browser ranges for prefixes and pxtorem.

Final version of `.babelrc`:

```
// .babelrc

{
  "presets": ["react"]
}
```

Final version of `postcss.config.js`:

```
// postcss.config.js

module.exports = {
  plugins: {
    'postcss-cssnext': {
      browsers: [
        'Chrome >= 62'
      ]
    },
    'postcss-import': {},
    'postcss-pxtorem': {
      rootValue: 16,
      unitPrecision: 5,
      propList: ['*'],
      selectorBlackList: ['html', 'body'],
      replace: true,
      mediaQuery: false,
      minPixelValue: 0
    },
    'postcss-nested': {}
  }
}
```

## Setting up electron

Next is Electron. This is the crucial part since we want to use Electron to build desktop apps. Electron uses one main JavaScript source file.  The most important part of this file is the main process. This process is something like a manager. It handles tasks such as creating app window, attaching listeners and actions and just anything that works with renderer processes.

The code I used is a slightly customized template provided by [Electron community]. Our version contains additional `if` statement for Webpack. It basically says whether we want to run our app on URL (localhost) via dev server or as a "standalone" app from build. URL, and dev server, is used only for development mode. Otherwise, we want to run the build of our app.

A very short version of what we do in this file is creating a new application, or a window, by defining the method that will be used for starting it and for shutting it down. Fortunately, people behind Electron did a great job and the code itself is well documented. If you want to know more about what features can you use for your desktop apps, take a look at the [official documentation].

Final version of `main.js`:

```
// main.js

'use strict'

// Import parts of electron to use
const { app, BrowserWindow } = require('electron')
const path = require('path')
const url = require('url')

// Keep a global reference of the window object, if you don't, the window will
// be closed automatically when the JavaScript object is garbage collected.
let mainWindow

// Keep a reference for dev mode
let dev = false

if (process.defaultApp || /[\\/]electron-prebuilt[\\/]/.test(process.execPath) || /[\\/]electron[\\/]/.test(process.execPath)) {
  dev = true
}

// Temporary fix broken high-dpi scale factor on Windows (125% scaling)
// info: https://github.com/electron/electron/issues/9691
if (process.platform === 'win32') {
  app.commandLine.appendSwitch('high-dpi-support', 'true')
  app.commandLine.appendSwitch('force-device-scale-factor', '1')
}

function createWindow() {
  // Create the browser window.
  mainWindow = new BrowserWindow({
    width: 1024,
    height: 768,
    show: false
  })

  // and load the index.html of the app.
  let indexPath

  // Implementing Webpack
  if (dev && process.argv.indexOf('--noDevServer') === -1) {
    indexPath = url.format({
      protocol: 'http:',
      host: 'localhost:8080',
      pathname: 'index.html',
      slashes: true
    })
  } else {
    indexPath = url.format({
      protocol: 'file:',
      pathname: path.join(__dirname, 'dist', 'index.html'),
      slashes: true
    })
  }

  mainWindow.loadURL(indexPath)

  // Don't show until we are ready and loaded
  mainWindow.once('ready-to-show', () => {
    mainWindow.show()

    // Open the DevTools automatically if developing
    if (dev) {
      mainWindow.webContents.openDevTools()
    }
  })

  // Emitted when the window is closed.
  mainWindow.on('closed', function() {
    // Dereference the window object, usually you would store windows
    // in an array if your app supports multi windows, this is the time
    // when you should delete the corresponding element.
    mainWindow = null
  })
}

// This method will be called when Electron has finished
// initialization and is ready to create browser windows.
// Some APIs can only be used after this event occurs.
app.on('ready', createWindow)

// Quit when all windows are closed.
app.on('window-all-closed', () => {
  // On macOS it is common for applications and their menu bar
  // to stay active until the user quits explicitly with Cmd + Q
  if (process.platform !== 'darwin') {
    app.quit()
  }
})

app.on('activate', () => {
  // On macOS it's common to re-create a window in the app when the
  // dock icon is clicked and there are no other windows open.
  if (mainWindow === null) {
    createWindow()
  }
})
```

## Creating the starting app

We are almost at the end. In order to start building our first desktop apps, we will need a couple more files. The most important will be `index.html`, `index.js` and `App.jsx`. Well, if you decided to let Webpack generate the template for you (note about `HtmlWebpackPlugin`), then you will need only `index.js`. `index.html` will be very simple.

This file will contain the default `DOCTYPE`, `html`, `head`, `body` tags along with `title` and meta for `http-equiv`. And, we will add a `div` as a place where we will render the main component of our React app. We will put this file into `public` folder.

The final version of `index.html`:

```
// public/index.html

<!DOCTYPE html>
<html>
  <head>
    <meta http-equiv="Content-type" content="text/html; charset=utf-8"/>

    <title>My Electron app</title>
  </head>
  <body>
    <div id="root"></div>
  </body>
</html>
```

### Adding React

Next is the `index.js`. This file will be simple as well. It will contain imports for `React` and `render`. And, we can also add another import for some styles we will create later. Below that, we will create the main `App` component. After that, we will use `render` and render the `App` component into the DOM, the `div` inside `index.html`.

Final version of `index.js`:

```
// src/index.js

import React from 'react'
import { render } from 'react-dom'

// Import some styles
import './styles/App.css'

// Create main App component
class App extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello, this is your first Electron app!</h1>

        <p>I hope you enjoy using this electron react app.</p>
      </div>
    )
  }
}

// Render the application into the DOM, the div inside index.html
render(<App />, document.getElementById('root'))
```

*Side note: if you decided to use template generated by Webpack and `HtmlWebpackPlugin`, you will need an additional code to `index.js`. You will need to create the `div` we have in `index.html` and append it to `body` element. Modified version of `index.js` is below.*

```
// src/index.js

import React from 'react'
import { render } from 'react-dom'

// Import some styles
import './styles/App.css'

// Create main App component
class App extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello, this is your first Electron app!</h1>

        <p>I hope you enjoy using this electron react app.</p>
      </div>
    )
  }
}

// Create your own root div in the body element before rendering into it
let root = document.createElement('div')

// Add id 'root' and append the div to body element
root.id = 'root'
document.body.appendChild(root)

// Render the application into the DOM, the div inside index.html
render(<App />, document.getElementById('root'))
```

### Adding styles

Now, we can add some styles, just to make sure Webpack loaders work. Let's style the main heading we used in `index.js`.

```
// src/styles/App.css

/* Example stylesheet */

h1 {
  font-family: helvetica;
  font-size: 21px;
  font-weight: 200;
}

```

## Final structure

We worked with a lot of files throughout this tutorial. If you followed all the steps, the final structure for our electron app will look something as the example below.

```
my-electron-react-app
├── builds/
├── dist/
├── node_modules/
├── public/
│   └── index.html
├── src/
│   └── components/
│   └── styles/
│       └── App.css
│   └── index.js
├── .babelrc
├── main.js
├── package.json
├── postcss.config.js
├── webpack.build.config.js
├── webpack.dev.config.js
└── yarn.lock
```

## Closing thoughts on building desktop apps with Election and React

And, this is all for this article! You created your own simple starting template for building desktop apps. I hope you've enjoyed this tutorial and learned something new. What now? Go ahead, take this template and build the app you always wished existed. The only limit is your imagination. Thank you for your time and have a great day!

*One warning. Building your own desktop apps can be highly addictive!*

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[GitHub]: https://github.com/electron-userland/electron-packager
[Webpack documentation]: https://webpack.js.org/configuration/
[Webpack Academy]: https://webpack.academy/
[Electron community]: https://github.com/electron/electron/blob/master/docs/tutorial/first-app.md
[official documentation]: https://github.com/electron/electron/tree/master/docs

<!--
#### Inspiration:
-
-->
