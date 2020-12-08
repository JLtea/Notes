# Frontend Concepts

### Virtual DOM

The virtual DOM (VDOM) is a programming concept where an ideal, or “virtual”, representation of a UI is kept in memory.
Then, it is synced with the “real” DOM by a library such as ReactDOM. This process is called reconciliation.

- React uses the virtual DOM and renders elements only when the user will have them into his/her HTML DOM.

### AJAX Asynchronous JavaScript And XML

AJAX:

- is not a programming language.
- uses a combination of a browser built-in XMLHttpRequest object (to request data from a web server), and JavaScript and HTML DOM (to display or use the data)
- allows web pages to be updated asynchronously by exchanging data with a web server behind the scenes AKA you can update parts of a web page, without reloading the whole page.

How it works:

1. An event occurs in a web page (the page is loaded, a button is clicked)
2. An XMLHttpRequest object is created by JavaScript
3. The XMLHttpRequest object sends a request to a web server
4. The server processes the request
5. The server sends a response back to the web page
6. The response is read by JavaScript
7. Proper action (like page update) is performed by JavaScript

### Debounce and Throttle

**Debounce** technique groups multiple sequential calls

Examples:

- Resizing a (desktop) browser window - emit many resize events while dragging the resize handle => trailing for the final value, after the user stops resizing the browser
- keypress on autocomplete form with Ajax request - instead send Ajax requests to the server every 50ms at every keystroke, only send the request when the user stops typing

**Throttle** don't allow function to execute more than once every X ms; different from Debounce in that it guarantees execution of function regularly, at least every X ms.

Example:

- Infinite Scrolling - when user is scrolling, if user is near the bottom, should request via Ajax more content

### DOM Events

- `event.target` – the deepest element that originated the event.
- `event.currentTarget` (=this) – the current element that handles the event (the one that has the handler on it)

The standard DOM Events describes 3 phases of event propagation:

1. Capturing phase – the event goes down to the element.
2. Target phase – the event reached the target element.
3. Bubbling phase – the event bubbles up from the element.

**Bubbling** goes from target element straight upwards until <html> and then document object, and then sometimes event window.

Usually we want to use handlers to decide that the event has been fully processed, and stop the bubbling.

Methods:

- `event.stopPropagation()`: stops the move upwards, but on the current element all other handlers will run.
- `event.stopImmediatePropagation()`: stop the bubbling and prevent handlers on the current element from running, no other handlers execute.

Instance where bubbling can create hidden pitfalls:

1. We create a nested menu. Each submenu handles clicks on its elements and calls stopPropagation so that the outer menu won’t trigger.
2. Later we decide to catch clicks on the whole window, to track users’ behavior (where people click). Some analytic systems do that. Usually the code uses document.addEventListener('click'…) to catch all clicks.
3. Our analytic won’t work over the area where clicks are stopped by stopPropagation. Sadly, we’ve got a “dead zone”.

**Capturing** goes downwards from <html> to target element

Two possible values of capture:

- `false(default)` the handler is set on bubbling phase
- `true` handler is set on capturing phase
