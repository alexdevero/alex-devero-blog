# How I Built My First [Electron App] & You Can Too Pt.2 – Preparing the Workflow

So, you want to build your own electron app? Do you have some interesting idea in mind, or just want to learn how to do it? You are on the right place! This mini series will help you learn all you need to achieve both. Today, in this part, our main goal and focus will be setting up the workflow for building our electron app. We will start with installing necessary dependencies and devDependencies. Then, we will set up npm scripts. Finally, we will end this part by preparing configs for Webpack. Now, let's begin!

<!--
Table of Contents:
## It all starts with a ... change
## Putting together the assets and prerequisites
### Installing dependencies
### Installing devDependencies
### Scripts and package.json
### Miscellaneous files
## Project structure and HTML
## Preparing Webpack
## Closing thoughts on building an electron app
How I Built My First [Electron App] & You Can Too [part 3].
-->
How I Built My First [Electron App] & You Can Too [part 1].

## It all starts with a ... change

This was not planned. I did not plan or thought about making a small change so early in the project. However, when it is necessary or beneficiary to make a change, it is better to do it immediately than to wait. So, what is this change I am talking about? First, don't worry. Our goal is still creating a simple electron app that will help us practice the Grease the Groove method, we discussed in the [first part]. This change is about the tech stack I decided to use to build this electron app.

To make the short story shorter, we will not use Parcel bundler. Yes, it started to backfire, a bit. Instead, we are going to use [Webpack]. This bundler made some big progress, especially in the version 4 that will be released soon. It is faster and, in version 4, config file will no longer be necessary, and it will get even faster. That's the first reason. The second reason is that I ran into some issues with putting together stable configuration that would make Parcel work with Electron, especially for builds.

The reason number three is that, paradoxically, putting together a simple config files that would make Webpack work with Electron was easier. So, for this reason I decided to drop Parcel and go with Webpack. Then, there is one moe thing. In the first part, I was not sure whether to use [electron-builder] or [electron-packager] to build our electron app. The winner is electron-packager. It seemed to me that electron-packager is just easier to work with. Let's see. And, that is all for changes.

## Putting together the assets and prerequisites

That was a brief memo about some project changes. Now, it is time to put together all the prerequisites and assets we will need to create our electron app. This is the best to do as soon as possible. Otherwise, we might run into some issues during the development phase. That is not the best time to solve these types of problems. So, let' make sure we have all libraries and plugins installed and ready. Our electron app will require a couple of them.

### Installing dependencies

Let's start with dependencies. We will need four dependencies. These dependencies are electron, react, react-dom, and the fourth one is styled-components. We will download and install each of them locally. My preferred choice is, as usual, yarn. However, feel free to choose package manager you like to use and work with, yarn, npm, pnpm or something else. Keep in mind, these are dependencies, not devDependencies. So, don't use the "-D" or "--save-dev" flag.

```
yarn add electron react react-dom styled-components
```
or

```
npm install electron react react-dom styled-components
```
or
```
pnpm install electron react react-dom styled-components
```

### Installing devDependencies

Next, when we have all the dependencies we need, it is time to download and install devDependencies. We will need again need eleven devDependencies in order to build our electron app. These are babel-core, babel-loader, babel-preset-env, babel-preset-react, babili-webpack-plugin, electron-packager, extract-text-webpack-plugin, file-loader, html-webpack-plugin, webpack and webpack-dev-server. Let's install them. Now, you can use the "-D" or "--save-dev" flag.

```
yarn add -D babel-core babel-loader babel-preset-env babel-preset-react babili-webpack-plugin electron-packager extract-text-webpack-plugin file-loader html-webpack-plugin webpack webpack-dev-server
```
or

```
npm install -D babel-core babel-loader babel-preset-env babel-preset-react babili-webpack-plugin electron-packager extract-text-webpack-plugin file-loader html-webpack-plugin webpack webpack-dev-server
```
or
```
pnpm install -D babel-core babel-loader babel-preset-env babel-preset-react babili-webpack-plugin electron-packager extract-text-webpack-plugin file-loader html-webpack-plugin webpack webpack-dev-server
```

```
"dependencies": {
  "electron": "^1.7.11",
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
  "electron-packager": "^10.1.2",
  "extract-text-webpack-plugin": "^3.0.2",
  "file-loader": "^1.1.6",
  "html-webpack-plugin": "^2.30.1",
  "webpack": "^3.10.0",
  "webpack-dev-server": "^2.11.1"
}
```

_Quick side note about versions: we will use the latest versions of dependencies and devDependencies. However, as the time goes, these versions will become obsolete. Use versions you want, probably the latest at the time you read this article. If you run into some issues and something will not work as it should, try to downgrade your dependencies and devDependencies to versions above. It can happen that there will be some breaking change that will break the code. In that case, feel free to contact me and let me know about it._

### Scripts and package.json

With this we are almost ready to start working and developing our electron app. But before we do that, we need to create a number of simple npm scripts. First, we need a script that will allow us to run the app in "dev" mode. Second, we should also add a script to run our app in production mode. Third, we need a script that will build the assets for our app. Fourth, a script that will package our app.

Finally, one more script that will take that package and use electron-packager to create a build we can run without command line. These scripts will be very easy and use some meaningful names, such as "build", "dev", "package", "postpackage" and "prod".

```
"scripts": {
  "build": "webpack --config webpack.build.config.js",
  "dev": "webpack-dev-server --hot --host 0.0.0.0 --config=./webpack.dev.config.js",
  "package": "webpack --config webpack.build.config.js",
  "postpackage": "electron-packager ./ --out=./builds",
  "prod": "webpack --config webpack.build.config.js && electron --noDevServer ."
}
```

Aside to these scripts, we should also add some additional information, such as "name", "version", "description", "license", "private", "repository", "homepage", "bugs", "author", "engines" and "main". Please, keep in mind that not all of these information are necessary or required. Adding all of those listed above is just a habit. If you are not sure whether your `package.json` is valid, you can do two things.

First, try to install dependencies and devDependencies. Invalid `package.json` will throw an error. Second, use a simple online [validator]. Some basic `package.json` may look like the example below. Feel free to customize and use this one or create your own.

```
{
  "name": "grease-the-groove-app",
  "version": "0.0.1",
  "description": "Electron app to help you practice Grease the Groove method to achieve your goals and get stronger 💪!",
  "license": "MIT",
  "private": false,
  "repository": {
    "type": "git",
    "url": "https://url.git"
  },
  "homepage": "https://url#readme",
  "bugs": {
    "url": "https://url/issues"
  },
  "author": {
    "name": "Your name",
    "email": "name@email.com",
    "url": "https://url.com/"
  },
  "engines": {
    "node": ">=9.0.0",
    "npm": ">=5.0.0",
    "yarn": ">=1.0.0"
  },
  "main": "main.js",
  "scripts": {
    "build": "webpack --config webpack.build.config.js",
    "dev": "webpack-dev-server --hot --host 0.0.0.0 --config=./webpack.dev.config.js",
    "package": "webpack --config webpack.build.config.js",
    "postpackage": "electron-packager ./ --out=./builds",
    "prod": "webpack --config webpack.build.config.js && electron --noDevServer ."
  },
  "dependencies": {
    "electron": "^1.7.11",
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
    "electron-packager": "^10.1.2",
    "extract-text-webpack-plugin": "^3.0.2",
    "file-loader": "^1.1.6",
    "html-webpack-plugin": "^2.30.1",
    "webpack": "^3.10.0",
    "webpack-dev-server": "^2.11.1"
  }
}
```

_Quick side note about version field: I am like to start every project with version "0.0.1" and change the "patch" version as I move through the development phase. Then, when the project is ready for the first official release, I change the version to "1.0.0". Again, this is just my habit. Keep in mind that you don't have to follow or use this versioning process if you don't want to. Use whatever versioning you like and that is comfortable for you._

### Miscellaneous files

One last thing. We need some icon. Our electron app will be able to hide itself into system tray when the user will minimalize it. As you may remember, this was one of the must-have features we discussed in the first part. In short, our goal is to make the app unobtrusive and not clutter user's desktop with yet another open window. However, this also means that we will need some icon. Otherwise, users will not be able to restore the app from system tray. They will not be able to see it. So, choose, buy or make some icon you like.

## Project structure and HTML

Before we get to setting up config files for Webpack, let's quickly discuss the structure of our electron app. If you are not familiar with Webpack, this may give you a better understanding of the Webpack configs. Right inside the root directory, on the first level, will be four directories: `builds`, `dist`, `node_modules` (created by installing dependencies and devDependencies) and `src`.

Then, also right inside the root, will be eight files: `.babelrc`, `.editorconfig`, `main.js, package.json`, `README.md`, `webpack.build.config.js`, `webpack.dev.config.js` and `yarn.lock` (if you installed dependencies and devDependencies with yarn). Again, not all of these files are necessary. So, feel free to leave out the `.editorconfig` and `README.md` if you want.

We will use the `builds` directory as a destination for the `package` and `postpackage` scripts. In other words, this is the directory where we will find ready to use builds for our electron app. Files generated by Webpack will be stored at `dist`. Finally, the `src` will be our main directory for development. Inside `src` will be another two directories, `app` and `assets`. `assets` will contain app icon and any other assets we may want to add. `app` will contain all JavaScript files, or React components, we will create.

React component will be stored inside `component` directory. On the same level, inside the `app` directory, we will also create "main" React file called `App.js` and use this file to import and render all components for our electron app. Right inside the `src` will also be `index.js`, a file where we will render main React component, `App` defined in `App.js`. I hope it still makes at least a bit sense. Let's rather use a quick "illustration":

```
grease-the-groove-app
├── builds
├── dist
├── node_modules
├── src
│   └── app
│       └── components
│       └── App.js
│   └── assets
│       └── grease-the-groove-icon.ico
│       └── grease-the-groove-icon.png
│       └── grease-the-groove-icon.svg
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

_Quick side note about HTML: You may have noticed that there is no `index.html` or any other HTML file. This is not a mistake or a typo. We will be using `HtmlWebpackPlugin` without an HTML template. We will let Webpack to create this file for use and store it inside the `dist` directory._

## Preparing Webpack

Now, let's finish this preparation phase, and our workflow, by putting together two simple Webpack configs. We will use one config for development and the other for production, or packaging and building our electron app. Probably the biggest differences between these configs is that the one for development will utilize `devServer` and `devtool` while the one for production will not. Another difference is that config for production will use `BabiliPlugin`.

Aside to these two differences, our Webpack configs will be pretty much the same. We will use the same `rules` (for `jsx` files, images and fonts), directories, files, `entry`, `output` `target` as well as plugins (except the `BabiliPlugin`). Let's take a look at the final form and shape of our Webpack configs. Again, first config, `webpack.dev.config.js` will be for development. The second, `webpack.build.config.js` will be for production, or packaging and building our electron app.

webpack.dev.config.js:
```
const webpack = require('webpack')
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')
const { spawn } = require('child_process')

// Config directories
const SRC_DIR = path.resolve(__dirname, 'src')
const OUTPUT_DIR = path.resolve(__dirname, 'dist')

// Any directories you will be adding code/files into, need to be added to this array so Webpack will pick them up
const defaultInclude = [SRC_DIR]

module.exports = {
  entry: SRC_DIR + '/index.js',
  output: {
    path: OUTPUT_DIR,
    publicPath: '/',
    filename: 'bundle.js'
  },
  module: {
    rules: [
      {
        test: /\.jsx?$/,
        use: [{ loader: 'babel-loader' }],
        include: defaultInclude
      },
      {
        test: /\.(jpe?g|png|gif|ico)$/,
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
    contentBase: OUTPUT_DIR,
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

webpack.build.config.js:
```
const webpack = require('webpack')
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')
const BabiliPlugin = require('babili-webpack-plugin')
const ExtractTextPlugin = require('extract-text-webpack-plugin')

// Config directories
const SRC_DIR = path.resolve(__dirname, 'src')
const OUTPUT_DIR = path.resolve(__dirname, 'dist')

// Any directories you will be adding code/files into, need to be added to this array so Webpack will pick them up
const defaultInclude = [SRC_DIR]

module.exports = {
  entry: SRC_DIR + '/index.js',
  output: {
    path: OUTPUT_DIR,
    publicPath: './',
    filename: 'bundle.js'
  },
  module: {
    rules: [
      {
        test: /\.jsx?$/,
        use: [{ loader: 'babel-loader' }],
        include: defaultInclude
      },
      {
        test: /\.(jpe?g|png|gif|ico)$/,
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

## Closing thoughts on building an electron app

This is the end of this, second, part of this mini series. It may not seem like much. In the end, we worked only on the workflow for this project. However, we should keep in mind that the work we did today was not meaningless, or a waste of time. We got done a decent amount of work that will help us in the future. How? All this work, setting up the workflow, we did today will help is create our electron app faster and easier. This was a worthy investments that will benefit us later on.

I know that, in the first part, I made a promise to you that we will get into code. Sure, there was some code here and there, at least in the end when we created those configs for Webpack. However, we still didn't work on our electron app itself. Despite that, I still hope you enjoyed this part. And, for the future? Don't worry. This will not happen again because, now, we are ready to get this project up and going. So, in the next part, we will jump right into the development phase and start writing first lines of code for our electron app.

Do you have any questions, recommendations, thoughts, advice or tip you would like to share with other readers of this blog, and me? Great! Please share it in a comment. Or, if you want to keep things more "private", feel free to contact me on [Twitter] or send me a [mail]. I would love to hear from you.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[part 1]: https://blog.alexdevero.com/electron-app-pt1/
[first part]: https://blog.alexdevero.com/electron-app-pt1/
[Webpack]: https://webpack.js.org/
[electron-builder]: https://github.com/electron-userland/electron-builder
[electron-packager]: https://github.com/electron-userland/electron-packager
[validator]: http://package-json-validator.com/
[Twiter]: https://twitter.com/AlexDevero
[mail]: https://alexdevero.com/contact.html

<!--
#### Inspiration:
-
-->
