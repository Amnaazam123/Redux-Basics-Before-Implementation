# Redux Key Points
# Immutability
"Mutable" means "changeable". If something is "immutable", it can never be changed.
JavaScript objects and arrays are all mutable by default.
### In order to update values immutably, your code must make copies of existing objects/arrays, and then modify the copies.(SPREAD OPERATOR)

# Spread operator:
It is used to copy the object
```
const obj = {
  a: {
    c: 3
  },
  b: 2
}

const obj2 = {
  //---------- copy obj
  ...obj,
 
  //---------- overwrite a
  a: {
    // -----copy obj.a
    ...obj.a,
    // -----overwrite c
    c: 42
  }
  
  //-------------- add d
  d : 10
}

//obj2 = {a:{c:42},b:2,d:10}

```
A critical rule of immutable updates is that you must make a copy of every level of nesting that needs to be updated.
Redux expects that all state updates are done immutably.
Actions are object with type(string contant) and payload.
Reducers must make immutable updates.
### Reducers must not do any side effects??
### The store is created by passing in a reducer, and has a method called getState that returns the current state value.
### State is Read-Only. The only way to change the state is to dispatch an action


# SUMMARY
Redux's intent can be summarized in three principles
Global app state is kept in a single store
The store state is read-only to the rest of the app
Reducer functions are used to update the state in response to actions
Redux uses a "one-way data flow" app structure?
State describes the condition of the app at a point in time, and UI renders based on that state
When something happens in the app:
The UI dispatches an action
The store runs the reducers, and the state is updated based on what occurred
The store notifies the UI that the state has changed
The UI re-renders based on the new state(sara UI? ya koi particular component?)

it's okay to have other state values outside of Redux!
actions should contain the smallest amount of information needed to describe what happened.


A Redux app really only has one reducer function: the "root reducer" function that you will pass to createStore later on.


# Pure functions vs side effects:
A "side effect" is any change to state or behavior that can be seen outside of returning a value from a function. 
Pure function returns result only on the basis of input values. It does not depend upon any third party dependency. There is no state change and nothing external is changed. Calling this function with same data produces same result always.
Console.log is side effect. It is changing the state of our application. It is changing what is rendered on screen.

# Spliting reducers:
one reducer can change only that state with which it is initialized.
When you want to split your data handling logic, you'll use reducer composition and create multiple reducers that can be combined together, instead of creating separate stores.

### store:
createStore can also accept second argument. You could use this to add initial data when the store is created.(initialState)
```
let preloadedState
const persistedTodosString = localStorage.getItem('todos')

if (persistedTodosString) {
  preloadedState = {
    todos: JSON.parse(persistedTodosString)
  }
}

const store = createStore(rootReducer, preloadedState)
```
Remember, every time we call store.dispatch(action):

The store calls rootReducer(state, action)
- That root reducer may call other slice reducers inside of itself, like todosReducer(state.todos, action)

The store saves the new state value inside
The store calls all the listener subscription callbacks
If a listener has access to the store, it can now call store.getState() to read the latest state value





















