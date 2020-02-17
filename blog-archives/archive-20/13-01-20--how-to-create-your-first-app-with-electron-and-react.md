# How to Create Your First App with [Electron and React]
Have you ever wanted to build your own desktop app with electron and React? This tutorial will show you how to do it. You will learn how to create React app from scratch, how to connect it with electron. Then, you will learn how to configure Webpack to handle both.<!--more-->
<!--
Table of Contents:
## Npm
## Creating react app
### Creating app components
### Adding CSS
## Adding electron
### Configuring main electron process
## Adding and configuring webpack
### Installing dependencies
### Adding configuration for babel
## Adding npm scripts and finishing package.json
## Final project structure
## Adding TypeScript (optional)
## Conclusion: How to Create Your First App with Electron and React
-->

## Npm

The first thing to do is creating `package.json`. This file will contain basic info about your app, npm scripts, dependencies, entry point to your app, homepage and other things. For now, let's define `name`, `productName`, `version`, `homepage` and `main`. The `name` is the name of the app. Spaces are not allowed to use here.

The `productName` is for `electron-packager`. It will use it to infer the name of your app when you bundle your app. The `version` specifies [semver version] of your app. The `homepage` is the URL to the project homepage. For the purpose of building electron and React app you will need to set the `homepage` to `./`.

Without this, the packaged electron app would not be able to find the .js and .css files. The `main` specifies the primary entry point to your app. In case of this electron and React app it will be a file with main electron process. This will be `main.js`. This is all for this part. You will deal with `dependencies` and `devDependencies` in the next step.

```json
// package.json
{
  "name": "electron-react-app",
  "productName": "electron-react-app",
  "version": "1.0.0",
  "homepage": "./",
  "main": "main.js",
  "scripts": {},
  "dependencies": {},
  "devDependencies": {}
}
```

## Creating react app

There are two ways to create React app. The first one is using [create-react-app] app generator. The second is creating the starter template, and configuration, from scratch. We will go with the second option. The reason for doing so is that it will give us more control over webpack configuration and customization.

More importantly, building this electron and React app from scratch will make it easier to run it. With `create-react-app`, you would need to run two processes (npm scripts) simultaneously. One for electron and one for React app. With app built from scratch, you will need to run only one process that will handle both, electron and React.

So, let's add dependencies required for developing React app. These are `react` and `react-dom`. Note that you don't have to add `react-scripts`. This dependency is not necessary because you will create webpack configuration for your React app from scratch.

```bash
# in cli
npm install react react-dom

# or

yarn add react react-dom
```

### Creating app components

After installing the dependencies for React app, it is time to create your first components. For now, let's create two. The first will contain code for rendering the main app component into the DOM. This component will be stored in `index.jsx`. Let's create `src` in the root folder and `index.jsx` file there.

The content of the `index.jsx` file will be simple. You will import necessary dependencies, main `App` component and also main CSS stylesheet. Next, you will create new `div` element in the `index.html`. You will use this `div` as the place where you will render your React app.

This is another thing you will not have to do, create `index.html` file. Instead, you will let webpack and [html-webpack-plugin] do this work for you. You will only have to create the div and append it to `body`. Don't worry, this will be easy and quick.

```jsx
// src/index.jsx

// Import dependencies
import React from 'react'
import { render } from 'react-dom'

// Import main App component
import App from './components/app'

// Import CSS stylesheet
import './assets/css/app.css'

// Since we are using HtmlWebpackPlugin WITHOUT a template, we should create our own root node in the body element before rendering into it
let root = document.createElement('div')

// Append root div to body
root.id = 'root'
document.body.appendChild(root)

// Render the app into the root div
render(<App />, document.getElementById('root'))
```

Next is creating the main `App` component. First, create a new folder in `src`, called `components`. Next, inside this folder create new file `app.jsx`. The code for `App` component will go into this file. For now, let's create a simple functional component containing heading and short text. After that, make sure to export the component.

```jsx
// src/components/app.jsx

// Import dependencies
import React from 'react'

// Create main App component
const App = () => (
  <div>
    <h1>Hello, electron!</h1>

    <p>Let's start building your awesome desktop app with electron and React!</p>
  </div>
)

// Export the App component
export default App
```

### Adding CSS

This will be last thing to do before moving on from React. In the `index.jsx` you imported CSS stylesheet. Let's create it now so it will not break the build later when you try to run your electron and React app. For now, you can add proper `box-sizing` for all elements, and some basic styles for typography, at least the main heading.

Another useful thing are styles for light and dark mode. Yes, electron now automatically detects the mode, or theme, of your operating system. So, let's add some styles for both modes, or themes to make sure the content will be rendered properly.

One thing. To keep the code tidy, we will put this stylesheet inside `css` directory. You will create this directory inside `assets` that will be inside `src`. So the complete path will be `src/assets/css/app.css`.

```css
/* src/assets/css/app.css */

/* Main CSS stylesheet */
html,
*,
*::before,
*::after {
  box-sizing: border-box;
}

body {
  font-size: 16px;
}

@media screen and (prefers-color-scheme: light), screen and (prefers-color-scheme: no-preference) {
  /* Light moe */
  body {
    color: #000;
    background-color: #fff;
  }
}

@media screen and (prefers-color-scheme: dark) {
  /* Dark moe */
  body {
    color: #fff;
    background-color: #000;
  }
}

h1 {
  font-family: Helvetica, Arial, sans-serif;
  font-size: 21px;
  font-weight: 200;
}
```

## Adding electron

You are done with React for now. As the next step, let's take care of electron. First, you will need to add necessary dependencies. These will be `electron` that will power your electron and React app and `electron-packager`. The [electron-packager] will help you package your app with OS-specific bundles, i.e. .app, .exe, .zip, .deb etc.

```bash
# in cli
npm install -D electron electron-packager

# or
yarn add -D electron electron-packager
```

You can also install [electron-devtools-installer]. This package will allow you install DevTool extensions into your Electron app. The electron contains default DevTool. However, there is no extension for React. With the help of `electron-devtools-installer` your app can download install this extension from Chrome WebStore.

This extension will help you develop and debug your Electron and React app. Mind you, adding this package is optional. It is not necessary to install it. Your app will work without it. However, it can improve your development and debugging workflow.

```bash
# in cli
npm install -D electron-devtools-installer

# or
yarn add -D electron-devtools-installer
```

### Configuring main electron process

The next step to make electron work is about configuring main electron process, or configuration. The main electron process takes care of a couple of things. First, it creates the app window. Second, it takes care of loading the `index.html` file created by webpack. Third, it also handles closing the app window.

It is also in the main electron process, or configuration, where you can add the React Developer Tools extension. For now, let's create new file called `main.js` in the root. If you want to change the filename or location of the file, remember to also change the `main` key in `package.json` because it refers to this file.

```js
// main.js

'use strict'

// Import parts of electron to use
const { app, BrowserWindow } = require('electron')
const path = require('path')
const url = require('url')

// Add React extension for development
const { default: installExtension, REACT_DEVELOPER_TOOLS } = require('electron-devtools-installer')

// Keep a global reference of the window object, if you don't, the window will
// be closed automatically when the JavaScript object is garbage collected.
let mainWindow

// Keep a reference for dev mode
let dev = false

// Determine the mode (dev or production)
if (process.defaultApp || /[\\/]electron-prebuilt[\\/]/.test(process.execPath) || /[\\/]electron[\\/]/.test(process.execPath)) {
  dev = true
}

// Temporary fix for broken high-dpi scale factor on Windows (125% scaling)
// info: https://github.com/electron/electron/issues/9691
if (process.platform === 'win32') {
  app.commandLine.appendSwitch('high-dpi-support', 'true')
  app.commandLine.appendSwitch('force-device-scale-factor', '1')
}

function createWindow() {
  // Create the browser window.
  mainWindow = new BrowserWindow({
    width: 1024, // width of the window
    height: 768, // height of the window
    show: false, // don't show until window is ready
    webPreferences: {
      nodeIntegration: true
    }
  })

  // and load the index.html of the app.
  let indexPath

  // Determine the correct index.html file
  // (created by webpack) to load in dev and production
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

  // Load the index.html
  mainWindow.loadURL(indexPath)

  // Don't show the app window until it is ready and loaded
  mainWindow.once('ready-to-show', () => {
    mainWindow.show()

    // Open the DevTools automatically if developing
    if (dev) {
      installExtension(REACT_DEVELOPER_TOOLS)
        .catch(err => console.log('Error loading React DevTools: ', err))
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

## Adding and configuring webpack

Both electron and React are ready. The next thing to do is setting up webpack. You will create two configuration files. One will be for development, `webpack.dev.config.js`, and the second for production, `webpack.build.config.js`. There will be two main differences between these two configuration files.

One difference is that config for development (dev) will use webpack devServer and source maps. The second difference is that the production configuration (build) will use `mini-css-extract-plugin` to extract and optimize CSS styles and babel based minifier `babili-webpack-plugin`. It will also show some bundle information.

Aside to these two, the content will be almost the same. There will be a rule for .css files that will use `style-loader` and `css-loader`. Next will be a rule for .jsx files using `babel-loader`. Last two rules will handle images and font files, using `file-loader`.

Webpack config for development:

```js
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
        test: /\.css$/,
        use: [{ loader: 'style-loader' }, { loader: 'css-loader' }],
        include: defaultInclude
      },
      {
        test: /\.jsx?$/,
        use: [{ loader: 'babel-loader' }],
        include: defaultInclude
      },
      {
        test: /\.(jpe?g|png|gif)$/,
        use: [{ loader: 'file-loader?name=img/[name]__[hash:base64:5].[ext]' }],
        include: defaultInclude
      },
      {
        test: /\.(eot|svg|ttf|woff|woff2)$/,
        use: [{ loader: 'file-loader?name=font/[name]__[hash:base64:5].[ext]' }],
        include: defaultInclude
      }
    ]
  },
  target: 'electron-renderer',
  plugins: [
    new HtmlWebpackPlugin(),
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

Webpack config for production:

```js
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
        test: /\.css$/,
        use: [
          MiniCssExtractPlugin.loader,
          'css-loader'
        ],
        include: defaultInclude
      },
      {
        test: /\.jsx?$/,
        use: [{ loader: 'babel-loader' }],
        include: defaultInclude
      },
      {
        test: /\.(jpe?g|png|gif)$/,
        use: [{ loader: 'file-loader?name=img/[name]__[hash:base64:5].[ext]' }],
        include: defaultInclude
      },
      {
        test: /\.(eot|svg|ttf|woff|woff2)$/,
        use: [{ loader: 'file-loader?name=font/[name]__[hash:base64:5].[ext]' }],
        include: defaultInclude
      }
    ]
  },
  target: 'electron-renderer',
  plugins: [
    new HtmlWebpackPlugin(),
    new MiniCssExtractPlugin({
      // Options similar to the same options in webpackOptions.output
      // both options are optional
      filename: 'bundle.css',
      chunkFilename: '[id].css'
    }),
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

### Installing dependencies

Webpack configs are read. Now, you need to install all necessary webpack dependencies. Install all of them as devDependencies. Core webpack plugins you will need are `webpack`, `webpack-cli` and `webpack-dev-server`. For babel, you will need `@babel/core`, `@babel/preset-react` and `babili-webpack-plugin`.

For loaders, you will need `babel-loader`, `css-loader`, `file-loader` and `style-loader`. Some additional plugins are `html-webpack-plugin` and `mini-css-extract-plugin`.

```bash
# in cli
npm install -D webpack webpack-cli webpack-dev-server @babel/core @babel/preset-react babili-webpack-plugin babel-loader css-loader file-loader style-loader html-webpack-plugin mini-css-extract-plugin

# or
yarn add -D webpack webpack-cli webpack-dev-server @babel/core @babel/preset-react babili-webpack-plugin babel-loader css-loader file-loader style-loader html-webpack-plugin mini-css-extract-plugin
```

### Adding configuration for babel

Webpack uses [babel], and the `@babel/preset-react` plugin, to transpile your React code. Unfortunately, webpack doesn't automatically know it should this plugin. In order to enable it you need to create new file called `.babelrc`, in the root directory.

Inside this file, you will create new json with "presets" key and an array containing the `@babel/preset-react` as the value. This will tell webpack to use this plugin. That's all for webpack and babel.

```
// .babelrc
{
  "presets": [
    "@babel/preset-react"
  ]
}
```

## Adding npm scripts and finishing package.json

The last step. Both, electron and React are ready. Webpack configuration is ready as well, babel is also enabled, and all dependencies are installed. Now, the very last thing to do is to create npm scripts. These scripts will run your app in development and productions modes, and build it and package it.

Scripts for running and building your app will use webpack, and appropriate webpack config. Script for packaging will use `electron-packager` to create a bundle of your app. Take a look at the [documentation] for this plugin to so you know all available options to configure this plugin.

Here is the complete `package.json` for this electron and React app:

```json
// package.json

{
  "name": "electron-react-app",
  "productName": "electron-react-app",
  "version": "1.0.0",
  "homepage": "./",
  "main": "main.js",
  "scripts": {
    "prod": "webpack --mode production --config webpack.build.config.js && electron --noDevServer .",
    "start": "webpack-dev-server --hot --host 0.0.0.0 --config=./webpack.dev.config.js --mode development",
    "build": "webpack --config webpack.build.config.js --mode production",
    "package": "npm run build",
    "postpackage": "electron-packager ./ --out=./builds"
  },
  "dependencies": {
    "react": "16.12.0",
    "react-dom": "16.12.0"
  },
  "devDependencies": {
    "@babel/core": "7.8.0",
    "@babel/preset-react": "7.8.0",
    "babel-loader": "8.0.6",
    "babili-webpack-plugin": "0.1.2",
    "css-loader": "3.4.2",
    "electron": "7.1.8",
    "electron-devtools-installer": "2.2.4",
    "electron-packager": "14.1.1",
    "file-loader": "5.0.2",
    "html-webpack-plugin": "3.2.0",
    "mini-css-extract-plugin": "0.9.0",
    "style-loader": "1.1.2",
    "webpack": "4.41.5",
    "webpack-cli": "3.3.10",
    "webpack-dev-server": "3.10.1"
  }
}
```

## Final project structure

Below is the final structure your new app built with electron and React. Use this to ensure you have all necessary files, in the right place.

```
electron-react-app/
├─node_modules
├─src
│ ├─assets
│ │ └─css
│ │   └─app.css
│ ├─components
│ │ └─app.jsx
│ └─index.jsx
├─ .babelrc
├─ main.js
├─ package.json
├─ webpack.build.config.js
└─ webpack.dev.config.js
```

## Conclusion: How to Create Your First App with Electron and React

Congratulations! You've just created your first app with electron and React from scratch. The next steps? Well, why stop here? Start your new electron and React app on dev server, using either `npm run start` or `yarn start`, and build something cool.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[semver version]: https://docs.npmjs.com/about-semantic-versioning
[create-react-app]: https://create-react-app.dev/
[html-webpack-plugin]: https://webpack.js.org/plugins/html-webpack-plugin/
[electron-packager]: https://github.com/electron/electron-packager
[Chrome WebStore]: https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi
[babel]: https://babeljs.io/
[documentation]: https://github.com/electron/electron-packager

<!--
#### Meta:
-
-->
