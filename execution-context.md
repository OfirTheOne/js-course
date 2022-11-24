


# Execution Context


Simply put, an execution context is an abstract concept of an environment where the Javascript code is evaluated and executed. 
When a fragment of JavaScript code runs, it runs inside an execution context. 
There are three types of code that create a new execution context:

* The global context is the execution context created to run the main body of your code; that is, any code that exists outside of a JavaScript function.
* Each function is run within its own execution context. This is frequently referred to as a "local context."
* <strike>Using the ill-advised eval() function also creates a new execution context.</strike>


```js
function main() {

    let str = "hello";
    function foo() {
        console.log(str);
    }

    function bar() {
        foo();
    }
    bar();
}

main();
```

![image](https://user-images.githubusercontent.com/37986794/203842189-11dc0923-cbd0-4a2d-9fd9-cca379e736b4.png)
