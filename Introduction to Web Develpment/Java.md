# Prototype:
--- 
- Defines properties and method for all instances of the object
- Objects inherit all properties and method from their prototype
- Prototype properties and method can be changed in one call 
```js
function Car(make, model,year,color){
	this.make = make;
	this.model = model;
	this.year = year;
	this.color = color;
}

Car.prototype.color = "Red";
```
- Scripts can override prototype properties and functions 
```js
Car.prototype.getName = function(){
	return this.make + ' ' + this.model + ' ' + this.year; 
}
```

# JavaScript APIs
--- 
## Definition
- An API, or Application Programming Interface, is a way for two applications to communicate with each other. It delivers your request to another device, such as a database, and returns the response back to you.
- ---
## JS API Functions
- Retrieve a reference node using `document.getelementById` and `document.getElementsByTagName`
- Create an element using `document.createElement` and place it using `insertBefore`, `appendChild`, or `replaceChild`
- Modify elements using `element.innerHTML`, `element.style` and `element.setAttribute`
- Manage a window object using functions that include `window.open` and `window.dump("message")
- --- 
# Scripting
---
```html
<script>
	// JavaScript code
</script>

<script src = "/source/script.js"></script>
<noscript>
	//browser run this code when scripts are not supported by the browser
</noscript>
```
---
# Good Practices
- Use Linter to standardize your codes 
- Avoid using global variables 
- Place Scripting codes at the bottom 
	- Add functionalities after event occurs
- Declare variables outside of the `for` statements 
