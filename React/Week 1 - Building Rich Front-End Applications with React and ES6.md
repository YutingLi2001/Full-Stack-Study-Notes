# Introduction to Front-End Frameworks and React
---
## React
- A framework for building client-side dynamic web applications
- Dynamic data binding and virtual document object model (DOM)

## JavaScript XML (JSX)
- React uses a special markup language called JSX
- Resembles HTML
- Can be compiled and interpreted as JavaScript by Babel
- Is embedded inside special script tags

## Packages
- React: components, their states and properties
- ReactDOM: glue between React and the DOM
- Babel: to compile and interpret the JSX

# Introduction to ES6
---
## ES6 features:
- let
- const
- Arrow functions
- Promise
- Class

## Let and const 
- let and const are introduced in addition to var 
- let allows you to restrict the scope of variables within the block where they are declared 
```jsx
{
	let num = 5;
	console.log(num);
	num = 6;
	console.log(num);
}
console.log(num);
{/*This line above will throw an error as num is out of scope*}
```
- const allows you to declare constants whose values cannot be changed
```jsx
const num = 5;
num = 6;
{/*Error*/}
```
## Arrow functions
- Arrow functions allow functions to be declared like variables
- This is a shorter and cleaner way to work with functions
- Can also be declared with let and const just like a variable
```jsx
const sayHello = ()=> console.log("ES6 function - Hello World!")
```
- Arrow functions can be called
- Arrow functions can be passed as parameters for callbacks
```jsx
const sayHello = ()=> console.log("ES6 function - Hello World!")
setTimeout(sayHello,1000);
```
- Arrow functions also take parameters like normal functions
```jsx
const oneParamArrowFunc = name => {return "hello " + name};

const twoParamArrowFuncWithoutReturn = (first, last) => console.log("hello " + first + " " + last);

const twoParamArrowFuncWithReturn = (first, last) => {return "hello " + first + " " + last};

const twoParamsTwoLinesArrowFunc = (first, last) => {
	const greeting = "hello ";
	return greeting + " " + first + " " + last;
}
```

## Promise
- The promise object represents the eventual completion of an asynchronous operation and its return value 
- When you invoke an asynchronous operation, a promise is in the *pending* state
- When the operation executes successfully, the promise is *fulfilled* 
- When the operation fails, the promise is *rejected* 
- A promise takes a function with two parameters:
	- Resolve says what should happen when it is fulfilled
	- Reject says what should happen when it fails 
```jsx
/*Promise Argument*/
let promiseArgument = (resolve,reject) => {
	setTimeout(() => {
		let currTime = new Date().getTime();
		if(currTime % 2 === 0){
			resolve("Success!")
		} else {
			reject("Failed!")
		}
	},2000)
};

/*Directly creating the function in tiem with the promise constructor*/
let myPromise = new Promise ((resolve,reject) => {
	setTimeout(() => {
		let currTime = new Date().getTime();
		if(currTime % 2 === 0){
			resolve("Success!")
		} else {
			reject("Failed!")
		}
	},2000)
})
/*Behaviour in both cases are identical*/
```

## Class
- Class in JavaScript are built on prototypes  
```jsx
function Person(name,age){
	this.name = name;
	this.age = age;
	return this;
}

let person1 = Person("Yuting",22);

console.log(person1);
console.log(person1.name);
console.log(person1.age);
```

- Constructor
```jsx
class Rectangle{
	constructor(height,width){
		this.height = height;
		this.width = width;
		console.log("Rectangle Created");
		console.log("Height " + this.height);
		console.log("Width " + this.width);
	}
};

let myRectangle = new Rectangle(10,5)
```

### Inheritance
- The class inheriting is the subclass
- The class being inherited is the superclass
- The subclass inherits all the attributes and methods of the superclass
- The subclass has a special privilege to call the superclass constructor with a `super()`  method call
```jsx
class Square extends Rectangular{
	constructor(height, width){
		if(height === width){
			super(height,width)
		} else {
			super(height, height);
		}
	}
}

let mySquare = new Square(5,5)
```

# Introduction to Typescript
---
- TypeScript is a superset of JavaScript meaning all JavaScript is TypeScript but not all TypeScript is JavaScript. 
- TypeScript is a compiled language that supports type-checking. TypeScript is statically typed. This means that variables are static. 
	- Can avoid "run-time errors"

# Introduction to JSX
---
## What is JXS?
- Extension to JavaScript
- Easier way to create UI components in React
- JSX produces React "elements" that can be used to render the component to DOM

## JSX syntax
- Like an XML or HTML-like syntax used by React that extends ECMAScrip

Example:
```jsx
const el1 = <h1> This is a sample JSX code snippet </h1>
```
- Like HTML uses a JavaScript-like variable that is neither HTML nor JavaScript 
- A syntax extension of regular JavaScript, used to create React elements
- Elements are rendered to the React Document Object Model or DOM
- ==Browsers don't understand JSX, so you need to use Babel to compile your JSX code.==
	- create-react-app command will take care of this compilation

## React code example
- In JSX:
```jsx
import React from 'react'
function App(){
	return(
		<div>
			<p> <This is a sample list> </p>
			<ul>
				<li> List item no.1 </li>
				<li> List item no.2 </li>
			</ul>
		<div>
	)
}
```
- In JavaScript:
```js
import React from 'react'
function App(){
	return React.createElement(
		"div",null,
			React.createElement("p", null, "This is a sample list">,
			React.createElement("ul,null,
			React.createElement("li",null, "List item no.1"),
			React.createElement("li",null, "List item no.2")));
	)
}
```

- ==JSX combines the beauty of HTML and the power of Javascript==

# Introduction to Components
---
## What is a component?
- Core building blocks of React
- Make the task of building user interface easier 
	- Break down UI into separate elements and merge them all into a parent component that forms the final UI 
		- Those can be reused and handled independently 
		- Take an optional input and returns a React object which is rendered on the screen

## State of component
- An object to describe the behaviour of a component. 
- React component can be either "stateful" pr "stateless"
	- Stateful components update as per the current state
	- Stateless components are function type 

## Types of React components
- Functional
	- Created by writing JavaScript function
	- May or may not receive data as parameters
	- Take in props and return JSX
	- Do not natively have state or lifecycle but can be added by implementing React Hooks 
		- Hooks: enable you to use react features without writing the class
		- Lifecycle methods are inbuilt React method that operate on components throughout their duration in the DOM
	-  Used to display information that is easy to read ,debug and test
	- Stateless
```jsx
const Democomponent = () =>
{
	return <h1>Welcome Message!</h1>
}
```
- Class
	- Can pass data to other class components
	- Can be created using JavaScript ES6 classes 
	- Can use React functions like state, props, and lifecycle methods
	- Stateful
```jsx
class Democomponent extends React.Component{
	render(){
		return <h1>Welcome Message!</h1>
	}
}
```
- Pure
	- Used to provide optimizations 
	- Simplest and fastest components to write
	- Do not depend on or modify the state of variables outside their scope 
	- Can replace simple functional components
- High-order
	- For reusing component logic
	- Not available in the API
	- A function that returns a component(s)
	- Used to share logic with other components 
```jsx
import React from 'react';
import { Text } from 'react-native';

const Helloword = () => {
	return(
		<Text>Hello, World!</Text>
	);
}


export default Helloworld;
/*This function can be imported in any application.*/
```

# Props and Event Handling
---
## Components
- Functional: returns JSX
	- Most useful when the component has properties but the lifecycle of the component doesn't have to be managed
	- User-defined properties(props) that are passed as parameters to the function
```jsx
function App(props){
	const compStyle = {
		color: props.color,
		fontSize: props.size "px"
	};
	return(
	<div>
		<span style={compStyle}>I am a sentence</span>
	</div>
	)
}
```
---
```jsx
	ReactDOM.render(
	<React.StrictMode>
		<App color="blue" size="25"/>
	</React.StrictMode>,
	document.getElementById('root')
	);
```
- Class
- 