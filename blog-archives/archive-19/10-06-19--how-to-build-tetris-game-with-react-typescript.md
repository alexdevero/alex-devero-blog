# How to Build Simple Tetris Game with React & TypeScript

Playing games is fun. What's better, and also more beneficial, is creating your own games. Why? It is a great way to learn new skills, or get better. In this tutorial, you will learn how to write your own Tetris game with React, JavaScript and TypeScript. Have fun and work on your programming skills at the same time!<!--more-->
<!--
Table of Contents:
## Project setup
## Tetris board component
## Main Tetris component
## Index
## Styles
## Epilogue: How to build simple Tetris game with React & TypeScript
-->

## Project setup

The first step is putting setting up the files you need for our Tetris game. You can do this quickly with the help of [create-react-app] package. This package can generate starting template for us. There are two ways to get this done. You can install the package globally on your computer, with your favorite dependency manager. This is the first way.

The second way is using it via [npx]. You don't have to install any package if you want to use it. Not even if you want to use it more often. If you have stable internet connection, you can use npx. It will temporarily download the package, let you use it, and then delete it. It is almost like using npm except that you don't bloat your disk.

One thing before you proceed to generating the template. This tutorial will use [TypeScript]. This means that you have to include `--typescript` flag when you use create-react-app. So, if you prefer the first way, use `npm create-react-app react-tetris-ts --typescript` or `yarn create-react-app react-tetris-ts --typescript`.

If you want to use npx just replace npm, or yarn, with npm. The rest will be the same: `npx create-react-app react-tetris-ts --typescript`. After npm, yarn or npx do its job, you are ready to start building our Tetris game. You don't need to add any other dependencies, unless you want to. If so, go ahead. Otherwise, you are good to go.

```
// package.json

{
  "name": "react-tetris-ts",
  "version": "0.1.0",
  "private": true,
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
  },
  "dependencies": {
    "react": "^16.8.6",
    "react-dom": "^16.8.6",
    "react-scripts": "3.0.1",
    "typescript": "3.5.1"
  },
  "devDependencies": {
    "@types/jest": "24.0.13",
    "@types/node": "12.0.7",
    "@types/react": "16.8.19",
    "@types/react-dom": "16.8.4"
  }
}
```

When you are done, this will be the structure for this project:

```
react-tetris-ts/
├─node_modules
├─public
│ ├─favicon.ico
│ ├─index.html
│ └─manifest.json
├─src
│ ├─components
│ │ └─tetris-board.tsx
│ │ └─tetris.tsx
│ ├─styles
│ │ └─styles.css
│ ├─index.tsx
│ └─react-app-env.d.ts
│ └─serviceWorker.ts
└─ package.json
└─ tsconfig.json
```

_Side note: If you want to prevent webpack from automatically opening the browser every time you start the project, do the following. In the root of your project, create `.env.development` file. Inside this file, add `BROWSER=none` and save it. From now on, webpack will no longer open the browser when you launch the `start` npm script._

## Tetris board component

Now, you can create your first component, the Tetris board. This will be very fast. At the top, you will start by importing React. Then, you will specify props for this component, for TypeScript. The component will be quite simple. There is no need for state or [lifecycle methods]. So, you will create it as a stateless component.

Inside this component, you will use `forEach()` loop and `map()` to iterate over content of `field` prop, create rows and columns for the board, and push everything into `rows` array. Columns and rows will be `div` elements. Next, you will create a small block with game stats, such as level and score.

Under this, inside a `div` will be rendered the `rows` array. This will be all the content returned by this component. Finally, make sure to [export] the component.

```
///
// src/components/tetris-board.tsx

// Import React
import * as React from 'react'

// Define props for TetrisBoard component
type TetrisBoardProps = {
  field: any[],
  gameOver: boolean,
  score: number,
  level: number,
  rotate: number
}

// Create TetrisBoard component
const TetrisBoard: React.FC<TetrisBoardProps> = (props) => {
  // Create board rows
  let rows: any[] = []

  props.field.forEach((row, index) => {
    // Create board columns
    const cols = row.map((column: any, index: number) => <div className={`col-${column}`} key={index} />)

    rows.push(<div className="tetris-board__row" key={index}>{cols}</div>)
  })

  return (
    <div className="tetris-board">
      {/* Game info */}
      <div className="tetris-board__info">
        <p className="tetris-board__text">Level: {props.level}</p>

        <p className="tetris-board__text">Score: {props.score}</p>

        {props.gameOver && <p className="tetris-board__text"><strong>Game Over</strong></p>}
      </div>

      {/* Game board */}
      <div className="tetris-board__board">{rows}</div>
    </div>
  )
}

export default TetrisBoard
```

## Main Tetris component

The second component will be the main part of your Tetris game. This is the place where you will implement the logic of the game. As such, this component will be quite complex. At the top, you will start with importing React and the `TetrisBoard` component. Then, you will define props for `Tetris` component and also for its `state`, for TypeScript.

Yes, you will create this component as a stateful component. In other words, you will create it using JavaScript [class]. Inside class constructor, you will use `boardHeight` and `boardWidth` props passed to this component, along with `for` loops, to generate rows and columns for the game board.

Next, you will specify the starting column, where tiles will appear. This will be in the middle of the first row. As the last thing, you will initialize the component `state` with some properties that will be necessary to make this Tetris game work.

One thing. Now, all tiles are defined the state, in the form of arrays and "binary state". If you want, you can extract this data into separate file, export it from there and import it here. This can help you reduce the amount of code in this component.

Next are two lifecycle methods, `componentDidMount` and `componentWillUnmount`. You will use the first, along with `setInterval` to start the game after component mounts. The interval (game speed) will be determined by the current game level. Higher level means higher speed. The `componentWillUnmount`, with `clearInterval`, will stop the game and tidy it up right before the component unmounts.

There will be three methods: `handleBoardUpdate`, `handlePauseClick` and `handleNewGameClick`. The `handlePauseClick` will be the simplest. It will pause and resume the game by changing `pause` property in `state`. The `handleNewGameClick` will restart the game by resetting, or regenerating, the game board and setting all properties inside `state` to their initial values.

The `handleBoardUpdate` will be the most important, and also the most complex. This method will handle basically everything. It will take care of creating new tiles. It will also handle moving the tiles horizontally and speeding up the fall of current tile. Lastly, it will also manage rotating the tiles.

In short, all this will be done by using the current data in the `state`, making changes based on player's commands (move, rotate, speed up) and then updating the `state` with new, modified, data. In other words, you will re-render, or re-create, the board during every interval, the natural downward movement of the tile (see `handleBoardUpdate` in `setInterval()` in class constructor).

You will also re-render the board every time the player interacts with the game. When player move, rotate or speed up the tile you will take the state of the board, and the position of the tile, make necessary modification, reset the board, apply the modifications and re-render it.

```
///
// src/components/tetris.tsx

// Import React
import * as React from 'react'

// Import TetrisBoard component
import TetrisBoard from './tetris-board'

// Define props for Tetris component
type TetrisProps = {
  boardWidth: any,
  boardHeight: any
}

// Define props for Tetris component state
type TetrisState = {
  activeTileX: number,
  activeTileY: number,
  activeTile: number,
  tileRotate: number,
  score: number,
  level: number,
  tileCount: number,
  gameOver: boolean,
  isPaused: boolean,
  field: any[],
  timerId: any,
  tiles: number[][][][]
}

// Create Tetris component
class Tetris extends React.Component<TetrisProps, TetrisState> {
  constructor(props: any) {
    super(props)

    // Generate board based on number of boardHeight & boardWidth props
    let field = []

    for (let y = 0; y < props.boardHeight; y++) {
      let row = []

      for (let x = 0; x < props.boardWidth; x++) {
        row.push(0)
      }

      field.push(row)
    }

    // Set starting column to center
    let xStart = Math.floor(parseInt(props.boardWidth) / 2)

    // Initialize state with starting conditions
    this.state = {
      activeTileX: xStart,
      activeTileY: 1,
      activeTile: 1,
      tileRotate: 0,
      score: 0,
      level: 1,
      tileCount: 0,
      gameOver: false,
      isPaused: false,
      field: field,
      timerId: null,
      tiles: [
        // 7 tiles
        // Each tile can be rotated 4 times (x/y coordinates)
        [
          // The default square
          [[0, 0], [0, 0], [0, 0], [0, 0]],
          [[0, 0], [0, 0], [0, 0], [0, 0]],
          [[0, 0], [0, 0], [0, 0], [0, 0]],
          [[0, 0], [0, 0], [0, 0], [0, 0]]
        ],
        [
          // The cube tile (block 2x2)
          [[0, 0], [1, 0], [0, 1], [1, 1]],
          [[0, 0], [1, 0], [0, 1], [1, 1]],
          [[0, 0], [1, 0], [0, 1], [1, 1]],
          [[0, 0], [1, 0], [0, 1], [1, 1]]
        ],
        [
          // The I tile
          [[0, -1], [0, 0], [0, 1], [0, 2]],
          [[-1, 0], [0, 0], [1, 0], [2, 0]],
          [[0, -1], [0, 0], [0, 1], [0, 2]],
          [[-1, 0], [0, 0], [1, 0], [2, 0]]
        ],
        [
          // The T tile
          [[0, 0], [-1, 0], [1, 0], [0, -1]],
          [[0, 0], [1, 0], [0, 1], [0, -1]],
          [[0, 0], [-1, 0], [1, 0], [0, 1]],
          [[0, 0], [-1, 0], [0, 1], [0, -1]]
        ],
        [
          // The inverse L tile
          [[0, 0], [-1, 0], [1, 0], [-1, -1]],
          [[0, 0], [0, 1], [0, -1], [1, -1]],
          [[0, 0], [1, 0], [-1, 0], [1, 1]],
          [[0, 0], [0, 1], [0, -1], [-1, 1]]
        ],
        [
          // The L tile
          [[0, 0], [1, 0], [-1, 0], [1, -1]],
          [[0, 0], [0, 1], [0, -1], [1, 1]],
          [[0, 0], [1, 0], [-1, 0], [-1, 1]],
          [[0, 0], [0, 1], [0, -1], [-1, -1]]
        ],
        [
          // The Z tile
          [[0, 0], [1, 0], [0, -1], [-1, -1]],
          [[0, 0], [1, 0], [0, 1], [1, -1]],
          [[0, 0], [1, 0], [0, -1], [-1, -1]],
          [[0, 0], [1, 0], [0, 1], [1, -1]]
        ],
        [
          // The inverse Z tile
          [[0, 0], [-1, 0], [0, -1], [1, -1]],
          [[0, 0], [0, -1], [1, 0], [1, 1]],
          [[0, 0], [-1, 0], [0, -1], [1, -1]],
          [[0, 0], [0, -1], [1, 0], [1, 1]]
        ]
      ]
    }
  }

  /**
   * @description Sets timer after component mounts
   * Uses level (this.state.level) to determine the interval (game speed)
   * and executes handleBoardUpdate() set to 'down' method during each interval
   * @memberof Tetris
   */
  componentDidMount() {
    let timerId

    timerId = window.setInterval(
      () => this.handleBoardUpdate('down'),
      1000 - (this.state.level * 10 > 600 ? 600 : this.state.level * 10)
    )

    this.setState({
      timerId: timerId
    })
  }

  /**
   * @description Resets the timer when component unmounts
   * @memberof Tetris
   */
  componentWillUnmount() {
    window.clearInterval(this.state.timerId)
  }

  /**
   * @description Handles board updates
   * @param {string} command
   * @memberof Tetris
   */
  handleBoardUpdate(command: string) {
    // Do nothing if game ends, or is paused
    if (this.state.gameOver || this.state.isPaused) {
      return
    }

    // Prepare variables for additions to x/y coordinates, current active tile and new rotation
    let xAdd = 0
    let yAdd = 0
    let rotateAdd = 0
    let tile = this.state.activeTile

    // If tile should move to the left
    // set xAdd to -1
    if (command === 'left') {
      xAdd = -1
    }

    // If tile should move to the right
    // set xAdd to 1
    if (command === 'right') {
      xAdd = 1
    }

    // If tile should be rotated
    // set rotateAdd to 1
    if (command === 'rotate') {
      rotateAdd = 1
    }

    // If tile should fall faster
    // set yAdd to 1
    if (command === 'down') {
      yAdd = 1
    }

    // Get current x/y coordinates, active tile, rotate and all tiles
    let field = this.state.field
    let x = this.state.activeTileX
    let y = this.state.activeTileY
    let rotate = this.state.tileRotate

    const tiles = this.state.tiles

    // Remove actual tile from field to test for new insert position
    field[y + tiles[tile][rotate][0][1]][x + tiles[tile][rotate][0][0]] = 0
    field[y + tiles[tile][rotate][1][1]][x + tiles[tile][rotate][1][0]] = 0
    field[y + tiles[tile][rotate][2][1]][x + tiles[tile][rotate][2][0]] = 0
    field[y + tiles[tile][rotate][3][1]][x + tiles[tile][rotate][3][0]] = 0

    // Test if the move can be executed on actual field
    let xAddIsValid = true

    // Test if tile should move horizontally
    if (xAdd !== 0) {
      for (let i = 0; i <= 3; i++) {
        // Test if tile can be moved without getting outside the board
        if (
          x + xAdd + tiles[tile][rotate][i][0] >= 0
          && x + xAdd + tiles[tile][rotate][i][0] < this.props.boardWidth
        ) {
          if (field[y + tiles[tile][rotate][i][1]][x + xAdd + tiles[tile][rotate][i][0]] !== 0) {
            // Prevent the move
            xAddIsValid = false
          }
        } else {
          // Prevent the move
          xAddIsValid = false
        }
      }
    }

    // If horizontal move is valid update x variable (move the tile)
    if (xAddIsValid) {
      x += xAdd
    }

    // Try to rotate the tile
    let newRotate = rotate + rotateAdd > 3 ? 0 : rotate + rotateAdd
    let rotateIsValid = true

    // Test if tile should rotate
    if (rotateAdd !== 0) {
      for (let i = 0; i <= 3; i++) {
        // Test if tile can be rotated without getting outside the board
        if (
          x + tiles[tile][newRotate][i][0] >= 0 &&
          x + tiles[tile][newRotate][i][0] < this.props.boardWidth &&
          y + tiles[tile][newRotate][i][1] >= 0 &&
          y + tiles[tile][newRotate][i][1] < this.props.boardHeight
        ) {
          // Test of tile rotation is not blocked by other tiles
          if (
            field[y + tiles[tile][newRotate][i][1]][
              x + tiles[tile][newRotate][i][0]
            ] !== 0
          ) {
            // Prevent rotation
            rotateIsValid = false
          }
        } else {
          // Prevent rotation
          rotateIsValid = false
        }
      }
    }

    // If rotation is valid update rotate variable (rotate the tile)
    if (rotateIsValid) {
      rotate = newRotate
    }

    // Try to speed up the fall of the tile
    let yAddIsValid = true

    // Test if tile should fall faster
    if (yAdd !== 0) {
      for (let i = 0; i <= 3; i++) {
        // Test if tile can fall faster without getting outside the board
        if (
          y + yAdd + tiles[tile][rotate][i][1] >= 0 &&
          y + yAdd + tiles[tile][rotate][i][1] < this.props.boardHeight
        ) {
          // Test if faster fall is not blocked by other tiles
          if (
            field[y + yAdd + tiles[tile][rotate][i][1]][
              x + tiles[tile][rotate][i][0]
            ] !== 0
          ) {
            // Prevent faster fall
            yAddIsValid = false
          }
        } else {
          // Prevent faster fall
          yAddIsValid = false
        }
      }
    }

    // If speeding up the fall is valid (move the tile down faster)
    if (yAddIsValid) {
      y += yAdd
    }

    // Render the tile at new position
    field[y + tiles[tile][rotate][0][1]][x + tiles[tile][rotate][0][0]] = tile
    field[y + tiles[tile][rotate][1][1]][x + tiles[tile][rotate][1][0]] = tile
    field[y + tiles[tile][rotate][2][1]][x + tiles[tile][rotate][2][0]] = tile
    field[y + tiles[tile][rotate][3][1]][x + tiles[tile][rotate][3][0]] = tile

    // If moving down is not possible, remove completed rows add score
    // and find next tile and check if game is over
    if (!yAddIsValid) {
      for (let row = this.props.boardHeight - 1; row >= 0; row--) {
        let isLineComplete = true

        // Check if row is completed
        for (let col = 0; col < this.props.boardWidth; col++) {
          if (field[row][col] === 0) {
            isLineComplete = false
          }
        }

        // Remove completed rows
        if (isLineComplete) {
          for (let yRowSrc = row; row > 0; row--) {
            for (let col = 0; col < this.props.boardWidth; col++) {
              field[row][col] = field[row - 1][col]
            }
          }

          // Check if the row is the last
          row = this.props.boardHeight
        }
      }

      // Update state - update score, update number of tiles, change level
      this.setState(prev => ({
        score: prev.score + 1 * prev.level,
        tileCount: prev.tileCount + 1,
        level: 1 + Math.floor(prev.tileCount / 10)
      }))

      // Prepare new timer
      let timerId

      // Reset the timer
      clearInterval(this.state.timerId)

      // Update new timer
      timerId = setInterval(
        () => this.handleBoardUpdate('down'),
        1000 - (this.state.level * 10 > 600 ? 600 : this.state.level * 10)
      )

      // Use new timer
      this.setState({
        timerId: timerId
      })

      // Create new tile
      tile = Math.floor(Math.random() * 7 + 1)
      x = parseInt(this.props.boardWidth) / 2
      y = 1
      rotate = 0

      // Test if game is over - test if new tile can't be placed in field
      if (
        field[y + tiles[tile][rotate][0][1]][x + tiles[tile][rotate][0][0]] !== 0 ||
        field[y + tiles[tile][rotate][1][1]][x + tiles[tile][rotate][1][0]] !== 0 ||
        field[y + tiles[tile][rotate][2][1]][x + tiles[tile][rotate][2][0]] !== 0 ||
        field[y + tiles[tile][rotate][3][1]][x + tiles[tile][rotate][3][0]] !== 0
      ) {
        // Stop the game
        this.setState({
          gameOver: true
        })
      } else {
        // Otherwise, render new tile and continue
        field[y + tiles[tile][rotate][0][1]][x + tiles[tile][rotate][0][0]] = tile
        field[y + tiles[tile][rotate][1][1]][x + tiles[tile][rotate][1][0]] = tile
        field[y + tiles[tile][rotate][2][1]][x + tiles[tile][rotate][2][0]] = tile
        field[y + tiles[tile][rotate][3][1]][x + tiles[tile][rotate][3][0]] = tile
      }
    }

    // Update state - use new field, active x/y coordinates, rotation and activeTile
    this.setState({
      field: field,
      activeTileX: x,
      activeTileY: y,
      tileRotate: rotate,
      activeTile: tile
    })
  }

  /**
   * @description Stops and resumes the game
   * @memberof Tetris
   */
  handlePauseClick = () => {
    this.setState(prev => ({
      isPaused: !prev.isPaused
    }))
  }

  /**
   * @description Resets the game
   * @memberof Tetris
   */
  handleNewGameClick = () => {
    // Create an empty board
    let field: any[] = []

    for (let y = 0; y < this.props.boardHeight; y++) {
      let row = []

      for (let x = 0; x < this.props.boardWidth; x++) {
        row.push(0)
      }

      field.push(row)
    }

    // Set starting column to center
    let xStart = Math.floor(parseInt(this.props.boardWidth) / 2)

    // Initialize state with starting conditions
    this.setState({
      activeTileX: xStart,
      activeTileY: 1,
      activeTile: 2,
      tileRotate: 0,
      score: 0,
      level: 1,
      tileCount: 0,
      gameOver: false,
      field: field
    })
  }

  render() {
    return (
      <div className="tetris">
        {/* Tetris board */}
        <TetrisBoard
          field={this.state.field}
          gameOver={this.state.gameOver}
          score={this.state.score}
          level={this.state.level}
          rotate={this.state.tileRotate}
        />

        {/* Buttons to control blocks */}
        <div className='tetris__block-controls'>
          <button className="btn" onClick={() => this.handleBoardUpdate('left')}>Left</button>

          <button className="btn" onClick={() => this.handleBoardUpdate('down')}>Down</button>

          <button className="btn" onClick={() => this.handleBoardUpdate('right')}>Right</button>

          <button className="btn" onClick={() => this.handleBoardUpdate('rotate')}>Rotate</button>
        </div>

        {/* Buttons to control game */}
        <div className="tetris__game-controls">
          <button className="btn" onClick={this.handleNewGameClick}>New Game</button>

          <button className="btn" onClick={this.handlePauseClick}>{this.state.isPaused ? 'Resume' : 'Pause'}</button>
        </div>
      </div>
    )
  }
}

export default Tetris
```

## Index

The last piece of React/JavaScript/TypeScript you need is the index, or `index.tsx`. This will be very fast, similarly to the Tetris board component. Aside to the default imports, added by create-react-app, you will need to import the `Tetris` component from "components" and main stylesheet from "styles".

You will then render the `Tetris` component into the DOM. Make sure to add the `boardWidth` and `boardHeight` props with some numeric value. Remember that these two props are used to specify the number of rows, and columns in each row. In other words, they specify the width and height of the game board.

```
///
// src/index.tsx

// Import React and ReactDOM
import * as React from 'react'
import * as ReactDOM from 'react-dom'

// Import Tetris component
import Tetris from './components/tetris'

// Import styles
import './styles/styles.css'

// Import service worker
import * as serviceWorker from './serviceWorker'

ReactDOM.render(<Tetris boardWidth="14" boardHeight="20" />, document.getElementById('root'))

// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: https://bit.ly/CRA-PWA
serviceWorker.unregister()
```

## Styles

As the very last step, you can add some styles to make your Tetris game look better. Well, at least some styles so player can distinguish between empty board column and tiles, and also other types of tiles. You can use `background-color` to do this (see "Colors for tiles" part). The rest is up to you.

```
/* Main styles */
html {
  box-sizing: border-box;
  font: 16px sans-serif;
}

*,
*::before,
*::after {
  box-sizing: inherit;
}

.tetris {
  padding: 8px;
  margin: 0 auto;
  width: 500px;
}

.tetris-board {
  display: flex;
  justify-content: space-between;
}

.tetris-board__info {
  width: 100px;
}

.tetris-board__text {
  font-size: 18px;
  color: #111;
}

.tetris-board__row {
  display: flex;
}

/* Styles for tiles */
[class*=col-] {
  padding: 12px;
  border: 1px solid #1a1c19;
}

/* Default (empty) board column */
.col-0 {
  background-color: #020202;
}

/* Colors for tiles */
.col-1 {
  background-color: #f21620;
}

.col-2 {
  background-color: #10ac84;
}

.col-3 {
  background-color: #5f27cd;
}

.col-4 {
  background-color: #d925cf;
}

.col-5 {
  background-color: #48dbfb;
}

.col-6 {
  background-color: #fd4964;
}

.col-7 {
  background-color: #72fa4e;
}

/* Styles for buttons */
.tetris__block-controls,
.tetris__game-controls {
  margin-top: 16px;
  display: flex;
  justify-content: center;
}

.tetris__game-controls {
  margin-bottom: 16px;
}

.btn {
  padding: 12px 21px;
  font-size: 15px;
  color: #fff;
  background-color: #3498db;
  border: 0;
  cursor: pointer;
  transition: background-color .25s ease-in;
}

.btn:hover {
  background-color: #2980b9;
}

.tetris__block-controls .btn:first-child,
.tetris__game-controls .btn:first-child {
  border-top-left-radius: 4px;
  border-bottom-left-radius: 4px;
}

.tetris__block-controls .btn:not(:first-child),
.tetris__game-controls .btn:not(:first-child) {
  border-left: 1px solid #2980b9;
}

.tetris__block-controls .btn:last-child,
.tetris__game-controls .btn:last-child {
  border-top-right-radius: 4px;
  border-bottom-right-radius: 4px;
}
```

## Epilogue: How to build simple Tetris game with React & TypeScript

Congratulations! You've just finished this tutorial and build your own Tetris game! The best part? You've also worked on your JavaScript, React and TypeScript skills and hopefully, also learned something new. As you can see, learning can be fun. Are you up for another challenge? How about adding history of games? You can find inspiration [here].

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[create-react-app]: https://github.com/facebook/create-react-app
[npx]: https://github.com/zkat/npx
[TypeScript]: https://www.typescriptlang.org/
[lifecycle methods]: https://reactjs.org/docs/react-component.html#the-component-lifecycle
[export]: https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt5/#the-export-statement
[here]: https://blog.alexdevero.com/how-to-build-simple-tic-tac-toe-game-with-react/#phase-4-storage
[class]: https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt7/#classes
[]:

<!--
### Meta:
-
-->

<!--
#### Resources:
-
-->
