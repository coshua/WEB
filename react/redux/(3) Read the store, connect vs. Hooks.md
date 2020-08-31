# Access to store
Since Redux uses a single container for the entire states, we need to access and use it when we build a React component which requires some of the state to render its content.

There are two ways to access store and place it into our React component, **connect()** and using **useSelector()** and **useDispatch()**.
## connect()
The **connect()** function connects a React component to a Redux store.
So we import it from 'react-redux' package.

It returns a new, connected component class that wraps the component you passed in. 
The wrapping component has the data it needs from the store, and the function it can use to dispatch actions to the store.


`function connect(mapStateToProps?, mapDispatchToProps?, mergeProps?, options?)`

The first two parameters are functions dealing with your state and dispatch, respectively. State and dispatch will be supplied to your each function as the first argument.

Let's look at each parameter more deeply.
1. mapStateToProps
2. mapDispatchToProps
3. mergeProps
4. options
### mapStateToProps?: (state, ownProps?) => Object
If the first agrument is specified, the connected component will subscribe to Redux store updates. Whenever the store is updated, this function will be called.
It must return a plain object, which will be merged into the wrapped component's props. If you do not want subscription, pass *null* or *undefined* in place of mapStateToProps.

It takes a maximum of two parameters. 
#### state: Object
If mapStateToProps is declared as taking one parameter, it will be called whenever the store state changes, and given the state as the only parameter.
In this case, state is value returned by a call to **store.getState()**.
`const mapStateToProps = state => ({ name : state.name });`

#### ownProps?: Object
If mapStateToProps is declared as taking two parameters, it will be called whenever the store state changes *or* the wrapper componet receives a new prop.
With the store state as the first parameter, the wrapper component's props is given as the second parameter.
```javascript
const mapStateToProps = (state, ownProps) => ({
  const { posts } = state;
  const { id } = ownProps;
  const post = getPostById(state, id);
  
  return {post, posts};
});

<Post id={1} />
//The rendered Post component now receives props.id, props.post, and props.posts
```

#### Return
The returned object, referred to as **stateProps**, will be merged as props to your connected component. 
Each field in the object will become a prop for your component. The values in the fields will be used to determine if the component needs to re-render.

If you define **mergeProps**, the object will be passed into its first parameter.

### mapDispatchToProps?: Object | (dispatch, ownProps?) => Object
The second parameter to connect() can either be an object, a function or not supplied.
It is used for dispatching actions to the store.

React components cannot access the store directly, *connect()** does it for you. Like we can access to the store with store.getState(), connect() also provides
store.dispatch() to trigger a change in the store.

By default, a connected component receives **props.dispatch()** and can dispatch actions. This means you can dispatch in the component if it is connected to the store even
when the second argument of the connect function is not supplied or null.

**connect** can accept an argument **mapDispatchToProps**, which lets you create functions that dispatch when called, and pass them as props to your component.

If you can dispatch actions without **mapDispatchToProps**, what are benifits in using it?
* More declarative
Rather than
```<button onClick={() => dispatch({ type: 'SOMETHING' })}/>```,

```<button onClick={doSomething}/>``` seems more easy to follow what the behavior is.

* Allow dispatching to child (unconnected) components
If you pass down the function prop that is able to dispatch to other child components, they could dispatch an action and thus access to the store, which is impossible otherwise.

Once you have wrapped all our actions creators with functions that dispatch actions, the component is free of the need of dispatch. Therefore, if you define your own
**mapDispatchToProps**, the component will no longer receive dispatch. If you need dispatch function, you can manually inject it (Most of the time you don't need it).
const mapDispatchToProps = dispatch => {
  return(
    dispatch,
    // ...
  );
};

Let's look at the case where mapDispatchToProps is defined as a function.
### mapDispatchToProps as a function
It takes a maximum of two parameters.
#### dispatch: function
*store.dispatch()* comes with the first parameter of it.
```javascript
const mapDispatchToProps = dispatch => {
  return(
    // dispatching plain actions
    increment: () => dispatch({ type: 'INCREMENT' }),
    decrementByAmount: () => dispatch({ type: 'DECREMENT', payload: currentAmount })
    //or with action creators
    onClickSaveButton: e => dispatch(save(e))
  );
};
```
#### ownProps?: Object
The connected component's props pass to the second parameter. It will be re-invoked whenever the component receives a new prop.

#### Return
It returns a plain object, where each field in the object will become a separate prop for your component. Usually, every value of fields should be a function.
And if you use action creators, it is convention to name the field key the same name as the action creator.

If you define **mergeProps**, the object will be passed into its first parameter.

This is an example providing functions that able to dispatch an action with action creators as props to Counter component.
```javascript
const Counter = ({ increment, decrementByAmount, amount }) => {
  return(
    <>
      <button onClick={increment}>+</button>
      <button onClick={decrementByAmount}>-</button>
    </>
  );
}

const increment = () => ({type: 'INCREMENT'});
const decrementByAmount = (amount) => ({
  type: 'DECREMENT_BY_AMOUNT',
  payload: amount
});

const mapDispatchToProps = (dispatch, ownProps) => {
  return {
    increment: () => dispatch(increment()),
    decrementByAmount: () => dispatch(decrementByAmount(ownProps.amount))
  };
};

export default connect(null, mapDispatchToProps)(Counter);
```


#### bindActionCreators
**bindActionCreators** turns an object whose values are action creators, into an object with the same keys, 
but with every action creator wrapped into a dispatch call so they may be invoked directly.

It accepts two parameters:
1. An action creator function or an object whose field is action creator
2. dispatch

```javascript
import { bindActionCreators } from 'redux'; //Note that it is not only for react-redux
const mapDispatchToProps = dispatch => {
  return bindActionCreators({ increment, decrementByAmount }, dispatch);
  // returns
  // {
  //   increment: (...args) => dispatch(increment(...args)),
  //   decrement: (...args) => dispatch(decrement(...args)),
  //   reset: (...args) => dispatch(reset(...args)),
  // }
}

export default connect(null, mapDispatchToProps)(Counter);
```
### mapDispatchToProps as an object
Dispatching Redux actions in a React component follows a similar design pattern: define an action creator, wrap it in another function that looks like
(..args) => dispatch(actionCreator(...args)), and pass this function as a prop to the component.
Because this is so common, we could do this with an 'object shorthand' form. 

If you pass on object full of action creators in the place of *mapDispatchToProps* instead of a function, 
**connect** will automatically call **bindActionCreators** for you internally.

Offical redux docs suggests to use this way rather than to define mapDispatchToProps as a custumized function.

```javascript
import { increment, decrementByAmount } from './actions';

const actionsCreators = {
  increment,
  decrementByAmount
};

export default connect(null, actionCreators)(Counter);
//or
export default connect(null, {increment, decrementByAmount})(Counter);
```

## useSelector()
We learned that the wrapping the top-level component with **provider** enables its child components to access its store throughout the application.

**useSelector** is one of the ways to use the store.

It allows you to extract data from the store, using a selector function.
Selector functions receive the whole **state** object in the store and return a value.
useSelector() subscribes to the Redux store, and run your selector whenever action is dispatched.

In other words, they re-ren whenever the store is updated. So components would re-render if values from selectors has been updated.

Selectors will be called with the entire store state as its only argument.
`const selectedData = useSelector(state => state.somevalue);`
But before we dig into the examples using selector, let's see how it works.

### Equality comparisons
When the function component renders, the provided selector function will be called and its result will be returned from the useSelector hook. 
However, when an action is dispatched to the store, useSelector() forces a re-render only if the selector result appears to be different than the last result.

The default comparison is a strict === reference comparison. 

You can think of selector as *mapStateToProps* argumnet to *connect*.ap
