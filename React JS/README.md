---
title: React JS
created: '2021-06-21T03:34:13.881Z'
modified: '2022-04-24T11:54:10.983Z'
---

# React JS

## The Virtual DOM

### The problem with actual DOM
Browser constructs a tree like structure called DOM. Whenever, any section is changed, the DOM is re-constructed and then rendered. Modern web applications involve a lot of large and small changes. The DOM manipulation is slower and what makes it more slower is that most frameworks update DOM much more frequently.

### The saviour : Virtual DOM
Virtual DOM or VDOM is a lightweight copy of actual DOM object. More specifically, it is a javascript object representation of DOM. It has the same properties as DOM but lacks the real power to directly change what's on screen.

### How does it optimize the website?
Here’s what happens when we try to update the DOM in React:

1. The entire virtual DOM gets updated, each DOM object.
2. The virtual DOM gets compared to what it looked like before you updated it. React figures out which objects have changed.
3. The changed objects, and the changed objects only, get updated on the real DOM.
4. Changes on the real DOM cause the screen to change.

Diffing : Process of figuring out exactly which virutal DOM objects have changed. The algorithm is called Diffing Algorithm.

## Why React?
* React is fast. Apps made in React can handle complex updates and still feel quick and responsive.

* React is modular. Instead of writing large, dense files of code, you can write many smaller, reusable files. React’s modularity can be a beautiful solution to JavaScript’s maintainability problems.

* React is scalable. Large programs that display a lot of changing data are where React performs best.

* React is flexible. You can use React for interesting projects that have nothing to do with making a web app. People are still figuring out React’s potential.

* React is popular. While this reason has admittedly little to do with React’s quality, the truth is that understanding React will make you more employable.

## JSX
JSX is a syntax extension for JavaScript. It was written to be used with React. JSX code looks a lot like HTML.

What does “syntax extension” mean? In this case, it means that JSX is not valid JavaScript. Web browsers can’t read it!

If a JavaScript file contains JSX code, then that file will have to be compiled. That means that before the file reaches a web browser, a JSX compiler will translate any JSX into regular JavaScript. So, a browser doesn't read JSX.

* If a JSX expression takes up more than one line, then you must wrap the multi-line JSX expression in parentheses.

```
const jsx = (
  <a href="https://www.example.com">
    <h1>
      Click me!
    </h1>
  </a>
);
```

* A JSX expression must have exactly one outermost element.
```
// wrong
const paragraphs = (
  <p>I am a paragraph.</p>
  <p>I, too, am a paragraph.</p>
);

// right
const paragraphs = (
  <div id="i-am-the-outermost-element">
    <p>I am a paragraph.</p>
    <p>I, too, am a paragraph.</p>
  </div>
);
```

* Any code in between the tags of a JSX element will be read as JSX, not as regular JavaScript! JSX doesn’t add numbers - it reads them as text, just like HTML. To make it treat as javascript variable, expression to be evaluated, enclose them in curly brackets.

* If the expression on the left of the `&&` evaluates as true, then the JSX on the right of the `&&` will be rendered. If the first expression is false, however, then the JSX to the right of the && will be ignored and not rendered.
```
const tasty = (
  <ul>
    <li>Applesauce</li>
    { !baby && <li>Pizza</li> }
    { age > 15 && <li>Brussels Sprouts</li> }
    { age > 20 && <li>Oysters</li> }
    { age > 25 && <li>Grappa</li> }
  </ul>
);
```

* A list needs `keys` if either of the following are true:

1. The list-items have memory from one render to the next. For instance, when a to-do list renders, each item must “remember” whether it was checked off. The items shouldn’t get amnesia when they render.

2. A list’s order might be shuffled. For instance, a list of search results might be shuffled from one render to the next.

### Render JSX on screen
```ReactDOM.render(<h1>Render me!</h1>, document.getElementById('container'));```

## React Components

`React.Component` is a JavaScript class. To create your own component class, you must subclass `React.Component`. You can do this by using the syntax class `YourComponentNameGoesHere extends React.Component {}`.

Component class variable names must begin with capital letters!

`render()` method must be present in custom component. It must return a statement which is usually, JSX expression.

```
import React from 'react';
import ReactDOM from 'react-dom';

class MyComponentClass extends React.Component {
  render() {
    return <h1>Hello world</h1>;
  }
}

// component goes here:
ReactDOM.render(<MyComponentClass />, document.getElementById('app'));
```

## Create A React App with Boilerplate
```npm create-react-app myfirstreactapp``` is used to create an app.
`create-react-app` has taken care of setting up the main structure of the application as well as a couple of developer settings

Its directory structure is:
![react app](../images/create-react-app.PNG)

### Directory Importance

#### .gitignore
This is the standard file used by the source control tool git to determine which files and directories to ignore when committing code. While this file exists, create-react-app did not create a git repo within this folder. If you take a look at the file, it has taken care of ignoring a number of items (even .DS_Store for Mac users)

#### package.json
This file outlines all the settings for the React app.

* `name` is the name of your app
* `version` is the current version
* `"private": true` is a failsafe setting to avoid accidentally publishing your app as a public package within the npm ecosystem.
* `dependencies` contains all the required Node modules and versions required for the application. In the screenshot above, the react version specified is ^16.13.1. This means that npm will install the most recent major version matching 16.x.x. In contrast, you may also see something like ~1.2.3 in package.json, which will only install the most recent minor version matching 1.2.x.
* `scripts` specifies aliases that you can use to access some of the react-scripts commands in a more efficient manner. For example, running npm test in your command line will run react-scripts test --env=jsdom behind the scenes.
You will also see two more attributes, `eslintConfig` and `browserslist`. Both of these are Node modules having their own set of values. `browserslist` provides information about browser compatibility of the app, while `eslintConfig` takes care of the code linting.
#### node_modules
This directory contains dependencies and sub-dependencies of packages used by the current React app, as specified by package.json. If you take a look, you may be surprised by how many there are.
#### package-lock.json
This file contains the exact dependency tree installed in node_modules/. This provides a way for teams working on private apps to ensure that they have the same version of dependencies and sub-dependencies. It also contains a history of changes to package.json, so you can quickly look back at dependency changes.
#### public
This directory contains assets that will be served directly without additional processing by webpack. index.html provides the entry point for the web app. You will also see a favicon (header icon) and a manifest.json.

The manifest file configures how your web app will behave if it is added to an Android user’s home screen (Android users can “shortcut” web apps and load them directly from the Android UI).

## Interaction among React Components
When you use React.js, every JavaScript file in your application is invisible to every other JavaScript file by default.

### Through import and export
import syntax
```import { Component } from './somefile.js'```
export syntax
```export const fun();```
```export let variable=5```

### Through `props`
Accessing all props in a component: ```this.props```

Passing props to a component:
```
<Example message="This is some top secret info." />
<Greeting myInfo={["top", "secret", "lol"]} />
<Greeting name="Frarthur" town="Flundon" age={2} haunted={false} />
```

Every component’s props object has a property named children.
`this.props.children` will return everything in between a component’s opening and closing JSX tags.

```
// Example 1
<BigButton>
  I am a child of BigButton.
</BigButton>

// this.props.children return 'I am a child...'

// Example 2
<BigButton>
  <LilButton />
</BigButton>

// this.props.children return <LilButton />

// Example 3
<BigButton />  // returns undefined
```
__NOTE__: If a component has more than one child between its JSX tags, then this.props.children will return those children in an array. However, if a component has only one child, then this.props.children will return the single child, not wrapped in an array.

Default props
```
class Button extends React.Component {
  render() {
    return (
      <button>
        {this.props.text}
      </button>
    );
  }
}

// defaultProps goes here:
Button.defaultProps = { // always a object
  text: 'I am a button'
} // will be displayed if no props are passed

ReactDOM.render(
  <Button />,
  document.getElementById('app')
);
```

### Through state
```
import React from 'react';
import ReactDOM from 'react-dom';

class Mood extends React.Component {
  constructor(props) {
    super(props);
    this.state = { mood: 'good' }; //initialize the state
    this.toggleMood = this.toggleMood.bind(this); // binding event handler to this keyword
  }

  toggleMood() { //event handler
    const newMood = this.state.mood == 'good' ? 'bad' : 'good';
    this.setState({ mood: newMood });
  }

  render() {
    return (
      <div>
        <h1>I'm feeling {this.state.mood}!</h1>
        <button onClick={this.toggleMood}>
          Click Me
        </button>
      </div>
    );
  }
}

ReactDOM.render(<Mood />, document.getElementById('app'));
```
State are specific to components. They may be passed down to other components as props.
States are not changed in `render()` function. They are always chanded through `this.setState()` wrapped in a function that gets triggered once a event occured.

*Reason behing binding*: State changing methods need to be bind with `this` keyword in constructor due to the way event handlers functions in js.

__NOTE__: *Why `this.setState` doesn't work inside `render()`?*
Any time that you call this.setState(), this.setState() AUTOMATICALLY calls .render() as soon as the state has changed.
Think of this.setState() as actually being two things: this.setState(), immediately followed by .render().
That is why you can’t call this.setState() from inside of the .render() method! this.setState() automatically calls .render(). __If .render() calls this.setState(), then an infinite loop is created.__

## Stateless and stateful components
Stateful Component: Component that has state and passes props down to stateless component
Stateless Component: Component that has no state and receives props from stateful component

Key point while creating components:
A component should never update `this.props`.

A React component should use props to store information that can be changed, but can only be changed by a different component.

A React component should use state to store information that the component itself can change.

### How does a stateless, child component update the state of the parent component?

Stateful component passes down an event handler to stateless component. Child component then uses it to update parent's state.

1. The parent component class defines a method that calls this.setState().

2. The parent component binds the newly-defined method to the current instance of the component in its constructor. This ensures that when we pass the method to the child component, it will still update the parent component.

3. Once the parent has defined a method that updates its state and bound to it, the parent then passes that method down to a child.

4. The child receives the passed-down function, and uses it as an event handler

__Benefit of using this programatic approach__:
Breaking down complex logic into separate classes that each have one job to do helps with testing and makes code more reusable.

## Component Lifecycle
The component lifecycle has three high-level parts:

1. Mounting, when the component is being initialized and put into the DOM for the first time
2. Updating, when the component updates as a result of changed state or changed props
3. Unmounting, when the component is being removed from the DOM
Every React component you’ve ever interacted with does the first step at a minimum. If a component never mounted, you’d never see it!
![component lifecycle](../images/react_diagram-lifecycle-flow.webp)

## Functional Component and Hooks
React Hooks, plainly put, are functions that let us manage the internal state of components and handle post-rendering side effects directly from our function components. Hooks don’t work inside classes — they let us use fancy React features without classes. Keep in mind that function components and React Hooks do not replace class components. They are completely optional; just a new tool that we can take advantage of.

__Benefits over class components__
No need to worry about binding functions to class instances, working with constructors, or dealing with the this keyword. With the State Hook, updating state is as simple as calling a state setter function.

### useRef Hook

`useRef` returns a reference object on which `current` stores the present value. It is similar to useState but on change of its value, re-render doesn't occur.

Calling `const reference = useRef(initialValue)` with the initial value returns a special object named reference. The reference object has a property current: you can use this property to read the reference value reference.current, or update `reference.current = newValue`. The reference object can't be modified to contain any other key. It won't also throw error in case it is modified like `reference.someThing=somevalue`.

Between the component re-renderings, the value of the reference is persistent.

References can also access DOM elements. Assign the reference to ref attribute of the element you'd like to access: `<div ref={reference}>Element</div>` — and the element is available at `reference.current: <div>Element</div>`. To set its style, we can do `reference.current.focus();`.

### useMemo Hook

`useMemo` hook is similar to useEffect except it is used in case of heavy computation. So, if there is some cryptoanalysis function or any other heavy computation function in a component, you might don't want to compute it everytime rerender happens.

```
import { useMemo } from "react";

const fibonacci = (num) => {
	if(num<=1) return 1;
	return fibonacci(num-1)+fibonacci(num+1);
}

const Component = () => {
	const [isGreen, setIsGreen] = useState(0);
	const [num, setNum] = useState(1);
	const fib = fibonacci(num);
	const fib = useMemo(() => fibonacci(num), [num]); // only computes if num has changed
	return (
		<div>
			<h1 style={{color: isGreen?'green':'red'}}>This is something</h1>
			<h2>Fibonancci of {num} is {fib}</h2>
			<button onClick={() => setNum(num+1)}></button>
		</div>
	);
}
```

`useMemo` only recalculates a value if the elements in its dependency array change (if there are no dependencies - i.e. the array is empty, it will recalculate only once). If the array is left out, it will recalculate on every render. Calling the function does not cause a re-render. Also it runs during the render of the component and not before.

`useEffect` runs after a render happens, while `useMemo` runs before


### useState Hook

`useState` returns an array consisting of two values, one is the state variable and other is its setter. So, we can use our local variable as reference to modify the state. It can also accept a function like `useState(() => {})`

`const [mood, changeMood] = useState('happy');`

Often, the next value of our state is calculated using the current state. In this case, it is best practice to update state with a callback function. If we do not, we risk capturing outdated, or “stale”, state values.
See example for state using previous state values:
```
import React, { useState } from 'react';

export default function Counter() {
  const [count, setCount] = useState(0);

  const increment = () => setCount(prevCount => prevCount + 1);

  return (
    <div>
      <p>Wow, you've clicked that button: {count} times</p>
      <button onClick={increment}>Click here!</button>
    </div>
  );
}
```
#### Review of useState
* With React, we feed static and dynamic data models to JSX to render a view to the screen

* Use Hooks to “hook into” internal component state for managing dynamic data in function components

* We employ the State Hook by using the code below:

  * `currentState` to reference the current value of state

  * `stateSetter` to reference a function used to update the value of this state

  * the `initialState` argument to initialize the value of state for the component’s first render

```
const [currentState, stateSetter] = useState( initialState );
```

* Call state setters in event handlers

* Define simple event handlers inline with our JSX event listeners and define complex event handlers outside of our JSX

* Use a state setter callback function when our next value depends on our previous value

* Use arrays and objects to organize and manage related data that tends to change together

* Use the spread syntax on collections of dynamic data to copy the previous state into the next state like so: `setArrayState((prev) => [ ...prev ])` and `setObjectState((prev) => ({ ...prev }))`

* Split state into multiple, simpler variables instead of throwing it all into one state object

### useCallback


`useCallback` is quite similar and indeed it's implemented with the same mechanisms as `useMemo`. Our goal is that `ExpensiveComputationComponent` only re-renders whenever it absolutely must. Typically whenever React detects a change higher-up in an app, it re-renders everything underneath it. This normally isn't a big deal because React is quite fast at normal things. However you can run into performance issues sometimes where some components are bad to re-render without reason.

In this case, we're using a new feature of React called `React.memo`. This is similar to `PureComponent` where a component will do a simple check on its props to see if they've changed and if not it will not re-render this component (or its children, which can bite you.) `React.memo` provides this functionality for function components. Given that, we need to make sure that the function itself given to `ExpensiveComputationComponent` is the _same_ function every time. We can use `useCallback` to make sure that React is handing _the same fibonacci_ to `ExpensiveComputationComponent` every time so it passes its `React.memo` check every single time. Now it's only if `count` changes will it actually re-render (as evidenced by the time.)

Try removing the useCallback call and see if you get the the count to 40+ that the page crawls as it updates every second.

[callback](https://codesandbox.io/s/github/btholt/react-hooks-examples-v4/tree/main?file=/src/Callback.js)

```
import { useState, useEffect, useCallback, memo } from "react";

const ExpensiveComputationComponent = memo(({ compute, count }) => { // wrap expensive component in memo, re-renders only if props change for example, spreadsheet component with 1000 lines
  return (
    <div>
      <h1>computed: {compute(count)}</h1>
      <h4>last re-render {new Date().toLocaleTimeString()}</h4>
    </div>
  );
});

const CallbackComponent = () => {
  const [time, setTime] = useState(new Date());
  const [count, setCount] = useState(1);
  useEffect(() => {
    const timer = setTimeout(() => setTime(new Date()), 1000);
    return () => clearTimeout(timer);
  });

  const fibonacci = (n) => {
    if (n <= 1) {
      return 1;
    }

    return fibonacci(n - 1) + fibonacci(n - 2);
  };

  return (
    <div>
      <h1>useCallback Example {time.toLocaleTimeString()}</h1>
      <button onClick={() => setCount(count + 1)}>
        current count: {count}
      </button>
      <ExpensiveComputationComponent
        compute={useCallback(fibonacci, [])}
        count={count}
      />
    </div>
  );
};

export default CallbackComponent;

```


### useEffect
We use the Effect Hook to run some JavaScript code after each render, such as:

* fetching data from a backend service
* subscribing to a stream of data
* managing timers and intervals
* reading from and making changes to the DOM

There are three key moments when the Effect Hook can be utilized:
1. When the component is first added, or mounted, to the DOM and renders
2. When the state or props change, causing the component to re-render
3. When the component is removed, or unmounted, from the DOM.

The first argument is a function and second is dependecy array for selective rendering. The Effect Hook is used to call another function that does something for us so there is nothing returned when we call the useEffect() function.

#### Why clean up essentail for event handlers and how to do it with useEffect?
If our effect didn’t return a cleanup function, then a new event listener would be added to the DOM’s document object every time that our component re-renders. Not only would this cause bugs, but it could cause our application performance to diminish and maybe even crash!

```
useEffect(()=>{
  document.addEventListener('keydown', handleKeyPress);
  return () => {
    document.removeEventListener('keydown', handleKeyPress);
  };
})
```

Because effects run after every render and not just once, React calls our cleanup function before each re-render and before unmounting to clean up each effect call.

If our effect returns a function, then the useEffect() Hook always treats that as a cleanup function. React will call this cleanup function before the component re-renders or unmounts. Since this cleanup function is optional, it is our responsibility to return a cleanup function from our effect when our effect code could create memory leaks.

#### Dependency array
The dependency array is used to tell the useEffect() method when to call our effect and when to skip it. Our effect is always called after the first render but only called again if something in our dependency array has changed values between renders.

If dependency array is empty, it will call effect when a component first mounts and if a cleanup function is returned by effect, calling that when the component unmounts.

If dependency array has some variables, that means, re-render will happen every time the variables change.

### useLayoutEffect

`useLayoutEffect` is almost the same as `useEffect` except that it's synchronous to render as opposed to scheduled like `useEffect` is. If you're migrating from a class component to a hooks-using function component, this can be helpful too because `useLayout` runs at the same time as `componentDidMount` and `componentDidUpdate` whereas `useEffect` is scheduled after. This should be a temporary fix.

The only time you _should_ be using `useLayoutEffect` is to measure DOM nodes for things like animations. In the example, I measure the textarea after every time you click on it (the onClick is to force a re-render.) This means you're running render twice but it's also necessary to be able to capture the correct measurments.

```
import { useState, useLayoutEffect, useRef } from "react";

const LayoutEffectComponent = () => {
  const [width, setWidth] = useState(0);
  const [height, setHeight] = useState(0);
  const el = useRef();

  useLayoutEffect(() => {
    setWidth(el.current.clientWidth);
    setHeight(el.current.clientHeight);
  });

  return (
    <div>
      <h1>useLayoutEffect Example</h1>
      <h2>textarea width: {width}px</h2>
      <h2>textarea height: {height}px</h2>
      <textarea
        onClick={() => {
          setWidth(0);
        }}
        ref={el}
      />
    </div>
  );
};

export default LayoutEffectComponent;
```

It is generally used for animations and measuring accurate layouts. If we would be using `useEffect`, we don't know when it will be called.

### useDebugValue

Here's another hook that's baked into React that I don't foresee many of you using but I still want you to know it's there. It, like useImperativeHandle, is more built for library authors.

useDebugValue allows you to surface information from your custom hook into the dev tools. This allows the developer who is consuming your hook (possibly you, possibly your coworker) to have whatever debugging information you choose to surfaced to them. If you're doing a little custom hook for your app (like the breed one we did in the Intro course) this probably isn't necessary. However if you're consuming a library that has hooks (like how react-router-dom has hooks) these can be useful hints to developers.

Normally you'd just use the developer tools built into the browser but CodeSandbox has the dev tools built directly into it. Just know that normally you'd use the browser extension.

```
import { useState, useEffect, useDebugValue } from "react";

const useIsRaining = () => {
  const [isRaining, setIsRaining] = useState(false);

  useEffect(() => {
    // pretend here you'd make an API request to a weather API
    // instead we're just going to fake it

    setIsRaining(Math.random() > 0.5);
  }, []);

  useDebugValue(isRaining ? "Is Raining" : "Is Not Raining");

  return isRaining;
};

const DebugValueComponent = () => {
  const isRaining = useIsRaining();

  return (
    <div>
      <h1>useDebugValue Example</h1>
      <h2>Do you need a coat today? {isRaining ? "yes" : "maybe"}</h2>
    </div>
  );
};

export default DebugValueComponent;

```

### Rules of Hooks
There are two main rules to keep in mind when using Hooks:

1. only call Hooks at the top level: When React builds the Virtual DOM, the library calls the functions that define our components over and over again as the user interacts with the user interface. React keeps track of the data and functions that we are managing with Hooks based on their order in the function component’s definition. For this reason, we always call our Hooks at the top level; we never call hooks inside of loops, conditions, or nested functions.
2. only call Hooks from React functions

#### Hooks gives us the flexibility to organize our code in different ways, grouping related data as well as separating concerns to keep code simple, error-free, reusable, and testable!

## Advanced React

### Styling
#### Inline style
```
<h1 style={{ color: 'red' }}>Hello world</h1>
```
The outer curly braces inject JavaScript into JSX. They say, “everything between us should be read as JavaScript, not JSX.”

The inner curly braces create a JavaScript object literal. They make this a valid JavaScript object

#### Style Name syntax
In regular JavaScript, style names are written in hyphenated-lowercase:
```
const styles = {
  'margin-top': '20px',
  'background-color': 'green'
};
```
In React, those same names are instead written in camelCase:
```
const styles = {
  marginTop: '20px',
  backgroundColor: 'green'
};
```

#### Style value syntax
In React, if you write a style value as a number, then the unit "px" is assumed.
`{ fontSize: 30 }` means 30px.
In regular JS, style values are almost always strings. Even if a style value is numeric, you usually have to write it as a string so that you can specify a unit. For example, you have to write "450px" or "20%".

### Separate container components from presentational component
Separating container components from presentational components is a popular React programming pattern. It helps to answer that question. It shows you when it might be a good time to divide a component into smaller components. It also shows you how to perform that division.

If a component has to have state, make calculations based on props, or manage any other complex logic, then that component shouldn’t also have to render HTML-like JSX.

The functional part of a component (state, calculations, etc.) can be separated into a container component.

The presentational component’s only job is to contain HTML-like JSX. It should be an exported component and will not render itself because a presentational component will always get rendered by a container component.

You divided the GuineaPigs component into a container component and a presentational component: containers/GuineaPigsContainer.js and components/GuineaPigs.js.

Here are the steps we took:

1. Identified that the original component needed to be refactored: it was handling both calculations/logic and presentation/rendering
2. Copied the original component to a new containers/ folder and renamed it GuineaPigsContainer
3. Removed all of the presentation/rendering code from the container component
4. Removed all of the calculation/logic code from the presentational component
5. Accessed the presentational component from within the container using import and export
6. Edited the container’s render() method to render the presentational component with the proper props

In this programming pattern, the container component does the work of figuring out what to display. The presentational component does the work of actually displaying it. __If a component does a significant amount of work in both areas, then that’s a sign that you should use this pattern!__

### PropTypes
Components interact among each other with passing of props. So, it is essentials that props must be validated for what they are intended for. Also, __PropTypes serve documentation of props__. So, one way is to check their type.

```
import React from 'react';
import PropTypes from 'prop-types'; // must import

export class Runner extends React.Component {
  render() {
  	let miles = this.props.miles;
    let km = this.props.milesToKM(miles);
    let races = this.props.races.map(function(race, i){
      return <li key={race + i}>{race}</li>;
    });

    return (
      <div style={this.props.style}>
        <h1>{this.props.message}</h1>
        { this.props.isMetric &&
          <h2>One Time I Ran {km} Kilometers!</h2> }
        { !this.props.isMetric &&
          <h2>One Time I Ran {miles} Miles!</h2> }
        <h3>Races I've Run</h3>
        <ul id="races">{races}</ul>
      </div>
    );
  }
}

Runner.propTypes = { // always at last
  // prop: PropTypes.expected_datatype
  //isRequired for prop must to be passed else, a console warning appears
  message:   PropTypes.string.isRequired,
  style:     PropTypes.object.isRequired,
  isMetric:  PropTypes.bool.isRequired,
  miles:     PropTypes.number.isRequired,
  milesToKM: PropTypes.func.isRequired,
  races:     PropTypes.array.isRequired
};
```

Same way, propTypes for a functional component can also be validated.

### React Forms
Think about how forms work in a typical, non-React environment. A user types some data into a form’s input fields, and the server doesn’t know about it. The server remains clueless until the user hits a “submit” button, which sends all of the form’s data over to the server simultaneously.

In React, as in many other JavaScript environments, this is not the best way of doing things.

The problem is the period of time during which a form thinks that a user has typed one thing, but the server thinks that the user has typed a different thing. What if, during that time, a third part of the website needs to know what a user has typed? It could ask the form or the server and get two different answers. In a complex JavaScript app with many moving, interdependent parts, this kind of conflict can easily lead to problems.

In a React form, you want the server to know about every new character or deletion, as soon as it happens. That way, your screen will always be in sync with the rest of your application.

#### Controlled vs Uncontrolled
There are two terms that will probably come up when you talk about React forms: controlled component and uncontrolled component. Like automatic binding, controlled vs uncontrolled components is a topic that you should be familiar with, but don’t need to understand deeply at this point.

An uncontrolled component is a component that maintains its own internal state. A controlled component is a component that does not maintain any internal state. Since a controlled component has no state, it must be controlled by someone else.

Think of a typical `<input type='text' />` element. It appears onscreen as a text box. If you need to know what text is currently in the box, then you can ask the `<input />`, possibly with some code like this:

```
let input = document.querySelector('input[type="text"]');

let typedText = input.value; // input.value will be equal to whatever text is currently in the text box.
```
The important thing here is that the `<input />` keeps track of its own text. You can ask it what its text is at any time, and it will be able to tell you.

The fact that `<input />` keeps track of information makes it an uncontrolled component. It maintains its own internal state, by remembering data about itself.

A controlled component, on the other hand, has no memory. If you ask it for information about itself, then it will have to get that information through props. Most React components are controlled.

__In React, when you give an `<input />` a value attribute, then something strange happens: the `<input />` BECOMES controlled. It stops using its internal storage.__ This is a more ‘React’ way of doing things.

### Deep Concepts

#### Why do multiple JSX tags need to be wrapped?

JSX looks like HTML, but under the hood it is transformed into plain JavaScript objects. You can’t return two objects from a function without wrapping them into an array. This explains why you also can’t return two JSX tags without wrapping them into another tag or a Fragment.

#### camelCase all most of the things!

JSX turns into JavaScript and attributes written in JSX become keys of JavaScript objects. In your own components, you will often want to read those attributes into variables. But JavaScript has limitations on variable names. For example, their names can’t contain dashes or be reserved words like class.

`
For historical reasons, aria-* and data-* attributes are written as in HTML with dashes.`

#### Rules of keys

- Keys must be unique among siblings. However, it’s okay to use the same keys for JSX nodes in different arrays.
- Keys must not change or that defeats their purpose! Don’t generate them while rendering.

#### Strict Mode

React offers a “Strict Mode” in which it calls each component’s function twice during development. By calling the component functions twice, Strict Mode helps find components that break these rules.

Notice how the original example displayed “Guest #2”, “Guest #4”, and “Guest #6” instead of “Guest #1”, “Guest #2”, and “Guest #3”. The original function was impure, so calling it twice broke it. But the fixed pure version works even if the function is called twice every time. Pure functions only calculate, so calling them twice won’t change anything—just like calling double(2) twice doesn’t change what’s returned, and solving y = 2x twice doesn’t change what y is. Same inputs, same outputs. Always.

Strict Mode has no effect in production, so it won’t slow down the app for your users. To opt into Strict Mode, you can wrap your root component into <React.StrictMode>. Some frameworks do this by default.

#### Keeping components pure

Pure functions don’t mutate variables outside of the function’s scope or objects that were created before the call—that makes them impure!
- Mind its own business
- same input, same output

React is designed around this concept. React assumes that every component you write is a pure function. This means that React components you write must always return the same JSX given the same inputs.


##### Local Mutation

```
function Cup({ guest }) {
  return <h2>Tea cup for guest #{guest}</h2>;
}

export default function TeaSet() {
  return (
    <>
      <Cup guest={1} />
      <Cup guest={2} />
      <Cup guest={3} />
    </>
  );
}
```


The component changed a preexisting variable while rendering. This is often called a “mutation” to make it sound a bit scarier. Pure functions don’t mutate variables outside of the function’s scope or objects that were created before the call—that makes them impure!

However, it’s completely fine to change variables and objects that you’ve just created while rendering. It’s fine because you’ve created them during the same render, inside TeaGathering. No code outside of TeaGathering will ever know that this happened. This is called “local mutation”—it’s like your component’s little secret.

#### Side Effects

These changes—updating the screen, starting an animation, changing the data—are called side effects. They’re things that happen “on the side”, not during rendering.

In React, side effects usually belong inside event handlers. Event handlers are functions that React runs when you perform some action—for example, when you click a button. Even though event handlers are defined inside your component, they don’t run during rendering! So event handlers don’t need to be pure.

#### Render Meaning

#### Analogy

Imagine that your components are cooks in the kitchen, assembling tasty dishes from ingredients. In this scenario, React is the waiter who puts in requests from customers and brings them their orders.

#### Phases

1. **Triggering** a render (delivering the guest’s order to the kitchen)
2. **Rendering** the component (preparing the order in the kitchen)
3. **Committing** to the DOM (placing the order on the table)

#### Step 1: Trigger a render

There are two reasons for a component to render:

1. It’s the component’s initial render.
2. The component’s (or one of its ancestors’) state has been updated.

##### Initial Render

When your app starts, you need to trigger the initial render. Frameworks and sandboxes sometimes hide this code, but it’s done by calling createRoot with the target DOM node, and then calling its render method with your component:

```
import Image from './Image.js';
import { createRoot } from 'react-dom/client';

const root = createRoot(document.getElementById('root'))
root.render(<Image />);
```

##### State Update - Re-render

Once the component has been initially rendered, you can trigger further renders by updating its state with the set function. Updating your component’s state automatically queues a render. (You can imagine these as a restaurant guest ordering tea, dessert, and all sorts of things after putting in their first order, depending on the state of their thirst or hunger.)


#### Step 2 : React renders a component

**“Rendering” is React calling your components.**

- On initial render, React will call the root component.
- For subsequent renders, React will call the function component whose state update triggered the render.

This process is recursive: if the updated component returns some other component, React will render that component next, and if that component also returns something, it will render that component next, and so on. The process will continue until there are no more nested components and React knows exactly what should be displayed on screen.

React will calculate which of their properties, if any, have changed since the previous render. It won’t do anything with that information until the next step, the commit phase.


> The default behavior of rendering all components nested within the updated component is not optimal for performance if the updated component is very high in the tree. If you run into a performance issue, there are several opt-in ways to solve it described in the Performance section. Don’t optimize prematurely!

#### Step 3 : React commits changes to DOM

After rendering (calling) your components, React will modify the DOM.

- For the initial render, React will use the appendChild() DOM API to put all the DOM nodes it has created on screen.
- For re-renders, React will apply the minimal necessary operations (calculated while rendering!) to make the DOM match the latest rendering output.

React only changes the DOM nodes if there’s a difference between renders. For example, here is a component that re-renders with different props passed from its parent every second. Notice how you can add some text into the `<input>`, updating its value, but the text doesn’t disappear when the component re-renders:

```
export default function Clock({ time }) {
  return (
    <>
      <h1>{time}</h1>
      <input />
    </>
  );
}
```

React only updates the content of `<h1>` with the new time. It sees that the `<input>` appears in the JSX in the same place as last time, so React doesn’t touch the `<input>`—or its value!


After rendering is done and React updated the DOM, the browser will repaint the screen. Although this process is known as “browser rendering”, we’ll refer to it as “painting” to avoid confusion throughout the docs.

__React does not touch the DOM if the rendering result is the same as last time__

### State as Snapshot

Updating the state triggers a re-render ie, the component is called again.  The JSX you return from that function is like a snapshot of the UI in time. Its props, event handlers, and local variables were all calculated **using its state at the time of the render**.

When React re-renders a component:

1. React calls your function again.
2. Your function returns a new JSX snapshot.
3. React then updates the screen to match the snapshot you’ve returned.

As a component’s memory, state is not like a regular variable that disappears after your function returns. State actually “lives” in React itself—as if on a shelf!—outside of your function. When React calls your component, it gives you a snapshot of the state for that particular render. Your component returns a snapshot of the UI with a fresh set of props and event handlers in its JSX, all calculated **using the state values from that render**!

```
import { useState } from 'react';

export default function Counter() {
  const [number, setNumber] = useState(0);

  return (
    <>
      <h1>{number}</h1>
      <button onClick={() => {
        setNumber(number + 1);
        setNumber(number + 1);
        setNumber(number + 1);
      }}>+3</button>
    </>
  )
}
```

Try guessing how what will be number finally?

**Setting state only changes it for the next render**. During the first render, `number` was `0`. This is why, in that render’s `onClick` handler, the value of `number` is still `0` even after `setNumber(number + 1)` was called:

```
<button onClick={() => {
  setNumber(number + 1);
  setNumber(number + 1);
  setNumber(number + 1);
}}>+3</button>
```

Here is what this button’s click handler tells React to do:

1. `setNumber(number + 1)`: `number` is 0 so `setNumber(0 + 1)`.
React prepares to change `number` to 1 on the next render.
2. `setNumber(number + 1)`: `number` is 0 so `setNumber(0 + 1)`.
React prepares to change `number` to 1 on the next render.
3. `setNumber(number + 1)`: `number` is 0 so `setNumber(0 + 1)`.
React prepares to change `number` to 1 on the next render.

Even though you called `setNumber(number + 1)` three times, in this render’s event handler number is always 0, so you set the state to 1 three times. This is why, after your event handler finishes, React re-renders the component with number equal to 1 rather than 3.

#### State over time

```
import { useState } from 'react';

export default function Counter() {
  const [number, setNumber] = useState(0);

  return (
    <>
      <h1>{number}</h1>
      <button onClick={() => {
        setNumber(number + 5);
		setTimeout(() => {
          alert(number);
        }, 3000);
        alert(number);
      }}>+5</button>
    </>
  )
}
```

Try guessing what will be alerted?

```
setNumber(0 + 5);
setTimeout(() => {
  alert(0);
}, 3000);
```

The state stored in React may have changed by the time the alert runs, but it was scheduled using a snapshot of the state at the time the user interacted with it!

**React keeps the state values “fixed” within one render’s event handlers**. You don’t need to worry whether the state has changed while the code is running.

##### Recap

- Setting state requests a new render.
- React stores state outside of your component, as if on a shelf.
- When you call useState, React gives you a snapshot of the state for that render.
Variables and event handlers don’t “survive” re-renders. Every render has its own event handlers.
- Every render (and functions inside it) will always “see” the snapshot of the state that React gave to that render.
- You can mentally substitute state in event handlers, similarly to how you think about the rendered JSX.
- Event handlers created in the past have the state values from the render in which they were created.

### Queuing a Series of State Updates

```
import { useState } from 'react';

export default function Counter() {
  const [number, setNumber] = useState(0);

  return (
    <>
      <h1>{number}</h1>
      <button onClick={() => {
        setNumber(number + 1);
        setNumber(number + 1);
        setNumber(number + 1);
      }}>+3</button>
    </>
  )
}
```

Consider this snippet, you could expect that number would be increased by 3 but as we discussed about the snapshot, it will be only 1. Other than snapshot, there is one more factor at play.

**React waits until all code in the event handlers has run before processing your state updates**. This is why the re-render only happens after all these `setNumber()` calls.

This might remind you of a waiter taking an order at the restaurant. A waiter doesn’t run to the kitchen at the mention of your first dish! Instead, they let you finish your order, let you make changes to it, and even take orders from other people at the table.

This lets you update multiple state variables—even from multiple components—without triggering too many re-renders. But this also means that the UI won’t be updated until after your event handler, and any code in it, completes. This behavior, also known as **batching**, makes your React app run much faster. It also avoids dealing with confusing “half-finished” renders where only some of the variables have been updated.

**React does not batch across multiple intentional events like clicks—each click is handled separately**. Rest assured that React only does batching when it’s generally safe to do. This ensures that, for example, if the first button click disables a form, the second click would not submit it again.


#### Updating the same state multiple times before next render

If you would like to update the same state variable multiple times before the next render, instead of passing the next state value like `setNumber(number + 1)`, **you can pass a function that calculates the next state based on the previous one in the queue, like `setNumber(n => n + 1)`**. This is called updater function. It is a way to tell React to “do something with the state value” instead of just replacing it.

```
import { useState } from 'react';

export default function Counter() {
  const [number, setNumber] = useState(0);

  return (
    <>
      <h1>{number}</h1>
      <button onClick={() => {
        setNumber(n => n + 1);
        setNumber(n => n + 1);
        setNumber(n => n + 1);
      }}>+3</button>
    </>
  )
}
```

This will update the state by +3 always.

See this snippet -

```
<button onClick={() => {
  setNumber(number + 5);
  setNumber(n => n + 1);
}}>
```

![State](../images/queuing_state_updates.png)

See this snippet -

```
<button onClick={() => {
  setNumber(number + 5);
  setNumber(n => n + 1);
  setNumber(42);
}}>
```

![](../images/queuing_state_updates2.png)

##### Summarize

- An updater function (e.g. `n => n + 1`) gets added to the queue.
- Any other value (e.g. number 5) adds “replace with `5`” to the queue, ignoring what’s already queued.

##### Naming Convention

It’s common to name the updater function argument by the first letters of the corresponding state variable:

```
setEnabled(e => !e);
setLastName(ln => ln.reverse());
setFriendCount(fc => fc * 2);
```

##### Recap

- Setting state does not change the variable in the existing render, but it requests a new render.
- React processes state updates after event handlers have finished running. This is called batching.
- To update some state multiple times in one event, you can use setNumber(n => n + 1) updater function.

### Updating object States

String, number, booleans are immutable. But objects and arrays are mutable. Meaning, we can directly modify them.

```
const [pointer, setPointer] = useState({x: 1, y: 2});
pointer.x = 2; // can be done but won't trigger re-render
```

It's permitted to do but it won't trigger a re-render as set state function is not being used. Hence, React is unaware of any changes in the state.

```
setPointer({x: 2, y: 2});
```

Also, local mutation is fine. This is incorrect -
```
position.x = e.clientX;
position.y = e.clientY;
```

This local mutation is absolutely fine -
```
const nextPosition = {};
nextPosition.x = e.clientX;
nextPosition.y = e.clientY;
setPosition(nextPosition);
```

Mutation is only a problem when you change existing objects that are already in state. Mutating an object you’ve just created is okay because no other code references it yet. Changing it isn’t going to accidentally impact something that depends on it. This is called a “local mutation”. You can even do local mutation while rendering. Very convenient and completely okay.

#### Using a single event handler for multiple fields

You can also use the [ and ] braces inside your object definition to specify a property with dynamic name. Here is the same example, but with a single event handler instead of three different ones:
```
import { useState } from 'react';

export default function Form() {
  const [person, setPerson] = useState({
    firstName: 'Barbara',
    lastName: 'Hepworth',
    email: 'bhepworth@sculpture.com'
  });

  function handleChange(e) {
    setPerson({
      ...person,
      [e.target.name]: e.target.value
    });
  }

  return (
    <>
      <label>
        First name:
        <input
          name="firstName"
          value={person.firstName}
          onChange={handleChange}
        />
      </label>
      <label>
        Last name:
        <input
          name="lastName"
          value={person.lastName}
          onChange={handleChange}
        />
      </label>
      <label>
        Email:
        <input
          name="email"
          value={person.email}
          onChange={handleChange}
        />
      </label>
      <p>
        {person.firstName}{' '}
        {person.lastName}{' '}
        ({person.email})
      </p>
    </>
  );
}
```

#### Writing concise logic with Immer

Immer is a popular library that lets you write using the convenient but mutating syntax and takes care of producing the copies for you. With Immer, the code you write looks like you are “breaking the rules” and mutating an object:

```
updatePerson(draft => {
  draft.artwork.city = 'Lagos';
});
```

But unlike a regular mutation, it doesn’t overwrite the past state!

##### How does Immer work?

The `draft` provided by Immer is a special type of object, called a [Proxy](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy), that “records” what you do with it. This is why you can mutate it freely as much as you like! Under the hood, Immer figures out which parts of the `draft` have been changed, and produces a completely new object that contains your edits.

### Updating Array State

Here is a reference table of common array operations. When dealing with arrays inside React state, you will need to avoid the methods in the left column, and instead prefer the methods in the right column:

![](../images/updating_states_in_array.png)


### Thinking about UI declaratively

In React, we think about UI declaratively. Consider React as a driver and we are sitting next to it. Now, there are two types of instructions possible. Either we direct the driver about each turn, road etc or we directly tell driver about the destination and React will take us there. The first approach is used by scratch JS where we define each and every action precisely. Second happens in React. We define only end goals and React is able to produce it.

Manipulating the UI imperatively works well enough for isolated examples, but it gets exponentially more difficult to manage in more complex systems. In React, you don’t directly manipulate the UI—meaning you don’t enable, disable, show, or hide components directly. Instead, you declare what you want to show, and React figures out how to update the UI.

Here is how you can think of UI declaratively -

1. Identify your component’s different visual states
2. Determine what triggers those state changes
3. Represent the state in memory using useState
4. Remove any non-essential state variables
5. Connect the event handlers to set the state

### All about states

- We should not use index as key because if array elements position changes, it will be hard to differenciate for React. Consider, reversing the list of items. See example for it [here](https://codesandbox.io/s/6wbche?file=/App.js&utm_medium=sandpack).

#### Extracting state logic into reducer

- To convert from useState to useReducer:
	1.  Dispatch actions from event handlers.
	2. Write a reducer function that returns the next state for a given state and action.
	3. Replace useState with useReducer.
- Reducers require you to write a bit more code, but they help with debugging and testing.
- Reducers must be pure.
- Each action describes a single user interaction.
- Use Immer if you want to write reducers in a mutating style.


### Context

We face problems with prop drilling. Context is an alternative in that case. We require three steps to mould it into our code -
1. Create a context with `createContext(defaultValue)`
	```
	import { createContext } from 'react';

	export const LevelContext = createContext(1);
	```
2. Use that context using `useContext`
	```
	export default function Heading({ children }) {
		const level = useContext(LevelContext);
		// ...
	}
	```
3. Provide that context from the component that specifies that data
	```
	import { LevelContext } from './LevelContext.js';

	export default function Section({ level, children }) {
	return (
		<section className="section">
		<LevelContext.Provider value={level}>
			{children}
		</LevelContext.Provider>
		</section>
	);
	}
	```

By default, component picks the data specified in creating the context. We need to provide it down the tree through `SomeContext.Provider`

We can also use and provide the context from same component -

```
import { useContext } from 'react';
import { LevelContext } from './LevelContext.js';

export default function Section({ children }) {
  const level = useContext(LevelContext);
  return (
    <section className="section">
      <LevelContext.Provider value={level + 1}>
        {children}
      </LevelContext.Provider>
    </section>
  );
}
```

#### Analysis of need of context

Context is very tempting to use! However, this also means it’s too easy to overuse it. Just because you need to pass some props several levels deep doesn’t mean you should put that information into context.

Here’s a few alternatives you should consider before using context:

1. **Start by passing props**. If your components are not trivial, it’s not unusual to pass a dozen props down through a dozen components. It may feel like a slog, but it makes it very clear which components use which data! The person maintaining your code will be glad you’ve made the data flow explicit with props.
2. **Extract components and pass JSX as children to them**. If you pass some data through many layers of intermediate components that don’t use that data (and only pass it further down), this often means that you forgot to extract some components along the way. For example, maybe you pass data props like posts to visual components that don’t use them directly, like `<Layout posts={posts} />`. Instead, make Layout take children as a prop, and render `<Layout><Posts posts={posts} /></Layout>`. This reduces the number of layers between the component specifying the data and the one that needs it.
If neither of these approaches works well for you, consider context.


#### Combining context with reducer

- You can combine reducer with context to let any component read and update state above it.
- To provide state and the dispatch function to components below:
	1. Create two contexts (for state and for dispatch functions).
	2. Provide both contexts from the component that uses the reducer.
	3. Use either context from components that need to read them.
- You can further declutter the components by moving all wiring into one file.
- You can export a component like TasksProvider that provides context.
- You can also export custom Hooks like useTasks and useTasksDispatch to read it.
- You can have many context-reducer pairs like this in your app.


### useEffect

Refer doc - https://react.dev/learn/synchronizing-with-effects

Effects are an escape hatch from the React paradigm. They let you “step outside” of React and synchronize your components with some external system like a non-React widget, network, or the browser DOM. If there is no external system involved (for example, if you want to update a component’s state when some props or state change), you shouldn’t need an Effect. Removing unnecessary Effects will make your code easier to follow, faster to run, and less error-prone.

**Effects run after every render.** This is why following code will produce an infinite loop

```
const [count, setCount] = useState(0);
useEffect(() => {
  setCount(count + 1);
});
```

**React always cleans up the previous render’s Effect before the next render’s Effect.**


#### How to write effects

To write an Effect, follow these three steps:

1. Declare an Effect. By default, your Effect will run after every render.
2. Specify the Effect dependencies. Most Effects should only re-run when needed rather than after every render. For example, a fade-in animation should only trigger when a component appears. Connecting and disconnecting to a chat room should only happen when the component appears and disappears, or when the chat room changes. You will learn how to control this by specifying dependencies.
3. Add cleanup if needed. Some Effects need to specify how to stop, undo, or clean up whatever they were doing. For example, “connect” needs “disconnect”, “subscribe” needs “unsubscribe”, and “fetch” needs either “cancel” or “ignore”. You will learn how to do this by returning a cleanup function.

#### Dependency

```
useEffect(() => {
  // This runs after every render
});

useEffect(() => {
  // This runs only on mount (when the component appears)
}, []);

useEffect(() => {
  // This runs on mount *and also* if either a or b have changed since the last render
}, [a, b]);
```

If you specify an empty dependency array and a state or prop is being used inside, then React throws error that `React Hook useEffect has a missing dependency: 'someProp'`.

Ref has been omitted from the dependency array. This is because the ref object has a stable identity: React guarantees you’ll always get the same object from the same useRef call on every render. It never changes, so it will never by itself cause the Effect to re-run. Therefore, it does not matter whether you include it or not.

**Effects are fired twice in development**. React intentionally remounts your components in development to find bugs. There are some APIs that may not allow to be called twice in a row. In that case, we should provide the cleanup function. React remounts the component once in development to verify that you’ve implemented cleanup well. For example -
```
useEffect(() => {
  const dialog = dialogRef.current;
  dialog.showModal();
  return () => dialog.close();
}, []);
```

If your Effect fetches something, the cleanup function should either abort the fetch or ignore its result:

```
useEffect(() => {
  let ignore = false;

  async function startFetching() {
    const json = await fetchTodos(userId);
    if (!ignore) {
      setTodos(json);
    }
  }

  startFetching();

  return () => {
    ignore = true;
  };
}, [userId]);
```

You can’t “undo” a network request that already happened, but your cleanup function should ensure that the fetch that’s not relevant anymore does not keep affecting your application. If the `userId` changes from 'Alice' to 'Bob', cleanup ensures that the 'Alice' response is ignored even if it arrives after 'Bob'.

In development, you will see two fetches in the Network tab. In production, there will be only one.

#### If needed?

Don’t rush to add Effects to your components. Keep in mind that Effects are typically used to “step out” of your React code and synchronize with some external system. This includes browser APIs, third-party widgets, network, and so on. If your Effect only adjusts some state based on other state, you might not need an Effect.


#### Pitfalls

- **Effects don’t run on the server**. This means that the initial server-rendered HTML will only include a loading state with no data. The client computer will have to download all JavaScript and render your app only to discover that now it needs to load the data. This is not very efficient.
- **Fetching directly in Effects makes it easy to create “network waterfalls”**. You render the parent component, it fetches some data, renders the child components, and then they start fetching their data. If the network is not very fast, this is significantly slower than fetching all data in parallel.
- **Fetching directly in Effects usually means you don’t preload or cache data**. For example, if the component unmounts and then mounts again, it would have to fetch the data again.
- **It’s not very ergonomic**. There’s quite a bit of boilerplate code involved when writing fetch calls in a way that doesn’t suffer from bugs like race conditions.

##### Remedies

- use a framework and use it's built-in data fetching mechanisms
- consider using or building a client-side cache

#### Recap

- Unlike events, Effects are caused by rendering itself rather than a particular interaction.
- Effects let you synchronize a component with some external system (third-party API, network, etc).
- By default, Effects run after every render (including the initial one).
- React will skip the Effect if all of its dependencies have the same values as during the last render.
- You can’t “choose” your dependencies. They are determined by the code inside the Effect.
- Empty dependency array ([]) corresponds to the component “mounting”, i.e. being added to the screen.
- In Strict Mode, React mounts components twice (in development only!) to stress-test your Effects.
- If your Effect breaks because of remounting, you need to implement a cleanup function.
- React will call your cleanup function before the Effect runs next time, and during the unmount.

#### Practice

```
import { useState, useEffect } from 'react';

export default function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    function onTick() {
      setCount(c => c + 1);
    }

    const intervalId = setInterval(onTick, 1000);
    return () => clearInterval(intervalId);
  }, []);

  return <h1>{count}</h1>;
}
```

Figure out why the second tick increases by two not one.

### Lifecycle

Every React component goes through the same lifecycle:

- A component mounts when it’s added to the screen.
- A component updates when it receives new props or state, usually in response to an interaction.
- A component unmounts when it’s removed from the screen.


### `useCallback`

`useCallback` caches the function so that it doesn't trigger non-required re-render. When a state changes, all of its children including the parent component is re-rendered. Suppose there is a event handler callback. On state change, this function will be different and hence, it will trigger re-render of all of its children.

`memo` lets you skip re-rendering a component when its props are unchanged.

```
function ProductPage({ productId, referrer, theme }) {
  // Every time the theme changes, this will be a different function...
  function handleSubmit(orderDetails) {
    post('/product/' + productId + '/buy', {
      referrer,
      orderDetails,
    });
  }

  return (
    <div className={theme}>
      {/* ... so ShippingForm's props will never be the same, and it will re-render every time */}
      <ShippingForm onSubmit={handleSubmit} />
    </div>
  );
}
```

For example, here on change of `theme`, the complete component re-renders. `ShippingForm` also re-renders because `handleSubmit` has changed. On each re-render, the function changes in Javascript. Since this is a change in prop, the child component `ShippingForm` will re-render. This adds an overhead if there would have been a large tree down the `ShippingForm`.

To avoid this and optimize it, we use `useCallback` which caches the function itself.

```
function ProductPage({ productId, referrer, theme }) {
  // Tell React to cache your function between re-renders...
  const handleSubmit = useCallback((orderDetails) => {
    post('/product/' + productId + '/buy', {
      referrer,
      orderDetails,
    });
  }, [productId, referrer]); // ...so as long as these dependencies don't change...

  return (
    <div className={theme}>
      {/* ...ShippingForm will receive the same props and can skip re-rendering */}
      <ShippingForm onSubmit={handleSubmit} />
    </div>
  );
}
```

As you can see, now if theme changes, it won't trigger re-render of `ShippingForm` as `handleSubmit` stays the same.

#### Difference between `useCallback` and `useMemo`

`useCallback` caches the function itself and `useMemo` caches the returned result of the function.

```
import { useMemo, useCallback } from 'react';

function ProductPage({ productId, referrer }) {
  const product = useData('/product/' + productId);

  const requirements = useMemo(() => { // Calls your function and caches its result
    return computeRequirements(product);
  }, [product]);

  const handleSubmit = useCallback((orderDetails) => { // Caches your function itself
    post('/product/' + productId + '/buy', {
      referrer,
      orderDetails,
    });
  }, [productId, referrer]);

  return (
    <div className={theme}>
      <ShippingForm requirements={requirements} onSubmit={handleSubmit} />
    </div>
  );
}
```

The difference is in what they’re letting you cache:

- **useMemo** caches the result of calling your function. In this example, it caches the result of calling computeRequirements(product) so that it doesn’t change unless product has changed. This lets you pass the requirements object down without unnecessarily re-rendering ShippingForm. When necessary, React will call the function you’ve passed during rendering to calculate the result.
- **useCallback** caches the function itself. Unlike useMemo, it does not call the function you provide. Instead, it caches the function you provided so that handleSubmit itself doesn’t change unless productId or referrer has changed. This lets you pass the handleSubmit function down without unnecessarily re-rendering ShippingForm. Your code won’t run until the user submits the form.


#### Should we use `useCallback` everywhere?

Caching a function with useCallback  is only valuable in a few cases:

- You pass it as a prop to a component wrapped in memo. You want to skip re-rendering if the value hasn’t changed. Memoization lets your component re-render only if dependencies changed.
- The function you’re passing is later used as a dependency of some Hook. For example, another function wrapped in useCallback depends on it, or you depend on this function from useEffect.

### `forwardRef`

`forwardRef` lets your component expose a DOM node to parent component with a ref.

```
const SomeComponent = forwardRef(render)
```

#### Usage

- Exposing a DOM node to the parent component
	```
	import { forwardRef } from 'react';

	const MyInput = forwardRef(function MyInput(props, ref) {
	const { label, ...otherProps } = props;
	return (
		<label>
		{label}
		<input {...otherProps} />
		</label>
	);
	});
	```

	```
	import { forwardRef } from 'react';

	const MyInput = forwardRef(function MyInput(props, ref) {
	const { label, ...otherProps } = props;
	return (
		<label>
		{label}
		<input {...otherProps} ref={ref} />
		</label>
	);
	});
	```

- Forwarding a ref through multiple components
- Exposing an imperative handle instead of a DOM node
