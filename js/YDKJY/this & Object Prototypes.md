### Common Mistunderstanding

This does not refer to the function itself or the lexical scope of it. Basically, scope is not accessible to JS code. Than's why we cannot use a **this** reference to look something up in a lexical scope.

Only named function can be used to refer to the function from inside itself.
```javascript
functino foo(){
  foo.count = 0;
}
```
On the other hand, an anonymous function(like the one passed into as parameters without name) has no way to refer to the function object itself.

**this** is a runtime binding. It is contextual based on the conditions of the function's invocation. When a function is invoked, an activation record(or execution context) is created.
This record contains information about where the function was called from (the call-stack), how the function was invoked, what parameters were passed, etc.
One of the properties of this record is the **this** reference, which will be used for the duration of that function's execution.

### this All Makes Sense Now

How learned how **this** binds is related with its call-site , which refers to the location where the function is called.
Try to understand what call-stack and call-site are.
```javascript
function baz() {
 // call-stack is: `baz`
 // so, our call-site is in the global scope
 console.log( "baz" );
 bar(); // <-- call-site for `bar`
}
function bar() {
 // call-stack is: `baz` -> `bar`
 // so, our call-site is in `baz`
 console.log( "bar" );
}
baz(); // <-- call-site for `baz`
```
There are four rules to determine what **this** references to
* Default Binding
```javascript
function foo() {
 console.log( this.a );
}
var a = 2;
foo(); // 2
```
The call-site of foo() is global, so **this** points at the global object. Note that variable a is a property of the global object.
If strict mode is in effect, the global object is not eligible for the default binding, so the this is instead set to undefined. However, the overall binding rules
are entirely based on the call-site, so the global object is only eligible
for the default binding if the contents of foo() are not running in strict mode. The strict mode state of the call-site of foo() is
irrelevant:
```javascript
function foo() {
 console.log( this.a );
}
var a = 2;
(function(){
 "use strict";
 foo(); // 2
})();
```

This is the default rule when no other rules are applied.
