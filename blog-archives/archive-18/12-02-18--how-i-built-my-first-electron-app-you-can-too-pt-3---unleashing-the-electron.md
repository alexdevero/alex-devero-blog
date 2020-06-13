# How I Built My First [Electron App] & You Can Too Pt.3 – Unleashing the Electron

Building an electron app doesn't have to be hard. It can be actually easy. In this mini series we will take a look at how to do it, step-by-step. In this part, we will put together the code that will power up our electron app. Then, we will create the first and also the main React component for our app with a simple UI. With that, we will finally have the chance to run our electron app and see the results of our work. So, without further ado, let's begin!
<!--
Table of Contents:
## Setting up Electron
## Preparing index.js
## Our first and main component
## Closing thoughts on building an electron app
How I Built My First [Electron App] & You Can Too [part 3].
-->
How I Built My First [Electron App] & You Can Too [part 1].
How I Built My First [Electron App] & You Can Too [part 2].

## Setting up Electron

Let's get right into the development of our electron app. Our first step will be putting together file called `main.js`. As you may remember from the [second part], this file should be in the root directory of our project. The purpose of this file is simple. It contains a script called `the main process` and this script is responsible for running the main process that then displays a GUI by creating web pages, which is done by creating one or more instances of `BrowserWindow`.

Each of these web pages and instances of `BrowserWindow` also runs its own renderer process. If one web page is closed, its renderer process is closed as well. And, the main process is something like a manager of these processes. There is a lot more and for anyone interested, take a look at the [Quick Start manual] on GitHub. However, that is not important for the purpose of putting together our electron app. All we need to know is that this file, the `main.js`, is necessary for running our app.

Luckily for us, we don't have to do so much with this file. We can use the default version of the file provided by [electron-quick-start] boilerplate. Well, almost. We will only need to add a few more lines to prepare for the features we want to have in our electron app, namelly the ability to minimize our app to system tray. Nxt, we will also add code to implement context menu. Finally, we will also need to make some changes in order to implement Webpack.

The full version of the `main.js` files that will power up our electron app is following.

```
'use strict'

// Require electron
const electron = require('electron')

// Module to control application life.
const app = electron.app

// Module to create native browser window.
const BrowserWindow = electron.BrowserWindow

const path = require('path')
const url = require('url')

// Module to check for platform
const platform = require('os').platform()

// Modules to create app tray icon and context menu
const Menu = electron.Menu
const Tray = electron.Tray

// Create variables for icons to prevent disappearing icon when the JavaScript object is garbage collected.
let trayIcon = null
let appIcon = null

// Determine appropriate icon for platform
if (platform == 'darwin') {
  trayIcon = path.join(__dirname, 'src', 'assets/grease-the-groove-icon.png')
} else if (platform == 'win32') {
  trayIcon = path.join(__dirname, 'src', 'assets/grease-the-groove-icon.ico')
}

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
  // with specific icon and don't show it until it is ready (show: false)
  mainWindow = new BrowserWindow({
    icon: trayIcon,
    height: 667,
    show: false,
    title: 'Grease the Groove',
    width: 375
  })

  // Create tray icon
  appIcon = new Tray(trayIcon)

  // Create RightClick context menu for tray icon
  // with two items - 'Restore app' and 'Quit app'
  const contextMenu = Menu.buildFromTemplate([
    {
      label: 'Restore app',
      click: () => {
        mainWindow.show()
      }
    },
    {
      label: 'Quit app',
      click: () => {
        mainWindow.close()
      }
    }
  ])

  // Set title for tray icon
  appIcon.setTitle('Grease the Groove')

  // Set toot tip for tray icon
  appIcon.setToolTip('Grease the Groove')

  // Create RightClick context menu
  appIcon.setContextMenu(contextMenu)

  // Restore (open) the app after clicking on tray icon
  // if window is already open, minimize it to system tray
  appIcon.on('click', () => {
    mainWindow.isVisible() ? mainWindow.hide() : mainWindow.show()
  })

  // and load the index.html of the app.
  let indexPath

  // Setup for Webpack
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

  // Minimize window to system tray
  mainWindow.on('minimize',function(event){
      event.preventDefault()
      mainWindow.hide()
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

## Preparing index.js

Next file that will be necessary to run our electron app is `index.js`. This file will be inside the `src` directory that is inside the root of this project. Inside this file, we will do two things. First, we will create a `div` element inside which we will render the main React component of our electron app. Remember, we are not using a static HTML template. Webpack will do the heavy lifting and create this template for us. So, we don't have to care about it anymore in any phase of development.

Then, there is the second thing we will do. We will import `React` library and `render` method from `React-dom` library. And then, we will import the main component for our electron app. Let's call this component simply called `App` and we will put it into `App.jsx` files inside `app` directory. This directory will be inside `src`. With that we can use the `render` method to render our `App` component inside the `div` we previously created.

```
// Import React
import React from 'react'

// Import React-dom
import { render } from 'react-dom'

// Import the main App component
import App from './app/App'

// Since we are using HtmlWebpackPlugin WITHOUT a template
// we should create our own root node in the body element before rendering into it
let root = document.createElement('div')

// Add id to root 'div'
root.id = 'root'

// Append 'root' div to the 'body' element
document.body.appendChild(root)

// Render the main component of our electron application into the 'root' div
render(<App />, document.getElementById('root'))
```

Let me show you the folder structure, we discssued in the second part. It will make understanding it and wrapping our head around it much easier. So, again, the directories and files we are working with at this monent are `src/`, `app/` `App.jsx` and `index.js`.

```
grease-the-groove-app
├── builds/
├── dist/
├── node_modules/
├── src/
│   └── app/
│       └── components/
│       └── App.jsx
│   └── assets/
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

Keep in mind that these files, the `main.js` and `index.js` are necessary for running our electron app. If you decide to change the names of any of these files, or the location, make sure to also update your Webpack configs, `webpack.build.config.js` and `webpack.dev.config.js`.

## Our first and main component

Okay. All dependencies we need are in place. Configs and workflow are prepared as well. Now, Electron is also ready. So, let's create the first React component for our electron app. This will be the `App` component, we talked about above, and we will put it inside `src/app/App.jsx` file. First, we will import `React` library. Next, we can prepare another import for the Timer component. Since we don't have this component prepared yet, let's comment it out.

Next comes the component itself. We want to use app state in this component. So, for this reason, we will use JavaScript `class` and create a stateful component. At the top of the component will be `constructor` method with `state` nested inside. `State` will contain four keys. The first two, `isSettingsOpen` and `isTimerShown`, will be boolean and both will be `false` as default. We will use these keys to determine whether to show/hide `Timer` component and whether to open/close settings box.

The second pair of keys, `numOfSets` and `restPauseLength` will be both integers. We will use these to store the number of sets user wants to do and the length of rest pause she wants to have between the sets. When we are done with `constructor` and `state`, we can create a simple method for generating list of items where each item will represent one set the user wants to do. All items will contain a `checkbox` and `span` (for text) wrapped inside a `label`.

Inside this list, we will use `for` loop and `numOfSets` key, from the app `state`, to generate amount of sets users specified in settings. Inside this, we will push each of these list items inside an array we will then return, and render. After that, we will create two very simple methods, `toggleSettings` for opening/closing settings box and `toggleTimer` for showing/hiding `Timer` component. Each of these methods will change the `isSettingsOpen` and `isTimerShown` keys inside app `state` via the `setState` method.

Next, let's create another two simple methods, `updateNumOfSets` and `updateRestPauseLength`. These two will also change specific keys inside app `state`, `numOfSets` and `restPauseLength` via the `setState` method. We are almost done. The last thing we need to get our electron app up and running is creating some UI and putting it into the `render` method. For now, let's put the majority of the parts of the UI inside this file. We can refactor it and split it into smaller components later.

About the UI. It will be relatively simple. We will create one main heading, some additional text, one button for opening settings and one button for showing timer and list with sets to do. Settings box will contain two number inputs, one for specifying number of sets and one for specifying the length of the rest pause. There will be also some additional for each of these inputs. The result will look like this.

```
// Import React library
import React from 'react'

// Import timer (not implemented yet)
// import Timer from './components/Timer'

// Create the main component for our electron app
class App extends React.Component {
  constructor() {
    super()

    // Create and setup the app state
    this.state = {
      isSettingsOpen: false,
      isTimerShown: false,
      numOfSets: 6,
      restPauseLength: 90
    }
  }

  // Create a method for generating list of items, one for each set the user wants to do
  // each item will contain checkbox and label
  generateSetsList() {
    // Prepare empty array for list items
    let setsItems = []

    // Generate number of list items based on 'numOfSets'
    for(let i = 0; i<this.state.numOfSets; i++) {
      setsItems.push(<li key={i}>
        <label htmlFor={`set${i}`}>
          <input id={`set${i}`} name={`set${i}`} type="checkbox"/>

          <span>Set number {i+1}</span>
        </label>
      </li>)
    }

    // Return the array with list items
    return setsItems
  }

  // Create a method to open/close collapsible div with options
  toggleSettings(e) {
    e.preventDefault()

    // Change specific keys in app state to either open settings or show timer
    this.setState({
      isSettingsOpen: !this.state.isSettingsOpen,
      isTimerShown: false
    })
  }

  // Create a method to show/hide collapsible div with timer
  toggleTimer(e) {
    e.preventDefault()

    // Change specific keys in app state to either show timer or open settings
    this.setState({
      isSettingsOpen: false,
      isTimerShown: !this.state.isTimerShown
    })
  }

  // Create a method to update the 'numOfSets' key stored inside app state
  updateNumOfSets(e) {
    this.setState({
      numOfSets: e.target.value
    })
  }

  // Create a method to update the 'restPauseLength' key stored inside app state
  updateRestPauseLength(e) {
    this.setState({
      restPauseLength: e.target.value
    })
  }

  // Create the main render method
  render() {
    return (
      <div>
        <h1>Grease the Groove!</h1>

        <p>Are you ready to get stronger?</p>

        {/* Button to open/close the settings div */}
        <a href="#" onClick={(e) => this.toggleSettings(e)}>Settings</a>

        {/* Button to show/hide the Timer */}
        <a href="#" onClick={(e) => this.toggleTimer(e)}>Timer</a>

        {/* If the value of `isSettingsOpen` is true, open settings. */}
        {this.state.isSettingsOpen && <div className="settings">
          <p>How many sets do you want to do?</p>

          {/* Number input to let the user specify the number of sets he wants to do in a day. */}
          <input type="number" placeholder={this.state.numOfSets} onChange={(e) => this.updateNumOfSets(e)} />

          <p>How long should the rest pause be (in minutes)? You can use decimal numbers for seconds, i.e.: 0.2 for 12s.</p>

          {/* Number input to let the user specify the rest pause between sets. */}
          <input type="number" value={this.state.restPauseLength} onChange={(e) => this.updateRestPauseLength(e)} />
        </div>}

        {/* If the value of `isTimerShown` is true, show timer */}
        {/* and provide the timer with data about the length of the rest pause,
        stored inside app state via 'pauseLength' prop */}
        {/* Timer is not implemented yet */}
        {/* this.state.isTimerShown && <Timer pauseLength={this.state.restPauseLength} /> */}

        {/* Create list of sets to do */}
        <ul>
          {this.generateSetsList()}
        </ul>
      </div>
    )
  }
}

// Export the main component
export default App
```

And, that's all we need before we can run our electron app. So, let's finally see the results of our work and run it for the first time. We can run the "dev" version of our electron app by using `yarn run dev` or `npm run dev`.

## Closing thoughts on building an electron app

Congratulations! You just finished the third part of this mini series. And, what's even more important, you finally had the first chance to actually run the app and see the fruits of your labor. Well, unless something unexpected happened. In that case, double-check your code and make sure there is not some typo in it. If that doesn't help, check if your project structure is correct and if you have installed all dependencies. CMD and console will help solve most of the issues. If the problem persists, let me know.

Now, what will be our job the fourth part? A couple of things. First, we will create component for Timer and implement it. Next, we create another component for both, visual and sound, notifications. After that, we will work on styles and polish the UI. Until then, get ready because we will have a lot of work to do.

Do you have any questions, recommendations, thoughts, advice or tip you would like to share with other readers of this blog, and me? Great! Please share it in a comment. Or, if you want to keep things more "private", feel free to contact me on [Twitter] or send me a [mail]. I would love to hear from you.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[part 1]: https://blog.alexdevero.com/electron-app-pt1/
[part 2]: https://blog.alexdevero.com/electron-app-pt2/
[second part]: https://blog.alexdevero.com/electron-app-pt2/
[Quick Start manual]: https://github.com/electron/electron/blob/master/docs/tutorial/quick-start.md
[electron-quick-start]: https://github.com/electron/electron-quick-start
[Twitter]: https://twitter.com/AlexDevero
[mail]: https://alexdevero.com/contact.html

<!--
#### Resources:
- build scripts for different platforms: https://www.christianengvall.se/electron-packager-tutorial/
-->
