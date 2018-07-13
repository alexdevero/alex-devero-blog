# How I Built My First [Electron App] & You Can Too Pt.5 – Polishing, Building & Shipping

Wanting to create an electron app is one thing. Shipping it is another. Today, we are going to finish our app and ship! We will start by improving the UI. We will use `styled-components` to create components for custom checkboxes and lists. Then, we will implement a simple top menu. After that, we will use `electron-packager` and setup npm scripts so we can create builds for our new electron app for all major platforms. With that, our app will be ready for release. Let's begin!
<!--
Table of Contents:
## Creating custom checkboxes
### It all starts with React
### ...And continues with a bit of CSS
## Polishing the list
## Adding a simple app menu
## Adding build scripts
## Closing thoughts on building an electron app
-->
How I Built My First Electron App & You Can Too [part 1].
How I Built My First Electron App & You Can Too [part 2].
How I Built My First Electron App & You Can Too [part 3].
How I Built My First Electron App & You Can Too [part 4].

As in previous parts, let me begin by quickly showing you the current folder structure of this project. It will make our work and moving, thourg the project, faster and easier. Whenever you will not know where to go, you can take a look here. So, here is the updated version of the file structure. And, with that, we can now continue working on our electron app.

```
grease-the-groove-app
├── builds/
├── dist/
├── node_modules/
├── src/
│   └── app/
│       └── components/
│           └── Timer.jsx
│       └── App.jsx
│   └── assets/
│       └── definite.mp3
│       └── grease-the-groove-icon.icns
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

## Creating custom checkboxes

AS the first thing, let's start with something that is easier and simpler. If you remember, one of the features of our electron app is showing the user how many sets there is to do, through the day. We implemented this feature in the [third part] by using a simple `checkbox` with `span` as a label both wrapped inside a real `label`. Our solution works well. Well, it is hard to screw something up on a `checkbox` and `label`. The only issue is that native checkboxes look quite bad.

### It all starts with React

The good news is that we can fix this with just a little bit of CSS. So, let's use `styled-components` and create new React component for custom checkbox. First, we will need to change the structure of our code. At this moment, the `checkbox` element is wrapped inside the `label`, along with `span` wrapping up the text. If we want to make our custom checkbox work only with CSS, we will need to change the order of these elements.

First, we will replace the `label`, now the wrapper, with `span` and place the `checkbox` and `label` inside it. Make sure to put the `label` right after the `checkbox`. Otherwise, the CSS, and our custom checkbox, will not work. Next, we can work on the visual side. To do so, we will use `styled-components`. This also means that we will need to import this library, as well as `React` at the top of the file with our custom checkbox.

The whole React component for our custom `checkbox` will be composed of four parts: `CheckboxWrapper` (`span` element), HTML `input` (`checkbox`) and `CheckboxLabel` (`label` element). In addition, this component will accept two parameters: `id` and `label`. We will use the `id` to generate unique value for `htmlFor` attribute for the `label` as well as for `id` and `name` attributes for the `checkbox`. Content pass via `label` will be rendered inside the `label` as a text.

### ...And continues with a bit of CSS

The way our custom checkbox will work is very simple. First, we will hide the original HTML `checkbox` element. Then, we will use CSS `::before` and `::after` pseudo-elements to create our custom checkbox. The `::before` will be for checkbox and `::after` for check mark. Finally, we will "watch" for `:checked` and `:not(:checked)` "states" of the real HTML `checkbox` to switch between different CSS styles for `::before` and `::after`.

Simply said, when checkbox is unchecked, we will show gray box (via `::before` pseudo-element). When it is checked, we will change the border color (via `::before` pseudo-element) and show checkmark (via `::after` pseudo-element). The final code will look like this.

```
// Checkbox component

// Import React library
import React from 'react'

// Import styled-components
import styled from 'styled-components'

const CheckBoxWrapper = styled.span`
  & [type=checkbox]:not(:checked) + label::after,
  & [type=checkbox]:checked + label::after,
  & [type=checkbox]:not(:checked) + label::before,
  & [type=checkbox]:checked + label::before {
    position: absolute;
    transition: all .2s;
  }

  & [type=checkbox]:not(:checked) + label::before,
  & [type=checkbox]:checked + label::before {
    content: '';
    top: 0;
    left: 0;
    width: 18px;
    height: 18px;
    background: #fff;
    border: 1px solid #ccc;
    border-radius: 4px;
  }

  & [type=checkbox]:not(:checked) + label::after,
  & [type=checkbox]:checked + label::after {
    top: 4px;
    left: 3px;
    content: '\u2714';
    font-family: Arial, sans-serif;
    font-size: 18px;
    line-height: 0.8;
    color: #ff8b09;
  }

  & > [type=checkbox]:not(:checked) + label::after {
    opacity: 0;
    transform: scale(0);
  }

  & > [type=checkbox]:checked + label::after {
    opacity: 1;
    transform: scale(1.15);
  }

  & > [type=checkbox]:checked + label::before,
  & > [type=checkbox] + label:hover::before {
    border: 1px solid #ff8b09;
  }
`

const CheckboxLabel = styled.label`
  position: relative;
  padding-left: 1.95em;
  cursor: pointer;
`

const Checkbox = ({id, label}) => {
  return(
    <CheckBoxWrapper>
      <input id={id} name={id} type="checkbox" hidden />

      <CheckboxLabel htmlFor={id} id={id} name={id} type="checkbox">{label}</CheckboxLabel>
    </CheckBoxWrapper>
  )
}

export default Checkbox
```

Now, we can put this code into a new file called `Checkbox.jsx` and put this file into `src\app\components\`. Then, we can import it into it into the main file for our electron app, the `App.js` inside `src\app\`. After that, we can replace the code for the HTML `checkbox` with this component. One more thing, make sure to pass some data for the `id` and `label` arguments.

```
// App.jsx
// Import React library
import React from 'react'

// Import checkbox
import Checkbox from './components/Checkbox'

// Import timer
import Timer from './components/Timer'

// Create the main component for our electron app
class App extends React.Component {

  // ... previous code

  // Create a method for generating list of items, one for one set we want to do
  // each item will contain checkbox and label
  generateSetsList() {
    // Prepare empty array for list items
    let setsItems = []

    // Generate number of list items based on 'numOfSets'
    for(let i = 0; i<this.state.numOfSets; i++) {
      setsItems.push(<li key={i}>
        {/* */}
        {/* NEW CHECKBOX COMPONENT GOES HERE: */}
        {/* */}
        <Checkbox
          id={`set${i}`}
          label={`Set number ${i+1}`}
        />
      </li>)
    }

    // Return the array with list items
    return setsItems
  }

  // ... the rest of the code
}
```

## Polishing the list

This one will be very quick. We will remove the default bullet points and `padding` and add some `margin` to the top. Then, we will also apply some `margin` between `list items`. After that, we will export our new `List` component as default. Finally, we will import the list in the `App.jsx` file, just like we did with `Checkbox` component. We are creating the `List` component as a pure set of styles, by using `styled-components`. So, we don't need or have to import `React`.

```
// List component - List.jsx
// Import only styled-components
import styled from 'styled-components'

const List = styled.ul`
  padding: 0;
  margin: 18px 0 0;
  list-style-type: none;

  li + li {
    margin-top: 12px;
  }
`

export default List
```

```
// App.jsx
// Import React library
import React from 'react'

// Import checkbox
import Checkbox from './components/Checkbox'

// Import lists
import List from './components/List'

// Import timer
import Timer from './components/Timer'

// Create the main component for our electron app
class App extends React.Component {

  // ... previous code

  // Create the main render method
  render() {
    return (
      <div>

        {/* ... previous code */}

        {/* Create list of sets to do */}
        {/* */}
        {/* NEW LIST COMPONENT GOES HERE: */}
        {/* */}
        <List>
          {this.generateSetsList()}
        </List>
      </div>
    )
  }
}

// Export the main component
export default App
```

## Adding a simple app menu

You probably noticed this. When we run the dev version of our electron app, with `npm run dev`, there is a native menu at the top of the window. However, when we build the production version of our electron app, this menu is no longer present. This is not such a problem unless we have some useful options for the user that could be inside the menu. For example, we may add an option to reload the app, change zooming, visit documentation or website dedicated to the app and so on.

So, let's implement a simple menu as one of the last things we will do in this tutorial. There is a number of steps we have to do if we want to create this menu. Since we already have `Menu` module imported, we don't need to import it again. We used it for implementing tray icon. Instead, we can skip this step and go to the step number two. This second step is about creating a template for the menu. This template will be an `array` of objects. Each object is for one main group of items in the menu.

For example, the dev version of our electron app has following main groups in the menu: "File", "Edit", "View", "Window" and "Help". Each of these objects (menu groups) contains a `label` or `role` key and specific value for this key. In case of `label`, the value is a text that will be shown. Next, there is a second key, `submenu`. This contains an `array` of object, one object for one item in the dropdown. And, inside this object is again `label` or `role` key (role for something native to electron) and specific value for this key.

If it is something native to electron, `role` key and value is all we need. Otherwise, we use key `label` with some text to be shown as a value and something else. For example, we can add a method for `click` event. It may not make too much of a sense now, but it will get better when you will see the code. Let's call this variable `menuTemplate`. The third step is using the `Menu` module we imported and one of its methods, namely `buildFromTemplate`. We will pass the variable with the template of our menu as an argument and store everything inside another variable, `menu`.

The fourth step is using the `Menu` module again, and now with `setApplicationMenu` method passing the variable we created in the previous, third, step. Now, when we run our electron app, we should see our new menu in place, in both dev and production version (build). One more thing. We will put the code for the menu into `main.js` file right inside the root directory and inside the `createWindow` function. Let's take a look at the code.

```
// main.js
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


  //
  // TEMPLATE FOR APP MENU BEGINNING
  //
  const menuTemplate = [
    {
      label: 'Edit',
      submenu: [
        {role: 'undo'}, // Native electron features
        {role: 'redo'}, // Native electron features
        {role: 'cut'}, // Native electron features
        {role: 'copy'}, // Native electron features
        {role: 'paste'}, // Native electron features
        {role: 'delete'} // Native electron features
      ]
    },
    {
      label: 'View',
      submenu: [
        {role: 'reload'}, // Native electron features
        {role: 'forcereload'}, // Native electron features
        {role: 'resetzoom'}, // Native electron features
        {role: 'zoomin'}, // Native electron features
        {role: 'zoomout'} // Native electron features
      ]
    },
    {
      role: 'window',
      submenu: [
        {role: 'minimize'}, // Native electron features
        {role: 'close'} // Native electron features
      ]
    },
    {
      role: 'help',
      submenu: [
        {
          label: 'Documentation',
          click: () => {require('electron').shell.openExternal('https://url.com/documentation')} // Opens a URL in a new window
        },
        {
          label: 'FAQ',
          click: () => {require('electron').shell.openExternal('https://url.com/faq')} // Opens a URL in a new window
        },
        {
          label: 'Issues',
          click: () => {require('electron').shell.openExternal('https://url.com/issues')} // Opens a URL in a new window
        }
      ]
    }
  ]

  // Build app menu from menuTemplate
  const menu = Menu.buildFromTemplate(menuTemplate)

  // Set menu to menuTemplate - "activate" the menu
  Menu.setApplicationMenu(menu)

  //
  // TEMPLATE FOR APP MENU END
  //


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

## Adding build scripts

Now, the final thing. All users should be able to use our electron app, regardless of what operating system they use. So, let's add build scripts for all major platforms, Linux, OSX (also Mac App Store, or mas) and Windows. To do this, we will add one script for each platform into `package.json`. Then, we will also add one additional script that will build our electron app for all platforms at once.

We will use `electron-packager` to create a build for each platform via `--platform` flag, with specific icon via `--icon` flag into a specific directory via `--out`. And, we will also use `--overwrite` flag. This flag will force `electron-packager` to always overwrite any existing builds. One thing about icons. To make sure all platforms has working icon, we will need three formats: `png` for icon in the dock, `incs` for OS X and `ico` for Windows.

Fortunately, we don't need to specify the icon format for every build. All we need to do is just specify the name of the icon image and its location. `electron-packager` will do the rest of the work for us and use proper icon for every build. Let's take a look at the final version of `package.json`.

```
// package.json
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
    "package:all": "npm run build && electron-packager ./ --out=./builds --overwrite --platform=all --icon=src/assets/grease-the-groove-icon",
    "package:linux": "npm run build && electron-packager ./ --out=./builds --overwrite --platform=linux --icon=src/assets/grease-the-groove-icon",
    "package:macappstore": "npm run build && electron-packager ./ --out=./builds --overwrite --platform=mas --icon=src/assets/grease-the-groove-icon",
    "package:osx": "npm run build && electron-packager ./ --out=./builds --overwrite --platform=darwin --icon=src/assets/grease-the-groove-icon",
    "package:win": "npm run build && electron-packager ./ --out=./builds --overwrite --platform=win32 --icon=src/assets/grease-the-groove-icon",
    "prod": "npm run build && electron --noDevServer ."
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

## Closing thoughts on building an electron app

This is it! You just finished the fifth and final part of this mini series and created our first electron app. Congratulations! You've done a lot of work today, as well as in the previous parts. Thanks to your effort and patience, your first electron app not only works well, it also looks, or let's say decently. What's more, you had a lot of opportunities to practice, or learn about, React and styled-components libraries and electron framework. Still, the best part is that you have something you can be proud of, your first electron app!

This is also one of the reasons why I believe that learning by doing is simply the best. There is no another way that will help you learn something in such a speed, and have something tangible, something you can show, at the end. Thanks to that, no matter how hard the learning process could be, there is still that good feel when you can see some results of your work, such as the electron app we were working on through this mini series.

This mini series showed you how you how to build a small and simple electron app. So, my final question is following. What is next for you? I hope this will be only the first app you built, that you will take one of your ideas and turn them into a real thing, real app. Remember, learning is not enough and knowledge that is not used is, well, useless. So, take what you learned in this mini series and start new project. Build some cool electron app!

One final note. I was writing this mini series while working on a real version of the electron app called Grease the Groove, or GtG. You can find it on [GitHub] and [npm].

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[part 1]: https://blog.alexdevero.com/electron-app-pt1/
[part 2]: https://blog.alexdevero.com/electron-app-pt2/
[part 3]: https://blog.alexdevero.com/electron-app-pt3/
[part 4]: https://blog.alexdevero.com/electron-app-pt4/
[third part]: https://blog.alexdevero.com/electron-app-pt3/
[GitHub]: https://github.com/alexdevero/grease-the-groove-app
[npm]: https://www.npmjs.com/package/grease-the-groove-app

<!-- ### Inspiration
-
-->
