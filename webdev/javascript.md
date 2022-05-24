# JavaScript

## Types

JavaScript is a loosely typed programming language, meaning that the variable types are not declared with the variable. It's also a dynamically typed language where type checking happens at run time. This means that variables don't have types, but values do.

`undefined`, `string`, `number`, `boolean`, `object`, and `symbol` are the primitive types in JavaScript, and you can use the `typeof` operator to check the type of a value.

However, both declared variables with no assigned value and undeclared variables will return `undefined` as the type when using `typeof`.

There is also a historical bug present in JavaScript where `typeof null` will return `object`.

## Truthy and falsy

Because of JavaScript's type coercion, values will be coerced into booleans when encountered in certain contexts, e.g., an `if`-statement.

All values are "truthy" except for a set of values that will always be "falsy". These values are `false`, `0`, `-0`, `NaN`, `""`, `null`, and `undefined`.

## Equality

The two equality operators in JavaScript differ in that `==` allows type coercion and `===` does not.

```js
2 == "2"  // true
2 === "2" // false

null == undefined  // true
null === undefined // false
```

## Functions and callbacks

Functions can be both declared as well as stored in variables. A variable containing a function can then be used as an argument to another function as a callback.

Callback functions can also be created anonymously and used as a callback without begin stored in a variable.

It's worth considering using named function expressions instead of arrow functions if this increases readability.

```js
// Function declaration
function add(x, y) {
    return x + y;
}

add(6, 2);

// Function expression
let subtract = function(x, y) {
    return x - y;
};

// Function with callback parameter
function doMath(x, y, cb) {
    return cb(x, y);
}

doMath(6, 2, subtract);

// Anonymous arrow function as callback
doMath(6, 2, (x, y) => {
    return x * y;
});

// Named function expression as callback
doMath(6, 2, function divide(x, y) {
    return x / y;
});
```

## Scope

`var` is globally scoped when declared outside a function, and functionally scoped when declared inside. `let` is block scoped.

```js
var a = "a"; // global scope
let b = "b"; // global scope

function foo() {
    var c = "c"; // function scope
    let d = "d"; // function scope
}

if (true) {
    var e = "e"; // also global scope
    let f = "f"; // block scope
}

// only a, b, and e are available here
```

## Closure

> A closure is a function that remembers its outer variables and can access them.

[Closure - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)

[Closure - JavaScript.Info](https://javascript.info/closure)

## Classes and this

When referring to `this` in the global scope or inside a function, `this` will refer to the **global object** which in a browser is the `Window` object.

Inside an object (classes are objects in JavaScript), `this` refers to the object.

```js
class User {
    constructor(userName) {
        this.name = userName;
    }
    login(password) {
        console.log(`Logging in as ${this.name}`);
        application.auth(this.name, password);
    }
}

let myUser = new User("Sindre");
myUser.login(encryptedPassword);
```

It's possible to provide the context of `this` for a function by using the `call` function.

```js
function login(password) {
    console.log(`Logging in as ${this.user}`);
    application.auth(this.user, password);
}

let userContext = {
    user: "Sindre"
};
login.call(userContext, encryptedPassword);
```