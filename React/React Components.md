# Introduction to States
---
## What is State?
- An object that specifies different types of data
- A built-in state object stores property values belonging to the component
- Change in state results in ==re-rendering== of component

## Types of React state
- Shared state
	- Shared by multiple components 
	- Ex) orders in an order application
- Local state
	- Present only in a single component

## States in React components
- A plain JS object used to represent an information about the component's current situation
- Determines how the component ==renders and behaves==
- Allows you to create components that are ==dynamic and interactive==

## Need of state
- For components that changes during interaction
- Tracks the change 

## State Example:
```jsx
class TestComponent extends React.Component{
	constructor(props){
		super(props);
		this.state = {
			id: 1,
			name: "John",
			age:28
		};
	}
	render(){
		return(
			<div>
				<p>{this.state.name}</p>
				<p>{this.state.age}</p>
			</div>
		);
	}
}
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<TestComponent />)
```

## What are props in React?
- Props:
	- Short for ''properties", used to pass data between React components
	- ==React's data flow between components is uni-directional from parent to child only.==
	- Read-only components
- Behavior:
	- Store the value of attributes of a tag and work like the HTML attributes
	- Function arguments that can be passed to the component
	- Immutable and cannot be modified from inside the component
	- Should not be changed in a child component 
	- Allow child components to access methods defined in the parent component 

## Props Example
```jsx
//component
class TestComponent extends React.component{
	render(){
		return <div>Hi{this.props.name</div>
		}
	}
}
//passing the props as examples to the test component
<TestComponent name='John'/>
<TestComponent name='Jill'/>
```

## Compare state and props
- Use
	- State:
		- Class components natively
		- Need to use state hook to include stateful features
	- Props:
		- Can reuse the component by giving it an ability to receive data as input from the parent component
- Purpose
	- S: For managing data
	- P: For passing data
- Modify
	- S: 
		- Can create and manage their own data
		- Cannot be accessed or modified outside of the component
		- Can be modified by its own but is private
		- Modify with setState() method
	- P: 
		- Receive data from outside
		- Can receive data from the parent component
		- Read-only and cannot be modified from outside
		- Can only be passed from parent component to child
- 
# Passing Data and States Between Components
---
## Component phases
- Mounting: component creation
- Updating: component rendered on a change of state or props
- Unmounting: component removed from the DOM
- Examples: https://www.w3schools.com/react/react_lifecycle.asp

## Mounting
Four methods are called in the same order:
1. constructor()
	1.  Constructs the object
2. getDerivedStateFromProps()
	1. Used only when the state depends on the changes to props
3. render()
	1. This method is mandatory in a React component
	2. Must return a DOM element
4. componentDidMount()
	1. Invoked immediately after a component is mounted or inserted into the DOM tree

## Updating
Five methods are called in the same order
1. getDerivedStateFromProps()
	1. Only when the state depends on the changes to props
2. shouldComponentUpdate()
	1. By default returns true 
	2. Every time there is a change in state, this method is called to check if the component should update 
	3. Make this method return false if you don't want to render the changes in state
3. render()
4. getSnapshotBeforeUpdate()
	1. Invoked just before the changes are rendered
	2. It helps keep track of what has changed
	3. Any value returned by this lifecycle will be passed as a parameter to the componentDidUpdate()
5. componentDidUpdate()
	1. Invoked immediately after updating occurs.

## Unmounting
When a component is unmounted, the `componentWillUnmount()` method is called

## Passing data between components
- From parent to child using props
- From child to parent using callbacks
	- Parent pass callback function as a property to the child 
- between siblings using Redux
# Components Lifecycle
---
## Component phases
1. Initialization
	1. Component is constructed with props and default state
2. Mounting - first render
	1. JSX is rendered
3. Updating - change due to user activities
	1. Component is changed
4. Unmounting
	1. Component is removed


# Connecting React to External Services
---
## Connecting to an external server
- HTTP: GET, POST, UPDATE, DETELE
	- Ex) `app.post()`, `app.get()`
- Use promises to make calls to an external server asynchronous.
# Testing React Components
## Why test React components?
- Tests functionality by replicating the actions of the end users 
- Validates any updates done do not affect the working of the overall application
- Prevent regression (reappearance of a previous fixed bug)

## Approaches
- Render ==component trees== in a simple test environment and assert their output
- Run application in a realistic browser environment to do end-to-end testing

## Phases of React component testing
==Arrage-Act-Assert==
- Arrange: component properties are prepared
- Act: component renders its DOM to the user interface, registers any user actions or events that may trigger programmatically 
- Assert: expectations are set, verifying certain side effects

## Choosing the right tool
- Speed vs. environment
- What to mock

## React testing libraries/tools
- Mocha: test runner
- Chai: assertion library
- Sinon: spies, stubs, mocks
- Enzyme: render components

## Popular React testing libraries:
- Jest: combined power of Mocha, Chai, Sinon
- React Testing Library: sets of helpers 

## Testing with Jest
- JS test runner 
- Can be combined with Enzyme or React Testing Library
- Can access DOM
- Great iteration speed
- Command line tool 
- Mock functions
- Offers snapshot testing
- A dependency to React 

## Testing with React Testing Library
- Light utility functions on top of react-dom 
- Facilitate querying the DOM, finding form elements, and finding links and buttons
- Finds elements where the text is not understandable 
- Encourage applications to be more accessible 
- Is a replacement for Enzyme

## Example React Testing Library
```jsx
import {render, screen} from '@testing-library/react'
import userEvent from '@testing-library/user-event'
import '@testing-library/jest-dom'
import Fetch from './fetch'

test('loads and displays greeting', async () =>{
	// ARRANGE
	render(<Getch url="/greeting" />)

	// ACT
	await userEvent.click(screen.getByTest('Load Greeting'))
	await screen.findByRole('heading')

	// ASSERT
	expect(screen.getByRole('heading')). toHaveTextContent('hello there')
	expect(screen.getByRole('button')).toBeDisabled()
})
```

## Benefits of React Test Library
- Test the way as an end user would use them
- Users don't care about the back-end, RTL enables you to write your tests based on the component output visible to the end users
- Rewriting your tests increases your productivity 