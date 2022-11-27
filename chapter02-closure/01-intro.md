

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

Consider the following code example:
```js
function makeCounter() {
  let count = 0;
  function counter() {
    count++;
    return count;
  }
  return counter;
}

const counter = makeCounter();
console.log(counter()); // 1
console.log(counter()); // 2

```

Notice the inner function is returned from the outer function before being executed.

At first glance, it might seem unintuitive that this code still works. In some programming languages, the local variables within a function exist for just the duration of that function's execution. Once `makeCounter()` finishes executing, you might expect that the `count` variable would no longer be accessible. However, because the code still works as expected, this is obviously not the case in JavaScript.

The reason is that - functions in JavaScript form closures. 
A closure is the combination of a function and the lexical environment within which that function was declared. 
**This environment consists of any local variables that were in-scope at the time the closure was created.** 

The instance of `counter` maintains a reference to its lexical environment, within which the variable `count` exists.

<br>

Consider the following code example:

```js
function makePadZero(length) {
  function padZero(str) {
    return str.padEnd(length, '0');
  }
  return padZero;
}

const pad10Zero = makePadZero(10);
const pad8Zero = makePadZero(8);

console.log(pad10Zero('test')); // 'test000000'
console.log(pad8Zero('test'));  // 'test0000'

```

In the above example, the function factory `makePadZero` creates two new functions — one that pad 10 zeros its argument, and one that pad 8.
`pad10Zero` and `pad8Zero` are both closures. They share the same function body definition, but store different lexical environments. In `pad10Zero`'s lexical environment, `length` is 10, while in the lexical environment for `pad8Zero`, `length` is 8.


### Resource : 

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures

https://www.w3schools.com/js/js_function_closures.asp