## Redux
Many are using redux with react, but it is essentially an independent library managing states. According to the Redux website, Redux is a **predictable state container for JS apps**.
Redux helps users manage global state. It is especially useful when we have multiple components that need to share and use the same state. The main idea of Redux is to extract the shared
state from the components and manage it in a centralized location. It enforces components to follow specific patterns to access and update the global state of an application, making it more predictable.

### Action
An action is a plain JS object that has a **type** field. 
You can think of an action as an event that describes something that happened in the application. 
You could include other information of what happened in a field **payload**(name is not fixed, but we use it conventionally).
```javascript
const add = text => {
  return {
    type: 'ADD',
    payload: {
      amount: 1,
      text: text
    }
  }
}
```
Above is a function called **action creator** that creates and returns an action object.

### Reducer
A reducer is a function that receives a current state and an action object, and decides how to update the state and returns the new state.
The new state is calculated based only on a current state and an action, and it does by copying existing state first to make immutable updates. 

It's name comes from Array.reduce() method in JS, so to understand it helps you to figure out clearly.

#### Array.reduce()
It takes a callback function to be called each time in the array. With this callback function, **reduce method** reduces the array down to one value.
The callback function takes two arguments; **previousResult** and **currentItem**. The former is an accumulator which becomes the return value for reducer, and the latter is the current item in the array.
**Reduce** needs a second argument **initialValue** to be used as previousResult in it's first iteration.

```javascript
const numbers = [1, 3, 5, 7];
const total = numbers.reduce((accumulator, currentItem) => accumulator += currentItem, 0);
```

### Again, Reducer
If you grasp clearly how reduce method works, you could think of **Reducer** as it takes a previous result(state) and the current item(action). 
In conclusion, **Reducer** reduces a set of actions into a single state throughout the lifetime of your application.

### Store
The Redux state lives in an object called **store**.
The store is created by passing in a reducer, and has a method called **getState** that returns the current state.
```javascript
import { createStore } from 'redux';
import rootReducer from './reducers';
const store = createStore(rootReducer);
```

## Dispatch
The only way to update the state is to call **store.dispatch()** and pass in an action object. **Dispatch** is a method of Redux store. `store.dispatch({type:'INCREMENT'})`

The Redux application flollows the structured steps.
* State describes the condition of the app at a specific point of time
* The UI is rendered based on the state
* When something happens, the state is updated (In this stage, **dispatch** is like an event handler and **reducer** is like an event listener)
* UI is re-rendered based on the updated state
