


# Execution Context


Simply put, an execution context is an abstract concept of an environment where the Javascript code is evaluated and executed. 
When a fragment of JavaScript code runs, it runs inside an execution context. 
There are three types of code that create a new execution context:

* The **global context** is the execution context created to run the main body of your code; that is, any code that exists outside of a JavaScript function.
* Each function is run within its own execution context. This is frequently referred to as a "**local context**."
* <strike>Using the ill-advised eval() function also creates a new execution context.</strike>

<br>

____

<br>

Each context is, in essence, a level of scope within your code.  When a context is created, it is placed on the execution context stack. When it exits, the context is removed from the context stack.
Consider the JavaScript program below:

```js
function main() {
    let str = "hello";
    function foo() {
        console.log(str);
    }
    function baz() {
        str = str + " world"
    }

    function bar() {
        baz()
        foo();
    }
    bar();
}

main();
```

In this screenshot you can see each level in context of the running program : 

![image](https://user-images.githubusercontent.com/37986794/203842189-11dc0923-cbd0-4a2d-9fd9-cca379e736b4.png)

<u>Let's go over each step if the execution flow :</u>

TL;DR see [Illustration](#illustration-of-the-context-stack-)

* Upon starting the program, the global context is created.

* When `main` is reached, a context is created for the `main()` function;
it's pushed onto the execution context stack.

* When `bar` is reached, a context is created for the `bar()` function; 
it's pushed onto the execution context stack.

* When `baz` is reached, a context is created for the `baz()` function;
it's pushed onto the execution context stack.
When `baz` returns, the context for baz() is removed from the execution stack and destroyed. 
`baz` continues to execute where it left off.

* When `foo` is reached, a context is created for the `foo()` function; 
it's pushed onto the execution context stack.
   
* When `console.log` is reached, a context is created for the `console.log()` function;
it's pushed onto the execution context stack.
When `console.log` returns, the context for console.log() is removed from the execution stack and destroyed. 
`console.log` continues to execute where it left off.         

* When `foo` returns, the context for foo() is removed from the execution stack and destroyed. 
`foo` continues to execute where it left off.

<br>
<br>

#### Illustration of the context stack :

```
│               │     │               │     │               │     │   baz         │     │               │   
├───────────────┤     ├───────────────┤     ├───────────────┤     ├───────────────┤     ├───────────────┤   
│               │     │               │     │   bar         │     │   bar         │     │   bar         │   
├───────────────┤     ├───────────────┤     ├───────────────┤     ├───────────────┤     ├───────────────┤   
│               │     │   main        │     │   main        │     │   main        │     │   main        │   
├───────────────┤     ├───────────────┤     ├───────────────┤     ├───────────────┤     ├───────────────┤   
│   global      │     │   global      │     │   global      │     │   global      │     │   global      │   
└───────────────┘     └───────────────┘     └───────────────┘     └───────────────┘     └───────────────┘   


│   console.log │     │               │     │               │     │               │     │   console.log │    
├───────────────┤     ├───────────────┤     ├───────────────┤     ├───────────────┤     ├───────────────┤ 
│   bar         │     │   bar         │     │               │     │   foo         │     │   foo         │ 
├───────────────┤     ├───────────────┤     ├───────────────┤     ├───────────────┤     ├───────────────┤ 
│   main        │     │   main        │     │   main        │     │   main        │     │   main        │ 
├───────────────┤     ├───────────────┤     ├───────────────┤     ├───────────────┤     ├───────────────┤ 
│   global      │     │   global      │     │   global      │     │   global      │     │   global      │ 
└───────────────┘     └───────────────┘     └───────────────┘     └───────────────┘     └───────────────┘ 


│               │     │               │     │               │
├───────────────┤     ├───────────────┤     ├───────────────┤
│   foo         │     │               │     │               │
├───────────────┤     ├───────────────┤     ├───────────────┤
│   main        │     │   main        │     │               │
├───────────────┤     ├───────────────┤     ├───────────────┤
│   global      │     │   global      │     │   global      │
└───────────────┘     └───────────────┘     └───────────────┘

```


![image](https://user-images.githubusercontent.com/37986794/203842836-8fff1c44-5155-433f-9f4d-6ed57a97f486.png)
