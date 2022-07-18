# React JavaScript Framework
======
#### Features
+  fast
+  modular
+  scalable
+  flexible
+  popular
+ 

#### JSX (JavaScript Syntax Extension)
A React-like feature that allows HTML-like elements to be saved in JavaScript variables.  JSX compiler needs to be used before browsers can read.
#### Virtual DOM
React keeps a copy of the virtual DOM object, then diffs the changes at rendertime.  This way, only changes are updated.  
#### Components
React application are made out of components.  A component is a small, resusable chunk of code responsible for one job (often to render some HTML).
#### Imports
+ import React from 'react'
+  import ReactDOM from 'react-dom'
+ 


## Syntax
------
#### Semicolons
all expressions end with semicolon
#### Variables
variables must be declared with const.
#### JSX Expressions
If multi-line, JSX must be surrounded by parentheses.  Must have an outer element.
#### If Statements
disallowed inside of JSX (will not compile)

## Imports
------
#### import React from 'react'

#### import ReactDOM from 'react-dom'
ReactDOM.render(JSX,document.getElementById('app'))

## Event Listeners
------
#### Special Attributes that execute on events
<a href="https://reactjs.org/docs/events.html#supported-events">https://reactjs.org/docs/events.html#supported-events</a>

## Conditionals
------
#### Use if statement outside of JSX
```

if(condition){
    do_thing1;
}else{
do_thing2;
}
```
#### Ternary Operators
{conditional ? do_thing1 : do_thing2 }
#### &&
Expression on right will render if conditional is true (conditional && JSX)

## Important Functions and Patterns
------
#### "map"
```

const people = ['Abby', 'Billy', 'Charles'];
const peopleLis = people.map((person,i) => 
  <li key={'person_' + i}>{person}</li>
);
ReactDOM.render(<ul>{peopleLis}</ul>,document.getElementById('app'));
```
#### "React.createElement()"
React.createElement("div",null,"Hello World");
#### Component Classes
```

class MyComponentClass extends React.Component{
	//Component Class names must begin with Capital letters.
	render(){
		return <h1>Hello world</h1>;
	}
};
ReactDOM.render(<MyComponentClass />,document.getElementById('app'));
```
#### Event Listener
function (i.e. alert(){}) within class that can be called by an event handler attribute.
#### Stateless function components (no render() method)
```
export const MyComponentClass = () => {
  return <h1>Hello world</h1>;
}
```
#### Another function component with props
```
export function NewFriend (props) {
    return (
      <div>
        <img src={props.src} />
      </div>
    );
}
```
#### React Hooks examples
+ useState()
+ useEffect()
+ useContext()
+ useReducer()
+ useRef()
+ 

#### Spread Syntax
i.e. ...prev .  Previous data structure or array copied to new array.

## Hooks
------
#### useState
in order to use, import React, { useState } from 'react';.  This returns the current state and a state "setter".  Example: const [ toggle, setToggle ] = useState();  Calling the state setter function automatically calls React to re-render.

## Imports and Exports
------
#### Import a component in another file
import { NamedComponent } from './namedComponent.js'
#### Export a varibale in another file
export const myGlobalParam = <h1>This is global.</h1>;
#### Import multiple variables from anoter file
import { myGlobal1, myGlobal2 } from './globals';

## Props
------
#### Prop definition
information passed from one component to another.  React Components have props accessible as an attribute.  They can also be used by stateless functions.
#### Example
<PropExample propname="prop.value"/>.  Props are passed through attribute-like features on React Components
#### Default values
PropExample.defaultProps = { 'propname' : "foobar"}

## State
------
#### State
A property declared inside a constructor method, from the inside.
#### Defining state
```

class Example extends React.Component {
	constructor(props){
		super(props);
		this.state = { mood: 'good' };
		this.myFunc = this.myFunc.bind(this);
	}
}
```
#### Setting
this.setState(); //input a state object
#### Usage
this.state is the only component that may be used within the DOM that will automatically re-render.  Calls to setState call .render() as soon as state changes.

## Component Lifecycle
------
#### Mounting
when the component is being initialized and put into the DOM for the first time (constructor, render, componentDidMount)
#### Updating
when the component updates as a result of changed state or changed props (new props, setState, forceUpdate, render, componentDidUpdate)
#### Unmounting
when the component is being removed from the DOM (componentWillUnmount)
#### constructor()
called when a class is instantiated during mounting phase.
#### render()
executes during both mounting and updating phases.
#### componentDidMount()
Final method called during the mounting phase.  Placing functions in here allows them to run after construction and after render, but continually update.
#### componentWillUnmount()
Performs a function after DOM unmounts (so dangling JS functions don't keep running)

## Examples
------
#### Simple Function
```
function makeDoggy(e) {
  // Call this extremely useful function on an <img>.
  // The <img> will become a picture of a doggy.
  e.target.setAttribute('src', 'https://content.codecademy.com/courses/React/react_photo-puppy.jpeg');
  e.target.setAttribute('alt', 'doggy');
}
```
#### Simple Class
```
export class NavBar extends React.Component {
  render() {
    const pages = ['home', 'blog', 'pics', 'bio', 'art', 'shop', 'about', 'contact'];
    const navLinks = pages.map(page => {
      return (
        <a href={'/' + page}>
          {page}
        </a>
      )
    });

    return <nav>{navLinks}</nav>;
  }
}
```
#### Clock Component
```

import React from 'react';

export class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = { date: new Date() };
  }
  render() {
    return (
      <div>
        {this.props.isPrecise
          ? this.state.date.toISOString()
          : this.state.date.toLocaleTimeString()}
      </div>
    );
  }
  componentDidMount() {
    this.startInterval();
  }
  componentDidUpdate(prevProps){
    if (this.props.isPrecise == prevProps.isPrecise){
      return;
    }
    clearInterval(this.intervalID);
    this.startInterval();
  }
  componentWillUnmount() {
    clearInterval(this.intervalID);
  }
  startInterval(){
    let delay;
    delay = this.props.isPrecise? 100 : 1000;
    this.intervalId = setInterval(() => {
      this.setState({date : new Date()});
    }, delay);
  }
}

```
#### Phone Number Handler Component
```

import React, { useState } from 'react';

// regex to match numbers between 1 and 10 digits long
const validPhoneNumber = /^\d{1,10}$/;

export default function PhoneNumber() {
  // declare current state and state setter 
  const [ phone, setPhone ] = useState('');
  const handleChange = ({ target })=> {
    const newPhone = target.value;
…      <label for='phone-input'>Phone: </label>
      <input value={phone} onChange={handleChange} id='phone-input'/>
    </div>
  );
}
```
#### Quiz Navigation Bar Component
```
import React, { useState } from 'react';

export default function QuizNavBar({ questions }) {
  const [questionIndex, setQuestionIndex] = useState(0);

  // define event handlers 
  const goBack = () => setQuestionIndex( prevQuestionIndex => prevQuestionIndex - 1);
  const goToNext = () => setQuestionIndex( prevQuestionIndex => prevQuestionIndex + 1 );
  // determine if on the first question or not 
  const onFirstQuestion = questionIndex === 0; 
  const onLastQuestion = questionIndex === questions.length - 1;
  return (
    <nav>
      <span>Question #{questionIndex + 1}</span>
      <div>
        <button onClick={goBack} disabled={onFirstQuestion}>
          Go Back
        </button>
        <button onClick={goToNext} disabled={onLastQuestion}>
          Next Question
        </button>
      </div>
    </nav>
  );
}
```
