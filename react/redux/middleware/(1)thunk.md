## Middleware
Since reducers are supposed to be pure, it cannot change anything outside their scope. We cannot do any API calls or dispatch actions from inside a reducer. This is where the concept of middleware comes from. Middleware performs extra operations before the action reaches out to reducers. It hijacks all actions and decide whether to dispatch action or perform asynchronous requests before reducers notice something has happened. One useful example using middleware is when we request an API call, it dispatches a *loading* action and then *success* or *failure* action when the fetching is done. We apply middleware to our store with **applyMiddleware** when we create it.
`const store = createStore(reducers, applyMiddleware(anyMiddleware));`

## Thunk
Thunk is a kind of redux middleware. The term **thunk** refers to a delayed computation. 
With **thunk**, we can employee an action creator where a function, not an action object, returns.
If you well understood what middleware's role is, then it makes sense you could handle essential tasks and dispatch with their results inside that function. 
It can be used to delay the dispatch of an action, or to dispatch only if certain conditions are met. 
The inner function receives the store methods **dispatch** and **getState** as parameters. Thunk only cares functions, so if the action is not a function, it passes it reducer or next middleware if any.

This is what redux-thunk library code looks like. Though we could not fully understand how *createThunkMiddleware* or *next* works exactly, it helps you a lot.
```javascript
function createThunkMiddleware(extraArgument) {
  return ({ dispatch, getState }) => next => action => {
		// This gets called for every action you dispatch.
		// If it's a function, call it.
    if (typeof action === 'function') {
      return action(dispatch, getState, extraArgument);
    }

		// Otherwise, just continue processing this action as usual
    return next(action);
  };
}

const thunk = createThunkMiddleware();
thunk.withExtraArgument = createThunkMiddleware;

export default thunk;
```
After we apply thunk, every action we dispatch in our application will pass through this code.

The following is an example of asynchronous dispatching. It is basically a closure pattern, so understand closure first if is seems massive how chaining arrow function works(or how functions inside a function work).
```javascript
const INCREMENT_COUNTER = 'INCREMENT_COUNTER';

function increment(amount = 1) {
 return {
  type: INCREMENT_COUNTER,
  payload: amount
 };
}

function incrementAsync(amount, sec) {
  return (dispatch, getState) => {
    const { execute } = getState();
    if(!execute) { return; }
    
    setTimeout(() => {
      dispatch(increment(amount));
    }, sec);
  };
}
//Arrow function
const decrementAsync = (amount, sec) => dispatch => {
  setTimeout(() => {
   dispatch(incremet(-amount));
  }, sec);
};
```

When we discussed about middleware, I mentioned that middleware is useful when we need API call to update the state.
```javascript
const loginRequest = () => {
 return{
  type: 'REQUEST'
 };
};

const loginFail = err => {
 return{
  type: 'FAIL',
  payload: err
 };
};

const loginSuccess = response => {
 return{
  type: 'SUCCESS',
  payload: response
 };
};

const tryLogin = () => async(dispatch, getState) => {
 dispatch(loginRequest());
 try {
  const response = await someLoginLink.post(`api/login/${getState.id}`);
  dispatch(loginSuccess(response));
 } catch (err) {
  dispatch(loginFail(err);
 }
};
