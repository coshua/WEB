## Thunk
A **thunk** is a special kind of Redux function that can contain asynchronous logic. It allows you to write action creators that return a function instead of an action.
It can be used to delay the dispatch of an action, or to dispatch only if certain conditions are met. The inner function receives the store methods **dispatch** and **getState** as parameters.

```javascript
const INCREMENT_COUNTER = 'INCREMENT_COUNTER';

function increment() {
 return {
  type: INCREMENT_COUNTER
 };
}

function incrementAsync() {
  return (dispatch, getState) => {
    const { execute } = getState();
    if(!execute) { return; }
    
    setTimeout(() => {
      dispatch(increment());
    }, 1000);
  };
}
```
