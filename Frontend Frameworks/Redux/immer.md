# Immer Notes

"Immer (German for: always) is a tiny package that allows you to work with immutable state in a more convenient way. It is based on the copy-on-write mechanism."

Main Idea:

Apply all changes to a temporary **draftState**, a proxy of **currentState**, producing the **nextState** based on mutations in draft state. -- you can interact with your data by simply modifying it while keeping all the benefits of immutable data.

### Object Mutations

```
import produce from "immer"

const todosObj = {
    id1: {done: false, body: "Take out the trash"},
    id2: {done: false, body: "Check Email"}
}

// add
const addedTodosObj = produce(todosObj, draft => {
    draft["id3"] = {done: false, body: "Buy bananas"}
})

// delete
const deletedTodosObj = produce(todosObj, draft => {
    delete draft["id1"]
})

// update
const updatedTodosObj = produce(todosObj, draft => {
    draft["id1"].done = true
})
```

### Array Mutations

```
import produce from "immer"

const todosArray = [
    {id: "id1", done: false, body: "Take out the trash"},
    {id: "id2", done: false, body: "Check Email"}
]

// add
const addedTodosArray = produce(todosArray, draft => {
    draft.push({id: "id3", done: false, body: "Buy bananas"})
})

// delete by index
const deletedTodosArray = produce(todosArray, draft => {
    draft.splice(3 /*the index */, 1)
})

// update by index
const updatedTodosArray = produce(todosArray, draft => {
    draft[3].done = true
})

// insert at index
const updatedTodosArray = produce(todosArray, draft => {
    draft.splice(3, 0, {id: "id3", done: false, body: "Buy bananas"})
})

// remove last item
const updatedTodosArray = produce(todosArray, draft => {
    draft.pop()
})

// remove first item
const updatedTodosArray = produce(todosArray, draft => {
    draft.shift()
})

// add item at the beginning of the array
const addedTodosArray = produce(todosArray, draft => {
    draft.unshift({id: "id3", done: false, body: "Buy bananas"})
})

// delete by id
const deletedTodosArray = produce(todosArray, draft => {
    const index = draft.findIndex(todo => todo.id === "id1")
    if (index !== -1) draft.splice(index, 1)
})

// update by id
const updatedTodosArray = produce(todosArray, draft => {
    const index = draft.findIndex(todo => todo.id === "id1")
    if (index !== -1) draft[index].done = true
})

// filtering items
const updatedTodosArray = produce(todosArray, draft => {
    // creating a new state is simpler in this example
    // (note that we don't need produce in this case,
    // but as shown below, if the filter is not on the top
    // level produce is still pretty useful)
    return draft.filter(todo => todo.done)
})
```
