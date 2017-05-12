# js-code-snippet
JavaScript tricky code snippets

* Simple function recursion

```
function simpleRecursion(n) {  
  return n > 0 ? simpleRecursion(n-1) + 'e' : 'Yep';
}
console.log(simpleRecursion(3)); >>> output 'Yepeee'
```
> In ES6
```
const simpleRecursion = n => n > 0 ? simpleRecursion(n-1) + 'e' : 'Yep';
console.log(simpleRecursion(10)); >>> output 'Yepeee'
```
