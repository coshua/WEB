## createSlice
It is a function from redux-toolkit, and it generates action creators and action types that correspond to the reducers and state.
It receives a single configuration object parameter, with the following options; name, initialState, reducers, extraReducers.

### name
Generated action type constants will use this as a prefix.

### initialState
The initial state value for this slice of state.

### Reducers
An object containing redux case reducer functions, equivalent to a single case statement in a switch.

Immutability
---
Immutability is one of the core concepts in managing states. When you update a certain state, it expects you to do it without chaning the original(previous) state.
**createSlice** uses a library called *immer* inside. It tracks all the changes you have made, and uses that list of changes to return a immutably updated value.
```javascript
function reducerWithImmer(state, action) {
  state.first.second[action.id].fourth = action.value //functioning as if you spread all the original data into a new object
}
```
Remember, you can only write this logic in Redux Toolkit's *createSlice* and *createReducer* because they use Immer inside.

### With Example
```javascript
export const counterSlice = createSlice({
  name: 'counter',
  initialState: {
    value: 0
  },
  reducers: {
    increment: state => {
      state.value += 1
    },
    decrement: state => {
      state.value -= 1
    },
    incrementByAmount: (state, action) => {
      state.value += action.payload
    }
  }
})
```
When the first of two reducers, we don't need to look at action to know how to update the state. It will be passed anyway, but we could build a logic for update using reducer without the parameter action. However, type 'incrementByAmount' needs a second parameter action to know how to update the state.
