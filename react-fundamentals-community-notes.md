# React Fundamentals

## Create DOM with Javascript

Type `"module"` is what you want for your script type as opposed to the old `"text/Javascript"`

```
<script type="module">
```

The benefit of working with React is that working with the DOM is imperative and while imperative code isn't bad, an application with _just_ imperative code allows for bugs to easily slip in.

## Create DOM with React

React: responsible for creating react elements (kinda like `document.createElement()`)
ReactDOM: responsible for render react elements to the DOM (kinda like `rootElement.append()`)

There exists a special `typeof` operator that gets the data type of its operand, either a literal or a data structure, and returning the data type.

The keys of strings need to be unique.
  - When it's a primitive value, React doesn't need a key because there's no state to be maintained with certain elements

## Create Dom with JSX

JSX is not Javascript, it's a special syntax built on top of Javascript.

Kent's :key:: Being able to look at JSX and understand what that looks like if you were to rewrite it to `React.createElement`, will help you a lot in understanding what's possible with JSX.

Because it's not standard syntax, it needs to be compiled (typically Babel or Typescript).

`${}` will let it know to go to Javascript when interpolating JSX.

If we want to exit 'JSX land' and enter 'Javascipt land', then come back to 'JSX land' to interpolate some values, that's where JSX interpolation comes into play.

An interpolated value can only be an expression.

The order in which you apply the spreading of props matters, as the **latest** one will win out and take preference. Whatever comes last in the event of a conflict will win.

## Create Custom Components

Components are functions that return things that are renderable.

React Fragments group a list of children without adding extra nodes to the DOM.
- Good read: [React Fragments](https://reactjs.org/docs/fragments.html)

We capitalize types in JSX to indicate the tag refers to a React component.

_User Question_: Why function and not the format `const ... = () => {}`?
- Kent  uses `function` because using `function` doesn't matter where it appears in a Javascript file, the definition and declaration get hoisted to the top of the closure. However, if you use the `const ... = () => {}` format in the wrong place, you get errors.

## Styling

There exist two primary methods to style React components
- Inline styles with `style` prop
- Regular CSS with the `className` prop

It doesn't matter what order the `className` shows up, but for the `style` prop it does matter which order it shows up in.

## Simple Forms

You are able to attach a submit handler to a form element with the `onSubmit` prop, which will be called with the submit event that has a `target`.
- The `target` is simply a reference to the `<form>` DOM node which has a reference to the elements of the form which can be used to get the values out the form.

_SyntheticEvent_: A fake event. React does this because it has a pool of objects that it grabs events from. Basically, it passes the SyntheticEvent to you, you do stuff with it, then it puts it back in the pool of objects.
- [Synthetic Events Read](https://reactjs.org/docs/events.html)

## Dynamic Forms

The way you use _state_ is with a special hook called `useState`.
- `React.useState` accepts a default initial value and returns an array. Most of the time, you will destructure the array to get the _state_ and a _state updater function_.

Ternaries are very useful in implementation to save errors from certain inputs.

## Controlled Forms

You can't switch from _uncontrolled_ to _controlled_ form, so you must begin by controlling originally.

**Controlled Form**: Where you control the state of the form. When you provide a value, you control it by storing the state somewhere and keeping it up to date yourself.

**Uncontrolled Form**: Where React is managing/updating the state as the user made changes and it would call your on-change handler.
- State is handled internally.


## Rendering Lists of Data

An array of renderable things is also a renderable thing. Due to this, you can use it as a child. There are problems when you make changes to the order of them or changes over time.

We have to uniquely identify elements in arrays.

`array.filter` filters items and creates a new array with all elements that pass the test implemented by the provided function.

If you don't provide a key, the array index is the default for that value.

If what you are rendering _needs_ to maintain states, you need a proper key.
- If you _don't provide_ a key, React will assume array index as the key),
- If you _provide_ a proper key, it let's React determine what happened between the different renders.
