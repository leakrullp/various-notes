
## 1. HTML
- [x] Basic HTML tags for document structure and content
- [x] Table elements
- [x] HTML forms [Basics](https://www.w3schools.com/tags/tag_form.asp) [Tutorial](https://www.w3schools.com/html/html_forms.asp)
- [x] Block vs Inline elements: https://www.w3schools.com/htmL/html_blocks.asp
- [x] HTML 5 semantic elements 
- [x] HTML Events: [Basics](https://www.w3schools.com/tags/ref_eventattributes.asp)
- [x] Universal Resource Locators (URLs)
- [ ] What is a Website?

## 2. CSS
- [x] CSS Rules, CSS selectors, CSS properties
- [x] Box Model layout and positioning
- [x] Flexible Box layout and positioning [W3Schools](https://www.w3schools.com/css/css3_flexbox.asp)
- [x] How to add CSS in a HTML document
- [x] Responsive Web Design - Media Queries

## 3. Website design
- [ ] Website Development Process
- [ ] Information architecture
- [ ] Site structural patterns
- [ ] Web interface design principles
	- [ ] Usability 
	- [ ] Jakob Nielsen’s 10 Interaction Design principles
- [ ] Wireframe

## 4. JavaScript
- [ ] Scope of variables
- [ ] Objects, properties, and methods
- [ ] Functions (regular, anonymous, arrow functions)
- [ ] Arrays: iterating, adding and removing array elements
- [ ] Arrays: map, reduce and filter methods
- [ ] Template literals (template strings)
- [ ] DOM API: finding/adding/changing/deleting elements
- [ ] Asynchronous programming (callback functions, promises, async/await)
- [ ] Destructuring assignment and destructuring of function arguments
- [ ] Spread operator `...`
### My focus:
- Promises
- Spread operators
- Scope of variables
- Destructuring

## 5. Typescript
- [ ] Typescript vs JavaScript
- [ ] Type inference
- [ ] Interface
- [ ] Classes and Inheritance
- [ ] Union, Intersection, Tuple
- [ ] Generics
	- [ ] Generic Interfaces
	- [ ] Generic Classes
	- [ ] Generic Functions
- [ ] Modules and import/export

## 6. Software architectures
- [ ] Architectural patterns (styles)
- [ ] Logical vs physical architecture
- [ ] Two-layer vs Three-layer architecture
- [ ] Model-View-Controller (MVC) pattern
- [ ] Multi-Page vs Single-Page Web Applications

## 7. RESTful web services/Express framework
- [ ] REST architectural style
- [ ] RESTful services
- [ ] HTTP Protocol: requests and responses
- [ ] JavaScript Object Notation (JSON)
- [ ] Routing HTTP requests
- [ ] Invoking RESTful API with JavaScript Fetch API
- [ ] RESTful API software architecture

## 8. React framework
- [ ] React approach vs Model-View-Controller
- [ ] Class components
- [ ] Functional components
- [ ] React JSX notation
- [ ] Updating state of components
- [ ] Dynamic composition of components
- [ ] Routing and navigation.
- [ ] Rendering a list of components
- [ ] Application state management
- [ ] Context API in React
- [ ] Updating context state
- [ ] Forms and data entry
- [ ] Data validation in forms.


# Connection to ILOs
1. Apply HTML, CSS, and JavaScript as well as the principles of user interface design in developing websites and dynamic client-side Web applications.
2. Apply fundamental object-oriented and functional programming techniques of JavaScript and Typescript in developing Web applications.
3. Explain basic Web standards, protocols and architectural styles used in distributed Web applications.
4. Develop moderately complex dynamic client-side Web applications using modern Web frameworks.
5. Design and develop server-side Web services based on REST architectural style (RESTful APIs).

# Project document
The project document describes your developed software system explaining the following points:
- **Web design of the client-side application (2-5 pages)**
	- The information architecture and the website design principles: used taxonomies, hierarchies of information, site navigation concepts, etc.
- **Design of the RESTful API (1-3 pages)**
	- A short explanation of the implemented web service endpoints (operations/list of resources), including the table from the “Template for RESTful API specification” with HTTP methods and paths.
	- Note: the detailed operation specifications based on the provided template form the second mini project should be put in the appendix of the project document and these pages are not counted.
- **Software architecture of your developed system (2-5 pages)**
	- Explaining the overall logical/physical architecture of your software system (components you developed and used third-party components and their roles)
	- Software styles/patterns and solutions used in your developed components in both client-side React application and RESTful API application, including your own, built-in React or Express standard components, third-party frameworks (e.g. react-bootstrap), React patterns and techniques used (e.g. prop drilling, lifted state, Context API), your data storage solution, etc.

# Oral Exam Structure (30 min)
- **Project presentation session (10 min)** online (live) presentation of your developed system:
	- Demonstration of the system functionality (2-3min)
		- Show how the required functional requirements are implemented (using live app)
	- Explanation of the web UI design (2-3 min)
		- Discuss how the web design principles are applied (using live app).
	- Explanation of the system software architecture (3-5 min)
		- Discuss which architectural styles, software patterns, frameworks and components are used (using live app/source code/UML diagrams).
- **Discussion/Questioning session (10 min):**
	- Extra questions/discussion regarding the presented project
	- 2 questions drawn randomly from the list of selected areas (I-VIII topics).
- **Grade deliberation (5 min)**
- **Grade and feedback (5 min)**

```js
const thisisglobal = "hehe"

function Foo(){
	var y = 0;
	for(let i = 0, i > 10, i++){
		var x = 0;
	}
}
```

```js
const person = {
  name: "Lars",
  greet() {
    const inner = (name) => {
      console.log(name)
    };
    inner();
  }
};

const result = (function(n) { return n * n; })(5);

const products = [/* gak og løger*/]
const country = "Denmark"
products.filter((p) => p.country === country)

products.reduce((acc, cur) => acc + cur.originalPrice, 0)

```

```js
const total = items.reduce((sum, item) => sum + (item.quantity || 0),0,);
```