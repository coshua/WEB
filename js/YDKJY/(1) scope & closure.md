## Hoisting

Consider the following codes.

```javascript
a = 2;
var a;
console.log(a);
```

A line of code like `var a = 2;` actually consists of two parts: **var a** and **a = 2**;. 
The declaration part is processed during the compilation phase, while the assignment part is left for the execution phase.
So javascript handles the snippet of codes like this:
```javascript
var a; //handled during compilation
a = 2; //handled during execution
console.log(a);
```

Then guess the result of the following code after execution.

```javascript
console.log(a);
var a = 2;
//It would print undefined.  
```

So one could understand it like declarations are moved to top of the code(or more exactly, scope). This gives rise to the name *hoisting*.    

In function, only declarations are hoisted, not expressions. See an example. Make sure it does not have any kind of ReferenceError.
```javascript
foo(); //TypeError
var foo = function bar(){
  //...
}
```

let&const
---
Hoisting is the way JavaScript deal with variables inside certain scope. Usually, declarations being taken as existing for the entire scope in which they occur.
This means following codes would work without error.

```javascript
console.log(foo);
var foo = 'Hi';
```       

However, declarations made with **let** keyward are not 'exist' in the block until the declaration statement.

```javascript    
console.log(foo);
let foo = 'Hi'; //ReferenceError
```

It is useful to know that **const** variables are affected under block scope.


Closure
---
Closure is when a function is able to remember and access its lexical scope even when it is executing outside its lexical scope. Loot at the following code.
```javascript
function foo() {
  var a = 2;
  function bar() {
    console.log(a);
  }
  return bar;
}
var baz = foo();
baz();
```

The function bar is invoked outside of its author-time lexical scope. Closure lets the function continue to access the lexical scope it was defined in at author time.
