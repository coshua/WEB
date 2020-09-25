It is a common mistake to pass String to a child component's prop where number needed actually. If so, your component would render unexpectedly.

**PropTypes** is a way of making runtime assertions about what type of data a React component requires in order to render properly. 
It explicitly specifies what type the component needs. 

`import PropTypes from 'prop-types';`

PropTypes object provides a type validator to assure the type other components are trying to pass is matched with the required type.

```javascript
Component.PropTypes = {
  optionalArray: PropTypes.array,
  optionalBool: PropTypes.bool,
  optionalFunc: PropTypes.func,
  optionalNumber: PropTypes.number,
  optionalObject: PropTypes.object,
  optionalString: PropTypes.string,
  optionalSymbol: PropTypes.symbol,
  
  //Or you can specify any type be required, so it prints warning in console if not supplied
  requiredFunc: PropTypes.func.isRequired,
  requiredAnyType: PropTypes.any.isRequired
};
```
```javascript
//It can also specify the complicated object like these:
UserProfie.propTypes = {
  user: PropTypes.shape({
    id: PropTypes.number.isRequired,
    name: PropTypes.string.isRequired,
    preference: PropTypes.shape({
      theme: PropTypes.oneOf(["black", "white"]).isRequired,
      image: PropTypes.instanceOf(Image),
    }),
  }).isRequired,
  friends: PropTypes.arrayOf(
    PropTypes.shape({
      id: PropTypes.number.isRequired,
      name: PropTypes.string.isRequired,
    }).isRequired
  ),
}
```
