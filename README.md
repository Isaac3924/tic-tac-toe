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

Moving to out `style.css` file, it is what defines the styles for the React App. The instructions refer to the first two CSS selectors `*` and `body` which defines the majority of the style for the app. I do notice that those selectors are listed twice in the expected code provided. Some quick research seems to suggest this is a typo duplicate code, as the values inside the selectors are identical. I will see about removing them later.

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
