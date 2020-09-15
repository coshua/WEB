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

* Implicit Binding

Another rule matters when the call has a context object.
```javascript
function foo() {
 console.log( this.a );
}
var obj = {
 a: 2,
 foo: foo
};
obj.foo(); // 2
```
It is misguided that 'obj' contains or owns 'foo()' even if foo() is declared inside 'obj' (not this case). However, the call-site uses the obj context to reference the function, so you could understand the obj having foo() reference at the time it is called.

When there is a context object for a function reference, the implicit binding rules so that the context object should be used for the function call's 'this' binding.
Because obj is the 'this' for the foo() call, 'this.a' is a synonymous with 'obj.a

* Explicit Binding

Almost all of javascript functions have access to 'call()' and 'apply()' method. They are used to bind 'this' with the intended reference explicitly.
Both take an object to use for 'this' as first parameter, and then invoke the function with that 'this'.
```javascript
function foo() {
 console.log( this.a );
}
var obj = {
 a: 2
};
foo.call( obj ); // 2
```
We call it hard-binding because it does not loss its binding later regardless of the call-site.
The following shows its usage.
```javascript
function foo(something) {
  console.log(this.a, something);
  return this.a + something;
}

function bind(fn, obj) {
  return function(){
    fn.call(obj, arguments);
  };
}

var obj = {
  a: 2
};

var bar = bind(foo, obj);

var b = bar(3); //2, 3
console.log(b); //5
```
This kind of binding is such a common pattern, ES5 provides build-in utility, 'Function.prototype.bind'.
```javascript
//...same
var bar = foo.bind(obj);
//...same
```

* new Binding

First of all, JavaScript 'new' keywork is totally different from it of class-oriented concept.

In JavaScript, constructors are just functions with the 'new' operator in front of them. They are not attached to a class, nor are they instantiating a class.
We call this construction call.

In conclusion, these rules can be applied to the call-site, in this order of precedence:
1. Called with new? Use the newly constructed object.
2. Called with call or apply (or bind)? Use the specified object.
3. Called with a context object owning the call? Use that context
object.
4. Default: undefined in strict mode, global object otherwise.

#### Arrow Function this
ES6 arrow-functions use lexical scoping for 'this' binding, which means they inherit the 'this' binding from its enclosing function call.
Pre-ES6 can also manifest this functionality by leveraging 'this' reference like this: `var self = this;`
