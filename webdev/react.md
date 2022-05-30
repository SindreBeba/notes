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

### Other hooks

There are many more hooks, and you can even create your own custom hooks. Some of the other hooks are:

- `useContext`
- `useRef`

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