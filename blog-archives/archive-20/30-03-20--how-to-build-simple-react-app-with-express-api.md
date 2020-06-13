# How to Build a Simple React App With Express API
Have you ever wanted to build React app with express API? This tutorial will show you how. You will learn how to create a simple React app and how to fetch data from different API endpoints. Then, you will learn how to build API with Express.js, how to create controllers and routes and how to implement them.<!--more-->
<!--
Table of Contents:
## Introduction
## Project structure
## Creating React app
### App component
### Index
### Styles
## Updating project workflow
### Adding dependencies
### Adding npm scripts
### Setting proxy
### Creating build script
## Building Express backend
### Adding mock data
### Creating Controllers
### Creating Routes
### Building the server
## Conclusion: How to build React app with express API
-->

## Introduction

The goal of this tutorial is to show you how to build React app with Express. To be more specific, you will learn three things. The first thing is how to create React app. The second thing is how to create Express API. The third thing is how to connect the React app with Express API.

## Project structure

To keep everything tidy we will keep the whole app in a single directory. This directory will contain three folders: `public` for static files, `server` for express server and `src` for React app. The `server` directory will also contain three folders: `controllers` for API controllers, `routes` for API endpoints and `data` for mock data.

Aside to these folders there will be `server.js` file. This file will contain the configuration for your express server. The `src` directory will contain two folders: `components` for React components and `css` for styles. On the root level, there will be main file for your React app, the `index.js`.

If you use TypeScript in source folder will also be `react-app-env.d.ts` for TypeScript definitions and `tsconfig.json`. At least if you decide to generate your React app using `create-react-app` and TypeScript template. The last file in root directory will be `buildScript.js`. This file contains script for building the React app and moving it to server directory.

```
react-express-app/
├─ node_modules
├─ public
│ ├─ favicon.ico
│ ├─ index.html
│ ├─ logo192.png
│ ├─ logo512.png
│ ├─ manifest.json
│ └─ robots.txt
├─ server
│ ├─ controllers
│ │ ├─ home-controller.js
│ │ └─ users-controller.js
│ ├─ data
│ │ └─ users.json
│ ├─ routes
│ │ ├─ home-route.js
│ │ └─ users-route.js
│ └─ server.js
├─ src
│ ├─ components
│ │ └─ app.tsx
│ ├─ css
│ │ └─ index.css
│ ├─ index.tsx
│ ├─ interfaces.ts
│ ├─ react-app-env.d.ts
│ └─ serviceWorker.ts
├─ .env.development
├─ buildScript.js
├─ package.json
└─ tsconfig.json
```

*Note: If you don't want the browser to automatically open every time you start your app there is a way to stop this. Create `.env.development` file in the root directory of your app, where is `package.json`. Inside this file write add `BROWSER=none`.*

## Creating React app

Let's start with the front-end part, the React app as first. The fastest way to do this is by using [create-react-app]. Using this boilerplate is very easy. If you use npm you can use `npm init react-app react-express-app --typescript`. Another option is using `npx`. This will allow you to use the boilerplate without installing it.

To use `npx` use `npx create-react-app react-express-app --typescript` command. If you use yarn use `yarn create react-app react-express-app --typescript`. I will be using [TypeScript], a superset of JavaScript. However, you don't have to use it if you don't want. If you don't want to use it, omit the `--typescript` flag at the end of chosen command.

### App component

For the purpose of this tutorial, we will do the work mostly in just one component, the `App`. Inside it, we will use `useState` to store short welcome message and array with users. We will fetch both these information from our express API. For fetching the data we will use native [fetch API].

When the components mounts, we will always fetch the welcome message. To do this, we will create `fetchApi` function. Next, we will use `useEffect()` react hook and call `fetchApi()` from there. To ensure this hook will fire only once, on initial render, we will pass `[]` into the `useEffect()` hook as the second argument.

Unlike fetching the welcome message fetching users will not be automatic. Instead, we will create `fetchUsers()` function and add is as `onClick` handler on a button. So, when you click the button, app will fetch specific endpoint for users and update app `state`. This will mount simple table component listing all users and their data.

```JavaScript
// src/components/app.tsx

// Import necessary dependencies
import React, { useEffect, useState } from 'react'

// Create interface for user object (TypeScript only)
interface UserUI {
  id: string;
  username: string;
  name: string;
  email: string;
}

// Create App component
function App() {
  // Prepare state hook for welcome message
  const [welcomeMessage, setWelcomeMessage] = useState('')

  // Prepare state hook for users list
  // Note: <UserUI[]> is for TypeScript
  // It specifies the shape of usersList state
  const [usersList, setUsersList] = useState<UserUI[]>([])

  // Create async function for fetching welcome message
  const fetchMessage = async () => {
    // Use Fetch API to fetch '/api' endpoint
    const message = await fetch('/api')
      .then(res => res.text()) // process incoming data

    // Update welcomeMessage state
    setWelcomeMessage(message)
  }

  // Use useEffect to call fetchMessage() on initial render
  useEffect(() => {
    fetchMessage()
  }, [])

  // Create async function for fetching users list
  const fetchUsers = async () => {
    const users = await fetch('/users/all')
      .then(res => res.json()) // Process the incoming data

    // Update usersList state
    setUsersList(users)
  }

  return (
    <div className="app">
      <header className="app-header">
        {/* Display welcome message */}
        <p>{welcomeMessage}</p>

        {/* Button to fetch users data */}
        <button onClick={fetchUsers}>Fetch users</button>

        {/* Display table of users after fetching users data */}
        {usersList.length > 0 && <table>
          <thead>
            <tr>
              <th>ID</th>
              <th>Username</th>
              <th>Name</th>
              <th>Email</th>
            </tr>
          </thead>

          <tbody>
            {usersList.map((user: UserUI) => (
              <tr key={user.id}>
                <td>{user.id}</td>
                <td>{user.username}</td>
                <td>{user.name}</td>
                <td>{user.email}</td>
              </tr>
            ))}
          </tbody>
        </table>}
      </header>
    </div>
  )
}

export default App
```

Note that the `fetchMessage()` uses `text()` to process data from API while the `fetchUsers()` uses `json()`. This is on purpose. The "/api" endpoint, we are going to create, returns a simple text. The "/users/all" returns a json. Make sure to use correct method. Otherwise, you will run into issues.

### Index

The `index.tsx` will stay pretty much the same as the default created by `create-react-app` boilerplate.

```JavaScript
// src/index.tsx

// Import necessary dependencies
import React from 'react'
import ReactDOM from 'react-dom'

// Import App component
import App from './components/app'

// Import styles
import './css/index.css'

// Import service workers
import * as serviceWorker from './serviceWorker'

// Render App component in the DOM
ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
  , document.getElementById('root')
)

// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: https://bit.ly/CRA-PWA
serviceWorker.unregister()
```

### Styles

In case of styles, we will add some general styles and resets such as proper `box-sizing`, no `margin` on `body`, font settings and some styles for users table. Other than that, feel free to add your own CSS styles to change how the React apps looks like.

```css
/* src/css/index.css */

/* General styles & resets */
html,
*,
*::before,
*::after {
  box-sizing: border-box;
}

html {
  font-size: 16px;
}

body {
  margin: 0;
  font: 1rem -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', 'Oxygen',
    'Ubuntu', 'Cantarell', 'Fira Sans', 'Droid Sans', 'Helvetica Neue',
    sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

/* Layout styles */
.app {
  text-align: center;
}

.app-header {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-size: calc(10px + 2vmin);
  color: #222;
}

/* Table styles */
table th,
table td {
  padding: 8px;
  font-size: 16px;
  text-align: left;
}
```

## Updating project workflow

The front-end part of our React app is ready. Now, before we start working on the API, the express sever, we need to make some updates to our workflow. We need to add some new dependencies and scripts.

### Adding dependencies

The first thing we will need is to add new dependencies necessary for express API. The most important dependency is `express`. Then, we will also add some middleware. Middleware are functions that help you execute some very useful tasks in a very easy way. For example, they can help you parse request bodies, add response headers, compress HTTP responses, enable CORS, HTTPS and more.

The middleware we will add, and use, will be `body-parser` (parses HTTP request body), `compression` (compresses HTTP responses), `cookie-parser` (parses cookie header and populates req.cookies), `cors` (enables CORS) and `helmet` (enables HTTPS). Take a look at [express docs] for the full list of available middleware.

```bash
npm i express body-parser compression cookie-parser cors helmet

# or
yarn add express body-parser compression cookie-parser cors helmet
```

Aside to these we will also add some additional useful dependencies. These are `concurrently`, `cross-env` and `nodemon`. The `concurrently` will help us run multiple npm scripts at once. This is useful if you want to run your React app and express API at once in one terminal window.

The `cross-env` makes it easier to set, and use, Node environment variables that work on all platforms. Lastly, the `nodemon`. This dependency will make it easier to develop the express server because it can watch for changes in specific files or directories.

So, when you change something, you don't have to restart the server. `nodemon` will automatically refresh/restart the server so you can continue working.

```bash
npm i -S concurrently cross-env nodemon

# or
yarn add -D concurrently cross-env nodemon
```

```json
// /package.json
// ...
"dependencies": {
  "body-parser": "1.19.0",
  "compression": "^1.7.4",
  "cookie-parser": "^1.4.5",
  "cors": "2.8.5",
  "express": "4.17.1",
  "helmet": "^3.22.0",
  "react": "16.13.1",
  "react-dom": "16.13.1"
},
"devDependencies": {
  "@testing-library/jest-dom": "4.2.4",
  "@testing-library/react": "9.4.0",
  "@testing-library/user-event": "7.2.1",
  "@types/jest": "24.9.1",
  "@types/node": "13.9.5",
  "@types/react": "16.9.26",
  "@types/react-dom": "16.9.5",
  "concurrently": "5.1.0",
  "cross-env": "^7.0.2",
  "nodemon": "2.0.2",
  "react-scripts": "3.4.1",
  "typescript": "~3.8.3"
}
// ...
```

### Adding npm scripts

At this moment, your `package.json` contains only scripts for running, building, testing and ejecting the React app. We also need to add scripts for running express server, running both, the server and also the app in parallel and also for building the app.

First we will rename current script for running React app, the `start`, to `start-front`. The script for building, the `build`, to `build-front`. Next, we will add script for running the express server, `start-server`. This script will use `cross-env` to set Node environment variable and `nodemon` to run, and watch, the server.

Main task for building the app will be `build`. This will use Node to execute scripts in `buildScript.js`.

```json
// /package.json
// ...
"scripts": {
  "build": "node ./buildScript",
  "start-server": "cross-env NODE_ENV=development nodemon server/server.js --watch server/*",
  "start-front": "react-scripts start",
  "build-front": "react-scripts build",
  "eject": "react-scripts eject",
  "test": "react-scripts test",
  "start": "concurrently \"npm run start-server\" \"npm run start-front\" --kill-others"
},
// ...
```

### Setting proxy

There is one more thing to do. We need to add `proxy`. This will allow us to redirect any requests, such as fetching data, to our API to specific host and port. The important thing here is to use the same host and port your express is running on. In this tutorial we will run our express app on `http://localhost:4000`.

We need to use the same host and port and set it as `proxy` in `package.json`. Now, when we try to fetch `/users/all` app will automatically fetch `http://localhost:4000/users/all`.

```json
// ...
"proxy": "http://localhost:4000"
// ...
```

The whole `package.json` looks like this:

```json
// /package.json

{
  "name": "react-express-app",
  "version": "1.0.0",
  "private": true,
  "eslintConfig": {
    "extends": "react-app"
  },
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  },
  "proxy": "http://localhost:4000",
  "scripts": {
    "build": "node ./buildScript",
    "start-server": "cross-env NODE_ENV=development nodemon server/server.js --watch server/*",
    "start-front": "react-scripts start",
    "build-front": "react-scripts build",
    "eject": "react-scripts eject",
    "test": "react-scripts test",
    "start": "concurrently \"npm run start-server\" \"npm run start-front\" --kill-others"
  },
  "dependencies": {
    "body-parser": "1.19.0",
    "compression": "^1.7.4",
    "cookie-parser": "^1.4.5",
    "cors": "2.8.5",
    "express": "4.17.1",
    "helmet": "^3.22.0",
    "react": "16.13.1",
    "react-dom": "16.13.1"
  },
  "devDependencies": {
    "@testing-library/jest-dom": "4.2.4",
    "@testing-library/react": "9.4.0",
    "@testing-library/user-event": "7.2.1",
    "@types/jest": "24.9.1",
    "@types/node": "13.9.5",
    "@types/react": "16.9.26",
    "@types/react-dom": "16.9.5",
    "concurrently": "5.1.0",
    "cross-env": "^7.0.2",
    "nodemon": "2.0.2",
    "react-scripts": "3.4.1",
    "typescript": "~3.8.3"
  }
}
```

### Creating build script

I briefly mentioned that we will use customs script to build the React app. We will use this script in npm `build` script. Put simply, what this script does is it runs `react-scripts build` and then copies the whole build of the React app to "./server/build" directory.

```JavaScript
// /buildScript.js

const fs = require('fs')
const fse = require('fs-extra')
const childProcess = require('child_process')

if (fs.existsSync('./build')) {
  fse.removeSync('./build')
}

// Run 'react-scripts build' script
childProcess.execSync('react-scripts build', { stdio: 'inherit' })

// Move app build to server/build directory
fse.moveSync('./build', './server/build', { overwrite: true })
```

## Building Express backend

Okay. React app is ready and dependencies and scripts are ready as well. It is time to create our simple express sever. Let's get started.

### Adding mock data

As you remember, the app contains function to fetch list of users. We need to get those data from somewhere. For the sake of simplicity, we will create a short json, in `data` directory, containing data of couple of users. When the React app fetch the `/users/all` endpoint, our express app will send this json as a response.

```json
// server/data/users.json
[
  {
    "id": "u0001",
    "name": "Leanne Graham",
    "username": "bret",
    "email": "Sincere@april.biz"
  },
  {
    "id": "u0002",
    "name": "Ervin Howell",
    "username": "antonette",
    "email": "Shanna@melissa.tv"
  },
  {
    "id": "u0003",
    "name": "Clementine Bauch",
    "username": "samantha",
    "email": "Nathan@yesenia.net"
  },
  {
    "id": "u0004",
    "name": "Patricia Lebsack",
    "username": "karianne",
    "email": "Julianne.OConner@kory.org"
  },
  {
    "id": "u0005",
    "name": "Chelsey Dietrich",
    "username": "kamren",
    "email": "Lucio_Hettinger@annie.ca"
  }
]
```

### Creating Controllers

Next are controllers. One easy way to think about controllers is to imagine functions used to process requests on API endpoints. When your React app fetch some endpoint the response will be created by these functions, or controllers. For now, we will create two controllers, one for home (`/api` endpoint) and one for users (`/users` endpoint).

The controller for home will be very simple. It will contain only one function. This function will be used to process `GET` request to `/api` endpoint. As a response, it will send a simple message. This is the welcome message displayed in React app after `App` component mounts. It is where we use `.text()` to process the data from API.

```JavaScript
// server/controllers/home-controller.js

// Create controller for GET request to '/api'
exports.homeGet = async (req, res) => {
  res.send('Welcome back commander.')
}
```

Controller for users will look like the previous. It will contain one functions to process `GET` requests. It will process request to `/users/all` endpoint. It will take the list of users, stored in `users.json`, and send it in json format as a response. This is the data we use to render the table of users. It is also where we use `.json()` to process the data from API.

```JavaScript
// server/controllers/home-controller.js

// Import json with list of users
const users = require('./../data/users.json')

// Create controller for GET request to '/users/all'
exports.usersGetAll = async (req, res) => {
  // res.send('There will be dragons, not posts.')
  res.json(users)
}
```

### Creating Routes

When we have controllers. Now, we need to create routes. These routes will use specific controllers on specific API endpoints. Every request the React sends first goes through a route created for specific endpoint and type of request. It then applies correct controller that then handles the response.

We will need to create two routes, one for home (`/api` endpoint) and one for users (`/users` endpoint). In each router, we will import `express` framework and use it to create new [router]. We will then use this router, and `get` method, to will handle `GET` request coming to `/` endpoint.

It is also this router method, `get` in this case, that specifies which controller should be used on which endpoint. For the home (`/api` endpoint) we will set the router method to use the `homeGet` controller. As the last thing, we will export the router so we can later import it and use it in main server file.

```JavaScript
// Import express
const express = require('express')

// Import home controller
const homeControllers = require('../controllers/home-controller.js')

// Create express router
const router = express.Router()

// Create rout between homeControllers and '/' endpoint
router.get('/', homeControllers.homeGet)

// Export router
module.exports = router
```

The router for users (`/users` endpoint) will look almost like the endpoint for home (`/api`). The difference is that now we will import `usersController` and `usersGetAll()` controller we created previously. Then, we will create new route for `/all` endpoint.

One important thing to remember is that we don't use `/users/all` here, but only `/all` even though we are actually creating route for `/users/all`. The reason is that when we implement this router in the express app, in `server.js`, we implement it for `/users` endpoint.

The result of this is that all users routes defined here will be basically "prefixed" with "/users". So, if we create route for `/all` endpoint here it will become `/users/all`. Express will automatically add the "/users" to the `/all` route.

This is why, in the React app, we fetch `/users/all` endpoint instead of fetching `/all` endpoint and it works.

```JavaScript
// Import express
const express = require('express')

// Import users controller
const usersController = require('./../controllers/users-controller.js')

// Create express router
const router = express.Router()

// Create rout between usersController and '/all' endpoint
// Note:
// Main route (in server.js) for users
// is set to '/users'
// This means that all users routes
// will be prefixed with /users'
// i.e.: '/all' will become '/users/all'
router.get('/all', usersController.usersGetAll)

// Export router
module.exports = router
```

### Building the server

You are in the finale. This is the last thing we need to do to get our express server up and running. Now, we need to do few things. First, we will import express framework and middleware dependencies. Next, we import both routers, for home and users. After that, we will create variable for default port and create express app.

When we have this we can implement all middleware we have. We can do this by using `app` and its `use()` method. Here, middleware is passed as an argument. One thing to remember. We need to implement middleware before we implement routes, if we want the middleware to be applied on those routes. Put simply, middleware has to be placed above routes.

When we are done with applying middleware we can implement both routers. We do this also by using `app` and its `use()` method. In the case of routers, we will pass two arguments. The first will be the endpoint, i.e. `/api` and `/users`. The second argument will be router that should be used on each route.

The last thing we have to do is to launch this express server. This is done by using `app` and `listen()` method. This method takes one parameter, which is a port where the server should be running. You can also pass optional callback function. This can be useful for logging message that says that server started and where.

```JavaScript
// Import express framework
const express = require('express')

// Import middleware
const bodyParser = require('body-parser')
const cookieParser = require('cookie-parser')
const compression = require('compression')
const helmet = require('helmet')
const cors = require('cors')

// Import routes
const homeRouter = require('./routes/home-route')
const usersRouter = require('./routes/users-route')

// Setup default port
const PORT = process.env.PORT || 4000

// Create express app
const app = express()

// Implement middleware
app.use(cors())
app.use(helmet())
app.use(compression())
app.use(express.json())
app.use(express.urlencoded({ extended: false }))
app.use(cookieParser())
app.use(bodyParser.json())

if (process.env.NODE_ENV && process.env.NODE_ENV !== 'development') {
    app.get('*', (req, res) => {
      res.sendFile('build/index.html', { root: __dirname })
  })
}

// Implement route for '/api' endpoint
app.use('/api', homeRouter)

// Implement route for '/users' endpoint
// ! Note:
// '/users' will prefix all post routes
// with '/users' => '/all' will become '/users/all'
app.use('/users', usersRouter)

// Implement route for errors
app.use((err, req, res, next) => {
   console.error(err.stack)

   res.status(500).send('Something broke!')
})

// Start express app
app.listen(PORT, function() {
  console.log(`Server is running on: ${PORT}`)
})
```

## Conclusion: How to build React app with express API

Congratulations, you've just built your own React app with express! I hope you enjoyed this tutorial. Let's quickly recap what you did today. As the first thing, you created a simple React app. In this app, you created functions and used them, along with React hooks, to fetch data from different API endpoints and displayed these data.

Next, you extended the `create-react-app` boilerplate workflow with new scripts, dependencies and proxy. After that, you built the express server. You've created controllers, routes and implemented them, along with middleware, in your express app. Now, start your new React express app with `npm run start` or `yarn start` and build something.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[create-react-app]: https://github.com/facebook/create-react-app
[TypeScript]: https://typescript-play.js.org/
[fetch API]: https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch
[express docs]: https://expressjs.com/en/resources/middleware.html
[router]: https://expressjs.com/en/guide/routing.html

<!--
### Meta:
-
-->

<!--
#### Resources:
-
-->
