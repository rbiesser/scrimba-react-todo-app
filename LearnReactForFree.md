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

## 27. Class-base Components

https://scrimba.com/p/p7P5Hd/c3bNDCz

