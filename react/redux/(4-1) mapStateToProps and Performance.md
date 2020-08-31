### Return values determine if component re-renders
React Redux internally implements **componentShouldUpdate** method such that the wrapper component re-renders when the data the component needs has changed.
It uses a shallow comparison to see whether the returning contents of the object is different. Thus, returning a mutated object of the same reference does not re-render the component.

 run when| (state) => stateProps | (state, ownProps) => stateProps
--- | --- | ---
mapStateToProps run when | store state changes | store state changes or any field of ownProps is different
components re-render when | any field of stateProps is different | any field of stateProps is different or any field of ownProps is different

The wrapper component subscribes the store. Every time an action is dispatched, it calls store.getState() and checks if lastState === currentState.
If the two state values are identical by reference, then it will not re-run matStateToProps function.

### Return new object references only if needed
It is a common mistake to return the same object reference when you update the state. But you have to cautious not to return a new object even the data is actully the same.
Following operators result in new object or array references being created:
* array.map() or array.filter()
* Merging with array.concat()
* Selecting portion with array.slice()
* Copying values with Object.assign()
* Copying values with spread operator {...oldState, newData}
