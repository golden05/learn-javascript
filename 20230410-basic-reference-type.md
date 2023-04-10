---
title: reference type
tags: ["javascript"]
---

# the Date type

`let now = new Date();`

## inherited methods

toLocaleString() toString() only for debugging purposes, not for display purposes
valueOf()

## Date-Formatting Methods

toDateString() toTimeString() toLocaleDateString() toLocaleTimeString()
toUTCString()

## Date/Time Component Methods

getTime() setTime() getFullYear() getUTCFullYear() setFullYear() setUTCFullYear
getMonth() getUTCMonth() setMonth() setUTCMonth() getDate() getUTCDate()
setDate() setUTCDate() getDay() getUTCDay()...

# The RegExp type

/pattern/flags
character classes, quantifiers, grouping, lookaheads backreferences

- g global mode
- i case-insensitive mode
- m multiline mode
- y sticky mode
- u unicode mode

## RegExp instance properties

- global a boolean value
- ignoreCase a boolean value
- unicode a boolean value
- lastIndex an integer indiction position
- multiline a boolean value
- source string source
- flags

## RegExp instance Methods

- exec() return array , contained two properties : index and input
- test() accept a string argument and return a boolean value

## RegExp constructor properties

- input \$\_
- lastMatch \$&
- lastParen \$+
- leftContext \$`
- rightContext \$'

## pattern limitations

# primitive wrapper types

three special types : Boolean, Number, String

```
let s1 = "some text";
let s2 = s1.substring(2);
```

readonly access s1 , three step back :

1. create new String object
2. call the special method on the instance
3. desteroy the instance

reference class vs primitive wrapper instance has difference:

1. instantiate a reference type by new , destroy when goes out of scope
2. primitive wrapper object exist for only one line of code

```
let s1 = "some text"; //primitive wrapper object
s1.color = "red";  //
console.log(s1.color);  // undefined
```

typeof an instance of primitive wrapper is **object**
`Object` constructor act as a factory method return an instance of primitive wrapper

```
let obj =new Object("some text");
console.log(obj instanceOf String); // true
```

new primitive wrapper's constructor function is object
casting function of the same name is number string boolean

# singleton built-in objects

is already instantiated. such as Object, Array and String.
two singleton built-in objects: Global and Math

## Global Object

don't have an owning object.

### URI-encoding method

## Math Object
