

## Chapter02 - Closure - Section01

# Intro

<br>

## What are closure ?

Closure do not have a one clear definition, 

[In Mozilla docs wording](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures) -
> "A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment). In other words, a closure gives you access to an outer function's scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time."

[W3School phrase it](https://www.w3schools.com/js/js_function_closures.asp) - 
> "A closure is a function having access to the parent scope, even after the parent function has closed."

Closures are important because they control what is and isn’t in scope in a particular function, along with which variables are shared between sibling functions in the same containing scope.
Closures are frequently used in JavaScript for object data privacy, in event handlers and callback functions, and in partial applications, currying, and other functional programming patterns.


<br>
 
### Resource : 

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures

https://www.w3schools.com/js/js_function_closures.asp