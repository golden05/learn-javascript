---
title: variable scope memory
tags: ["javascript"]
---

# primitive and reference value

six primitive types: Undefined, Null, Boolean, Number, String, Symbol
access by value

## dynamic properties

between new and not new different

## copying values

primitive: value copying
reference: address copying

## argument pass

function pass argument
primitive: value copying
reference: address copying

## determine type

operator `typeof`: best way to determine if a variable is a primitive type
operator `instanceof`: return true if the variable is an instance of the given reference type

# execution context and scope

every context has an associated --variable object--
browser global context is window:

- all global variables and functions defined with var
- let and const at the top level are not in global context , but can resolved identically

- context stack
- when execution flow into a function, function context push context stack
- when code is executed in a context, a scope chain of variable objects is created.
- if the context is a function, activation object is used as variable object: start has `arguments`

## scope chain argumentation

only two primary types of execution context:

- global and function ,
- the third is eval()
- other ways is argument the scope chain: add a variable object
  - catch block in `try-catch` statement
  - `with` statement

## variable declaration

ES6 has let const

### function scope declaration using var

var in the function scope:

- function's local context
- in a `with` statement is function context
- is initialized without declaration add to **global context**

### let Block scope declaration

scoped at the block level, nearest set of enclosing curly brace {}
means: if, while, function
`let` cannot be declare twice inside the same block scope throw a SyntaxError.

### const declaration

using const must be initialized to some value, rule like let
but different to Contant

### identifier lookup

identifier lookup maybe switch scope from top level to global level.
scope chain

# Garbage Collection

the garbage collection must keep track of which variables can and cannot be used.

## mark sweep

1. when garbage collection runs, it marks all variables store in memory.
2. the variables marked after that are considered ready for deletion
3. the garbage collection do a memory sweep.

## performance

garbage collector run can noticeably degrade the speed. the best strategy is to organize your code in
such a way that garbage collector to do its job quickly.

## managing memory

the amount of memory available for use in browser is much less than desktop app.
the best way to optimize memory usage is: when data is no longer necessary, it's best set it to null

### performance boost with const and let

const and let good for garbage collection. because they based for block scope.

### hidden classes and delet operation

V8 javascript engine associate hidden class for every object to keep track their properties.
class only just one. but associate their objects have many. example :

```
function Article(){
    this.title = 'Inaugration Ceremany';
}
let a1 = new Article();
let a2 = new Article();
```

under the V8 these two object chare same class. they have butter performance. if:

```
a2.author = 'Joke'; // add properties
```

because a2 add another propertie, so the two object donot share same Class.
so to resolve this problem . to initiaizie all properties in the constructor function.

#### delete operation

```
function Article(){
    this.title = 'Inaugration Ceremany';
    this.author = 'Jake';
  }
let a1 = new Article();
let a2 = new Article();
delete a2.author;
```

after `delete` operation . the two objects donot share same class.  
the best operation is set property to null.

### memory leaks

- global variable
- interval times
- closure

### static allocation and object pool

to minimizing the number of garbage collection operations in the browser.
if lots of object are being instantiated and then going out of scope, the browser will gabrage collection
more aggressively.
instead of the dynamic object creation, changed the method to use an existing object.
use object pool that manage a collection of recyclable objects. like this:

```
let vectorPool = new Array(100);
let vector = new Vector();
vectorPool.push(vector);
let v1 = vectorPool.allocate();
let v2 = vectorPool.allocate();
let v3 = vectorPool.allocate();
addVector(v1,v2,v3);
vectorPool.free(v1);
vectorPool.free(v2);
vectorPool.free(v3);
v1 = null;
v2 = null;
v3 = null;
```
