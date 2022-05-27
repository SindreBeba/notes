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

There are two types of React components.

- Function components
- Class components

Below is an example of a simple function component. The `return` statement uses JSX to write HTML directly inside the JavaScript. This is later compiled to JavaScript by Babel using `React.createElement`.

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

## Hooks

Hooks are variables that can be listened to and updated in your code. They should always appear in the same sequence each time the code runs and thus they should never be put in conditional statements or loops.

### useState

```jsx
const [name, setName] = useState("Ola Nordmann") // argument is default value

setName("Sindre Beba"); // more commonly some user input

return (
    <h1>Hello {name}!</h1>
);
```

### Other hooks

There are many more hooks. Some of them are:

- useEffect
- useContext
- useRef
- Custom hooks

## React Router

Use to create a single page application (SAP).