# SMRT

SMRT is a **SM**all experimental library from building functional and **R**eactive web **T**emplates.

> I am so smart, SMRT, I mean SMART.
>
> Homer J. Simpson

SMRT can be used to add reactivity to an existing webpage, or to build a whole app.

[🎮 View the Code Playground here](https://codesandbox.io/s/smrt-playground-xby6v?file=/src/index.js)

## Getting Started

Add SMRT to your web page or app either as a package or as a script.

`npm install smrt` or `<script src="https://unpkg.com/smrt"></script`

## Example
```
import smrt from 'smrt';

const myApp = smrt();

const helloWorldState = {
  userName: 'World',
};

const appTitle = {
  tag: 'h1',
  innerHTML: () => `Hello ${helloWorldState.userName} 👋`,
};

const userNameInput = {
  tag: 'input',
  value: () => helloWorldState.userName,
  events: {
    input: event => {
      helloWorldState.userName = event.target.value;
    },
  },
};

const helloWorldApp = {
  tag: 'div',
  children: [
    appTitle,
    userNameInput,
  ],
};

const parent = document.querySelected('#app');
myApp.run(helloWorldApp, parent, [myAppState]);
```

**IMPORTANT** Notice how in the example above `userNameInput.value` and `appTitle.innerHTML` are functions that return a value from `helloWorldState`? This makes that part of your DOM reactive to state changes.

[Further examples can be found here](https://github.com/jjohnson1994/smrt/tree/master/examples)

## Docs

- [Reactivity](#reactivity)
  - [How Reactivity Works](#how-reactivity-works)
- [Creating Components](#creating-components)

### Reactivity
Component values can be reactive, or non reactive. A value will only be reacted to if it is read from a function in a components spec.

#### How Reactivity Works
Reactivity works by replacing each value in a state with a pair of getters and setters. When a component is first rendered, any template updates that require a value from state are recorded again that state item (in an array of observers). Then when a state item is change, the recorded updates are replayed, keeping the DOM upto date.

### Creating Components
A component can be defined as either a function or an object. Functions are useful when you want to:
- Pass a value to a component when it's fist rendered e.g. a prop,
- Write [helpers for commonly used elements](https://github.com/jjohnson1994/smrt/blob/master/examples/common-elements.js),
- Run an action when you component is first rendered e.g. a call to the server.

Otherwise most components will be simple objects.
