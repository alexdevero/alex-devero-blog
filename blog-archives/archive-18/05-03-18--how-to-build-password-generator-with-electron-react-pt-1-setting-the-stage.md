# How to Build Password Generator with Electron & React Pt.1 - Setting the Stage

Have you ever wanted to build your own password generator? And, what about an app? This tutorial will show you how! In this mini series, we will learn how to use electron and React and build desktop password generator app. Today, we will start by putting together all dependencies. Then, we will create `package.json` and prepare npm scripts. Finally, we will prepare configs for Webpack and main file for electron.

<!--
Table of Contents:
## Putting together all dependencies
## Package.json and npm scripts
## Outlining the project structure
## Setting up Webpack and babel
## Setting up electron
## Closing thoughts on how to build password generator
-->

## Putting together all dependencies

Let's start, as always, with putting together all prerequisites and assets we will need to create our password generator app. Doing so is a good and easy way to start this project. It will also help us prevent some of the potential issues that could occure later. Our password generator will require a couple of dependencies and devDependencies. Let's start with devDependencies. These are `babel-core`, `babel-loader`, `babel-preset-env`, `babel-preset-react`, `babili-webpack-plugin`, `cross-env`, `electron-packager`, `extract-text-webpack-plugin`, `file-loader`,`. `html-webpack-plugin`, `webpack`, `webpack-cli` and `webpack-dev-server`.

When it comes to dependencies, our password manager wil need just four: `electron`, `react`, `react-dom` and `styled-components`. Now, when we know what packages to install, we can use either npm, yarn, pnpm or any other package manager and install them. One thing to keep in mind is that dependencies are installed without any flag while devDependencies are installed with `-D` or `--save-dev` flag.

`yarn add -D babel-core babel-loader babel-preset-env babel-preset-react babili-webpack-plugin cross-env electron-packager extract-text-webpack-plugin file-loader html-webpack-plugin webpack webpack-cli webpack-dev-server`

`yarn add electron react react-dom styled-components`

_Side note: `webpack-cli` package is reuqired since the release of Webpack 4._

### Package.json and npm scripts

Next step is setting up some basic version of `package.json`. The absolute minimum amount of information required for `package.json` are just two keys with some value: `name` and `version`. According to [npm docs], this is a must. Everything else is, let's say a bonus. I usually like to add more, much more, information in my projects. Aside to these two required keys, it is completely up to you to choose how much information you want to add and add them. My `package.json` would look like something like this.

```
{
  "name": "password-generator",
  "version": "0.0.1",
  "description": "Awesome Password generator app, built with Electron and React.",
  "license": "MIT",
  "private": false,
  "repository": {
    "type": "git",
    "url": "https://url.com.git"
  },
  "homepage": "https://url.com#readme",
  "bugs": {
    "url": "https://url.com/issues"
  },
  "author": {
    "name": "Your Name",
    "url": "https://url.com/"
  },
  "contributors": [
    {
      "name": "",
      "email": "",
      "url": ""
    }
  ],
  "keywords": [
    "app",
    "electron",
    "electron-app",
    "generator",
    "javascript",
    "open",
    "open-source",
    "password",
    "react",
    "reactjs",
    "source",
    "tool"
  ],
  "engines": {
    "node": ">=9.x",
    "npm": ">=5.x",
    "yarn": ">=1.x.x"
  },
  "main": "main.js",
  "scripts": {},
  "dependencies": {
    "electron": "^1.8.2",
    "react": "^16.2.0",
    "react-dom": "^16.2.0",
    "styled-components": "^3.1.6"
  },
  "devDependencies": {
    "babel-core": "^6.26.0",
    "babel-loader": "^7.1.2",
    "babel-preset-env": "^1.6.1",
    "babel-preset-react": "^6.24.1",
    "babili-webpack-plugin": "^0.1.2",
    "cross-env": "^5.1.3",
    "electron-packager": "^11.1.0",
    "extract-text-webpack-plugin": "^4.0.0-beta.0",
    "file-loader": "^1.1.9",
    "html-webpack-plugin": "^3.0.4",
    "webpack": "^4.1.0",
    "webpack-cli": "^2.0.10",
    "webpack-dev-server": "^3.1.0"
  }
}
```

With these information, our `package.json` is almost perfect. There is only one remainig thing we need to add. This thing are npm scripts. We will need a number of npm scripts in order to develop, package and preview our password generator app. Let's call these scripts `start` for development, `build` and `package` for packaging and `preview` for previewing the build of our password generator, before packaging.

All our scripts, except the `package`, will use webpack configs. The `build` and `preview` scripts will use configs for "build" or production while the `start` script will use config for "dev". The same applies to webpack modes. The `build` and `preview` scripts will use `production` mode while `start` will use `development` mode. The `preview` script will use webpack in `production` mode along with `electron`. Finally, we will add variants of the `package` script so we create a build our password generator for all platforms. The section with scripts will then look something like this.

```
"scripts": {
  "build": "cross-env NODE_ENV=production webpack --config webpack.build.config.js --mode production",
  "package:all": "npm run build && electron-packager ./ --out=./builds --overwrite --platform=all",
  "package:linux": "npm run build && electron-packager ./ --out=./builds --overwrite --platform=linux",
  "package:macappstore": "npm run build && electron-packager ./ --out=./builds --overwrite --platform=mas",
  "package:osx": "npm run build && electron-packager ./ --out=./builds --overwrite --platform=darwin",
  "package:win": "npm run build && electron-packager ./ --out=./builds --overwrite --platform=win32",
  "preview": "cross-env NODE_ENV=production webpack --config webpack.build.config.js --mode production && electron --noDevServer .",
  "start": "cross-env NODE_ENV=development webpack-dev-server --hot --host 0.0.0.0 --config=./webpack.dev.config.js --mode development"
}
```

_Side note: as you can see, some scripts also use `cross-env` to set `NODE_ENV` variable. This can be handy during development when you want to use `NODE_ENV` to run snippets of code only in "development" or "production" mode. However, this is not necessary. It is just a practice that became a habit. So, feel free to use it or remove it. The same applies to `cross-env` dependency. If you don't want to use the `NODE_ENV`, you don't need to install this dependency._

_Side note no.2: as you can see, there are some additional flags for electron-packager such as `--out`, `--overwrite`, `--platform`. In a short, `--out` specifies the destination directory for where `electron-packager` will save generated builds or packages. The `--overwrite` means that `electron-packager` will always run and overwrite any already generated builds. The `--platform` specifies the target platform for every build._

## Outlining the project structure

Next, let’s quickly discuss the structure of our password generator project. Knowing about the project will later help us gain a better understanding of where all files are and how to import them in the right way. Right inside the root directory, or on the first level if you want, will be four directories. These directories are: `builds`, `dist`, `node_modules` (created by installing dependencies and devDependencies) and `src`.

We will work mainly with and inside the `src` directory. The `build` will serve as a destination where will Webpack generate compiled files for our password generator. The `builds` directory is a place dedicated to builds, or packages, created by `electron-packager`. So, when you build the password generator, for any platform, you will find the build, or package, inside this directory.

Still inside the root and on the first level, will be eight files: `.babelrc`, `.editorconfig`, `main.js`, `package.json`, `README.md`, `webpack.build.config.js`, `webpack.dev.config.js` and `yarn.lock`. Sure, the `yarn.lock` will be there only if you installed dependencies and devDependencies with yarn. If you used npm instead, tehre will probably be `package-lock.json`. One thing I should mention is that the `.editorconfig` and `README.md` are not necessary. So, feel free to leave out these two if you want.

Now, let's take a look at the `src` directory. Inside this directory be one directory called `App`. `App` will contain the main file for our app called `App.jsx`. We will use this file to import and render all components for our app. Along with the `App.jsx` will be one directory called `components` with all components we will later create for our password generator and one called `assets`. The `assets` directory will contain app icon and any other assets we may want to add.

Still inside the `src` directory will be one file called `index.js`. This file will be a place where we will do a couple of things. First, we will import the main React component, the `App` defined in `App.jsx`. Second, we will create a `div` element and append it to the `body` element. This will be a "root" for React. Third, we will render the `App` component inside the "root" `div` we just created. I hope it still makes some sense. Here is a visual representation of the structure of this project.

```
password-generator-app
├── builds/
├── dist/
├── node_modules/
├── src/
│   └── App/
│       └── components/
│       └── App.jsx
│   └── assets/
│       └── password-generator-icon.icns
│       └── password-generator-icon.ico
│       └── password-generator-icon.png
│       └── password-generator-icon.svg
│   └── index.js
├── .babelrc
├── .editorconfig
├── main.js
├── package.json
├── README.md
├── webpack.build.config.js
├── webpack.dev.config.js
└── yarn.lock
```

## Setting up Webpack and babel

Now, let's take a look at the config files for Webpack. As we discussed above, we will use two configs, one for development and one for build. The difference between these configs is that config for development will use `devtool` and `devServer`. Config for production will not. One more thing, config for production will also use `BabiliPlugin` plugin. This is a minifier based on babel.

With the release of Webpack 4, we no longer have to specify the entry points for `src` and `dist`. The same is true about specifying the location of `index.js`. Webpack will do all this work for us. This will make our config files a bit shorter. We will specify only `rules`, `extensions`, `target`, `plugins`, and `devtool` and `devServer` in the case of config for development. Here is how the Webpack config for development will look like.

```
// webpack.dev.config.js
const webpack = require('webpack')
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')
const { spawn } = require('child_process')

module.exports = {
  module: {
    rules: [
      {
        test: /\.jsx?$/,
        use: [{ loader: 'babel-loader' }]
      },
      {
        test: /\.(jpe?g|png|gif|ico)$/,
        use: [{ loader: 'file-loader?name=img/[name]__[hash:base64:5].[ext]' }]
      }
    ]
  },
  resolve: {
    extensions: ['.js', '.jsx'],
  },
  target: 'electron-renderer',
  plugins: [
    new HtmlWebpackPlugin({
      title: "Password Generator"
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

And here is the config for production
```
// webpack.build.config.js
const webpack = require('webpack')
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')
const BabiliPlugin = require('babili-webpack-plugin')
const ExtractTextPlugin = require('extract-text-webpack-plugin')

module.exports = {
  module: {
    rules: [
      {
        test: /\.jsx?$/,
        use: [{ loader: 'babel-loader' }]
      },
      {
        test: /\.(jpe?g|png|gif|ico)$/,
        use: [{ loader: 'file-loader?name=img/[name]__[hash:base64:5].[ext]' }]
      }
    ]
  },
  resolve: {
    extensions: ['.js', '.jsx'],
  },
  target: 'electron-renderer',
  plugins: [
    new HtmlWebpackPlugin({
      title: "Password Generator"
    }),
    new ExtractTextPlugin('bundle.css'),
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

Now, there is one more thing we need to look at to make sure that our password generator works as it should. It is about babel. We need to specify what presets do we want to use. These presets are `env` and `react` and we will specify them in the `.babelrc` file that is right inside the root directory of this project.

```
{
  "presets": [
    "env",
    "react"
  ]
}
```

## Setting up electron

Let's finish this first part by creating the main file for electron. This is the `main.js` file right inside the root directory of this project. This file is crucial since for getting our password generator up and running. It contains the setup for all the processes of our app, such as creating, activating and closing the window that will contain our app. The code inside this file was created by electron authors as a "Quick Start" template. And, we don't really need to know or care about it so much.

One part we may be interested in is `createWindow` function, especially the part at the top of this function where electron uses `BrowserWindow` object to create a new window. Hre, we can customize some of the properties of our app. For example, we can change the default `width` and `height` of the window. We can also say whether we want the top navigation bar to be show, when the window itself should be shown or what should be the title of our app. There are many [options] we can use. For now, let's stick to these five.

```
// main.js
'use strict'

const electron = require('electron')

// Module to control application life.
const app = electron.app

// Module to create native browser window.
const BrowserWindow = electron.BrowserWindow

const path = require('path')
const platform = require('os').platform()
const url = require('url')

// Keep a global reference of the window object, if you don't, the window will
// be closed automatically when the JavaScript object is garbage collected.
let mainWindow

// Keep a reference for dev mode
let dev = false

if (process.defaultApp || /[\\/]electron-prebuilt[\\/]/.test(process.execPath) || /[\\/]electron[\\/]/.test(process.execPath)) {
  dev = true
}

// Temporary fix for broken High DPI scale factor on Windows (125% scaling)
// info: https://github.com/electron/electron/issues/9691
if (process.platform === 'win32') {
  app.commandLine.appendSwitch('high-dpi-support', 'true')
  app.commandLine.appendSwitch('force-device-scale-factor', '1')
}

function createWindow() {
  // Create the browser window.
  mainWindow = new BrowserWindow({
    'auto-hide-menu-bar': true,
    height: 520,
    show: false,
    title: 'Password Generator',
    width: 560
  })

  // and load the index.html of the app.
  let indexPath

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

_Side note: you may have noticed that there is a line with "Temporary fix for broken High DPI scale factor". This is not contained in the original version of `main.js` provided by the authors and developers of electron. However, I decided to include it because this issue was not solved yet and some of you could otherwise encounter this issue, when the content of the app is not scaled properly._

## Closing thoughts on how to build password generator

This is all for the first part of this tutorial. In a recap, today we started by putting together and installing the dependencies for this project. Then, we created `package.json` and prepared npm scripts for building our password generator app. After that, we quickly outlined the structure of this project. Finally, we prepared development and production configs for Webpack, config for babel and main file for electron.

The remaining question is, what is coming next? In the next part, our main goal and focus will be creating and then polishing the UI for our password generator. We will create all the components our app will need and use `styled-components` to make them look great. I hope you enjoyed this first part and I look forward to seeing you here again the next week. Until then, have a great time!

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[npm docs]: https://docs.npmjs.com/getting-started/using-a-package.json
[options]: https://github.com/electron/electron/blob/master/docs/api/browser-window.md
