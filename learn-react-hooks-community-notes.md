# Learn React Hooks Community Notes

A workshop by Kent C. Dodds

## useState: greeting

Common built-in hooks include:
- `React.useState`
- `React.useEffect`
- `React.useContext`
- `React.useRef`
- `React.useReducer`

React has a feature called **one-way data flow** (sometimes referred to as **one-way binding**) that keeps everything _modular_ and _fast_. It means the data has one way to be transferred to other parts of an application. In React, this is usually implying the state is passed to the `View` and `child` components.

There are **controlled** and **uncontrolled** inputs - a _controlled_ component has the form data handled by state within a component, while an _uncontrolled_ component stores its data in the DOM, not the component.

Hooks can only be called in the body of a function component or within other hooks.

## useEffect: persistent state

The way you should think about `useEffect()` is that its purpose is to _synchronize_ the state of the world (i.e. bluetooth API, HTTP request, geolocation, DOM manipulation) with the state of the application.
- Kent's :key:: Keep things synchronized, then optimize from there.

`useEffect()` accepts a second argument.

## Lifting state

Useful read: [Rules of Hooks](https://reactjs.org/docs/hooks-rules.html)

Plugin: [eslint-plugin-react-hooks](https://www.npmjs.com/package/eslint-plugin-react-hooks)

To share state between two sibling components, we need to '_lift the state_'.
- **Lift the state**: performance to find the lowest common parent shared between the two components and placing the state management there, and then passing the state and a mechanism for updating that state down into the components that need it.

The only thing that distinguishes a _regular function_ from a _custom hook_ is that a custom hook uses other hooks.

All custom hooks must start out with the prefix `use...()` so we know they should only be called within a function component and nowhere else.

Often, we lump state into any data that changes the state. While it's true, we can categorize it into different things.
- _UI State_: The dropdown is open/the according is open/a checkbox is checked
- _Server Cache_: Not state at all, it's a cache of what state lives on the server. It's accessed by components all over an application and usually managed by a third party library.

One thing to keep in mind is when you are creating a React app is that performance is not necessarily an issue, as React is generally very fast so refactoring for it _can_ be redundant to a certain extent.

## useState: tic tac toe

When you need to use more than one element of state in a component, `React.useState` will be called more than once.
- It is important to note each call to `React.useState` will give you a unique state and updater function.

When you have derived state that is a little more than complicated, it can be helpful to put it in a _separate_ function.

Anytime you're updating state and referencing the previous state, you should probably use an **update handler** or an **update function** because you'll run into fewer bugs. It is especially important if you're doing that asynchronously.
- Kent's :key:: If you don't like complicated rules, always use the function form because you won't run into any problems doing this.

We don't manipulate state in React, we update it.

**Managed State**: State that you need to explicitly manage
**Derived State**: State that you can calculate based on other state

## useRef and useEffect: DOM interaction

Dandy library: [vanilla-tilt.js](https://micku7zu.github.io/vanilla-tilt.js/)

**useRef()**: A hook that gives you a reference to a DOM node or a reference to anything
- The point of `useRef()` is so that you can store something that's attached to a specific component and you can change that value without triggering a re-render.

Typically you have to access the DOM in React and manipulating the DOM is a common side effect. You'll typically do that in a `React.useEffect()`.
- There's a special ref prop you can apply to React elements to JSX that'll give you a reference to the DOM node when it's been created.

Only after React has updated the DOM do you have access to the DOM.

The beauty of React components is that they're tight boxes, operating totally independent of one another. Essentially, you can use as many as you would like.

Using refs that makes your function _not_ item potent can be problematic.

## useEffect: HTTP requests

`useEffect()` returns a cleanup function, so you can't use async-await as your callback. You can, but you have to structure it differently.
- If you want to use async-await, your callback function can't be async-await.

When making HTTP requests, we do it within a `useEffect()` hook callback, which assures us whenever certain changes take place, we apply the side-effects based on those changes.
- With the `useEffect()` hook, you can't return anything other than a cleanup function.
