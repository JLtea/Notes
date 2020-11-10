# Redux-saga Notes

Redux middleware, between **dispatching** and reaching the **reducer**
using ES6 Generators to make asynchronous

Tackles side effects of asynchronous code in a synchronous state management system.

### Generators

`Generators` are functions that can be exited and later re-entered, saving their context across re-entrances.

```
function* generator(i) {
    yield i;
    yield i + 10;
}

const gen = generator(10);
console.log(gen.next()) // {value: 10, done: false}
console.log(gen.next()) // {value: 20, done: false}

```

Denoted by an asterisk \* and returns a generator object, similar to an iterator.

### Watchers and Workers

The saga file is usually split into two types:

- **watchers** match actions dispatched to the redux store, and assign it to its worker saga
- **workers** run all the side effects it was meant to do

### Middleware Setup

component.js

```
import { createStore, applyMiddleware } from 'redux'
import createSagaMiddleware from 'redux-saga'
import reducer from './reducers'

import { exampleSaga } from './sagas'

const sagaMiddleware = createSagaMiddleware()
const store = createStore(
    reducer,
    applyMiddleware(sagaMiddleware)
)
sagaMiddleware.run(exampleSaga)

const action = type => stores.dispatch({type})

...

return (
    <Component>
        value = {store.getState()}
        onClick{() => action('CLICK_ACTION')}
        onAsync{() => action('CLICK_ASYNC')}
    </Component>
)
```

sagas.js

```
import { put, takeEvery } from 'redux-saga/effects'

//example async
const delay = (ms) => new Promise(res => setTimeout(res,ms))

export function* actionAsync() {
    yield delay(1000)
    yield put({ type: 'CLICK_ASYNC'})
}
export function* watch_actionAsync() {
    yield takeEvery('CLICK_ASYNC', actionAsync)
}
```

### Saga Helpers (Effects)

Saga Helpers API Reference: [https://redux-saga.js.org/docs/api/]
