# How to Build an App with React, Express and SQLite
This tutorial will show you how to build your own app with React, Express and SQLite. First, you will create SQLite database. Next, you will create express server and connect it with the database. After that, you will build a React app, use `axios` to send requests to the server and use React hooks to store received data.<!--more-->
<!--
Table of Contents:
## Introduction
## Project structure
## Dependencies and package.json
## TypeScript and tsconfig
## SQLite Database
## Express
### Controllers
### Routes
### Express server
## React
### BookshelfListRow component
### BookshelfList component
### Bookshelf component
### Index
## Styles
### Bookshelf list styles
### Bookshelf styles
### General styles
## Conclusion: How to build an app with React, Express and SQLite
-->

Code for this tutorial is available on [GitHub].

## Introduction

This tutorial will consist of four steps. In the first step, you will learn how to create SQLite database. In the second step, you will learn how to create API with express. You will create necessary API endpoints for our app and setup the server. In the third step, you learn how to create simple React app, a bookshelf.

You will create few small functional components. Next, you use `useEffect` hook to automatically fetch express API, and database. Then, you will use `useState` hook to store the data you received from the server. You will also use `useState` hook to store data about the book you want to add. You will then send these data to express server and store them in the database.

When this is done, the app will fetch the API again to refresh the data, i.e. books, displayed on the bookshelf list. In the last step, you will create a simple `index.html` file where you will render the bookshelf React app. Now, let's take a look at the structure of this project.

## Project structure

All parts of this project, the server, database and React app will be in one directory, a "bookshelf-app". Files related to server will be in "server" directory. The files related to database will be also inside "server". Specifically, the SQLite database itself, `database.sqlite`, will be inside "db" directory inside "server". The config file for the DB, `db.js`, will be in root "server" directory.

The React app will be in "src" directory. This might not be the proper name for the front-end app. The reason for this name is that we will use [react-scripts] to run and build the React app. These scripts are configured to look for "src" directory as place where the React app, the `index.js` or `index.tsx`, "lives".

Related to the React app, you will also need "public" directory. In this directory will be the main `index.html`. It is also here where you can add favicons for your app, manifest, robots, and other files. For the sake of this tutorial, we will add just the `index.html`. Also related to React app will be `react-app-env.d.ts`.

The `react-app-env.d.ts` file contains type reference for `react-scripts` for TypeScript. Although this tutorial will be written in [TypeScript] you can use JavaScript if you want. Aside to these files, there will also be `buildScript.js` file which will contain build script for this app. Next will be `tsconfig.json` with configuration for TypeScript and `package.json` with project info and list of dependencies.

One more thing. When you start the Rect app it always automatically opens browser window. If you want to stop this behavior, create `.env.development` file in the root directory of your app, i.e. right in "bookshelf-app". Inside this file, add `BROWSER=none`.

```
bookshelf-app/
├─ node_modules
├─ public
│ ├─ index.html
├─ server
│ ├─ controllers
│ │ └─ books-controller.js
│ ├─ db
│ │ └─ database.sqlite
│ ├─ routes
│ │ └─ books-route.js
│ ├─ db.js
│ └─ server.js
├─ src
│ ├─ components
│ │ ├─ bookshelf-list-row.tsx
│ │ ├─ bookshelf-list.tsx
│ │ └─ bookshelf.tsx
│ ├─ css
│ │ ├─ bookshelf-list.css
│ │ ├─ bookshelf.css
│ │ └─ styles.css
│ ├─ index.tsx
│ └─ react-app-env.d.ts
├─ .env.development
├─ buildScript.js
├─ package.json
└─ tsconfig.json
```

## Dependencies and package.json

Before we start, let's ensure you have all dependencies you need to get this app up and ready. In root directory, the "bookshelf-app", create new file called `package.json` and paste the code below there, without the comment on the first line. Then, run either `npm i` or `yarn` to install all dependencies listed as `dependencies` and `devDependencies`.

```json
// bookshelf-app/package.json

{
  "name": "bookshelf-react-express-sqlite-app",
  "version": "1.0.0",
  "description": "App for collecting books built with React, Express and SQLite.",
  "private": false,
  "license": "MIT",
  "browserslist": [
    "last 7 versions",
    "not dead",
    "not ie <= 11",
    "not op_mini all"
  ],
  "main": "src/index.tsx",
  "prox": "http://localhost:4001",
  "scripts": {
    "build": "node ./buildScript",
    "build-front": "react-scripts build",
    "eject": "react-scripts eject",
    "start-server": "nodemon server/server.js --watch server/*",
    "start-front": "react-scripts start",
    "start": "concurrently \"npm run start-server\" \"npm run start-front\" --kill-others --kill-others-on-fail",
    "test": "react-scripts test --env=jsdom"
  },
  "dependencies": {
    "axios": "0.19.2",
    "body-parser": "1.19.0",
    "compression": "1.7.4",
    "cors": "2.8.5",
    "express": "4.17.1",
    "helmet": "3.22.0",
    "knex": "0.20.13",
    "react": "16.13.1",
    "react-dom": "16.13.1"
  },
  "devDependencies": {
    "@types/express": "4.17.6",
    "@types/react": "16.9.34",
    "@types/react-dom": "16.9.6",
    "concurrently": "5.1.0",
    "nodemon": "2.0.3",
    "react-scripts": "3.4.1",
    "sqlite3": "4.1.1",
    "typescript": "3.8.3"
  }
}
```

A quick explanation for all the dependencies. The `body-parser`, `compression`, `cors` and `helmet` are middleware for express app. The `express` is the main library for express framework. `axios` is a library we will use to send requests to express API. `react` and `react-dom` are main libraries for React framework.

Anything starting with "@types/" is a type definition for specific dependency for TypeScript. These are not necessary, but very useful for intellisense. We will use `react-scripts` to run and build the React app. `nodemon` is a monitoring library for node.js apps. It detects changes and automatically restarts the app. We will use this to run express server.

The `concurrently` will help us run scripts for express API and React app in parallel. `typescript` is necessary for writing the React app in TypeScript. Finally, the `sqlite3` and `knex`. `sqlite3` is a library containing SQLite bindings for node.js. Put simply, it allows node.js to work with SQLite database. The `knex`? `knex` will make it easier to work with the SQLite database.

## TypeScript and tsconfig

The code for this tutorial will use TypeScript. This is optional. If you want to stick to JavaScript, you can. Otherwise, add `tsconfig.json` file to provide TypeScript with some configuration. Below is the default `tsconfig.json` shipped with [create-react-app].

```json
// bookshelf-app/tsconfig.json

{
  "include": [
    "./src/*"
  ],
  "compilerOptions": {
    "lib": [
      "dom",
      "es2015"
    ],
    "jsx": "react",
    "esModuleInterop": true,
    "target": "es5",
    "allowJs": true,
    "skipLibCheck": true,
    "allowSyntheticDefaultImports": true,
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "module": "esnext",
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true
  }
}
```

And, for the `react-app-env.d.ts`:

```TypeScript
// bookshelf-app/src/react-app-env.d.ts

/// <reference types="react-scripts" />
```

## SQLite Database

In this tutorial, we will work with SQLite database. SQLite database might not be the fastest or the best. There are two reasons I chose SQLite database. First, SQLite database doesn't require installing any software on your computer. All you need is add npm dependency to your project and you are good to go.

Second, with SQLite database, you don't have to create an account for storing your database in the cloud. Even if it is for free, although with limited capabilities, it is still a redundant step. If you want to use other database, you can. Just replace the code in `db.js` with configuration you need and your React app will work.

That being said, let's create the SQLite database. First, you will need to import (require) two libraries, `knex` and `path`. With the help of `knex`, you will create the SQLite database. The `path` will help you import (require) file for the SQLite database. You will also need to create an empty file called `database.sqlite` in `bookshelf-app/server/db/`.

Next, you can use `path` to resolve the correct path to this file. Then, you can reference it in `knex` config object in `connection` as a `filename`. If you want to use other database than SQLite, that is also supported by `knex`, change the `knex` config object as you need. When you are done with this, you can create new table called "books" in the database, with all required columns.

For now, we will configure the database so that each row, or book, will contain four columns. These are `id`, `author`, `title`, `pubDate` and `rating`. The `id` will be used as the primary identifier and it will be automatically incremented with each new record, new book added. If you want to add, or remove, any information about books you can do it here.

Add new columns inside the `createTable` callback function, or remove any existing. When you are done with this, make sure export the database, i.e. the instance of `knex` stored in `knex` variable, so you can require it and use it in express. This is all you need to do in order to create and setup your new SQLite database.

```JavaScript
// bookshelf-app/server/db.js

// Import path module
const path = require('path')

// Get the location of database.sqlite file
const dbPath = path.resolve(__dirname, 'db/database.sqlite')

// Create connection to SQLite database
const knex = require('knex')({
  client: 'sqlite3',
  connection: {
    filename: dbPath,
  },
  useNullAsDefault: true
})

// Create a table in the database called "books"
knex.schema
  // Make sure no "books" table exists
  // before trying to create new
  .hasTable('books')
    .then((exists) => {
      if (!exists) {
        // If no "books" table exists
        // create new, with "id", "author", "title",
        // "pubDate" and "rating" columns
        // and use "id" as a primary identification
        // and increment "id" with every new record (book)
        return knex.schema.createTable('books', (table)  => {
          table.increments('id').primary()
          table.integer('author')
          table.string('title')
          table.string('pubDate')
          table.integer('rating')
        })
        .then(() => {
          // Log success message
          console.log('Table \'Books\' created')
        })
        .catch((error) => {
          console.error(`There was an error creating table: ${error}`)
        })
      }
    })
    .then(() => {
      // Log success message
      console.log('done')
    })
    .catch((error) => {
      console.error(`There was an error setting up the database: ${error}`)
    })

// Just for debugging purposes:
// Log all data in "books" table
knex.select('*').from('books')
  .then(data => console.log('data:', data))
  .catch(err => console.log(err))

// Export the database
module.exports = knex
```

## Express

Now, it is time for the second step, creating express server for this React app. This will include three parts, creating controllers, creating routes and creating the server.

### Controllers

If you don't know what controllers are think them as simple functions. The server uses these functions to process all requests coming to specific API endpoints. So, when in your React app you fetch endpoint to get all books on your bookshelf list, the response you will receive will be created by one of these functions.

For this tutorial, you will create four controllers. One controller for retrieving all books in the database, one for adding new book to the database, one for deleting specific book from the database and one controller for deleting all books, or resetting the bookshelf list.

The first controller, for retrieving all books, will query the "books" table in the database and return all records, or books. The second controller, for creating a new book, will insert new record, or book, to the database, using data we will provide it with in the request.

The third controller will use `id` to find specific book in the database and remove it. We will provide this `id` in the request send to the server. The last controller, for removing all books on the list, will select all records in "books" table and remove them.

Similarly to database, or the instance of `knex`, make sure to export each controller. Without this, you will not be able to require these controllers in routes and use them.

```JavaScript
// bookshelf-app/server/controllers/books-controller.js

// Import database
const knex = require('./../db')

// Retrieve all books
exports.booksAll = async (req, res) => {
  // Get all books from database
  knex
    .select('*') // select all records
    .from('books') // from 'books' table
    .then(userData => {
      // Send books extracted from database in response
      res.json(userData)
    })
    .catch(err => {
      // Send a error message in response
      res.json({ message: `There was an error retrieving books: ${err}` })
    })
}

// Create new book
exports.booksCreate = async (req, res) => {
  // Add new book to database
  knex('books')
    .insert({ // insert new record, a book
      'author': req.body.author,
      'title': req.body.title,
      'pubDate': req.body.pubDate,
      'rating': req.body.rating
    })
    .then(() => {
      // Send a success message in response
      res.json({ message: `Book \'${req.body.title}\' by ${req.body.author} created.` })
    })
    .catch(err => {
      // Send a error message in response
      res.json({ message: `There was an error creating ${req.body.title} book: ${err}` })
    })
}

// Remove specific book
exports.booksDelete = async (req, res) => {
  // Find specific book in the database and remove it
  knex('books')
    .where('id', req.body.id) // find correct record based on id
    .del() // delete the record
    .then(() => {
      // Send a success message in response
      res.json({ message: `Book ${req.body.id} deleted.` })
    })
    .catch(err => {
      // Send a error message in response
      res.json({ message: `There was an error deleting ${req.body.id} book: ${err}` })
    })
}

// Remove all books on the list
exports.booksReset = async (req, res) => {
  // Remove all books from database
  knex
    .select('*') // select all records
    .from('books') // from 'books' table
    .truncate() // remove the selection
    .then(() => {
      // Send a success message in response
      res.json({ message: 'Book list cleared.' })
    })
    .catch(err => {
      // Send a error message in response
      res.json({ message: `There was an error resetting book list: ${err}.` })
    })
}
```

### Routes

After controllers, routes will be the quick and easy part. First, you will require `express` library and the controllers you've just created. Next, you will use that `express` library to create router. Now, you can create routes, and request, for all API endpoints, i.e. to get all books, to create and delete a book and to delete all books.

Each request method accepts two parameters. The first one is the API endpoint to which that route responds to. The second parameter is the controller, you've just created, a specific function that will process the request coming to that specific endpoint, and send appropriate response.

The route for getting all books will respond to GET requests, so you will use `get` method. Route for creating new book will respond to POST requests, so you will use `post` method. Routes for deleting a book and deleting all books will both respond to PUT requests, so you will use `put` method. When you are done, export the router, the `router` variable.

```JavaScript
// bookshelf-app/server/routes/books-route.js

// Import express
const express = require('express')

// Import books-controller
const booksRoutes = require('./../controllers/books-controller.js')

// Create router
const router = express.Router()

// Add route for GET request to retrieve all book
// In server.js, books route is specified as '/books'
// this means that '/all' translates to '/books/all'
router.get('/all', booksRoutes.booksAll)

// Add route for POST request to create new book
// In server.js, books route is specified as '/books'
// this means that '/create' translates to '/books/create'
router.post('/create', booksRoutes.booksCreate)

// Add route for PUT request to delete specific book
// In server.js, books route is specified as '/books'
// this means that '/delete' translates to '/books/delete'
router.put('/delete', booksRoutes.booksDelete)

// Add route for PUT request to reset bookshelf list
// In server.js, books route is specified as '/books'
// this means that '/reset' translates to '/books/reset'
router.put('/reset', booksRoutes.booksReset)

// Export router
module.exports = router
```

### Express server

Controllers and routes are ready. The last step is to create express server. First, you will need to import `express` library and also the middleware, i.e. the `body-parser`, `compression`, `cors` and `helmet`. Next you will need to import routes you've just created. As next, you can define the default port for express server.

This is the port your express server will be running on. Make sure to choose different port than `3000`. `3000` is used by React app. When you have all dependencies ready, create instance of `express` and store it in variable `app`. After that, use the `app` variable and `use()` method to apply all middleware dependencies.

It is important to implement any middleware at the top. Middleware is applied only to anything that follows after it. If you apply middleware after you implement routes, middleware will not be applied on those routes. After middleware, you can implement route for "books" endpoint. This is also done with the `use()` method.

The difference is that, in case of middleware, you specified only one parameter, the middleware. Now, in case of routes, you specify two parameters, the API endpoint and specific router express server should use for this endpoint. After this, you can also add routes for handling errors, the 500 and 404.

Now, the last and most important thing. You need to start the express server. To do that, you will use `listen()` method. This method requires at least one parameter. This is the port where your express server should run. Here, you can use port you define in the beginning of this part. You can also pass in second parameter.

This is a callback function that is invoked when the server starts. It is a regular practice to use this function to log a short message to the console, along with the port. Then, you don't have to remember what port is used for the server.

```JavaScript
// bookshelf-app/server/server.js

// Import dependencies
const express = require('express')
const bodyParser = require('body-parser')
const compression = require('compression')
const cors = require('cors')
const helmet = require('helmet')

// Import routes
const booksRouter = require('./routes/books-route')

// Set default port for express app
const PORT = process.env.PORT || 4001

// Create express app
const app = express()

// Apply middleware
// Note: Keep this at the top, above routes
app.use(cors())
app.use(helmet())
app.use(compression())
app.use(bodyParser.urlencoded({ extended: false }))
app.use(bodyParser.json())

// Implement books route
app.use('/books', booksRouter)

// Implement 500 error route
app.use(function (err, req, res, next) {
  console.error(err.stack)
  res.status(500).send('Something is broken.')
})

// Implement 404 error route
app.use(function (req, res, next) {
  res.status(404).send('Sorry we could not find that.')
})

// Start express app
app.listen(PORT, function() {
  console.log(`Server is running on: ${PORT}`)
})
```

## React

Database is ready and express server as well. The last thing you have to do is to create the React app that will run on the front-end.

### BookshelfListRow component

Let's start with the easiest component. This will be `BookshelfListRow` component. The React app will use this component to render rows in the bookshelf list, or table. This component will be very simple. It will be created as a functional component that contains only HTML code for a single table row.

This table row will contain six cells, one for position, title, author, pubDate, rating and remove button. Data for these cells will come through `props`. For TypeScript, you will also create interface to define the shape of `props` for this component.

```tsx
// bookshelf-app/src/components/bookshelf-list-row.tsx

// Import deps
import React from 'react'

// Create interfaces
interface BookshelfListRowUI {
  position: number;
  book: {
    id: number;
    author: string;
    title: string;
    pubDate: string;
    rating: string;
  }
  handleBookRemove: (id: number, title: string) => void;
}

// Create BookshelfListRow component
export const BookshelfListRow = (props: BookshelfListRowUI) => (
  <tr className="table-row">
    <td className="table-item">
      {props.position}
    </td>

    <td className="table-item">
      {props.book.title}
    </td>

    <td className="table-item">
      {props.book.author}
    </td>

    <td className="table-item">
      {props.book.pubDate}
    </td>

    <td className="table-item">
      {props.book.rating}
    </td>

    <td className="table-item">
      <button
        className="btn btn-remove"
        onClick={() => props.handleBookRemove(props.book.id, props.book.title)}>
        Remove book
      </button>
    </td>
  </tr>
)
```

### BookshelfList component

Next will be component for bookshelf list. This component will be a table. It will render HTML for the `thead` and `tbody`. Inside the `tbody`, it use `map()` to iterate over array of books and render the `BookshelfListRow` component, you've just created, for each book. If the array is empty, i.e. there are no books, it will show a message.

All these data will come through component `props`. There will also be one additional property, called `loading`. This will be a boolean. You will use this property to show loading message when the table is loading. This will be after the app sent request to the server and before it gets the response with data, i.e. books.

Similarly to the `BookshelfListRow` component, you will also create interface for TypeScript to define the shape of `props` for this component. This time, you will create two interfaces. One for book array and one for `props` of `BookshelfListRow`. Interface for `props` will use the interface for book array.

```tsx
// bookshelf-app/src/components/bookshelf-list.tsx

// Import deps
import React from 'react'

// Import components
import { BookshelfListRow } from './bookshelf-list-row'

// Import styles
import './../styles/bookshelf-list.css'

// Create interfaces
interface BookUI {
  id: number;
  author: string;
  title: string;
  pubDate: string;
  rating: string;
}

interface BookshelfListUI {
  books: BookUI[];
  loading: boolean;
  handleBookRemove: (id: number, title: string) => void;
}

// Create BookshelfList component
export const BookshelfList = (props: BookshelfListUI) => {
  // Show loading message
  if (props.loading) return <p>Leaderboard table is loading...</p>

  return (
    <table className="table">
        <thead>
          <tr>
            <th className="table-head-item" />

            <th className="table-head-item">Title</th>

            <th className="table-head-item">Author</th>

            <th className="table-head-item">Pub. date</th>

            <th className="table-head-item">Rating</th>

            <th className="table-head-item" />
          </tr>
        </thead>

        <tbody className="table-body">
          {props.books.length > 0 ? (
            props.books.map((book: BookUI, idx) => (
              <BookshelfListRow
                key={book.id}
                book={book}
                position={idx + 1}
                handleBookRemove={props.handleBookRemove}
              />
              )
            )
          ) : (
            <tr className="table-row">
              <td className="table-item" style={{ textAlign: 'center' }} colSpan={6}>There are no books to show. Create one!</td>
            </tr>
          )
        }
        </tbody>
    </table>
  )
}
```

### Bookshelf component

The `Bookshelf` component will be the most important. It will contain all logic data processing. It will be the place from which all other components will get data. At the top will be states for form for adding new book on the list and also for data received from the server and for loading indicator used in `BookshelfList` component.

You will create all these state created with `useState` React hooks. The second, and also last, React hook you will use will be `useEffect`. You will use this React hook to fetch all books on initial render, that is why there is that empty array (`[]`) at the end.

Aside to these React hooks, this component will contain six functions. Four of these functions will be used to send requests to the server: `fetchBooks` to get all books, `handleBookCreate` to create new book, `handleBookRemove` to remove existing book and `handleListReset` to remove all books.

The remaining two will be `handleBookSubmit` and `handleInputsReset`. The first will check all input fields for creating new book. If all of them are filled, it will call `handleBookCreate` function that will create new book in the database. Then, it will call the `handleInputsReset` function. This function will reset all input fields for creating new book.

Now, to the `render` method. This component will render a simple form for adding new book to the database, the `BookshelfList` component and button. This button will reset the list, remove all books. And, that's it.

One thing about sending requests to the server. We will use `axios` library because it has very good browser support and it is easy to use. Another, native, option is [fetch API].

```tsx
// bookshelf-app/src/components/bookshelf.tsx

// Import deps
import React, { useEffect, useState } from 'react'
import axios from 'axios'

// Import components
import { BookshelfList } from './bookshelf-list'

// Import styles
import './../styles/bookshelf.css'

// Create Bookshelf component
export const Bookshelf = () => {
  // Prepare states
  const [author, setAuthor] = useState('')
  const [title, setTitle] = useState('')
  const [pubDate, setPubDate] = useState('')
  const [rating, setRating] = useState('')
  const [books, setBooks] = useState([])
  const [loading, setLoading] = useState(true)

  // Fetch all books on initial render
  useEffect(() => {
    fetchBooks()
  }, [])

  // Fetch all books
  const fetchBooks = async () => {
    // Send GET request to 'books/all' endpoint
    axios
      .get('http://localhost:4001/books/all')
      .then(response => {
        // Update the books state
        setBooks(response.data)

        // Update loading state
        setLoading(false)
      })
      .catch(error => console.error(`There was an error retrieving the book list: ${error}`))
  }

  // Reset all input fields
  const handleInputsReset = () => {
    setAuthor('')
    setTitle('')
    setPubDate('')
    setRating('')
  }

  // Create new book
  const handleBookCreate = () => {
    // Send POST request to 'books/create' endpoint
    axios
      .post('http://localhost:4001/books/create', {
        author: author,
        title: title,
        pubDate: pubDate,
        rating: rating
      })
      .then(res => {
        console.log(res.data)

        // Fetch all books to refresh
        // the books on the bookshelf list
        fetchBooks()
      })
      .catch(error => console.error(`There was an error creating the ${title} book: ${error}`))
  }

  // Submit new book
  const handleBookSubmit = () => {
    // Check if all fields are filled
    if (author.length > 0 && title.length > 0 && pubDate.length > 0 && rating.length > 0) {
      // Create new book
      handleBookCreate()

      console.info(`Book ${title} by ${author} added.`)

      // Reset all input fields
      handleInputsReset()
    }
  }

  // Remove book
  const handleBookRemove = (id: number, title: string) => {
    // Send PUT request to 'books/delete' endpoint
    axios
      .put('http://localhost:4001/books/delete', { id: id })
      .then(() => {
        console.log(`Book ${title} removed.`)

        // Fetch all books to refresh
        // the books on the bookshelf list
        fetchBooks()
      })
      .catch(error => console.error(`There was an error removing the ${title} book: ${error}`))
  }

  // Reset book list (remove all books)
  const handleListReset = () => {
    // Send PUT request to 'books/reset' endpoint
    axios.put('http://localhost:4001/books/reset')
    .then(() => {
      // Fetch all books to refresh
      // the books on the bookshelf list
      fetchBooks()
    })
    .catch(error => console.error(`There was an error resetting the book list: ${error}`))
  }

  return (
    <div className="book-list-wrapper">
      {/* Form for creating new book */}
      <div className="book-list-form">
        <div className="form-wrapper" onSubmit={handleBookSubmit}>
          <div className="form-row">
            <fieldset>
              <label className="form-label" htmlFor="title">Enter title:</label>
              <input className="form-input" type="text" id="title" name="title" value={title} onChange={(e) => setTitle(e.currentTarget.value)} />
            </fieldset>

            <fieldset>
              <label className="form-label" htmlFor="author">Enter author:</label>
              <input className="form-input" type="text" id="author" name="author" value={author} onChange={(e) => setAuthor(e.currentTarget.value)} />
            </fieldset>
          </div>

          <div className="form-row">
            <fieldset>
              <label className="form-label" htmlFor="pubDate">Enter publication date:</label>
              <input className="form-input" type="text" id="pubDate" name="pubDate" value={pubDate} onChange={(e) => setPubDate(e.currentTarget.value)} />
            </fieldset>

            <fieldset>
              <label className="form-label" htmlFor="rating">Enter rating:</label>
              <input className="form-input" type="text" id="rating" name="rating" value={rating} onChange={(e) => setRating(e.currentTarget.value)} />
            </fieldset>
          </div>
        </div>

        <button onClick={handleBookSubmit} className="btn btn-add">Add the book</button>
      </div>

      {/* Render bookshelf list component */}
      <BookshelfList books={books} loading={loading} handleBookRemove={handleBookRemove} />

      {/* Show reset button if list contains at least one book */}
      {books.length > 0 && (
        <button className="btn btn-reset" onClick={handleListReset}>Reset books list.</button>
      )}
    </div>
  )
}
```

### Index

The last thing you need to put together to get your React app up and running, the `index.tsx`. This will be very fast. First you need to import necessary dependencies: `React` and `renderer` method. Next, you need to import the `Bookshelf` component and some general styles. After that, you can render the `Bookshelf` component in the DOM.

```tsx
// bookshelf-app/src/index.tsx

// Import deps
import React from 'react'
import { render } from 'react-dom'

// Import components
import { Bookshelf } from './components/bookshelf'

// Import styles
import './styles/styles.css'

// Find div container
const rootElement = document.getElementById('root')

// Render Bookshelf component in the DOM
render(<Bookshelf />, rootElement)
```

## Styles

The SQLite database, express server and React app are all ready. The last thing you can do is to add some styles and polish how your new app looks. Here are some styles to help you get started.

### Bookshelf list styles

First, let's add some styles for the bookshelf list, or the table. For starters, let's make it easier to distinguish between table head, and headings, and table body by changing font sizes, weights and colors. Then, we can also use different background colors for even and odd table rows. This will make the table easier to scan.

```CSS
/* bookshelf-app/src/styles/bookshelf-list.css */

/* Bookshelf list/table */
.table {
  width: 100%;
  border-collapse: collapse;
}

.table-body {
  background: rgb(219, 233, 250) none repeat scroll 0 0;
}

.table-head-item {
  padding: 6px 12px;
  width: 20%;
  font-size: 12px;
  font-weight: 500;
  color: rgba(0, 0, 0, .38);
  text-align: right;
  text-transform: uppercase;
}

.table-row:nth-child(even) {
  background: rgb(236, 243, 252) none repeat scroll 0 0;
}

.table-item {
  overflow: hidden;
  padding: 12px;
  height: 24px;
  font-size: 14px;
  line-height: 24px;
  text-align: right;
  text-overflow: ellipsis;
}

.table-head-item:not(:first-child):not(:last-child),
.table-item:not(:first-child):not(:last-child) {
  text-align: left;
}

.table-item:first-child {
  width: 5%;
}

.table-item:nth-child(2) {
  width: 30%;
}

.table-item:nth-child(3) {
  width: 25%;
}

.table-item:nth-child(4) {
  width: 10%;
}

.table-item:nth-child(5) {
  width: 10%;
}

.table-item:last-child {
  width: 10%;
  min-width: 100px;
}

.table-row--active {
  font-size: 30px;
  color: #fff;
  background: #4990e2;
}
```

### Bookshelf styles

In case of the bookshelf component, we can change the background of the whole book list wrapper and add some `box-shadow`. This will help it stand out. After that, we can also add some styles to make those form elements more pleasing.

```CSS
/* bookshelf-app/src/styles/bookshelf.css */

/* Bookshelf form */
.book-list-wrapper {
  padding: 16px;
  margin: 64px auto 0;
  max-width: 768px;
  background: #fff;
  border-radius: 4px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, .1);
}

.book-list-form {
  margin-bottom: 32px;
}

.form-row {
  display: flex;
  flex-wrap: wrap;
}

.form-row + .form-row {
  margin-top: 18px;
}

.form-wrapper fieldset {
  padding: 0;
  margin: 0;
  width: 50%;
  border: 0;
}

.form-wrapper fieldset:first-child {
  padding-right: 4px;
}

.form-wrapper fieldset:last-child {
  padding-left: 4px;
}

.form-label {
  display: block;
  margin-bottom: 6px;
  font-size: 12px;
  color: #2c3e50;
}

.form-input {
  padding: 8px;
  width: 100%;
  font-size: 14px;
  border: 1px solid #dedede;
  border-radius: 4px;
  transition: border-color .25s ease-out;
}

.form-input:focus {
  border-color: #3498db;
  box-shadow: 0 0 2px #3498db;
  outline: 0;
}

.btn,
.btn-remove,
.btn-reset {
  display: block;
  border: 0;
  cursor: pointer;
  transition: all .25s ease-out;
}

.btn-add {
  padding: 12px 18px;
  margin: 12px auto 0;
  font-size: 14px;
  font-weight: 700;
  color: #fff;
  background-color: #3498db;
  border-radius: 4px;
}

.btn-add:hover {
  background-color: #2980b9;
}

.btn-remove,
.btn-reset {
  padding: 0;
  font-size: 12px;
  font-style: italic;
  color: hsl(6, 63%, 46%);
  background-color: transparent;
}

.btn-remove:hover,
.btn-reset:hover {
  color: hsl(6, 63%, 26%);
}

.btn-reset {
  margin: 21px auto 0;
}
```

### General styles

Lastly, let's add some general styles to fix various issues with layout and browser inconsistencies.

```CSS
/* bookshelf-app/src/styles/styles.css */

/* General styles */
html,
*,
*::before,
*::after {
  box-sizing: border-box;
}

html,
body,
#root {
  min-height: 100vh;
}

html {
  font-size: 16px;
}

body {
  margin: 0;
  background: #eee;
  font: 1rem / 1.414 -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, 'Noto Sans', sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji';
  color: #333;
}
```

## Conclusion: How to build an app with React, Express and SQLite

Good job! You've just built your own app with React, Express and SQLite. I hope you enjoyed this tutorial and learned something new. Let's do a quick recap. First, you've learned how to create SQLite database. Next, you've learned how to create express server, controllers and routes for endpoints, how to connect them with SQLite database, and how to implement them, along with middleware.

After that, you've learned how to build a React app. Here, you've learned how to use `axios` to send requests to express server and how to use React hooks to store the data you received. Next steps? Add more endpoints such as to update existing books. Or, add more columns in the database table to store more information about each book. You can also use what you've learned today to build something completely different.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[GitHub]: https://github.com/alexdevero/bookshelf-react-express-sqlite-app
[react-scripts]: https://www.npmjs.com/package/react-scripts
[TypeScript]: https://www.typescriptlang.org/
[create-react-app]: https://github.com/facebook/create-react-app
[fetch API]: https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API

<!--
### Meta:
-
-->

<!--
#### Resources:
-
-->
