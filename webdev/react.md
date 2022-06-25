# React

>  **Source:**
> [Complete Intro to React v7 and Intermediate React v4 (Brian Holt, Frontend Masters)](https://btholt.github.io/complete-intro-to-react-v7)

React uses two packages: **React** and **ReactDOM**.

```jsx
import { render } from "react-dom";
import * as React from "react";
import { useEffect, useState } from "react";  // destructuring
```

## Components

React does not use the MVC design pattern. The general idea is to instead separate concerns by components. You combine the model, view, and controller for a component together in a single file, but keep each component separate. This leads to lots of small components where components can also be used to build other components.

There are two types of React components.

### Function components

Below is an example of a simple function component. The `return` statement uses JSX to write HTML directly inside JavaScript. This is later compiled to JavaScript by Babel using `React.createElement()`.

Function components are simpler to write and cover most use cases. Sometimes it may make more sense to use class components.

```jsx
const MyFunctionComponent = (props) => {
  const headerText = "Hello world!";
  
  return (
    <div>
    	<h1>{headerText}</h1>
    </div>
  );
};

export default MyFunctionComponent;
```

### Class components

Has largely been replaced by function components. The lifecycle function `ComponentDidMount` is largely equal to `useEffect`. Class components can still be useful if you need all the lifecycle functions.

## Hooks

Hooks are variables that can be listened to and updated in your code. They should always appear in the same sequence each time the code runs and thus they should never be put in conditional statements or loops.

The most common hooks by far are `useState` and `useEffect`.

### useState

```jsx
const [name, setName] = useState("Ola Nordmann") // destructuring; argument is default value

setName("Sindre Beba"); // more commonly some user input

return (
  <h1>Hello {name}!</h1>
);
```

### useEffect

```jsx
useEffect( () => {
  /* code that will be called outside the render function, usually side-effect type actions */
  return /* cleanup routine, runs at component unmount  */
}, [ name ] ); // will run whenever the "name" state is updated
```

- `useEffect` is how you recreate `componentDidMount`, `componentDidUpdate`, and `componentDidUnmount`.
- Having an empty array as the second argument will cause `useEffect` to only be called once in the beginning.
- Providing no second argument will cause `useEffect` to be called every time a state is updated.

### useContext

```jsx
const UserContext = createContext([
  {
    userName: "DefaultUserName"
  },
  (obj) => obj
]);

const TopLevelComponent = () => {
  const userState = useState({ userName: "sindre" });
  
  return (
    <UserContext.Provider value={userState}>
    	<LowerLevelComponent />
    </UserContext.Provider>
  );
};

const LowerLevelComponent = () => {
  const [user, setUser] = userContext(UserContext);
  
  return (
    <p>{`User is ${user.userName}`}</p>
  );
};
```

- `useContext` solves the "prop drilling" problem where you previously had to pass a value through several layers of components to use it at one of the lower levels.
- It should be used sparingly as it can make it harder to debug your code since it makes it less obvious where values are updated. A rule of thumb is to only use it for application wide states such as a user context or enabling dark theme.
- Context values can also be updated from the lower level component and the updated values will be available in the top level component.

### useRef

```jsx
const counterRef = useRef(0);
// ...
console.log(counterRef.current)

const headerElement = useRef();
// ...
<h1 ref={ (element) => headerElement.current = element }
```

- `useRef` is useful when you need the most current value across renders, or if you need the same value across components.

### useReducer

```jsx
const reducer = (state, action) => {
  switch (action.type) {
    case "INCREMENT":
    	return Object.assign({}, state, { value: value + 1});
    case "DECREMENT":
    	return Object.assign({}, state, { value: value - 1});
    default:
      return state;
  }
}
// ...
const [{ value }, dispatch] = useReducer(reducer, { value: 0 });
// ...
<button onClick={ () => dispatch({ type: "INCREMENT" }) }>+</button>
<button onClick={ () => dispatch({ type: "DECREMENT" }) }>-</button>
```

- Provides Redux-style reducers. A reducer takes a state and an action and returns an updated state.
- `useReducer` makes the code testable using unit tests since the same arguments will always produce the same result.

### Other hooks

There are more hooks in React, but they are rarely used. It's also possible to create your own custom hooks.

Some of the other hooks are `useMemo`, `useCallback`, `useLayoutEffect`, `useImperativeHandle`, `useDebugValue`, and `useId`.

## React Router

Use to create a single page application (SAP). Wraps everything inside a `<BrowserRouter>` tag.

## Other features

**Dev tools** - all browsers has a React dev tools extension.

**Error boundaries** - a way to catch errors from components.

**Next.js** - higher level framework built on top of React.

**Portals** - use the state in one component, but render in different parts of the DOM.

**Production mode** - build the application in production mode with `NODE_ENV=production`. It has a  smaller size and is faster. A bundler like Parcel can do this automatically.

**Redux** - handles state. `useContext` can often be used instead, but Redux is still useful for more complex cases.

**Remix** - higher level framework built on top of React.

**Strict mode** - the `<StrictMode>` tag can be used to future proof the code. By wrapping your code inside the tag, React will give you warnings about soon to be deprecated code.

## React Quick Start

Step 1: Create a new directory and initialize a Git repo

```sh
mkdir MyProject
cd MyProject
git init
```

Step 1.1: Set up a new npm project

```sh
npm init -y
```

Step 1.2: Add `.gitignore`

```
node_modules
.parcel-cache/
dist/
.env
.DS_Store
coverage/
.vscode/
```

Step 2: Set up Prettier

```sh
npm install --global prettier # if not already installed
npm install -D prettier
echo "{}" > .prettierrc
```

Step 2.1: Create a file `.prettierrc`

```json
{}
```

Step 2.2: Add script to `package.json`

```json
"format": "prettier --write \"src/**/*.{js,jsx}\""
```

Step 3: Install ESLint

```sh
npm install -D eslint eslint-config-prettier
```

Step 3.1: Create a file `.eslintrc.json`

```json
{
  "extends": ["eslint:recommended", "prettier"],
  "plugins": [],
  "parserOptions": {
    "ecmaVersion": 2022,
    "sourceType": "module",
    "ecmaFeatures": {
      "jsx": true
    }
  },
  "env": {
    "es6": true,
    "browser": true,
    "node": true
  }
}
```

Step 3.2: Add script to `package.json`

```json
"lint": "eslint \"src/**/*.{js,jsx}\" --quiet"
```

Step 4: Install Parcel

```sh
npm install -D parcel
```

Step 4.1: Add script to `package.json`

```json
"dev": "parcel src/index.html"
```

Step 5: Install React

```sh
npm install react react-dom
```

Step 6: Install TypeScript

```sh
npm install -D typescript
npx tsc --init
```

Step 6.1: Update `tsconfig.json`

```json
"target": "es2021",
"jsx": "preserve",
```

Step 6.2: Install types

```sh
npm install -D @types/react @types/react-dom
```

