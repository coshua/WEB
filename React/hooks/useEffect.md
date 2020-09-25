The Effect hook lets you perform side effects in function component.

What is side effect(or just effect)? 
There are two common kinds of side effects in React components: those that don’t require cleanup, and those that do. Let’s look at this distinction in more detail.

### Effects without Cleanup
When we run some additional code after React has updated the DOM, network requests or logging being common examples, we call them effects that don't require a cleanup bacause we call it and forget about it.

In class component, *render* method should not cause any side effect. We want our effects to perform after React has updated the DOM. 
That's why we deal with side effects in *componentDidMount* and *componentDidUpdate* method. Two methods are different in terms of the timing they being called.
Even if we want the same side effect after every update, we use both methods to fulfill our needs.

By using **useEffect*, you could tell React that your component needs to do something after render. 
Then it calls the function we pass into **useEffect** as the first parameter, effect, after render by default.
React guarantees the DOM has beed updated by the time it runs the effects.

```javascript
function example() {
  const [formData, setFormData] = useState('');
  
  useEffect(()=> {
    document.title = `Hi, ${formData}`;
  })
```

### Effects with Cleanup
Some effects do need cleanup. 

### Skipping Effects
You can tell React to skip applying an effect if certain values havn't changed between re-renders. To do so, pass an array as an optional second argument to useEffect.
