


## Chapter01 - Execution Context - Section03

# Execution context structure

<br>

// The execution context relation with the call stack determine the order of the program.

The structure of the execution context can be represented as an object with three properties:

```js
ExecutionContext = {
    thisBinding: this,
    lexicalEnvironment: { },
    variableEnvironment: { }
}
```

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

<br>


**Global Execution context :**

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
<br>


**`pow2` Execution context :**

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
## <u> Variable Environment </u>


<br>
<br>

----

<br>

### Resource : 

https://developer.mozilla.org/en-US/docs/Web/API/HTML_DOM_API/Microtask_guide/In_depth#javascript_execution_contexts