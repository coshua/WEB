## useSelector()
We learned that the wrapping the top-level component with **provider** enables its child components to access its store throughout the application.

**useSelector** is the other way to use the store.

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
