# Hooks
---
## What are Hooks?
- Encapsulate stateful behaviour and side effects in user interfaces
- Allow ==function== components to have access to ==state== and other React features

## Why Hooks? 
- To use state without classes
- Makes complex forms simpler without the use of classes
- To write functional component with state

## Best practices of using Hooks
- Can be called only from inside React function components
- Can only be called at the top level of a component
- Cannot be conditional

## Standard Hooks
- useState: adds state to a function component
- useEffect: manages side effects
- useContext: manages context changes
- useReducer: manages redux state changes

## Custom Hooks
- Allow you to add special unique functionality to your application
- Are named with prefix as 'use'
	- Ex) useLocalStorage or useAuthentication
- Is a composition of one or multiple hooks
- Are reusable, can be broken into smaller hooks, testable 

## Example Hooks:
```jsx
import React, {useState} from 'react';
function FavoriteColor() {
  const [color, setColor] = useState("");
}
```

# Implementing Forms
---
## What are forms
- Allow users to interact with web page
- Handle data using ==components==
- Store data in component state
	- Informations are not sent directly to the server
	- Form information are captured on the client side, the data is sent to the server or displayed using additional JS code
- Control changes and update the state using event handlers 

## Types of inputs
- Uncontrolled input
- Controlled input

## Uncontrolled input
- Browser handles the form
- Manage their own value in the input's DOM node
- Elements will be updated when input value changes
- Ref function is used to get the form values from DOM

## Controlled input 
- Create state to hold, update, display value 
- Functions govern passing of data
- Better control over form elements and data 
- Props take current value and notifies changes
- A parent component controls the changes

## React Hook Form
- Package for creating web forms
- Reduces amount of code
- Uses ref to control form inputs

## Advantages of React Hook Form
- Reduces number of re-renders
- Tiny size with zero dependencies
- Uses constraint-based validation API
- Painless integration with UI libraries 

# Introduction to Redux
---
## What is Redux?
- A state management library 
- Follows a pattern known as Flux architecture 
- State is handled globally and allows you to change the state from anywhere in the application. 
	- The larger the application, the more Redux may become necessary. 
- Not specific to React and can be used with other libraries 

## Why Redux?
- Manage large application with large number of states
- Instead of components handling their own state, Redux offers a centralized state management system 
- Reduces complexity of code 
- Maintenance elements in Redux make it easy to test and debug the application

# Essential Concepts of Redux Stores, Procedures and Actions
---
## Basic principles of Redux
- Centralized state management system - a single store, not by individual components
- Component's properties are immutable 
- Action updates State re-renders Component updates Component Properties displays Result

## Redux concept
- Actions: what your app can do
- Store: singular location and authoritative source of the app state 
- Reducers: actions which return the new state

## What are Actions?
- Events fired by user action
- JSON objects that contain information about changes that need to be made to state
- Produces by functions called action creators 
- Contains type of Action, time of occurrence, and which states it aims to change 

## Behaviour of actions
- Dispatched by various parts of your application and received by the store 
- JS objects that describe what happened but do not describe how the state will change
- Sent to your store to update the application state 

## Store
- Contains the Redux application state
- An object that contains state, functions, and other objects 
- Can dispatch and receive actions 
- Provides subscriptions to Store updates
- Holds the entire application list in the form of the 'state tree'

## Reducers
- Receive the Action from the Store 
- Makes appropriate changes to the state
- A pure function that receives current state and an Action 
	- Returns a new state with the actions performed 
- Acts as an event listener, reads the Action payloads, and updates Store
- Takes two parameters, previous app state and Action, returns new app state


# Async with Redux
---
## What is sync and async?
- Sync
	- Runs in sequence from top to bottom
	- Each operation waits for the previous to complete
- Async
	- Runs in parallel
	- An operation can occur while another is still being processed
	- Preferable when execution can be blocked indefinitely
		- Ex) networking request, long-running calculations, file system operations
	- ==Page remains responsive==
	- JS is a single-threaded, non-blocking, asynchronous, concurrent programming language with lots of flexibility. 
		- JS does not wait for responses when executing a function
		- Instead, it continues execution of other functions

## Why async in Redux? 
- The flow of Redux's state management tasks is completely synchronous

## Introducing middleware
- In Redux, Actions and Reducers complement your app's architecture
- To use asynchronous operations, Actions and Reducers are not enough 
- Interact with asynchronous data in your React Redux app using middleware
	- Middle ware can intercept or delay the actions supporting asynchronous operations
	- Once the asynchronous process completes, the rest of the Redux flow continues as usual

## Middleware techniques
- Thunk middleware
- Saga middleware
- Promise-based middleware
- Async/Await middleware

## Redux Thunk
- Allow to pass functions within action creators to create async Redux
- Allows writing action creators
- Allows dispatch delay of action
- Allows dispatching an action
- Passes dispatch() and getState() as parameters to the function

## Thunk Advantages vs. Disadvantages
- Advantages
	- Suitable for simple applications
	- Enables async operations without a lot of boilerplate code
	- Easy to set up and implement
- Disadvantages
	- Cannot act in response to an action
	- Difficult to handle concurrency problems that may occur
	- Imperative - not easy to test
	- Does not scale well

## Saga middleware
- Uses Generators to enable async operations 
- Exposes a set of helper functions to create declarative JS objectives
- Handles the objects yielded in the backend 

## Saga Pros and Cons
- Pros
	- Expressing complex logic as functions
	- Easy to test
	- Can be time-traveled
	- Easier to scale complex applications
	- Easier to catch errors and handle failures
	- Well documented
- Cons
	- Not suitable for simple apps
	- More boilerplate code
	- Need to have the knowledge of generators
	- Higher learning curve 

## Choosing middleware
Thunk is the preferred because:
- Can communicate with actions before reach Reducer
- Can use many use cases around practical web apps
- Understanding Thunk is easier for those learning Redux the first time 

# Binding Redux and Flow
---
## State change in React
- State change:
	- Triggers the re-rendering of DOM in React 
	- Change in the state may involve the transfer of data and long chain of props
	- Requires state management done by Redux 
	- Managed in React Redux using a single Store and Reducers

## Redux building blocks 
- Central Store
- Actions
- Reducer
- Subscription: triggered in the components whenever the state is updated in the store 

## Data flow 
- Unidirectional
	- UI (Invokes Action Creator) 
	- Action Creator (Dispatching Action) 
	- Root Reducer (Handles Action and returns new state) 
	- Store (Updates the UI)

## Why one way data flow?
- Affect browser performance
- Difficult to keep track of the data flow 
- Easier to manage state when actions on UI and update of state are separate
- Enable reuse of the containers, actions, and reducers in React Native 
- 
