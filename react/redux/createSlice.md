## createSlice
It is a function from redux-toolkit, and it generates action creators and action types that correspond to the reducers and state.
It receives a single configuration object parameter, with the following options; name, initialState, reducers, extraReducers.

### name
Generated action type constants will use this as a prefix.

### initialState
The initial state value for this slice of state.

### Reducers
An object containing redux case reducer functions, equivalent to a single case statement in a switch.
