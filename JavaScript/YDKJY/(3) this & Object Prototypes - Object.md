## Type
There are six primary types in JS: string, number, boolean, null, undefined, and object.
Function is a subtype of object. Arrays are also a form of objects.

There are several other object subtypes, usually referred to as built-in objects: String, Number, Boolean, Object, Function, Array, Data, RegExp, Error.

When we declare a value like following:
`var str = "Hi";`,
It is actually just a primitive. JavaScript automatically coerces a string primitive to a String object when necessary, so we almost never need to declare it as an object.

null and undefined have no object wrapper form, only their primitive values. By contrast, Data values can only be created with their constructed object form, as they have no literal form counterpart.
Objects, Arrays, Functions, and RegExp are all objects regardless of whether the literal or constructed form is used.
Error objects are rarely created explicitly in code, but usually created when exceptions are thrown.

## Contents
The contents of an object consist of values (any type) stored at specifically named locations, which we call properties.
The engine stores pointers (references) to where the values are stored.

To access the value at the location a in myObject, we need to use either the . operator or the [] operator like following.

`myobject.a; myobject['a'];`

The former is referred to as 'property access', whereas the latter is referred to as 'key access'. In reality, they both access the same location and pull out the same value, so the terms can be used interchangeably.
The latter is used when you want to reference a property of the name like "Super-Fun!", since it can take any UTF-8/Unicode-compatible strings as the name for the property.
Also, [] syntax uses a string's value to specity the location, so it can take string variables like `myObject[mystr];`.

In objects, property names are always strings.

## Property Versus Method
When an object has a junction property, we do not call it method. The function could be related to the object with 'this binding' at runtime, but fundamentally it is a misconception that the object possesses a function like in object-oriented programming.

Even when you declare a function expresstion as part of the object literal, you could declare a variable outside the object referring that function and use it exactly in the same manner.

`var foo = myObject.foo;`

## Arrays
Arrays in JS have no restriction on what type of values are stored. The values are stored in locations, usually called indices beginning from zero index.
Arrays are objects, you could add properties onto the array.

`myArray.foo = "hi";`

But the named property does not change the length of the array.

If you try to add a property to an array, but the property name looks like a number, it wil end up instead as a numeric index.

`myArray["3"] = "foo";`
`myArray.length; //4`

## Duplicating Objects
There are no clear standard in duplicating objects if JS.

ES6 has defined Object.assign() to return the target that has copied the source objects as its subsequent parameters via = assignment.

## Property Descriptors
With ES5, all properties are described in terms of a property descriptor, which tells the property is read-only or not, for example.
```javascript
var myObject = {
 a: 2
};
Object.getOwnPropertyDescriptor( myObject, "a" );
// {
// value: 2,
// writable: true,
// enumerable: true,
// configurable: true
// }
```
We can use Object.defineProperty() to add a new property, or modify an existing-one (if its configurable), with the desired characteristics.
```javascript
var myObject = {};
Object.defineProperty( myObject, "a", {
 value: 2,
 writable: true,
 configurable: true,
 enumerable: true
} );
myObject.a; // 2
```

### Writable
The ability for you to change the value of a property is controlled by *writable*.
```javascript
var myObject = {};
Object.defineProperty( myObject, "a", {
 value: 2,
 writable: false, // not writable!
 configurable: true,
 enumerable: true
} );
myObject.a = 3; // got TypeError in strict mode
myObject.a; // 2
```
### Configurable
As long as a property is currently *configurable*, we can modify its descriptor definition, using the defineProperty().
```javscript
Object.defineProperty( myObject, "a", {
 value: 4,
 writable: true,
 configurable: false, // not configurable!
 enumerable: true
} );
myObject.a; // 4
myObject.a = 5;
myObject.a; // 5
Object.defineProperty( myObject, "a", {
 value: 6,
 writable: true,
 configurable: true,
 enumerable: true
} ); // TypeError regardless of strict mode
```
Changing configurable to false is a one-way direction, it cannot be undone.
Another thing configurable: false prevents is the ability to use the delete operator to remove an existing property.

Delete is used to delete object properties. If an object property is the last remaining reference to some object/function, and you delete it, that removes the reference and that is now garbage-collected.
### Enumerable
This characteristic  controls whether a property will show up in certain object-property enumerations, such as the for...in loop.
You can manipulate this property if you want to hide a certain property from enumeration.

## Immutability

### Object constant
By combining writable and configurable false, you can create a constant property.
### Prevention extensions
You can use `Object.preventExtensions(myObject)` to prevent an object from having new properties.

## Get
When you reference myObject.a, the behavior behind it is slightly complex.
```javascript
var myObject = {
 a: 2
};
myObject.b; // undefined
```
If you reference a variable that cannot be resolved within the applicable lexical scope lookup, the result would be a ReferenceError, not undefined.
myObject.a or myObject.b code performs a get operation.

## Put
When invoking put operation, how it behaves differs by whether the property is already present on the object or not.
If the property exists, the put algorithm will check:
Is the property an accessor descriptor? If so, call the setter, if any. Is the property a data descriptor with writable of false? Otherwise, set the value to the existing property as normal.

//fix later

## Getters and Setters
The default Put and Get operations for objects completely control how value are set to existing or new properties, or retrieved from existing properties, respectively.

ES5 can override part of these default operations on a per-property level through the use of getters and setters. Getters are properties that actually call a hidden function to retrieve a value.
Setters are properties that call a hidden function to set a value.

When you define a property to have either a getter or a setter, its definition becomes and 'accessor descriptor' (as opposed to a data descriptor).
For accessor descriptor, the value and writable characteristics of the descriptor are moot and ignored, and instead JS considers the set and get characteristics of the property.

```javascript
var myObject = {
 // define a getter for `a`
 get a() {
 return 2;
 }
};
myObject.a = 3;
myObject.a; // 2
```

Since we only defined a getter for a, the set operation would be ignored.
Even if there was a valid setter, our hard-coded getter would return 2.

To make the scenario moer sensible, properties should also be defined with setters, which override the default Put operation (aka assignment), per property.
The common pattern suggests to declare both getter and setter always, preferably.
```javascript
var myObject = {
 // define a getter for `a`
 get a() {
 return this._a_;
 },
 // define a setter for `a`
 set a(val) {
 this._a_ = val * 2;
 }
};
myObject.a = 2;
myObject.a; // 4
```

## Existence
myObject.a results in undefined value if either the explicit undefined is stored or there is no 'a' property. How could we distinguish them?

We can check via *hasOwnProperty*, or *in* operator.
`("a" in myObject); myObject.hasOwnProperty("a");`

The in operator checks to see if the property is in the object, or if it exists at any higher level of the Prototype chain object traversal.
By contrast, hasOwnProperty checks to see if only myObject has the property or not.

hasOwnProperty is accessible for all normal objects via delegation to Object.prototype. But its possible to create an object that does not link to Object.prototype.
In this case, hasOwnProperty approach would fail.

In that scenario, a more robust way of checking is Object.prototype.hasOwnProperty.call(myObject, "a"), which borrows the base hasOwnProperty(...) and uses explicit binding to apply it against myObject.

## Enumeration
If you define a property that has an enumarable value of false, it exists and has an accesible value but it doesn't show up in a for...in loop.
It is because 'enumerable' means 'will be included if the object's properties are iterated through.'

It's good idea to use for...in loop only on objects, and traditional for loops for arrays.

*propertyIsEnumerable* tests whether the given property name exists directly on the object and is also enumarable: true.

Object.keys() returns an array of all enumerable properties, whereas Object.getOwnPropertyNames() returns an array of all properties.

There is no way to get a list of all properties that is equivalent to what the *in* operator test would consult (traversing all properties on the entire Prototype chain).

## Iteration
forEach() will iterate over all values in the array, and it ignores any callback return values. every() keeps going until the end or the callback returns a falsy value whereas some() keeps going until the end or the callback returns a truthy value. These helpers accept a function callback to apply to each element in the array.

These special return values inside every() and some() act like *break*, in that they stop the iteration early before it reaches the end.

It is important to know that the order of iteration over an object's properties is not guaranteed and may vary between different JS engines, whereas iteration over an array's indice is performed orderly.

For objects, you can iterate the object's properties with a for...in loop. With ES6, for.. of loop syntax iterates over arrays (and objects, if the object defines its own custom iterator).

The for..of loop asks for an iterator object of the thing to be iterated, and the loop than iterates over the successive return values from calling that iterator object's next() method, once for each loop iteration.

Arrays have built-in @@iterator.

The return value from an iterator's next() call is an object form {value: ..., done: ...}, where value is the current iteration value, and done impies whether the iteration is end.

Contrast to arrays, regular objects do not have a built-in @@iterator. You can declare your own iterator for any object.

```javascript
var myObject = {
 a: 2,
 b: 3
};

Object.defineProperty(myObject, Symbol.iterator, {
 enumarable: false,
 writable: false,
 configurable: true,
 value: function() {
  var o = this;
  var idx = 0;
  var ks = Object.keys(o);
  return {
   next: function() {
    return {
     value: o[ks[idx++]],
     done: (idx > ks.length)
    };
   }
  };
});

// iterate `myObject` manually
var it = myObject[Symbol.iterator]();
it.next(); // { value:2, done:false }
it.next(); // { value:3, done:false }
it.next(); // { value:undefined, done:true }
// iterate `myObject` with `for..of`
for (var v of myObject) {
 console.log( v );
}
// 2
// 3
```
Or you can define iterator using a computed property name, like following.

`var myObject = {a: 2, b: 3, [Symbol.iterator]: function() {...} };`


