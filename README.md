# js-code-snippet
JavaScript tricky code snippets

### Simple function recursion

```
function simpleRecursion(n) {  
  return n > 0 ? simpleRecursion(n-1) + 'e' : 'Yep';
}
console.log(simpleRecursion(3)); >>> output 'Yepeee'
```
### Context
> Context in function
```
function func() { 
  console.log(this); 
}
func(); 
output >>> Gloabl object 
```
> Context in method
```
var obj = {
  func: function() {
    console.log(this);  
  }
};
obj.func();
outpue >>> Object {func: function() {console.log(this)}}
```
> Modifying context - using ```call``` and ```apply``` method
* Example 1
```
var obj = {};
function func() {
  console.log(this);
}
func(); >>> output global object
func.call(obj); >>> output obj
func.apply(obj); >>> output obj
```
* Example 2
```
function func(a, b) { 
  return a + b;
}
console.log(func.call(null,5,6)); >>> output 11 - call takes individual arguments
console.log(func.apply(null,[10,20])); >>> output 30 - apply takes array of arguments
```

### Passing variable arguments
* Example 1
```
function greet() { console.log(arguments); }

greet('hello', 'world'); >>> [object Arguments] { 0: "hello", 1: "world"}
greet('hello', 'world', 'hi'); >>> [object Arguments] { 0: "hello", 1: "world", 2: "hi"}
```
* Example 2  - in ES6 using rest & spread operator
```
const greet = (...args) => console.log(...args);

greet('hello', 'world'); >>> 'hello' 'world'
greet('hello', 'world', 'hi'); >>> 'hello' 'world' 'hi'
```

### Piping - passing one function's output to another function's input
```
function add(a, b) {
  return a + b;
}

function inc(c) {
  return c + 11;
}
```
* Method - 1
```
var res = add(10,20);
var final = inc(res);
console.log(final);
```
* Method - 2
```
var final = inc(add(10,20));
console.log(final);
```
* Method - 3 - create a utility function pipe
```
function pipe(fn1, fn2) {
  return function(a,b) {
     return fn2(fn1(a,b));
  }
}

var final = pipe(add, inc);
console.log(final(1000,2000));
```
* Method - 4 - variable arguments in pipe function
```
function pipe() {
  var param = Array.prototype.slice.call(arguments, 0);
  return function(a,b) {
    return param[1](param[0](a,b));
  }
}

var result = pipe(add, inc);
console.log(result(10,20));
```
* Method - 5 
```
function add(a, b, c, d) {
  return a + b + c + d;
}

function multiply(m) {
  return m * 2;
}

function divide(d) {
  return d / 20;
}

function sub(s) {
  return s - 1;
}

function _pipe(fn1, fn2) {
  return function() {
     var param = Array.prototype.slice.call(arguments, 0);
     return fn2(fn1.apply(null, param));
  }
}

// ES6 version
const _pipe = (fn1, fn2) => (...args) => fn2(fn1(...args));

function pipe() {
  var fns = Array.prototype.slice.call(arguments, 0);
  return fns.reduce(_pipe);
}

// ES6 version
const pipe = (..fns) => fns.reduce(_pipe);

var result = pipe(add, multiply, divide, sub);
console.log(result);
console.log(result(10,20,30,40));
```
### Partial applications
```
function add(a) {
  return a + 1;
}

function add(a, b) {
  return a + b;
}


function add(a, b, c) {
  return a + b + c;
}


function partial(fn) {
  var param = Array.prototype.slice.call(arguments, 1);
  return function() {
      return fn.apply(null, param.concat(Array.prototype.slice.call(arguments,0)));
  }
}

// ES6
const partial = (fn, ...args) => fn.bind(null, ...args); 

var res = partial(add);
console.log(res(10, 30,40));

res = partial(add, 3);
console.log(res(10, 30));

res = partial(add, 1, 2);
console.log(res(10));
```
