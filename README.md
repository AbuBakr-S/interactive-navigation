# interactive-navigation
In this project I will be building a landing page that uses JavaScript to create an interactive navigational experience for the user.

# Syntax
## Hoisting
Hoisting is a result of how JavaScript is interpreted by your browser. Essentially, before any JavaScript code is executed, all variables declared with `var` are "hoisted", which means they're raised to the top of the function scope.

## let and const Variables
Variables declared with `let` and `const` eliminate this specific issue of hoisting because they’re scoped to the block, not to the function. Previously, when you used var, variables were either scoped globally or locally to an entire function scope.

### Variable Scope - Temporal Dead Zone
If a variable is declared using `let` or `const` inside a block of code (denoted by curly braces `{ }`), then the variable is stuck in what is known as the temporal dead zone until the variable’s declaration is processed. This behavior prevents variables from being accessed only until after they’ve been declared.

### Rules for using let and const
* Variables declared with `let` can be reassigned, but can’t be redeclared in the same scope.
* Variables declared with `const` must be assigned an initial value, but can’t be redeclared in the same scope, and can’t be reassigned.

### Use cases
* use `let` when you plan to reassign new values to a variable
* use `const` when you don’t plan on reassigning new values to a variable.

Since `const` is the strictest way to declare a variable, we suggest that you always declare variables with `const` because it'll make your code easier to reason about since you know the identifiers won't change throughout the lifetime of your program. If you find that you need to update a variable or change it, then go back and switch it from `const` to `let`.

## Template Literals
Template literals are essentially string literals that include embedded expressions.
Denoted with backticks (` `) instead of single quotes ( '' ) or double quotes ( "" ), template literals can contain placeholders which are represented using `${expression}`. This makes it much easier to build strings.
Here's the previous examples using template literals.

``` let message = `${student.name} please see ${teacher.name} in ${teacher.room} to pick up your report card.`; ```

## Destructuring
In ES6, you can extract data from arrays and objects into distinct variables using destructuring.

### Examples Without Destructuring
**PRE-ES6 | Extracting values from an array.**
```
const point = [10, 25, -34];

const x = point[0];
const y = point[1];
const z = point[2];

console.log(x, y, z);
```
**Prints:** 10 25 -34


**PRE-ES6 | And this example shows extracting values from an object.**
```
const gemstone = {
  type: 'quartz',
  color: 'rose',
  carat: 21.29
};

const type = gemstone.type;
const color = gemstone.color;
const carat = gemstone.carat;

console.log(type, color, carat);
```
**Prints:** quartz rose 21.29


### Examples With Destructuring
In ES6, you can **extract data from arrays and objects into distinct variables** using destructuring.
Destructuring borrows inspiration from languages like Perl and Python by allowing you to specify the elements you want to extract from an array or object on the left side of an assignment. Let’s take a look at both examples rewritten using destructuring.

**ES6 | Destructuring values from an array**
```
const point = [10, 25, -34];
const [x, y, z] = point;

console.log(x, y, z);
```
**Prints:** 10 25 -34


In this example, the brackets `[ ]` represent the array being destructured and `x`, `y`, and `z` represent the variables where you want to store the values from the array. Notice how you don’t have to specify the indexes for where to extract the values from because the **indexes are implied.**

**TIP:** You can also ignore values when destructuring arrays. For example, const `[x, , z] = point;` **ignores the `y` coordinate and discards it.**

**ES6 | Destructuring values from an object**
```
const gemstone = {
  type: 'quartz',
  color: 'rose',
  carat: 21.29
};

const {type, color, carat} = gemstone;

console.log(type, color, carat);
```
**Prints:** quartz rose 21.29


In this example, the curly braces `{ }` represent the object being destructured and `type`, `color`, and `carat` represent the variables where you want to store the properties from the object. Notice how **you don’t have to specify the property from where to extract the values.** Because `gemstone` has a property named `type`, the value is automatically stored in the `type` variable. Similarly, `gemstone` has a `color` property, so the value of `color` automatically gets stored in the `color` variable. And it's the same with `carat`.

**TIP:** You can also specify the values you want to select when destructuring an object. For example, let {color} = gemstone; will only select the color property from the gemstone object.

#### Exercise 1
```
const circle = {
  radius: 10,
  color: 'orange',
  getArea: function() {
    return Math.PI * this.radius * this.radius;
  },
  getCircumference: function() {
    return 2 * Math.PI * this.radius;
  }
};

let {radius, getArea, getCircumference} = circle;

getArea()
```

#### Exercise 2
When you destructure the object and store the `getArea()` method into the `getArea` variable, it no longer has access to this in the circle object which results in an area that is `NaN`.

 **Programming Quiz: Destructuring Arrays (1-3)**
 **Use destructuring to initialize the variables `one`, `two`, and `three` with the colors from the `things` array.**

```
const things = ['red', 'basketball', 'paperclip', 'green', 'computer', 'earth', 'udacity', 'blue', 'dogs'];
const [one, , , two, , , , three] = things;

const colors = `List of Colors
1. ${one}
2. ${two}
3. ${three}`;

console.log(colors);
```

## Object Literal Shorthand

From:
```
const gemstone = {
  type: 'quartz',
  color: 'rose',
  carat: 21.29
};
```

To:
`const {type, color, carat} = gemstone;`

### Shorthand Method Names
From:
```
const gemstone = {
  type,
  color,
  carat,
  calculateWorth: function() {
    // will calculate worth of gemstone based on type, color, and carat
  }
};
```

To:
```
let gemstone = {
  type,
  color,
  carat,
  calculateWorth() { ... }
};
```

## Loops
The `for...of` loop is the most recent addition to the family of for loops in JavaScript.

It combines the strengths of its siblings, the `for` loop and the `for...in` loop, to **loop over any type of data that is iterable (meaning it follows the iterable protocol which we'll look at in lesson 3)**. By default, this includes the data types String, Array, Map, and Set—notably absent from this list is the Object data type (i.e. {}). Objects are not iterable, by default.

### for loop
While for loops certainly have an advantage when looping through arrays, some data is not structured like an array, so a for loop isn’t always an option.

```
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

for (let i = 0; i < digits.length; i++) {
  console.log(digits[i]);
}
```
**Prints:** 0 1 2 3 4 5 6 7 8 9


#### Evaluation
**Strengths:** 
* Ideal for looping through arrays

**Weakness:** 
* Having to keep track of the counter (i) and exit condition (digits.length).

 
### for...in loop
The for...in loop improves upon the weaknesses of the for loop by eliminating the counting logic and exit condition.

```
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

for (const index in digits) {
  console.log(digits[index]);
}
```
**Prints:** 0 1 2 3 4 5 6 7 8 9


Also, the for...in loop can get you into big trouble when you need to add an extra method to an array (or another object). Because for...in loops loop over all enumerable properties, this means if you add any additional properties to the array's prototype, then those properties will also appear in the loop.

```
Array.prototype.decimalfy = function() {
  for (let i = 0; i < this.length; i++) {
    this[i] = this[i].toFixed(2);
  }
};

const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

for (const index in digits) {
  console.log(digits[index]);
}

Prints: 
0 
1 
2 
3 
4 
5 
6 
7 
8 
9
function() {
 for (let i = 0; i < this.length; i++) {
  this[i] = this[i].toFixed(2);
 }
}
```

**Strength:** 
* Eliminating the counting logic and exit condition.

**Weakness:** 
* You still have to deal with the issue of using an index to access the values of the array, and that stinks; it almost makes it more confusing than before.

* You could get into big trouble when you need to add an extra method to an array (or another object). Because for...in loops loop over all enumerable properties, this means if you add any additional properties to the array's prototype, then those properties will also appear in the loop.

* This is why for...in loops are discouraged when looping over arrays.

 
**NOTE:** The forEach loop is another type of for loop in JavaScript. However, forEach() is actually an array method, so it can only be used exclusively with arrays. There is also no way to stop or break a forEach loop. If you need that type of behavior in your loop, you’ll have to use a basic for loop.


### for...of loop
The `for...of` loop is used to loop over **any type of data that is iterable**. This makes the `for...of` loop the most concise version of all the for loops.

```
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

for (const digit of digits) {
  console.log(digit);
}
```

**Strength:** 
* You can stop or break a for...of loop at anytime.
* And you don’t have to worry about adding new properties to objects. The for...of loop will only loop over the values in the object.

```
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

for (const digit of digits) {
  if (digit % 2 === 0) {
    continue;
  }
  console.log(digit);
}
```
**Prints:** 1 3 5 7 9

**TIP:** It’s good practice to use plural names for objects that are collections of values. That way, when you loop over the collection, you can use the singular version of the name when referencing individual values in the collection. For example, `for (const button of buttons){...};`


#### Exercise 3
Instructions: Capitalise the first letter of each day.

```
const days = ['sunday', 'monday', 'tuesday', 'wednesday', 'thursday', 'friday', 'saturday'];

for (const day of days){
    const firstLetter = day.charAt(0).toUpperCase();
    const remainingLetters = day.slice(1); 
    console.log(firstLetter + remainingLetters);
}
```

## Spread operator | Spread Elements Out
The spread operator, written with three consecutive dots ( `...` ), is new in ES6 and gives you the ability to expand, or spread, iterable objects into multiple elements.

Let’s take a look at a few examples to see how it works.

```
const books = ["Don Quixote", "The Hobbit", "Alice in Wonderland", "Tale of Two Cities"];
console.log(...books);
```
**Prints:** Don Quixote The Hobbit Alice in Wonderland Tale of Two Cities

```
const primes = new Set([2, 3, 5, 7, 11, 13, 17, 19, 23, 29]);
console.log(...primes);
```
**Prints:** 2 3 5 7 11 13 17 19 23 29

### Spread instead of Concat - Arrays

#### Exercise 4
Instructions: Use the spread operator to combine the `fruits` and `vegetables` arrays into the `produce` array.

```
const fruits = ["apples", "bananas", "pears"];
const vegetables = ["corn", "potatoes", "carrots"];

const produce = [...fruits, ...vegetables];

console.log(produce);

```
**Prints:** `[ 'apples', 'bananas', 'pears', 'corn', 'potatoes', 'carrots' ]`


## Rest Parameter | Bundle Elements Together

The rest parameter, also written with three consecutive dots ( `...` ), allows you to represent an indefinite number of elements as an array. This can be helpful in a couple of different situations.

One situation is when assigning the values of an array to variables. For example,

```
const order = [20.17, 18.67, 1.50, "cheese", "eggs", "milk", "bread"];
const [total, subtotal, tax, ...items] = order;
console.log(total, subtotal, tax, items);
```
**Prints:** `20.17 18.67 1.5 ["cheese", "eggs", "milk", "bread"]`

### Variadic functions
Another use case for the rest parameter is when you’re working with variadic functions. Variadic functions are functions that take an indefinite number of arguments.

```
function sum(...nums) {
  let total = 0;  
  for(const num of nums) {
    total += num;
  }
  return total;
}
```

#### Exercise 5
Instructions: Use the rest parameter to create an average() function that calculates the average of an unlimited amount of numbers.

```
function average(...nums) {
  let total = 0;
  for (const num of nums) {
    total += num;
  }
  return total === 0 ? 0 : total / nums.length;
}

console.log(average(2, 6));
console.log(average(2, 3, 3, 5, 7, 10));
console.log(average(7, 1432, 12, 13, 100));
console.log(average());
```

# The DOM
The DOM stands for "Document Object Model" and is a tree-like structure that is a representation of the HTML document, the relationship between elements, and contains the content and properties of the elements. The DOM is constructed from the browser and is globally accessible by JavaScript code using the document object.

[DOM](https://developer.mozilla.org/en-US/docs/Glossary/DOM)

1. HTML is received
2. HTML tags are converted to tokens
3. tokens are converted to Nodes
4. Nodes are converted to the DOM

When you request a website, no matter what backend language is powering that website, it will respond with HTML. The browser receives a stream of HTML. The bytes are run through a complicated (but fully documented) parsing process that determines the different characters (e.g. the start tag character <, an attribute like href, a closing angle bracket like >). After parsing has occurred, a process called tokenization. Tokenization takes one character at a time and builds up tokens. The tokens are:

* DOCTYPE
* start tag
* end tag
* comment
* character
* end-of-file

The DOM is standardized by the W3C. There are a number of specifications that make up the DOM, here are few:

* Core Specification
* Events Specification
* Style Specification
* Validation Specification
* Load and Save Specification

## Accessing Elements
* document.getElementById()
* document.getElementsByClassName()
* document.getElementsByTagName()
* document.querySelector()
* document.querySelectorAll()

## Node Interface
The Node Interface is a blueprint for all of the properties (data) and methods (functionality) that every real node has after it's been created. `Document`, `Element`, `Comment` and `DocumentFragment` are a few examples of nodes. 

[Node](https://developer.mozilla.org/en-US/docs/Web/API/Node)

`interface` = blueprint
`properties` = data
`methods` = functionality

Node = Interface
node = Object

Node is an interface from which various types of DOM API objects inherit, allowing those types to be treated similarly; for example, inheriting the same set of methods, or being testable in the same way.

All of the following interfaces inherit the Node interface's methods and properties: Document, Element, Attr, CharacterData (which Text, Comment, and CDATASection inherit), ProcessingInstruction, DocumentFragment, DocumentType, Notation, Entity, EntityReference

Those interfaces may return null in certain cases where the methods and properties are not relevant. They may throw an exception — for example when adding children to a node type for which no children can exist.

## Element Interface
The Element Interface is a blueprint for creating elements. The Element Interface is a descendent of the Node Interface.

Element = Interface
element = Object

See the full list of available [Interfaces](https://developer.mozilla.org/en-US/docs/Web/API)

# Creating Content with JavaScript

## Update Existing Page Content

### An Element's Inner HTML
Every element inherits properties and methods from the Element Interface (remember this from the previous lesson!). This means that every element has an `.innerHTML` property. This property, as it's rightly named, represents the markup of the element's content. We can use this property to:

* get an element's (and all of its descendants!) HTML content
* set an element's HTML content

`.innerHTML` is a property that returns a string. `.textContent` will not display the content as HTML. Instead, it will still display everything as text - even the HTML characters!

### An Element's Text Content
If we just want the text content, we can use the fantastically named `.textContent` property!

The `.textContent` property will (set/get):

* set the text content of an element and all its descendants
* return the text content of an element and all its descendants

Setting an element's text content is easy, just set it like you would any other property:

`nanodegreeCard.textContent = "I will be the updated text for the nanodegreeCard element!";`

### Text Content Version 2
`.textContent` completely ignores any CSS styling and returns all of the element's HTML just as it's listed in the HTML. On the other hand, the `.innerText` property will take CSS styling into consideration and will return the text that is visibly rendered on the page.


## Add New Page Content

### Create an Elelemnt
Creating an element, `document.createElement()`, just creates it. It doesn't add it to the DOM.

### Add Element to the Page
We can use the `.appendChild()` method to add an element to the page. This needs to be called on another element, not the document object!

```
// create a brand new <span> element
const newSpan = document.createElement('span');

// select the first (main) heading of the page
const mainHeading = document.querySelector('h1');

// add the the <span> element as the last child element of the main heading
mainHeading.appendChild(newSpan);
```

## Update an Element's Text
Although you can create a new textNode to change text, it's easier and quicker to use the `.textContent` property.

```
const myPara = document.createElement('p');

myPara.textContent = 'I am the text for the paragraph!';
document.body.appendChild(myPara);
```

## Inserting HTML In Other Locations
The `.insertAdjacentHTML()` method has to be called with two arguments:

1. The location of the HTML
2. The HTML text that is going to be inserted

The first argument to this method will let us insert the new HTML in one of four different locations:

`beforebegin` – inserts the HTML text as a previous sibling 
`afterbegin` – inserts the HTML text as the first child 
`beforeend` – inserts the HTML text as the last child 
`afterend` – inserts the HTML text as a following sibling

```
<!-- beforebegin -->
<p>
    <!-- afterbegin -->
    Existing text/HTML content
    <!-- beforeend -->
</p>
<!-- afterend -->
```

Here's how we'd call .insertAdjacentHTML():

```
const mainHeading = document.querySelector('#main-heading');
const htmlTextToAdd = '<h2>Skydiving is fun!</h2>';

mainHeading.insertAdjacentHTML('afterend', htmlTextToAdd);
```

## Remove Child Element
We can move the child element directly with the .remove() method:

```
const mainHeading = document.querySelector('h1');`
mainHeading.remove();
```

# Style Page Content

## Specificity
The closer the style rule is to an element, the more specific it is. For example, a rule in a style attribute on an element will override a style rule for that element in a CSS stylesheet.

In this section, we'll be looking at controlling page and element styling using the following properties and methods:

* `.style.<prop>` - Individual
* `.cssText()` - Multiple Styles
* `.setAttribute`() - Not just for Styling
* `.className` - Returns a String of all Classes
* `.classList` - Returns an Array of all Classes (also has several properties of it's own, the most popular listed below)
    * `.add()` - to add a class to the list
    * `.remove()` - to remove a class from the list
    * `.toggle()` - to add the class if it doesn't exists or remove it from the list if it does already exist
    * `.contains()` - returns a boolean based on if the class exists in the list or not


# Working with Browser Events

## Seeing an Event
The Chrome browser has a special `monitorEvents()` function that will let us see different events as they are occurring. See [monitorevents](https://developers.google.com/web/tools/chrome-devtools/console/events#monitor_events) documentation. 

You should run this for developing/testing purposes only:
```
// start displaying all events on the document object
monitorEvents(document);

// turn off the displaying of all events on the document object.
unmonitorEvents(document);
```

### EventTarget <-- Node <-- Element (<-- Inherits)
The Event Target is an interface implemented by objects that can receive events and may have listeners for them. It is inherited by all nodes and elements. Everything on the web is an event target (e.g. the `document object`, a `<p>` element, etc.).

If you take a look at the EventTarget Interface, you'll notice that it doesn't have any properties and only three methods! These methods are:

* .addEventListener()
* .removeEventListener()
* .dispatchEvent()

## Adding An Event Listener
We've taken a brief look at this hidden world of events. Using the .addEventListener() method will let us listen for events and respond to them! I just said "listen for events". There are several ways to "phrase" this, so I want to give some examples:

* listen for an event
* listen to an event
* hook into an event
* respond to an event

An Event Listener - Syntax: `<event-target>.addEventListener(<event-type>, <event-listener>);`

So an event listener needs three things:
1. an event target - this is called the target
2. the type of event to listen for - this is called the type
3. a function to run when the event occurs - this is called the listener

**Note:** Remember, everything on the web is an event target (e.g. the document object, a <p> element, etc.).

```
const mainHeading = document.querySelector('h1');

mainHeading.addEventListener('click', function () {
  console.log('The heading was clicked!');
});
```

For a full list of Events you can listen for, check out this [full list](https://developer.mozilla.org/en-US/docs/Web/Events).

## Remove an Event listener
The `.removeEventListener()` method requires you to pass the same exact listener function to it as the one you passed to `.addEventListener()`. When doing so, **Make sure that the Objects are Equal in JS**. JavaScript has the double equality (`==`) operator that will allow type coercion. It also has the triple equality (`===`) symbol that will prevent type coercion when comparing.

Let's see some pseudo-code for the `.removeEventListener()`:

`<event-target>.removeEventListener(<event-to-listen-for>, <function-to-remove>);`

### Example 6.1
Does the following code evaluate to true or false?
```
var a = {
    myFunction: function quiz() { console.log('hi'); }
};
var b = {
    myFunction: function quiz() { console.log('hi'); }
};

a.myFunction === b.myFunction
```
**Prints:** False

### Example 6.2
Does the following code evaluate to true or false?
```
function quiz() { ... }

var a = {
    myFunction: quiz
};
var b = {
    myFunction: quiz
}

a.myFunction === b.myFunction
```
**Prints:** True

Remember, the listener function must be the exact same function as the one used in the .addEventListener() call...not just an identical looking function. Let's look at a couple of examples.

### Example 6.3
#### This code will successfully add and then remove an event listener:
```
function myEventListeningFunction() {
    console.log('howdy');
}

// adds a listener for clicks, to run the `myEventListeningFunction` function
document.addEventListener('click', myEventListeningFunction);

// immediately removes the click listener that should run the `myEventListeningFunction` function
document.removeEventListener('click', myEventListeningFunction);
```

### Example 6.4
#### This code will not work (it does not remove the event listener):
```
// adds a listener for clicks, to run the `myEventListeningFunction` function
document.addEventListener('click', function myEventListeningFunction() {
    console.log('howdy');
});

// immediately removes the click listener that should run the `myEventListeningFunction` function
document.removeEventListener('click', function myEventListeningFunction() {
    console.log('howdy');
});
```

## Event Phases
There are three different phases during the lifecycle of an event. They are:

1. the capturing phase
2. the at target phase
3. and the bubbling phase

Most event handlers run during the at target phase, such as when you attach a click event handler to the button. The event arrives at the button (its target), and there's only a handler for it right there, so the event handler gets run.

But sometimes you have a collection of items -- such as a list -- and want to have one handler cover every item (and still have the option of individual handlers for some items.) 

### Bubbling:
**By default**, if you click on a child item and a handler doesn't intercept the click, **the event will "bubble" upward** to the parent, and keep bubbling **until something handles it or it hits the document**.

### Capturing:
Capturing, on the other hand, lets the parent intercept an event before it reaches a child.

### Process
1. Triggering the Event starts the process.
2. Capturing Phase starts from the HTML element ans works it's way down.
3. Once it gets to the element that was triggered, e.g. clicked, it switches to the At Target Phase.
4. Then it switches to the Bubbling Phase and works it's way back up to the HTML element.

### Default to Bubbling | 2 arguments
The code below uses `.addEventListener()` with only two arguments, so it will invoke the listener during the bubbling phase:
```
document.addEventListener('click', function () {
   console.log('The document was clicked');
});
```

### Setting to Capturing Phase | 3rd Argument
However, in this code, `.addEventListener()` is called with three arguments with the third argument being true (meaning it should invoke the listener earlier, during the capturing phase!).
```
document.addEventListener('click', function () {
   console.log('The document was clicked');
}, true);
```

By setting an event to fire during the Capturing Phase, it will trigger before arriving at the Target Phase.

## The Event Object
When an event occurs, the browser includes an event object. This includes information about the event itself. According to MDN, the `.addEventListener()`'s listener function receives: *a notification (an object that implements the Event interface) when an event of the specified type occurs*

```
document.addEventListener('click', function (event) {  // ← the `event` parameter is new!
   console.log('The document was clicked');
});
```

## Prevent Default Action
One common use case for thr event object is to prevent the default action from happening, e.g. when you submit a form, by default, it will send the data to the location in its action attribute. What if we wanted to validate the data before sending it? Without the event object, we're stuck with the default actions. However, **the event object has a `.preventDefault()` method** on it that a handler can call to prevent the default action from occurring!

### Example 7
```
const links = document.querySelectorAll('a');
const thirdLink = links[2];

thirdLink.addEventListener('click', function (event) {
    event.preventDefault();
    console.log("Look, ma! We didn't navigate to a new page!");
});
```

## Adding Too Many Events
Write DRY code. By extracting the function from the loop and adding the event listener once to the div element, you can write more efficient code. Below is a single event listener and a single event function.

### Example 8
```
const myCustomDiv = document.createElement('div');

function respondToTheClick() {
    console.log('A paragraph was clicked.');
}

for (let i = 1; i <= 200; i++) {
    const newElement = document.createElement('p');
    newElement.textContent = 'This is paragraph number ' + i;

    myCustomDiv.appendChild(newElement);
}

myCustomDiv.addEventListener('click', respondToTheClick);

document.body.appendChild(myCustomDiv);
```

## Event Delegation
Event Delegation is the process of delegating to a parent element the ability to manage events for child elements.
The event object has a `.target` property. This property references the target of the event.

Let's say that you click on a paragraph element. Here's roughly the process that happens:

1. a paragraph element is clicked
2. the event goes through the capturing phase
3. it reaches the target
4. it switches to the bubbling phase and starts going up the DOM tree
5. when it hits the `<div>` element, it runs the listener function
6. inside the listener function, event.target is the element that was clicked

So event.target gives us direct access to the paragraph element that was clicked. Because we have access to the element directly, we can access its `.textContent`, modify its styles, update the classes it has - we can do anything we want to it!

However, there is nothing to ensure that it was actually a `<p>` tag that was clicked before running that message. 

```
const myCustomDiv = document.createElement('div');

function respondToTheClick(evt) {
    console.log('A paragraph was clicked: ' + evt.target.textContent);    // Grab the Text Content from the Clicked Target Element Paragraph
}

for (let i = 1; i <= 200; i++) {
    const newElement = document.createElement('p');
    newElement.textContent = 'This is paragraph number ' + i;

    myCustomDiv.appendChild(newElement);
}

document.body.appendChild(myCustomDiv);

myCustomDiv.addEventListener('click', respondToTheClick);
```

### Verifying Listener Functions | FAIL

The listener function will still fire when either one of the paragraph elements is clicked, too! In other words, this listener function is not verifying that the target of the event is actually a `<span>` element.

```document.querySelector('#content').addEventListener('click', function (evt) {
    console.log('A span was clicked with text ' + evt.target.textContent);
});
```

### Verifying Listener Functions | PASS

```
document.querySelector('#content').addEventListener('click', function (evt) {
    if (evt.target.nodeName === 'SPAN') {  // ← verifies target is desired element
        console.log('A span was clicked with text ' + evt.target.textContent);
    }
});
```

When a `<span>` element is clicked, it will have a .nodeName property of `"SPAN"`, so the check will pass and the message will be logged. However, if a `<p>` element is clicked, it will have a .nodeName property of `"P"`, so the check will fail and the message will not be logged.

The `.nodeName` property will return a capital string, not a lowercase one. So when you perform your check make sure to either:

* check for capital letters
* convert the .nodeName to lowercase

```
// check using capital letters
if (evt.target.nodeName === 'SPAN') {
    console.log('A span was clicked with text ' + evt.target.textContent);
}

> // convert nodeName to lowercase
if (evt.target.nodeName.toLowerCase() === 'span') {
    console.log('A span was clicked with text ' + evt.target.textContent);
}
```

# DOM Ready
When the HTML is received and converted into tokens and built into the document object model, it's a **sequential process**. When the parser gets to a `<script>` tag, it must wait to download the script file and execute that JavaScript code. This is the important part and the key to why the placement of the JavaScript file matters!

If the DOM is built sequentially, if the JavaScript code is moved to the very bottom of the page, then by the time the JavaScript code is run, all DOM elements will already exist!

An alternative solution would be to use **Browser Events!**

## The Content Is Loaded Event
When the document object model has been fully loaded, the browser will fire an event. This event is called the DOMContentLoaded event, and we can listen for it the same way we listen to any other events:

```
document.addEventListener('DOMContentLoaded', function () {
    console.log('the DOM is ready to be interacted with!');
});
```

## Using the DOMContentLoaded Event
Because we now know about the DOMContentLoaded event, we can use it to keep our JS code in the `<head>`.

Let's update the previous HTML code to include this event:

```
<!DOCTYPE html>
<html lang="en">
<head>
    <link rel="stylesheet" href="/css/styles.css" />
    <script>
      document.addEventListener('DOMContentLoaded', function () {
          document.querySelector('footer').style.backgroundColor = 'purple';
      });
    </script>
```
This will prevent the DOM-styling code from running when the browser gets to it. Then, when the DOM has been constructed, the event will fire and this code will run.

JavaScript code in the `<head>` will run before JavaScript code in the `<body>`, so if you do have JavaScript code that needs to run as soon as possible, then you could put that code in the `<head>` and wrap it in a DOMContentLoaded event listener. This way it will run as early as possible, but not too early that the DOM isn't ready for it.

# Performance

## Using a Loop to Add Content

```
const myCustomDiv = document.createElement('div');

for (let i = 1; i <= 200; i++) {
  const newElement = document.createElement('p');
  newElement.innerText = 'This is paragraph number ' + i;

  myCustomDiv.appendChild(newElement);
}

document.body.appendChild(myCustomDiv);
```

## Testing Code Performance
The standard way to measure how long it takes code to run is by using `performance.now()`. `performance.now()` returns a timestamp that is measured in milliseconds, so it's extremely accurate.

- Accurate to five thousandths of a millisecond (5 microseconds)
- It starts measuring from the time the page loaded

1. Use performance.now() to get the an initial start time for the code
2. Run the code you want to test
3. Execute performance.now() to get another time measurement
4. Subtract the initial time from the final time

### Example 9 
Here is a non-real-world test 

```
const startingTime = performance.now();

for (let i = 1; i <= 100; i++) { 
  for (let j = 1; j <= 100; j++) {
    console.log('i and j are ', i, j);
  }
}

const endingTime = performance.now();
console.log('This code took ' + (endingTime - startingTime) + ' milliseconds.');
```

## Using a DOM Fragment
So far, we've been creating an extraneous placeholder `<div>` element just to hold all the `<p>` tags so we can add them all at once and then we append this `<div>` to the `<body>` element. 

The browser is constantly working to make the screen match the DOM. When we add a new element, the browser has to run through a `reflow` calculation (to determine the new screen layout) and then `repaint` the screen. This takes time.

* Mimics the Document
* Doesn't affect the document, cause reflow, or incur any performance impact
* Changes happen off-screen

Create an empty DocumentFragment Object:
`const myDocFrag = document.createDocumentFragment();`

```
const fragment = document.createDocumentFragment();  // ← uses a DocumentFragment instead of a <div>

for (let i = 0; i < 200; i++) {
    const newElement = document.createElement('p');
    newElement.innerText = 'This is paragraph number ' + i;

    fragment.appendChild(newElement);
}

document.body.appendChild(fragment); // reflow and repaint here -- once!
```

**Note:** A Key Theme is to move initialization code out of the for loop.

## Reflow & Repaint
* `Reflow` is the process of calculating the dimensions and position of page elements. This is a computationally intensive (slow) tasks
* `Repaint` is the process of drawing the pixels to the screen. This is faster than reflow, but is still not a fast process. You want to make sure that your code causes the fewest number of reflows as possible.

If you add a CSS class to an element, the browser often recalculates the layout of the entire page—that's one `reflow` and one `repaint`!

In general, if you have to make a group of changes, hide/change all/show is a great pattern to use if the changes are relatively contained to reduce reflow/repaint. Hiding elements doesn't change the layout, however making it visible again is equal to one reflow and repaint.

## Virtual DOM
By the way, this is why React and other "virtual DOM" libraries are so popular. You don't make changes to the DOM, but make changes to another structure (a "virtual DOM") and the library calculates the best way to update the screen to match. The catch is you then have to rework your code to use whatever library you're adopting, and sometimes you can do a better job updating the screen yourself (because you understand your own unique situation).

# Performance

## Single Threading
* JavaScript can "process" one command at a time. 
* Run-to-completion nature.
* When invoked, all of the code in the function gets executed.
* One function at a time

## The Call Stack
The JavaScript engine keeps a call stack (basically a list) of the functions that are running. When a function is invoked, it is added to the list. When all of the code inside a function has been run, then the function is removed from the call stack. The cool part about a call stack is that a function doesn't have to complete before another function is added to the call stack.

## Code Synchronicity
Synchronous - In Order
Asynchronous - Executed later

## The Event Loop
The simplest explanation of JavaScript's concurrency model uses two rules: If some JavaScript is running, let it run until it is finished ("run-to-completion"). If no JavaScript is running, run any pending event handlers.

Since most JavaScript is run in response to an event, this is known as an event loop: **Pick up the next event, run its handler, and repeat.**

There are three parts you have to think about around the event loop:

* the Call Stack
* Web APIs/the browser
* an Event Queue

Not all of the code that we write is 100% JavaScript code. Some of the code is interacting with the Web APIs (also known as "browser APIs"). There are many more examples, but both `.addEventListener()` and `setTimeout()` are Web APIs.

When all of the functions in the Call Stack have finished (also known as idle time), then the Queue is checked to see if anything is waiting. If something is in the Queue, then it's run, creating an entry on the call stack.

1) current synchronous code runs to completion, and 2) events are processed when the browser isn't busy. Asynchronous code (such as loading an image) runs outside of this loop and sends an event when it is done.

## Running Code Later
The `setTimeout()` function takes:

* a function to run at some later time
* the number of milliseconds the code should wait before running the function

### Example 10
```
setTimeout(function sayHi() {
    console.log('Howdy');
}, 1000);
```

If we ran this code, the string 'Howdy' would appear in the console in about 1,000 milliseconds or in just about 1 second.

Since `setTimeout()` is an API provided by the browser, the call to `setTimeout()` gives the `sayHi()` function over to the browser which it starts a timer. After the timer is finished, the `sayHi()` function moves to the Queue. If the Call Stack is empty, then the `sayHi()` function is moved to the Call Stack and executed.

**`setTimeout()` with Delay of `0`**
An interesting aspect to `setTimeout()` is that we can pass it a delay of `0` milliseconds.
```
setTimeout(function sayHi() {
    console.log('Howdy');
}, 0);  // ← 0 milliseconds!
```

Since the timer ends immediately, the sayHi function will move to the Queue, and then to the Call Stack once the Call Stack has finished executing any currently-running tasks.

This technique can help us to convert potentially long-running code to one that's broken up to allow for the browser to handle user interactions!

## Break Up Long Running Code
Computing intensive code, such as a long loop / heavy reflow and repaint computations can block user interaction while the page is busy, e.g. clicking a form submit button. This is because JS runs synchronously (running to completion).

```
let count = 1

function generateParagraphs() {
    const fragment = document.createDocumentFragment();

    // Split into groups of 500
    for (let i = 1; i <= 500; i++) {
        const newElement = document.createElement('p');
        newElement.textContent = 'This is paragraph number ' + count;
        count = count + 1;

        fragment.appendChild(newElement);
    }

    document.body.appendChild(fragment);

    // Run the above loop 40 times
    if (count < 20000) {
        setTimeout(generateParagraphs, 0);
    }
}

generateParagraphs();
```

If you try running this code on a page, you can still interact with the page while the code is running. It doesn't lock up or freeze the page. And it doesn't lock up or freeze because of the `setTimeout()` calls.



