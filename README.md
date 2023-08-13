# Tic Tac Toe

This project is a React tutorial from React's documentation which can be found here: [Tutorial: Tic-Tac-Toe](https://react.dev/learn/tutorial-tic-tac-toe#inspecting-the-starter-code).

## Branches

I will document my work step by step here with each individual branch that I'll be merging alongside the names of the section of the tutorial.

### Overview

#### Inspecting the starter code

The beginnning steps are not quite as relevevant for me as I'm developing this locally in VSC as my development environment. It examines the CodeSandbox editor, but then checks the code in the App.js, which is the same.

Within `App.js` it creates a component And reminds us that compnents are used in React to represent part of a UI in an application.

The first line `export default function Square(){` defines a function naming it `Square`. With the `export` JS keyword I'm making it accessible outside of the `App.js` file and the `default` keyword alerts my other files using my code that it's the main function within my file.

The next line has `return <button className="square">X</button>;` with a closing curly bracket as the finishing line, closing off the component for now. Our one line of code in our `Square` compnent uses `return` to return the proceeding value, that value being a JSX element. As a reminder, a JSX element is a combination of JS code and HTML tags that helps describe what we wish to display. Now, `<button>` itself is a JSX element and has one property or prop listed with it, that property being `className="square"`. This prop tells CSS how to style the button. Finally, `X` is only the text being displayed inside the button, and we have the closing tag of `/button` for the JSX element.

Moving to our `style.css` file, it is what defines the styles for the React App. The instructions refer to the first two CSS selectors `*` and `body` which defines the majority of the style for the app. I do notice that those selectors are listed twice in the expected code provided. Some quick research seems to suggest this is a typo as duplicate code, as the values inside the selectors are identical. I will see about removing them later. As for the other mentioned selector of `.square`, it defines the style of any component that has the `className` of `square`, which as stated, our `Square` component does have a button JSX element with the `className` property set to it.

Finally, we look at the `index.js` file which we will not be changing throughout. This acts as the bridge between our `Square` component in our `App.js` file and the web browser. We have the first five lines looking as such:
```
import React, { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import "./styles.css";

import App from "./App";
```
These lines bring together all the necesary pieces we need: React, the React library to talk to web browsers or the React DOM(Document Object Module), the styles for our components, and the components we made in `App.js`. The rest of the file injects the end result into the index.html file by naming `root` and having it equal the the necessary information.

#### Building the Board

We'll be spending the rest of development within `App.js`, which currently only has a single square for our board. React components can only return a single JSX element though, so in order to actually make multiple squares to represent the board, we will need to use fragments which wraps mulptiple adjacent JSX elements like so:
```
<>
  <JSX_element></JSX_element>
  <JSX_element></JSX_element>
</>
```
However, if we just repeat this 9 times, we will merely have a row of squares. To remedy this, we would need to add some `div`s and CSS classes to differentiate them. Additionally, it recommends giving each square a number instead of an X to ensure they are placed correctly. Naming the divs `board-row` will let it use the css selector with the same name that is already setup in our css.

Running it, it displays as expected. For now before continuing, let's try getting rid of that extraneous code in our css.

Having gotten rid of it, is still runs with no issue.

Moving back to our App.js we do have a misnomer, our component isn't so much a square anymore than it is a board, so let's change `Square` to `Board`. Of course it still runs as our button classNames are still `square`.

### Passing Data Through Props

The next thing we should do is change how the buttons function; changing the value of a square from empty to "X" when clicked. With how it's currently built I would need to repeat the same same code 9 times which is not ideal. If you ever see similar code repeated take it as an opportunity to make a helper method or function, but in this case we are working in react which uses components, so we'll make a reuseable component here.

We'll have the function be called `Square` and have it return the button code for our squares and update our `board-row`s to use `Square` instead. Like this, we have each square displaying only the number 1. In order to rectify this, we'll use props to pass the value each square should have from the parent component of `Board` to the child `Square`.

The prop we're naming is `value` which is a JSX element, so we'll wrap it in curly brackets to be properly displayed in the return. But since none of our squares name the new value prop it'll be just an empty board. If we have each square name `value="X"` X being whatever, then we can easily fill out the numbers as they were.

### Making an Interactive component

Now to actually make it interactable. Let's declarea function within the Square component called `handleClick` that will do a console log of 'clicked!' for us. Then we'll add another prop named onClick for our button JSX element that's returned from `Square`, which will be equal to our `handleClick` function.

Running the app now and within our console, we should see a log of `clicked!`. The instructions expect to see this on a console tab in CodeSandbox. We can pull up our own console by inspecting the page and going to our own console tab seeing we are also accruing instances of it. But we want it to remember being clicked, so we will make sure to use state.

React provides this with a special function called `useState` that you can call from your component. Let's start by storing the current value of the `Square` in state, and change it when the `Square` is clicked.

We'll first mport `useState` at the top of the `App.js` file and remove the `value` prop from the `Square` component. We'll add in a new line at the start of the `Square` that calls `useState`. In that line of code we will have it return a state variable valled `value`.

`value` will store the value and `setValue` is a function we will use to change the value. The null passed into useState is used as the initial value for the state variable `value`, so we're making this equal to `null` and effectively letting the program remember that.

Looking further into this, `const [value, setValue]` is an array which is using Array destructuring to create 2 variables `value` and `setValue`. The first variable in the array will be assigned the corresponding value of `useState(null)` as stated earlier, and the `setValue` variable holds the function that allows us to update our afforementioned variable `value`. But for now it is not yet used. Let's get to that.

Our `Square` component no longer had props to accept, so let's get rid of those in our `board-row`s and let's use our `setValue` function in our `handleClick` function, giving it the value of 'X' to pass in.

So we'll be calling the `set` function from an `onClick` handler which will be telling React to re-render the `Square` whenever its `<button>` is clicked. Each `Square` at this point has its own state holding its own `value` stored there independent from one another.

### React Developer Tools
We'll be able to check the props and state of all of our React components by inspecting our webpage to see each of them. Working from Chrome you can richt-click th page and hit inspect to get to immediately get to the elements tab, or using the shortcut 'ctrl+shift+c'.

## Completing the Game

Now we're on the next section of fininshing the game, which will have us needing to alternate assigning the value of an "X" and "O" to our `Square`s on our `Board`.

### Lifting state up

So right now our `Square` components maintain a part of our game's state. To check for a winner in this game the `Board` will need to somehow know the state of each of the 9 `Square` components. What's our bestapproach for this? You could ask each square, but this seems a bad idea as it will bloat our code which will hurt its readability and leave it more succeptible to logic errors and bugs. What we should do instead is to store the game's state in the parent `Board` component instead of in each `Square`. The `Board` can tell each `Square` what to display by passing a prop.

**To collect data from multiple children, or have 2 child components communicate with each other, declare the shared state in their parent component instead. The parent component can pass that state back down to the children via props. This keeps the child components in sync with each other and wit their parent.**

It is common to lift state into a parent component when React components are refactored.

But enough talk, let's implement this. We will edit the `Board` component so that it delcares a state variable named `squares` that defaults to an array of 9 nulls for the 9 squares with the following code:
`const [squares, setSquares] = useState(Array(9).fill(null));`

More specifically, `Array(9).fill(null)` creates an array with 9 elements and sets each of them to `null`. With the `useState()` call around it, it delcares a `squares` state variable that's initally set to that array. Each entry in the array corresponds to the values of a square. When you fill the board in later, the `squares` array will look something like this:
`['O', null, 'X', 'X', 'X', 'O', 'O', null, null]` 

Now the `Board` component need to pass the `value` prop down to each `Square` that it renders, and edit the `Square` component to receive the `value` prop again. Which will require removing the componment's own stateful tracking of `value` and the `onClick` prop.

Next, we need to change what happens when a `Square` is clicked. The `Board` component now maintains which squares are filled, so we'll need to create a way for the `Square` to update the `Board`'s state. Since state is private to a component that defiens it, you cannot update the `Board`'s state directly from `Square`.

Instead, we'll pass down a function from the `Board` component to the `Square` component, and we'll have `Square` call that function when a square is clicked. We'll start with the function that the `Square` componet will call when it is clicked. We'll call that function `onSquareClick` and add it to the function to the `Square` component's props.

After that, we'll connect the `onSquareClick` prop to a function uin the `Board` component that we'll name `handleClick`. To connect `onSquareClick` to `handleClick` we'll pass a function to the `onSquareClick` prop of the first `Square` component.

Finally, we'll define the `handleClick` function inside the Board component to update the `squares` array holding our board's state. The function creates a copy of the `squares` array naming it `nextSquares` using the JS `slice()` Array method. Next, the function updates the new array copy i.e. `nextSquares` to add an "X" to the first element/starting index of `[0]`.

By calling the `setSquares` function we let React knpw that the state of the component had changed, which will trigger a re-render of the components that use the `squares` state in the `Board` as well as its child components which are the `Square` components that make up the board itself.

But this only works for our first square, as the `nextSquares` index is currently set to 0. So let's uopdate our `handleClick` function to actually act on an appropriate index.  So we'll have the function pass in an rgument of `i` as is typical to represent the index position.

So now that we have the parameter setup, we'll need to act on it. My first thought was to directly pass it in the `return` in the JSX like so: `<Square value={squares[0]} onSquareClick={handleClick(0)} />`

However, the tutorial says this will not work as th `handleClick(0)` will be a part of rendering the board component. Because `handleClick(0)` alters the state of trhe board component be calling `setSquares`, our entire board will be re-rendered again, which would run `handleClick(0)` again which makes an infinite loop.

When we were passing `onSquareClick={handleClick}` we were passing the `handleClick` function down as a prop, meaning we weren't calling it, but now we are calling the function right away which is why it would run too early. We don't want to call `handleClick` until the user clicks.

One solution suggested is create functions called `handleFirstSquareClick`, `handleSecondSquareClick` etc, that will call `handleClick(1)` etc. We would pass these functions down as props on each one which would solve the infinite loop, but defining 9 different functions is too severe a bloat as a solution for this problem. Instead, we'll use this new trick it teaches us.

`<Square value={squares[0]} onSquareClick={() => handleClick(0)} />` This will be the code we will be using. the focus here is `() =>`. This syntax is called an arrow function, it is a shorter way to define functions. When the square is clicked the code after the `=>` or the arrow will run, calling `handleClick(0)` and so on with each square. With this, we are able to place "X"s on our squares.

We now have state handling in the `Board` component, which passes props to the child `Square` components so that they can be displayed correctly. When clicking on a `Square`, the child `Square` component now asks the parent `Board` component to update the state of the board. When the `Board`'s state changes, both the `Board` component and every child `Square` re-renders automatically. Keeping the state of all squares in the `Board` component will also allow it to dtermine the winner in the future.

So, to summarize:
1. Cliking on a square runs the function that the `button` received as its `onClick` prop from the `Square`, which is set equal to the vaue passed in via the `onSquareClick` prop of the `Square` component. which we assign in the `Board` parent component directly with JSX, calling the `handleClick` function with a certain value, to represent the index. In the case of the first upper left most square, it is 0.
2. Using the passed in argument of 0 it  knows to update the first element of the `squares` array from null to "X".
3. Now the `squares` state of the `Board` component was updated, so the `Board` and all its children re-render. This then causes the `value` prop of the `Square` component with the index of 0 to change from null to "X".

Keep in mind that in React, the convention is to use `onSomething` names for props which represent events and `handleSomething` for the cfunction definitions which handle those events.

### Why immutability is important

Now, we're going to look into why in `handleClick` we called `.slice()` to vreate a copy of the `squares` array instead of modifying the existing array. To explain why, we need to discuss immutability and why immutability is important to learn.

There are genberally 2 approaches to changing data, the first approach is to mutate the data by directly changing the data's values and the second approach is to replace the data with new copy which has the desired changes. Do. since `.slice()` just creates a copy of the array, the actual array doesn't change which gives us several benefits. Immutability makes complex features much easier to implement, such as the "time travel" feature we will be implementing late that lets us review the game's history and "jump back" to past moves. This functionality isn't specific to games think of typical software's ability to undo and redo certain actions. Avoiding direct data manipulation lets us keep previous versions of the data intact, and reuse them later.

There is also another beneift to immutability. By default, all child-components re-render automatically whan the state of a parent component changes. This includes even the child components that weren't affected by the change. Although re-rendering is not by itself noticeable to the user (you shouldn't actively try to avoid it), you might want to skip re-rendering a part of the tree that clearly wasn't affected by it for performance reasons. Immutability makes it vey cheap for components to compare whehter their data has changed or not.

### Taking Turns

Now it's time to add in the next important feature to our game, being able to add "O"s to our board.

We'll set the first move to be "X" by default. Let's keep track of this by adding another piece of state to the board component by naming a state variable of `xIsNext` in an array with another varible named `setXIsNext`. They will be defined as `useState(true)` which will give them state and the ultimate boolean value of `true`.

We'll have it that each time the `handleClick` function is called the `xIsNext` vlaue will be flipped to determine which player goes next and the game's state will be saved. We'll update the `Board`'s `handleClick` function to flip the value of `xIsNext`.

This will aloow us to switch between this bool state when needed. However, we will still be able to affect an already marked square, able to overwrite its value of "X" with "O" and vice-versa. When we are marking establishing the value of a square we are not first checking to see if the square already has an "X", "O", or a null value there already. We can fix this bt returning early. We'll check to see if the square already has a value or it's null. If the square is already filled, we will `return` in the `handleClick` function early-before it tries to update the board state, thus ending the function before we can change it.

### Declaring a winner

Now that the players can take turns, we'll want to show when the game is won and there are no more turns to make. To do this, we'll need to add a helper function that we will name `calculateWinner` that will take an array of 9 squares, checks for a winner and returns `X`, `O`, or `null` as appropriate.

The logic is setup with a sqaures parameter to pass in. It defines the `lines` variable as an array of 8 arrays that each hold one of the 8 possible combinations of three index locations to win a game. Next, we have a for loop that runs 8 times via the length of our `lines` array, incrementing the value of `i` by 1, starting it at 0. Within the for loop we name an array of `[a, b, c]` and have it be equal to `lines[i]`. Next, we have an if check to see if `squares[a]` hasa a value, and if that value is equal to `squares[b]` and `squares[c]`. So each location of the value of `squares` we pass in is checled, and if it passes, then we return the value held in `squares[a]`. If it ddoesn't then we return null. This could definetly be refactored for faster time, though. If I ordered the array, I could use binary search to cut down on the potential search time. Not that it matters with data this small... a potential refactor for later. However, I think it's ultimately fruitless as our array will stay limited in size and keeping a linear search won't take up too much time or memory.

We'll run `calculateWinner(squares)` in our `Board` component's `handleClick` function to check if a player has won. We can perform this check at the same time we check if a user has clicked a square that already has an "X" or an "O".

To let players know that the game is over, we can display test such as "Winner: X" or "Winner: O". To do this we'll add a `status` section to our `Board` component. The status will display if the game is over and if the game is ongoing we'll display which player's turn is next.

The game can now recognize winners and tell us whose turn it is. But it cannot recognize draws, the search could be better optimized, and we still have to implement the time travel feature. Let's see about adding the win condition.

## Refactoring
Need to add in the logic for if the game ends in a draw.

### Draw 
To start, we will look in the `calculateWinner` function. If we add in an else if statement after checking to see if we have a winning combination, we'll havethis else if see if the `squares` prop passed in as an array will use the already defined method of `.every()` to see if each element is not `null`. If it does, then we know each square is filled, but none create a winning combo. We'll have `calculateWinner` return the string "Draw" which will give us the outcome of "Winner: Draw" if the condition is met.

## Adding time travel

Now, let's make it possible to return to previous turns.

### Storing a history of moves

If we mutated the `squars` array, immplementing 'time travel' would be very difficult.

However we used `slice()` to create a copy of the `squares` array after every move, treating the original array as immutable. This will allow us to store every past version of the `squares` array, and navigate between the turns that have already happened.

We'll store the past `squares` arrays in another array called `history`, which we'll store as a new state variable. The `history` array represents all boards states, from the first to the last move.

### Lifting state up, again

We will now write a new top-level componnent called `Game` to display a list of past moves, where we will place the `history` state that contains the entire game history.

Placing the `history` state into the `Game` component will let us remove the `squares` state from its child `Board` component. Just like when we "lifted state up" from the `Square` component into the `Board` component, we will now lift it up from the `Board` into the top-level `Game` component. This gives the `Game` component full control over the `Board`'s data and lets it instruct the `Board` to render previous turns from the `history`.

First, when creating the `Game` component we'll give it the `export default` declaration and remove it from the `Board` component. We'll then of course have it render the `Board` component and some markup. Again, remember that this tells our `index.js` file to use the `Game` coponent as the top-level componwnt instead of our `Board` component. The addditional `div`s returned by the `Game` component are making room for the game information we'll add to the board later.

Next, we'll add some state to the `Game` component to track which player is next and the history of moves.
```
const [xIsNext, setXIsNext] = useState(true);
const [history, setHistory] = useState([Array(9).fill(null)]);
```

Make note how `[Array(9).fill(null)]` is an array with a single item, which itself is an array of 9 `null`s.

To render the squares for the current move, you'll want to read the last squares array from the `history`. We don't need `useState` for this- we already have enough information to calcualte it during rendering: `const currentSquares = history[history.length - 1];`

Next, we'll create a `handlePlay` function with a parameter of `nextSquares` inside the `Game` component that will be called by the `Board` component to update the game. Pass `xIsNext`, `currentSquares`, and `handlePlay` as props to the `Board` component its props being `xIsNext`, `squares`, and `onPlay` respectively.

Now we'll make the `Board` component be fully controlled by the props it receives. We'll change the `Board` component to take the three aforementioned props, the third being a new function that `Board` can call with the updated squares array when a player mekes a move, additionally, we'll remove the first two lines of the `Board` function that call `useState`.

With `SetSquares` and `setXIsNext` removed, no longer defined in `Board`, we will need to remove our references of them in our logic within the `handleClick` function, replacingthem with a single call to our new `onPlay` function so that the `Game` component can update the `Board` when the user clicks a square.

The `Board` component is fully controlled by the props passed to it by the `Game` component. We need to implement the `handlePlay` function in the `Game` component to get the game working again.

`handlePlay` will need to now deal with our `useState` variables since `Board` no longer does. More specifically, it needs to update `Game`'s state to trigger a re-render but we don't have a `setSquares` function that we can call any more- we're now using the `history` state variable to store this information. We'll want to update `history` by appending the updated `squares` array as a new history entry. We also want to toggle `xIsNext`, just as Board used to do.

`[...history, nextSquares]` creates a new array taht contains all the items in `history`, followed by `nextSquares`. `...history` is using the spread syntax to enumerate all the items in `history`.

For example, if `history` is `[[null,null,null], ["X",null,null]]` and `nextSquare` is `["X",null,"O"]`, then the new `[...history, nextSquares]` array will be `[[null,null,null], ["X",null,null], ["X",null,"O"]]`.

At this point we've moved the state to live in the `Game` component, and the UI should be fully working, just as it was before the refactor.


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
