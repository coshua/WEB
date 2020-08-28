## How store connects?
When I encountered Redux the first time, the flow is easily figured out because there were *subscribe* and *store.dispatch* parts.
Every actions were dispatched through the method from the store. `store.dispatch(action)`

However, I got lost trying to grasp an real example.
```javascript
export const setAlert = (msg, alertType) => {
  dispatch({
    type: alertType,
    payload: msg
  });
};
```
See? I import nothing from nowhere, then where did *dispatch* method come from? And I could not be sure it communicates with store.

Hint is that the concept of Redux is to manage state globally. 
It provides store to App.js or Index.js, and any child components of it could access it.
```javascript
import { Provider } from 'react-redux';
import store from './store';

const App = () => {
  <Provider store={store}>
    ...contents
  </Provider>
}
```
