## createStore
We could create Redux store by `const store = createStore(rootReducer);`.    
We then pass this **store** object to the **Provider** component like this `<Provider store={store}> <App/> </Provider>`.     
This ensures that any time we connect to Redux in our app via **connect**, the store is available. `export default connect(mapStateToProps)(Alert);`.   

## redux-thunk
Many apps extend their Redux store functionality by adding **middleware** or **store enhancers**. Middleware adds extra functionality to the Redux **dispatch** functions;
enhancers add extra functionality to the Redux store.
