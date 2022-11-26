


## Chapter01 - Execution Context - Section03

# Execution context structure

<br>

The structure of the execution context can be represented as an object with three properties:

```js
ExecutionContext = {
    thisBinding: this,
    lexicalEnvironment: { },
    variableEnvironment: { }
}
```

> Note : <br>
In the JS language functions are objects, they can be passed as parameter to other functions, can be returned as a return value (farther more it execution can be delayed asynchronously and remain in a single thread with the synchronous program), etc, as a result of that behavior, a function can be executed in a total different environment from where it was initially defined, and so, for a function to "have every thing it needed" to reference, to properly run - it holds a **backpack** - that is, its Execution Context.

<br>

## <u> This Binding </u>

A function's this keyword behaves a little differently in JavaScript compared to other languages. 

* In the global execution context - `this` holds a reference to the global object. In the browser, it’s a window object.

* In a function execution context - the value of `this` depends on how the function is called. 
If it’s called as a method of an object, the value of `this` is set to that object. Otherwise, the value of `this` is set to the global object or `undefined` ([in strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)).

    > When using an arrow function, `this` is not bound at all. It just inherits from the parent execution context (callee).

<br>

## <u> Lexical Environment </u>

The Lexical Environment consists of two entries:

* Environment Record — a structure that maps identifiers to their values within the scope of its associated Lexical Environment. Such records store values of identifiers declared with let or const keywords.
* Outer reference — holds a reference to the parent Lexical Environment. It means that the JavaScript engine can look for variables inside the outer environment if they are not found in the current Lexical Environment.

    > In the global execution context.

<br>


Consider the JavaScript program below: 

```js
let num = 10;
function pow2(n) {
    let result = n * n;
    return result;
}
pow2(num);

```

Global Execution context :

```js
{
    thisBinding: Window,
    lexicalEnvironment: { 
        environmentRecord: {
            // Global variables ...
            num: 10,
            pow2: function { ... }
        },
        outer: null
    },
    variableEnvironment: { ... }
}
```

`pow2` Execution context :

```js
{
    thisBinding: Window,
    lexicalEnvironment: { 
        environmentRecord: {
            arguments: { 0: 10, length: 1 },
            n: 10,
            result: 100,
        },
        outer: <ref. GlobalLexicalEnvironment>
    },
    variableEnvironment: { ... }
}
```

<br>


## <u> Variable Environment </u>

[ECMA-262 specification](https://262.ecma-international.org/10.0/#table-23) :

> Variable Environment identifies the Lexical Environment whose EnvironmentRecord holds bindings created by VariableStatements within this execution context.

Simply put it, Variable Environment stores identifier-value mappings **declared with the `var` keyword** within its execution context.

<br>
<br>

----

## How is this useful 

this subject may not be as practical as other, but most of the time when a pice of js code behave in an unexpected way - the underline reason would be, its execution context reference values you'll not expect, so understanding this subject to its core will save you a lot of time guessing.


<br>

### Resource : 

https://developer.mozilla.org/en-US/docs/Web/API/HTML_DOM_API/Microtask_guide/In_depth#javascript_execution_contexts