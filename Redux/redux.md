# Redux Notes

### Global State Management

**state** source of truth | **view** description of UI based on current state | **actions** events that occur and update the state

Most useful when _multiple components that need to share and use the same state_

### Immutability

**mutable** = changeable / **immutable** = cannot be changed

## Key Terms

### Action

Typical Action Object:

```
const addTodoAction = {
    type: 'domain/eventName'
    payload: 'value'
}
```

Convention

- `type` field string with _domain_ - category that action belongs to, _eventName_ - event that happened
- `payload` additional information about event

### Reducer

Function receiving `state` and `action` object, and returns new state

Rules:

- New state calculated using only state and action arguments
- Make immutable updates using copied values
- No asynchronous logic

Example Reducer Function:

```
const initialState = { value: 0 }

function exampleReducer(state = initialState, action) {
    if (action.type === 'domain/eventName') {
        return {
            ...state,
            value: state.value // immutable update to state
            // state.value = 123 -- mutates original state (illegal)
        }
    }
    return state
}
```

### Store

Redux application object

Basic store setup:

```
import { configureStore } from '@reduxjs/toolkit'

const store = configureStore({ reducer: exampleReducer })

```

### Dispatch

Redux `store` method updating the state

Example use:

```
store.dispatch({ type: 'domain/eventName' })
```

### Selectors

Functions that extract state values from the Redux store

Example use:
```
const selectValue = state => state.value

const currentValue = selectValue(store.getState())
```

## Redux Slices

The root Redux state object is split into multiple `slices`

Folder Structure:
```
/src
|   index.js
|   App.js
|   /redux
|       store.js
|       /features
|           Slice.js
```

