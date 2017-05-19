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


