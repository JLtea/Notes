# Promises

### Constructor syntax for promise object

```
let promise = new Promise(function(resolve, reject) {
  // executor (the producing code)
});
```

The executor should call one of these callbacks:

- `resolve(value)` if the job finished successfully, with result _value_
- `reject(error)` if error occurred, _error_ is the error object

The **promise** object returned by the `new Promise` constructor has these internal properties:

- `state` -- initially **pending**, then changes to **fulfilled** when resolved or rejected
- `result` -- initially **undefined**, then changes to **value** or **error**

\* Try to reject with `Error` objects

### Consuming functions

.then -- runs when promise is resolved, receives the result

```
promise
    .then(result => console.log(result))
```

.catch -- runs when promise is rejected, recieves error

```
promise
    .then(null)
    .catch(error => console.log(error))
```

.finally -- runs whether promise was resolved or not

```
new Promise((resolve, reject) => {
  /* do something that takes time, and then call resolve/reject */
})
  // runs when the promise is settled, doesn't matter successfully or not
  .finally(() => stop loading indicator)
  // so the loading indicator is always stopped before we process the result/error
  .then(result => show result, err => show error)
```

\* lines after the try{} catch{} will not run when throwing an error, whereas finally will.

### Async / Await

`async` before a function declares the function to always return a promise

`await` waits until the promise settles and returns the result, has to be in an async function

```
async function f() {
    let value = await promise;
}
```

try{} catch{} throw

```
async function f() {
  try {
    let response = await fetch('/no-user-here');
    let user = await response.json();
  } catch(err) {
    // catches errors both in fetch and response.json
    throw err;
  }
}
```

### Promise Chaining

If we throw inside .catch, then the control goes to the next closest error handler. And if we handle the error and finish normally, then it continues to the next closest successful .then handler.

```
new Promise((resolve, reject) => {

  throw new Error("Whoops!");

}).catch(function(error) {

  alert("The error is handled, continue normally");

}).then(() => alert("Next successful handler runs"));
```

### API

`Promise.all` when executing and waiting for many promises in parallel

```
let promise = Promise.all([...promises]);
```

Using `forEach` and `map`

`Promise.allSettled` waits for all promises to settle, whereas Promise.all will reject as a whole if any one promise rejects

Resulting Array:

- {status:"fulfilled", value:result} for successful responses,
- {status:"rejected", reason:error} for errors.

`Promise.race` waits for only first settled promise and gets result

`Promise.any` waits for only first fulfilled promise and gets result

### fetch

```
let call = fetch(URL,{
    // Default options are marked with *

    method: // GET, POST, PUT, DELETE
    mode: // no-cors, *cors, same-origin
    cache: // *default, no-cache, reload, force-cache, only-if-cached
    credentials: // include, *same-origin, omit
    headers: {
        'Content-Type': // application/json, application/x-www-form-urlencoded
    }
    redirect: // manual, *follow, error
    referrerPolicy: // no-referrer, *no-referrer-when-downgrade, origin, origin-when-cross-origin, same-origin, strict-origin, strict-origin-when-cross-origin, unsafe-url
    body: // JSON.stringify(data) -- data type must match "Content-Type" header
});

const getData = () => {
    call
        .then(response => response.json())
}

# async/await version
const getData = async () => {
    let response = await call
    const data = response.json()
}

```

### axios

```
import axios from 'axios'

let call = axios({
  method: // get, post, put, delete
  url: // URL
  data: {} // equivalent to 'body' in fetch
  params: {} // query params
});

const getData = () => {
    call
        .then(response => response.data)
}

# async/await version
const getData = async () => {
    let response = await call
    const data = response.data
}
```

Response Schema

- `data` is the response that was provided by the server
- `status` is the HTTP status code from the server response
- `statusText` is the HTTP status message from the server response
- `headers` the HTTP headers that the server responded with
  All header names are lower cased and can be accessed using the bracket notation.
  Example: `response.headers['content-type']`
- `config` is the config that was provided to `axios` for the request
- `request` is the request that generated this response
  It is the last ClientRequest instance in node.js (in redirects)
  and an XMLHttpRequest instance in the browser

Creating an Instance

```
const instance = axios.create({
  baseURL: 'https://some-domain.com/api/',
  timeout: 1000,
  headers: {'X-Custom-Header': 'foobar'}
});
```
