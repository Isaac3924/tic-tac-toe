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

###Making an Interactive component

Now to actually make it interactable. Let's declarea function within the Square component called `handleClick` that will do a console log of 'clicked!' for us. Then we'll add another prop named onClick for our button JSX element that's returned from `Square`, which will be equal to our `handleClick` function.

Running the app now and within our console, we should see a log of `clicked!`. The instructions expect to see this on a console tab in CodeSandbox. We can pull up our own console by inspecting the page and going to our own console tab seeing we are also accruing instances of it. But we want it to remember being clicked, so we will make sure to use state.

React provides this with a special function called `useState` that you can call from your component. Let's start by storing the current value of the `Square` in state, and change it when the `Square` is clicked.

We'll first mport `useState` at the top of the `App.js` file and remove the `value` prop from the `Square` component. We'll add in a new line at the start of the `Square` that calls `useState`. In that line of code we will have it return a state variable valled `value`.

`value` will store the value and `setValue` is a function we will use to change the value. The null passed into useState is used as the initial value for the state variable `value`, so we're making this equal to `null` and effectively letting the program remember that.

Looking further into this, `const [value, setValue]` is an array which is using Array destructuring to create 2 variables `value` and `setValue`. The first variable in the array will be assigned the corresponding value of `useState(null)` as stated earlier, and the `setValue` variable holds the function that allows us to update our afforementioned variable `value`. But for now it is not yet used. Let's get to that.

Our `Square` component no longer had props to accept, so let's get rid of those in our `board-row`s and let's use our `setValue` function in our `handleClick` function, giving it the value of 'X' to pass in.

So we'll be calling the `set` function from an `onClick` handler which will be telling React to re-render the `Square` whenever its `<button>` is clicked. Each `Square` at this point has its own state holding its own `value` stored there independent from one another.

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
