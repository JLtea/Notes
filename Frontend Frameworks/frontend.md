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
