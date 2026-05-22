# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in your browser.

The page will reload when you make changes.\
You may also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can't go back!**

If you aren't satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you're on your own.

You don't have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn't feel obligated to use this feature. However we understand that this tool wouldn't be useful if you couldn't customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Code Splitting

This section has moved here: [https://facebook.github.io/create-react-app/docs/code-splitting](https://facebook.github.io/create-react-app/docs/code-splitting)

### Analyzing the Bundle Size

This section has moved here: [https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size](https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size)

### Making a Progressive Web App

This section has moved here: [https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app](https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app)

### Advanced Configuration

This section has moved here: [https://facebook.github.io/create-react-app/docs/advanced-configuration](https://facebook.github.io/create-react-app/docs/advanced-configuration)

### Deployment

This section has moved here: [https://facebook.github.io/create-react-app/docs/deployment](https://facebook.github.io/create-react-app/docs/deployment)

### `npm run build` fails to minify

This section has moved here: [https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify](https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify)



# Documentation:

# Tic Tac Toe Game in React — Documentation

## Overview

This project is a simple Tic Tac Toe game built with React. It allows two players to play turn by turn, detects a winner or draw, and includes a reset button to restart the game.

The component uses React hooks such as `useState` and `useRef` to manage game state and update the UI.

---

## Features

* Two-player turn-based gameplay
* Cross (`X`) and circle (`O`) symbols for players
* Winner detection for all 8 possible winning combinations
* Draw detection when all cells are filled
* Reset option to start a new game
* Simple and interactive UI

---

## Project Structure

The main logic is implemented in the `TicTacToe.jsx` component.

### Imported Modules

* `React, useRef, useState` from React
* `./TicTacToe.css` for styling
* `circle.png` as the circle icon
* `cross.png` as the cross icon

---

## Component Explanation

### 1. Game Data Storage

```js
let data = ["", "", "", "", "", "", "", "", ""]
```

This array stores the current value of each cell on the board.

* Empty string means the cell is empty
* `x` means the cross player has played
* `o` means the circle player has played

---

### 2. State Variables

```js
let [count, setCount] = useState(0);
let [lock, setLock] = useState(false);
```

* `count` tracks how many moves have been played
* `lock` prevents further moves after a win or draw

---

### 3. Refs

```js
let titleRef = useRef(null);
let cell1 = useRef(null);
...
let cell9 = useRef(null);
```

Refs are used to directly update:

* the title text
* each individual board cell

A list of all cell refs is stored here:

```js
let cell_array = [cell1, cell2, cell3, cell4, cell5, cell6, cell7, cell8, cell9];
```

---

## Main Functions

### `toggle(e, num)`

This function runs when a player clicks a cell.

#### What it does:

* Stops the move if the game is locked
* Checks whose turn it is using `count % 2`
* Inserts either a cross or circle image into the clicked cell
* Updates the `data` array
* Increases the move count
* Calls `checkWin()` after every move

#### Logic:

* Even count → cross player (`x`)
* Odd count → circle player (`o`)

---

### `checkWin()`

This function checks whether any player has won or whether the game is a draw.

#### Winning combinations checked:

* 3 horizontal rows
* 3 vertical columns
* 2 diagonals

If a winning pattern is found, it calls `won(winner)`.

If all 9 moves are played and there is no winner, it declares a draw.

---

### `won(winner)`

This function runs when a player wins.

#### What it does:

* Locks the game so no more moves can be made
* Updates the title to show the winner
* Displays the winning icon in the heading

If `winner === "x"`, the cross player wins.
If `winner === "o"`, the circle player wins.

---

### `reset()`

This function restarts the game.

#### What it does:

* Unlocks the board
* Clears the `data` array
* Resets move count to 0
* Restores the default title
* Clears all 9 cells

---

## Game Flow

1. The game starts with an empty board.
2. The first player clicks a cell.
3. The game places either `X` or `O` depending on the turn.
4. The board is checked for a winner.
5. If no one wins, the next player moves.
6. The game ends when a player wins or when all cells are filled.
7. The reset button starts a new match.

---

## Turn Handling

The game uses this logic to switch turns:

```js
if (count % 2 === 0)
```

* `0, 2, 4, 6, 8` → Cross player
* `1, 3, 5, 7` → Circle player

---

## Winning Combinations

The game checks these positions in the `data` array:

* Rows:

  * `[0, 1, 2]`
  * `[3, 4, 5]`
  * `[6, 7, 8]`

* Columns:

  * `[0, 3, 6]`
  * `[1, 4, 7]`
  * `[2, 5, 8]`

* Diagonals:

  * `[0, 4, 8]`
  * `[2, 4, 6]`

---

## UI Elements

* **Title**: Shows game status and winner message
* **Board**: 3×3 grid of clickable cells
* **Reset Button**: Clears the board and starts again

---

## Limitations

This version works correctly, but it directly manipulates the DOM using refs and `innerHTML`, which is not the most React-friendly approach.

### Possible improvements:

* Use React state to render the board instead of direct DOM updates
* Prevent repeated clicks on the same cell
* Show current player turn in the UI
* Add score tracking
* Add better accessibility support

---

## Summary

This Tic Tac Toe game is a basic React project that demonstrates:

* component creation
* state management
* refs
* conditional logic
* winner detection
* reset functionality

It is a good beginner project for understanding how React can be used to build interactive games.

