[TOC]

# Learn React for free

https://scrimba.com/g/glearnreact
- Bob Ziroll
- 58 scrims, 6 hours
- React.js in 2019

Going to be building a todo application. This document structure also works kind of like a checklist for starting a new project.

- Scrimba lets you watch live coding screencast and pause the demo and play with code during presentation.
- Note that your changes are overwritten when screencast resumes unless you check to save it.
- The numbers in the headings match the screencasts from the tutorial.

#### Learn about these:
- Components - reusable HTML
- JSX - React Javascript
- Styling
- Props - pass data
- State - maintain and change data
- Event Handling
- Lifecycle Methods - timing events
- HTTP - fetch data from API
- Forms - user experience
- More

#### Prerequisites
- HTML
- CSS
- Javascript
- ES6

## 5. Why React?
- Virtual Dom is fast
- Reusable Web Components
- Maintained by Facebook
- Hirable

## 6. ReactDOM & JSX
### ES6
- replaces `var` with `const` and `let`

### Import
```javascript
import React from "react"
import ReactDOM from "react-dom"
```

### Render
```javascript
ReactDOM.render(WHAT DO I WANT TO RENDER, WHERE DO I WANT TO RENDER IT)

// JSX
ReactDOM.render(<h1>Hello world!</h1>, document.getElementById("root"))
```
- You can't have two adjacent elements in render()

### index.html
```html
<div id="root"></div>
```
- container for entire application


## 8. React Functional Components

```javascript
function MyApp() {
    return (
        <JSX></JSX>
    )
}
<MyApp />
```

- functional components are created with a function
- Use Upper CamelCase for function names by convention
- You can't have two adjacent elements in return
- Components can be made up of other Components
- Will eventually put components in their own files

### 9. Practice

```javascript
// Objectives:
// 1. Set up the basic React code from scratch
// 2. Create a functional component called MyInfo that returns the following UI:
    // a. An h1 with your name
    // b. A paragraph with a little blurb about yourself
    // c. An ordered or unordered list of the top 3 vacation spots you'd like to visit
// 3. Render an instance of that functional component to the browser
// Extra challenge: learn on your own (Google!) how you can add some style to your page.
// (We will also cover this in an upcoming lesson).

import React from "react"
import ReactDOM from "react-dom"

function MyInfo() {
  return (
    <div>
      <h1>Your Name</h1>
      <p>Paragraph about yourself</p>
      <ul>
        <li>one</li>
        <li>two</li>
        <li>three</li>
      </ul>
    </div>
  )
}

ReactDOM.render(<MyInfo />, document.getElementById("root"))
```

## 11. Move Components into Separate Files

- create file `MyInfo.js` with JSX and export
- Recommends checking out ES6 intro

```javascript
export default MyInfo
```

- import `MyInfo` into `index.js`
- you can create your own structure, but creating `components` directory sounds good

```javasc
import MyInfo from "./components/MyInfo"
```

## 12. React Parent/Child Components

```javascript
import React from "react"
import Header from "./Header"
import MainContent from "./MainContent"
import Footer from "./Footer"

function App() {
    return (
        <div>
            <Header />
            <MainContent />
            <Footer />
        </div>
    )
}

export default App
```

- keep the `App` Component as all JSX and put HTML elements into separate files for cleaner code.
- In the DOM tree the functional component replaces the React Component tag. Look at the source to verify.

## 14. React Todo App - Phase 1

- Create the base App components

## 15. Style React with CSS Classes

- uses Vanilla Javascript DOM api to add class

```javascript
document.getElementById("something").className += " new-class-name"
```

becomes

```javascrip
<header className="navbar">This is the header</header>
```

and in `style.css`

```css
.navbar {
    background-color: purple;
}
```

## 16. Some Caveats

- semicolons at end of statements are optional and removing makes it easier to read
- ES6 has arrow functions, or anonymous functions, for shorter code

```javascript
const App = () => <h1>Hello world!</h1>
```

is equivalent to 

```javascript
function App() {
    return (
       <h1>Hello world!</h1>
    )
}
```

or

```javascript
const App = () => {
    return (
       <h1>Hello world!</h1>
    )
}
```

or 

```javascript
const App = () => (<h1>Hello world!</h1>)
```

## 17. JSX to JavaScript and Back

- You can put JavaScript within curly braces to interpret as JavaScript within a JSX Component.

```javascript
const firstName = "Bob"
const lastName = "Ziroll"

return (
    <h1>Hello {firstName + " " + lastName}!</h1>
)
```

or, with ES6 string interpolation using backticks

```javasc
<h1>Hello {`${firstName} ${lastName}`}!</h1>
```

You can perform complex JavaScript within JSX

```javascript
const date = new Date()
const hours = date.getHours()
let timeOfDay

if (hours < 12) {
    timeOfDay = "morning"
} else if (hours >= 12 && hours < 17) {
    timeOfDay = "afternoon"
} else {
    timeOfDay = "night"
}

return (
    <h1>Good {timeOfDay}!</h1>
)
```

## 18. React Inline Styles with the Style Property

```javascript
<h1 style={{color: "#FF8C00", backgroundColor: "#FF2D00"}}>Good {timeOfDay}!</h1>
```

- You need double curly braces to form valid JavaScript objects
- camelCase styles with dashes, i.e. `background-color` or you could put the name in quotes

```javascript
const styles = {
    color: "#FF8C00", 
    backgroundColor: "#FF2D00",
    fontSize: 200
}
<h1 style={styles}>Good {timeOfDay}!</h1>
```

- Declaring a separate `styles` object keeps from cluttering the HTML tag when adding new styles.

```javascript
styles.color = "#04756F"
```

- You can then also access the styles properties as an object and change programmatically in JavaScript.

## 19. React Todo App Phase 2

- add styles

## 22. React Props

- JSX elements have properties just like HTML elements have properties.
- Start noticing how a page can be divided up into separate components.
- A single component gets developed once and then data is changed through properties.
- This is what we call "Thinking in React".
- Conceptually React Props are the same thing as functional parameters

```javascript
function addNumbers(a, b) {
    return a + b
}
```

- props are usually passed in through a JSON data file or an API REST endpoint, but the tutorial shows a hardcoded example.
- For components with lots of properties it makes more sense to pass the props as an object instead of individual properties.

```javascript
contact={{name: "Mr. Whiskerson", imgUrl: "http://placekitten.com/300/200", phone: "(212) 555-1234", email: "mr.whiskaz@catnap.meow"}}
```

- and in `ContactCard.js`

```javascript
function ContactCard(props) {
    console.log(props)
    return (
        <div className="contact-card">
            <img src={props.contact.imgUrl}/>
            <h3>{props.contact.name}</h3>
            <p>Phone: {props.contact.phone}</p>
            <p>Email: {props.contact.email}</p>
        </div>
    )
}
```

- Ternary statements are common in React to only display elements if they contain a prop.

```javascript
<h3 style={{display: props.question ? "block" : "none"}}>Question: {props.question}</h3>
```

- Another method that is slightly less readable but a shorter format is the double ampersand.

```javascript
<h3 style={{display: !props.question && "none"}}>Question: {props.question}</h3>
```

## 25. Mapping Components in React

- React just uses Vanilla JavaScript to get a lot done that other frameworks might be doing behind the scenes.

```javascript
const nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
const doubled = nums.map(function(num) {
    return num * 2
})
console.log(doubled)
```

- other functions worth checking out are: map(), filter(), reduce()

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/some

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findindex

```javas
const jokeComponents = jokesData.map(joke => <Joke key={joke.id} question={joke.question} punchLine={joke.punchLine} />)
```

- map() returns an array of Components
- using JavaScript arrow function
- has an implicit return
- include the key prop to avoid warning about having unique items in an array
- then, you can put an array of components directly in JSX

```javascript
return (
    <div>
   		{jokeComponents}            
    </div>
)
```

- A note about `export default`: you can call your export anything you want and then import it as a totally separate name, since only the import name matters in that context.

## 26. React Todo App Phase 3

- data is loaded from a JSON file

## 27. Class-based Components

- started with Functional components because they are sometimes easier to understand when learning React.
- Class-based components are used in the same way as Functional components, but allow for management of props and state.
- You can easily change Functional components into a Class.

```javascript
class App extends React.Component {
    
    yourMethodHere() {
        
    }
    
    render() {
        return (
            <div>
                <h1>{this.props.whatever}</h1>
            </div>
        )
    }
}
```

- Access props in the class using `this.props`

## 29. React State

- state is the data that a components maintains
- You can't change props. You can only change states.

```javascript
constructor() {
    super()
    this.state = {
        answer: "Yes"
    }
}
```

- initialize states by using the `this.state` object in the constructor.
- `super()` calls the constructor of the parent class..

```javascript
<ChildComponent answer={this.state.answer}/>
```

- pass states down to child components as props

```javascript
React setState will be discussed later.
```

- Whenever the state changes with set state method, React will automatically update any components using that state.

## 32. React Todo App Phase 4

- Change App from functional component into class and manage todo data with the component state

## 33. Handling Events in React

- similar to Vanilla JavaScript events

https://reactjs.org/docs/events.html#supported-events

- supported events in React

```javascript
<button onClick={function() {console.log("I was clicked!")}}>Click me</button>
<button onClick={() => console.log("I was clicked!")}>Click me</button>
```

- inline with anonymous function can be shortened with ES6 arrow function syntax.

```
function handleClick() {
    console.log("I was clicked")
}
<button onClick={handleClick}>Click me</button>
```

- or add separate event function

## 34. React Todo App Phase 5

- add an event Handler

## 35. React setState: Changing the State

- don't directly modify the state.

```javascript
handleClick() {
    this.setState({ count: 1 })
}
```

- Create an event handler and completely replace using `setState()`

```javascript
this.handleClick = this.handleClick.bind(this)
```

- Add a bind statement to the constructor

```javascript
handleClick() {
    this.setState(prevState => {
        return {
            count: prevState.count + 1
        }
    })
}
```

- setState accepts an object literal or an anonymous function representing the previous state.

## 36. React Todo App Phase 6

```javascript
handleChange(id) {
    this.setState(prevState => {
        const updatedTodos = prevState.todos.map(todo => {
            if (todo.id === id) {
                todo.completed = !todo.completed
            }
            return todo
        })
        return {
            todos: updatedTodos
        }
    })
}
```

- create a new array based on the previous state
- and when it gets to the item that matches the id from the event property, switch states.

```javascript
if (todo.id === id) {
    return {
        ...todo,
        completed: !todo.completed
    }
}
```

- someone pointed out that the previous example modified the previous state, which you don't want to do directly.
- so, use the ES6 spread syntax to return a new object with the state changed for that one id.
- only the affected rows are shown here.

## 38. React Lifecycle Methods

https://engineering.musefind.com/react-lifecycle-methods-how-and-when-to-use-them-2111a1b692b1

https://reactjs.org/blog/2018/03/29/react-v-16-3.html#component-lifecycle-changes

- React components go through a lifecycle or phases

- React 16.3 deprecated some of the previous lifecycle methods

```javascript
render()
```

- a method that we have already been using

```java
componentDidMount() {
	// GET the data I need to correctly display
}
```

- Run the very first time React shows the component.
- Usually used to make a request to an API to get data

```javascript
componentWillReceiveProps(nextProps) {
    if (nextProps.whatever !== this.props.whatever) {
		// do something important here
	}
}
```

- Check to see if new props are different
- Deprecated after 16.3
- actually renamed to `UNSAFE_componentWillReceiveProps` until React 17 is released.

```javascript
shouldComponentUpdate(nextProps, nextState) {
    // return true if want it to update
    // return false if not
}
```

- React will render when states change and this method gives the developer a chance to decide if a component should update.

```javascript
componentWillUnmount() {
    // teardown or cleanup your code before your component disappears
    // (E.g. remove event listeners)
}
```

- end of the lifecycle
- cleanup or teardown for anything that might clutter the DOM

### Deprecated

```javascript
// componentWillMount() {

// }
// componentWillReceiveProps(nextProps) {
//     if (nextProps.whatever !== this.props.whatever) {
//         // do something important here
//     }
// }
// componentWillUpdate() {

// }
```

### New

```javascript
static getDerivedStateFromProps(props, state) {
    // return the new, updated state based upon the props
	// https://reactjs.org/docs/react-component.html#static-getderivedstatefromprops
    // https://reactjs.org/blog/2018/06/07/you-probably-dont-need-derived-state.html
}
```

- static method
- React team wrote blog about how you probably do not need derived state and discourages its use.

```javascript
 getSnapshotBeforeUpdate() {
     // create a backup of the current way things are
     // https://reactjs.org/docs/react-component.html#getsnapshotbeforeupdate
 }
```

- React team thinks it will not be very common though

### Update

https://scrimba.com/g/greacthooks

- Another Scrimba screencast that forgot to mention originally in this screencast

```javascript
componentDidMount() {
    console.log("Mounted")
}

componentDidUpdate() {
    console.log("Did Update")
}

render() {
    console.log("Render")
}
```

- Any changes first call the Render method
- Mounted on the first render
- And Updated on any changes

```javascript
componentDidUpdate(prevProps, prevState) {
    if(prevState.count !== this.state.count) {
        const newColor = randomcolor()
        this.setState({color: newColor})
    }
}
```

- if you need to change this state, make sure to avoid an infinite loop since setState() triggers a render every time the state is changed.
- randomcolor is an npm package that returns a random color.
- You can use this method to avoid duplicating code

## 41. React Conditional Render

- React Conditional Rendering is not the only way this can be done since you can also use Vanilla JavaScript

- use ternary operator to load different components based on some state value.

```javascript
componentDidMount() {
    setTimeout(() => {
        this.setState({
            isLoading: false
        })
    }, 1500)
}

render() {
    return (
        <div>
        {this.state.isLoading ?
         <h1>Loading...</h1> :
         <Conditional />}
        </div>
    )
}
```

- `componentDidMount` simulates the loading of data from an API and the changing of the rendered component when loading is finished.

```javas
this.state.unreadMessages.length > 0 && 
<h2>You have {this.state.unreadMessages.length} unread messages!</h2>
```

- the conditional && operator can simplify rendering if you are checking a state variable.
- We talked about this earlier, but bringing up again as another option here.

## 44. React Todo App Phase 7

- render a different style based on the state

## 45. Fetching Data from an API with React

https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/fetch

- using the Fetch built-in JavaScript tool
- componentDidMount acts like a hook

https://swapi.co/

- Star Wars API

https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-promise-27fc71e77261

- JavaScript promises
- There are a lot of other articles to get familiar with promises

```javascript
componentDidMount() {
    fetch("https://swapi.co/api/people/1")
        .then(response => response.json())
        .then(data => {
            this.setState({
                character: data
            })
        })
}
```

- fetch is global so it just works
- chain promises
- if you don't save data into some variable it will just disappear, so save it to a variable in the component state.

- remember to use a loading variable in the state object to display a message to the user in the case of a slow connection.

## 46. React Forms

https://reactjs.org/docs/forms.html

- React documentation on forms

- In Vanilla JavaScript, you would usually wait until the user clicks submit to check the form data
- In React you can 

```javascript
handleChange(event) {
    this.setState({
        [event.target.name]: event.target.value
    })
}
```

- set an event handler on the form object
- Example is two input boxes with an onChange event.
- You can create a generic function to follow the DRY principle
- `event` is a parameter that represents the event action and is automatically passed to the function
- use the square brackets for the key
- This is just being familiar with the JavaScript event object
- The name property of the form element should match the item in the state object.

```javascript
handleChange(event) {
    const {name, value} = event.target
    this.setState({
        [name]: value
    })
}

<input 
    type="text"  
    value={this.state.firstName} 
    name="firstName" 
    placeholder="First Name" 
    onChange={this.handleChange} 
    />
```

- looks a little cleaner
- The state should always be the source of truth for the value of a component.
- put properties on new lines when they start to wrap the first line

```javascript
 /**
 * Other useful form elements:
 * 
 *  <textarea /> element
 *  <input type="checkbox" />
 *  <input type="radio" />
 *  <select> and <option> elements
 */
handleChange(event) {
    const {name, value, type, checked} = event.target
    type === "checkbox" ? this.setState({ [name]: checked }) : this.setState({ [name]: value })
}

<textarea 
    value={"Some default value"}
    onChange={this.handleChange}
/>

<label>
	<input 
        type="checkbox" 
        name="isFriendly"
        checked={this.state.isFriendly}
        onChange={this.handleChange}
    /> Is friendly?
</label>

<label>
	<input 
        type="radio" 
        name="gender"
        value="male"
        checked={this.state.gender === "male"}
        onChange={this.handleChange}
    /> Male
</label>

<label>Favorite Color:</label>
<select 
    value={this.state.favColor}
    onChange={this.handleChange}
    name="favColor"
>
    <option value="blue">Blue</option>
    <option value="green">Green</option>
    <option value="red">Red</option>
    <option value="orange">Orange</option>
    <option value="yellow">Yellow</option>
</select>
```

- a React textarea allows a single tag with a value property.
- A checkbox is just a boolean value.
- update the event handler to handle different types of targets.
  - a checkbox and radio are special type of target that has a checked state.
- radios that are named the same only allows one to be checked when the form is submitted.
- Formik is a library that makes it easier to create React forms

```javascript
<form onSubmit={this.handleSubmit}>
    <button>Submit</button>
</form>
```

- in HTML5 the default action of a button in a form is to submit the form.
- put the submit action in the form tag with the name of a function that will be called.

## 49. React Container & Component Architecture

- it is easy to lose place in code with lots of scrolling
- separate view components and logic components
- states will be pass as props so change this to props
- link everything up and change names while debugging
- Redux changes this architecture?

## 51. Writing Modern React Apps

- It is interesting to note that this screencast is using React@16.4.0 and the latest version today is React@16.13.1 with the latest React@17.0.0 slated to be release later this year (2020).
- Bob makes the comment that tutorials from only 2 years ago are drastically different than today.
- Some features may be released as experimental, but I guess, how would you like to write code is the philosophy driving language updates.

```javascript
// Change to use arrow functions
handleChange = (event) => {
    const { name, value } = event.target
    this.setState({
        [name]: value
    })
}
```

- an arrow function no longer needs to be bound in the constructor since it will use the this context of the class.

```javascript
// Change to use class properties
state = {
    firstName: ""
}
```

- class properties can be declared on their own outside of the constructor and the constructor can be removed entirely.

Other modern/advanced React features/topics to learn:

* Official React Context API - https://reactjs.org/docs/context.html
  * VSchool dropped Redux and uses Context API instead

* Error Boundaries - https://reactjs.org/docs/error-boundaries.html

* render props - https://reactjs.org/docs/render-props.html

* Higher Order Components - https://reactjs.org/docs/higher-order-components.html

* React Router - https://reacttraining.com/react-router/core/guides/philosophy
  * Single Page Applications (SPA)

* React Hooks - https://reactjs.org/docs/hooks-intro.html
  * a way of including and modifying states within components

* React lazy, memo, and Suspense - https://reactjs.org/blog/2018/10/23/react-v-16-6.html
  * Suspense has to do with asynchronous loading

## React Hooks

- There has been a shift to phase out class components since functional components make them unnecessary
- "Hook into" state and lifecycle methods of components without using classes.
- Improve readability and organization of components

```javascript
useState()
useEffect()
```

### useState()

```javascript
import React from "react"

class App extends React.Component {
    constructor() {
        super()
        this.state = {
            answer: "Yes"
        }
    }
    
    render() {
        return (
            <div>
                <h1>Is state important to know? {this.state.answer}</h1>
            </div>
        )
    }
}
```

- can be replaced with:

```javascript
import React, {useState} from "react"

function App() {
    const [answer] = useState("Yes")
    return (
        <div>
            <h1>Is state important to know? {answer}</h1>
        </div>
    )
}
```

- this tells React that answer is a useState hook
- and the value is available in JSX

```javascript
function App() {
    const [count, setCount] = useState(0)
    
    return (
        <div>
            <h1>{count}</h1>
            <button onClick={() => setCount(prevCount => prevCount + 1)}>Change!</button>
        </div>
    )
}
```

- give a function in the useState declaration to be called when you want to update the state.
- what you have here is an anonymous arrow function that either accepts a value or a function as seen here
- prevCount has the value of the previous state

```javascript
function App() {
    const [count, setCount] = useState(0)
    
    function increment() {
        setCount(prevCount => prevCount + 1)
    }
    
    return (
        <div>
            <h1>{count}</h1>
            <button onClick={increment}>Increment</button>
        </div>
    )
}
```

- is it more readable to replace the arrow functions with a function inside the function?

```javascript
const [count, setCount] = useState(0)
const [answer, setAnswer] = useState("Yes")
```

- A function can have many useStates

### useEffect()

- replaces lifecycle methods -> componentDidMount, componentDidUpdate, componentWillUnmount
- focus on these uses for example:
  - Side effects?
  - Network request
  - Manual DOM manipulation
  - Event listeners or timeouts and intervals

```javascript
const [color, setColor] = useState("")

useEffect(() => {
    setColor(randomcolor())
}, [count])
```

- same scenario as before
- useEffect is called whenever the state is changed
- include the second parameter to tell it which variable state to listen for,  which can also be a list of variables
- make the second parameter an empty array to only use the effect on the first render, like a componentDidMount method.
- You could also pass the first effect in the useState declaration, but this demonstrates the idea.

```javascript
useEffect(() => {
    const intervalId = setInterval(() => {
        // setCount(prevCount => prevCount + 1)
    }, 1000)
    return () => clearInterval(intervalId)
}, [])
```

- you can have multiple useEffects and include a return to perform cleanup when the component unmounts

## 57. Project Ideas

https://medium.freecodecamp.org/every-time-you-build-a-to-do-list-app-a-puppy-dies-505b54637a5d

https://medium.freecodecamp.org/want-to-build-something-fun-heres-a-list-of-sample-web-app-ideas-b991bce0ed9a

https://medium.freecodecamp.org/summer-is-over-you-should-be-coding-heres-yet-another-list-of-exciting-ideas-to-build-a95d7704d36d