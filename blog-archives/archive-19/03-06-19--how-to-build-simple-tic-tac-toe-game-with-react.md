# How to Build Simple Tic Tac Toe Game with React
Have you ever wanted to create your own Tic Tac Toe game? You are on the right place. This tutorial will show you how to do it, using JavaScript and React. What's more, it will also show you how to use `localStorage` to store history of games. Get better in JavaScript and React and build your own Tic Tac Toe game!<!--more-->
<!--
Table of Contents:
## Phase 1: Setup
## Phase 2: React
### The Box component
### The Board component
### The Scoreboard component
### The App component
## Phase 3: Utils
## Phase 4: Storage
## Phase 5: Styling
## Epilogue: How to Build Simple Tic Tac Toe Game with React
-->

## Phase 1: Setup

In the first phase, let's create all files we need for our Tic Tac Toe game. To make this step easier we will use the [create-react-app] as our starting template. If you have it this package already installed on your computer, go ahead and use that with you favorite dependency manager. If not, I recommend using it via [npx].

There is no reason to install the create-react-app package, even if you plan to use it more often. Npx will allow you to use it, or any other package hosted on npm, without installing it, as global or local dependency. Using npx is almost like using npm. The only difference is that you replace the `npm` with `npx`. The rest is the same.

One important thing you have to remember. Npx will need to temporarily download the package so you can use it. This means that you must be connected to internet. About the package. Don't worry about cluttering your disk. Npx will automatically remove the package after you use it. The command to create the template for our Tic Tac Toe game is `npx create-react-app react-tic-tac-toe`.

After npx do its job, we will need to add one additional package. This will be `react-router-dom`. Our Tic Tac Toe game will have two views, or pages. The first will be a welcome screen showing list of scores from previous games. The second will be the Tic Tac Toe game board itself, with list of played moves.

We will use the `react-router-dom` to switch between these two views. And that will be all we need. If you want to use Sass or styled-components, or some other library for styling, go ahead and add it. In this tutorial, we will stick to good old CSS and stylesheets.

```
// package.json

{
  "name": "react-tic-tac-toe",
  "version": "0.1.0",
  "private": true,
  "dependencies": {
    "react": "^16.8.6",
    "react-dom": "^16.8.6",
    "react-router-dom": "^5.0.0",
    "react-scripts": "3.0.1"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  },
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
  }
}
```

One more thing. When we are done, this will be the final project structure:

```
react-tic-tac-toe/
├─node_modules
├─public
│ ├─favicon.ico
│ ├─index.html
│ └─manifest.json
├─src
│ ├─components
│ │ └─board-box.jsx
│ │ └─board.jsx
│ │ └─scoreboard.jsx
│ ├─storage
│ │ └─storage.jss
│ ├─styles
│ │ └─board.css
│ │ └─box.css
│ │ └─buttons.css
│ ├─utils
│ │ └─functions.js
│ ├─index.jsx
│ └─react-app-env.d.ts
└─ package.json
```

## Phase 2: React

In the second phase, our task will be to build all React components we will need for our Tic Tac Toe game. We will create four components, board-box.jsx, board.jsx, scoreboard.jsx and the index.jsx.

### The Box component

Let's start with the simplest component. This will be the `board-box.jsx`, component for individual boxes or squares on the board. We will create this component as a stateless. It will be a simple button with click handler and label, both passed by props.

```
///
// src/components/board-box.jsx
///
import React from 'react'

// Create Box component
export const Box = (props) => {
	return (
		<button className="board__box" onClick={props.onClick}>
			{props.value}
		</button>
	)
}
```

### The Board component

Next component will be the main board for our Tic Tac Toe game. This component will be a little bit more complex and also much bigger than the previous one. First, we will create this component as a stateful component. Component state will be initialized with three key/value pairs-`boxes`, `history` , `xIsNext`.

The `boxes` item will be an array containing nine items, one item for each board box. All these items will be `null`. So, when box is empty, not "x" or "o", it will be `null`. Otherwise, it will be either "x" or "o". The `history` will be an empty array. When player makes a move, we will push players name to `history` array.

The last one, the `xIsNext`, will be boolean. We will initialize it as `true`. This will help us determine which player should make a move as next. After this, we will create new instance of `Storage` object (we will create this object later). We will use it later to store game results in `localStorage`.

The board component will contain two click handlers. First will be `handleBoxClick` and it will handle clicking on board boxes. With every click, it will check if board contains winning combination or if all boxes are clicked. If one of these conditions is true, the game ends. Otherwise, we will check which player made move, mark the box and push the move to game history.

The second one will be `handleBoardRestart`. This one will restart the component state to its initial state. The `render` method will contain conditions to show status message-who is winner, game is drawn or who is the next one to move. Next, it will contain link to scoreboard, the main board with boxes list with history of moves and button to start new game.

For the link to scoreboard, we will use `Link` from `react-router-dom` library that will redirect the user on `/` (root) view, or page.

```
///
// src/components/board.jsx
///
import React from 'react'
import { Link } from 'react-router-dom'

// Import Storage object
import { Storage } from './../storage/storage'

// Import Box component
import { Box } from './board-box'

// Import utility functions
import * as utils from '../utils/functions'

// Create Board component
export class Board extends React.Component {
	constructor(props) {
    super(props)

		// Initialize component state
		this.state = {
			boxes: Array(9).fill(null),
			history: [],
			xIsNext: true
		}
	}

	// Create instance of Storage object
	storage = new Storage()

	// Handle click on boxes on the board.
	handleBoxClick(index) {
		// get current state of boxes
		const boxes = this.state.boxes.slice()

		// Get current state of history
		let history = this.state.history

		// Stop the game if board contains winning combination
		if (utils.findWinner(boxes) || boxes[index]) {
			return
		}

		// Stop the game if all boxes are clicked (filled)
		if(utils.areAllBoxesClicked(boxes) === true) {
			return
		}

		// Mark the box either as 'x' or 'o'
		boxes[index] = this.state.xIsNext ? 'x' : 'o'

		// Add move to game history
		history.push(this.state.xIsNext ? 'x' : 'o')

		// Update component state with new data
    this.setState({
			boxes: boxes,
			history: history,
			xIsNext: !this.state.xIsNext
		})
	}

	// Handle board restart - set component state to initial state
	handleBoardRestart = () => {
		this.setState({
			boxes: Array(9).fill(null),
			history: [],
			xIsNext: true
		})
	}

	render() {
		// Get winner (if there is any)
    const winner = utils.findWinner(this.state.boxes)

		// Are all boxes checked?
    const isFilled = utils.areAllBoxesClicked(this.state.boxes)

		// Status message
    let status

		if (winner) {
			// If winner exists, create status message
			status = `The winner is: ${winner}!`

			// Push data about the game to storage
			this.storage.update([`${winner} won`])
		} else if(!winner && isFilled) {
			// If game is drawn, create status message
			status = 'Game drawn!'

			// Push data about the game to storage
			this.storage.update(['Game drawn'])
		} else {
			// If there is no winner and game is not drawn, ask the next player to make a move
			status = `It is ${(this.state.xIsNext ? 'x' : 'o')}'s turn.`
		}

		return (
			<>
				{/* Link to scoreboard */}
				<Link to="/" className="board-link">Go back to scoreboard</Link>

				{/* The game board */}
				<div className="board-wrapper">
					<div className="board">
						<h2 className="board-heading">{status}</h2>

						<div className="board-row">
							<Box value={this.state.boxes[0]} onClick={() => this.handleBoxClick(0)} />

							<Box value={this.state.boxes[1]} onClick={() => this.handleBoxClick(1)} />

							<Box value={this.state.boxes[2]} onClick={() => this.handleBoxClick(2)} />
						</div>

						<div className="board-row">
							<Box value={this.state.boxes[3]} onClick={() => this.handleBoxClick(3)} />

							<Box value={this.state.boxes[4]} onClick={() => this.handleBoxClick(4)} />

							<Box value={this.state.boxes[5]} onClick={() => this.handleBoxClick(5)} />
						</div>

						<div className="board-row">
							<Box value={this.state.boxes[6]} onClick={() => this.handleBoxClick(6)} />

							<Box value={this.state.boxes[7]} onClick={() => this.handleBoxClick(7)} />

							<Box value={this.state.boxes[8]} onClick={() => this.handleBoxClick(8)} />
						</div>
					</div>

					<div className="board-history">
						<h2 className="board-heading">Moves history:</h2>

						{/* List with history of moves */}
						<ul className="board-historyList">
							{this.state.history.length === 0 && <span>No moves to show.</span>}

							{this.state.history.length !== 0 && this.state.history.map((move, index) => {
								return <li key={index}>Move {index + 1}: <strong>{move}</strong></li>
							})}
						</ul>
					</div>

					{/* Button to start new game */}
					{winner && <div className="board-footer">
						<button className="btn" onClick={this.handleBoardRestart}>Start new game</button>
					</div>}
				</div>
			</>
		)
	}
}
```

### The Scoreboard component

The `Scoreboard` component will be very simple. Similarly to `Board`, this will also be stateful component. Its state will contain one key/value pair, `scoreboard`. The value for this key will be an empty array. After `Scoreboard` component mounts we will use `Storage` object to load any data from local storage and update component state.

The `render` method will contain the list with previous games and link to start new game. For the link, we will again use `Link` from `react-router-dom` library that will redirect the user on `/board` view, or page.

```
///
// src/components/scoreboard.jsx
///
import React from 'react'
import { Link } from 'react-router-dom'

// Import Storage object
import { Storage } from './../storage/storage'

// Create Scoreboard component
export class Scoreboard extends React.Component {
  state = {
    scoreboard: []
  }

	// After component mounts, load any data from local storage and update component state
  async componentDidMount() {
    let storage = await new Storage().getData()

    this.setState({
      scoreboard: storage
    })
  }

  render() {
    return (
      <div className="game">
        <h1>Recent games:</h1>

				{/* List with previous games */}
        <ul>
          {this.state.scoreboard.map((leader, key) => {
            return <li key={key}>{leader}</li>
          })}
        </ul>

				{/* Link to start new game */}
        <Link to="/board">
          <button className="btn">Start new game</button>
        </Link>
      </div>
    )
  }
}
```

### The App component

The last component we need to create is the main App. Here, we will import `Board` and `Scoreboard` components/views we just created. We can also import CSS (or Sass) stylesheets to make our Tic Tac Toe game look better. However, the most important part of this component will be implementing `BrowserRouter` and `Routes` from `react-router-dom`.

We will use the router to create two routes, one for root (homepage) and one for the Tic Tac Toe game board. Root route will render the `Scoreboard` component. The board route will render `Board` component. As the last step we will render the `App` component into DOM.

```
///
// src/index.jsx
///
import React from 'react'
import ReactDOM from 'react-dom'
import { BrowserRouter, Route } from 'react-router-dom'

// Import Board and Scoreboard views
import { Board } from './components/board'
import { Scoreboard } from './components/scoreboard'

import './styles/board.css'
import './styles/box.css'
import './styles/buttons.css'

// Create App component
class App extends React.Component {
  render() {
    return (
      <div className="app">
        <BrowserRouter>
          <Route exact path="/" component={Scoreboard}/>
          <Route path="/board" component={Board}/>
        </BrowserRouter>
      </div>
    )
  }
}

// Render the App component into DOM
ReactDOM.render(<App />, document.getElementById('root'))
```

## Phase 3: Utils

Our Tic Tac Toe game is almost finished. However, before we can let anyone try our React Tic Tac Toe we need to create two utility functions. These functions will be `findWinner` and `areAllBoxesClicked`. The `findWinner` will contain an array with winning combinations and `for` loop.

The `for` loop will iterate over the array with winning combinations and check if the game board contains winning combination. If so, it will return the winner, either 'x' or 'o'. Otherwise, it will do nothing. The `areAllBoxesClicked` will use `forEach` loop to iterate over all boxes count those that are not empty (not `null`).

If the number of these not empty (not `null`) boxes is equal to 9, it will return `true`-all boxes are click (filled). Otherwise, it will return `false`.

```
///
// src/utils/functions.js
///
export function findWinner(boxes) {
	// Array with winning combinations
	const rows = [
		[0, 1, 2],
		[3, 4, 5],
		[6, 7, 8],
		[0, 3, 6],
		[1, 4, 7],
		[2, 5, 8],
		[0, 4, 8],
		[2, 4, 6]
	]

	// Iterate over array with winning combinations
	for (let i = 0; i < rows.length; i++) {
		const [a, b, c] = rows[i]

		// Check if the game board contains winning combination
		if (boxes[a] && boxes[a] === boxes[b] && boxes[a] === boxes[c]) {
			// Return the winner ('x' or 'o')
			return boxes[a]
		}
	}

	// Otherwise do nothing
	return null
}

export function areAllBoxesClicked(boxes) {
	// Declare variable to store number of clicked boxes.
	let count = 0

	// Iterate over all boxes
	boxes.forEach(function (item) {
		// Check if box is clicked (not null)
		if (item !== null) {
			// If yes, increase the value of count by 1
			count++
		}
	})

	// Check if all boxes are clicked (filled)
	if (count === 9) {
		return true
	} else {
		return false
	}
}
```

## Phase 4: Storage

The last thing our Tic Tac Toe game needs is the `Storage` object. We will use this object to create and update data in browser `localStorage` object. When initialized, it will check if localStorage contains any data from previous games. If not, it will create new item create new item in localStorage for our Tic Tac Toe game.

Next, we will add two methods, `getData` and `update`. The first one will get existing data localStorage. The second one will push new data into localStorage. With this, we will now be able to show records of previous games on the scoreboard view, or page.

```
///
// src/storage/storage.js
///
export class Storage {
  constructor(storageName = 'gameScoreboard', initialValue = '[]') {
    this.storageName = storageName

		// Check if localStorage contains any data from previous games
    if (!localStorage.getItem(storageName)) {
			// If not, create new item for our Tic Tac Toe game
      localStorage.setItem(storageName, initialValue)
    }
  }

	// Load data from previous games from localStorage
  getData() {
    return JSON.parse(localStorage.getItem(this.storageName))
  }

	// Update data in localStorage
  update(data) {
    localStorage.setItem(this.storageName, JSON.stringify(data))
  }
}
```

## Phase 5: Styling

Our Tic Tac Toe game is working and ready for first players. The last thing we can do is make look better. Here are some basic styles we can add.

Some styles for the board component.
```
/*
* src/styles/board.css
*/
.board-link {
	display: inline-block;
	margin-bottom: 16px;
	font-size: 15px;
	text-decoration: none;
	color: #111;
	border-bottom: 1px solid #111;
}

.board-wrapper {
  display: flex;
	flex-flow: row wrap;
}

.board {
	width: 250px;
}

.board-row {
  display: flex;
  flex-flow: row wrap;
}

.board-heading {
	margin-top: 0;
	margin-bottom: 8px;
	font: 700 18px / 1.618 sans-serif;
	list-style-type: none;
}

.board-history {
	margin-left: 18px;
}

.board-history-list {
	padding: 0;
	list-style-type: none;
}

.board-footer {
	width: 100%;
}
```

Some styles for the board box component.

```
/*
* src/styles/box.css
*/
.board__box {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0;
  width: calc(250px / 3);
  height: calc(250px / 3);
  font-size: 32px;
  color: #111;
  background-color: #fff;
  border: 1px solid #aaa;
}
```

And some styles for buttons.

```
/*
* src/styles/buttons.css
*/
/* Buttons */
.btn {
  padding: 12px 16px;
  margin-top: 18px;
  font-size: 14px;
  color: #fff;
  background-color: #3498db;
  border: 0;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color .25s ease-in-out;
}

.btn:hover {
  background-color: #2980b9;
}
```

## Epilogue: How to Build Simple Tic Tac Toe Game with React

Congratulations! You did it! You've just finished this tutorial and build your own Tic Tac Toe game. What's more. You've also learned how to use `localStorage` to store history of previous games. Thanks to this, you have working scoreboard where you can see all recent games. Want another challenge? How about allowing players to change their names?

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[create-react-app]: https://github.com/facebook/create-react-app
[npx]: https://github.com/zkat/npx

<!--
### Meta:
-
-->

<!--
#### Resources:
-
-->
