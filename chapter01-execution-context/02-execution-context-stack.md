


## Chapter01 - Execution Context - Section02

# Execution context stack

<br>

Each context is, in essence, a level of scope within your code. When a context is created, it is placed on the execution context stack (or "call stack"). When it exits, the context is removed from the context stack.
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

<img src="https://user-images.githubusercontent.com/37986794/203842189-11dc0923-cbd0-4a2d-9fd9-cca379e736b4.png" width="700px" />

<u>Let's go over each step if the execution flow :</u>

TL;DR see [Illustration](#illustration-of-the-context-stack-)

* Upon starting the program, the global context is created.

* When `main` is reached, a context is created for the `main()` function;
it's pushed onto the execution context stack.

* When `bar` is reached, a context is created for the `bar()` function; 
it's pushed onto the execution context stack.

* When `baz` is reached, a context is created for the `baz()` function;
it's pushed onto the execution context stack.

* When `baz` returns, the context for baz() is removed from the execution stack and destroyed. 
`baz` continues to execute where it left off.

* When `foo` is reached, a context is created for the `foo()` function; 
it's pushed onto the execution context stack.
   
* When `console.log` is reached, a context is created for the `console.log()` function;
it's pushed onto the execution context stack.

* When `console.log` returns, the context for console.log() is removed from the execution stack and destroyed. 
`console.log` continues to execute where it left off.         

* When `foo` returns, the context for foo() is removed from the execution stack and destroyed. 
`foo` continues to execute where it left off.

* When `main` returns, the context for main() is removed from the execution stack and destroyed. 
`main` continues to execute where it left off.

<br>
<br>

#### Illustration of the context stack :

```
push main ⤵            push bar ⤵            push baz ⤵            pop baz ⤴              push console.log ⤵

│               │      │               │      │               │      │   baz         │      │               │   
├───────────────┤      ├───────────────┤      ├───────────────┤      ├───────────────┤      ├───────────────┤   
│               │      │               │      │   bar         │      │   bar         │      │   bar         │   
├───────────────┤      ├───────────────┤      ├───────────────┤      ├───────────────┤      ├───────────────┤   
│               │      │   main        │      │   main        │      │   main        │      │   main        │   
├───────────────┤      ├───────────────┤      ├───────────────┤      ├───────────────┤      ├───────────────┤   
│   global      │      │   global      │      │   global      │      │   global      │      │   global      │   
└───────────────┘      └───────────────┘      └───────────────┘      └───────────────┘      └───────────────┘   


pop console.log ⤴      pop bar ⤴             push foo ⤵            push console.log ⤵    pop console.log ⤴

│   console.log │      │               │      │               │      │               │      │   console.log │    
├───────────────┤      ├───────────────┤      ├───────────────┤      ├───────────────┤      ├───────────────┤ 
│   bar         │      │   bar         │      │               │      │   foo         │      │   foo         │ 
├───────────────┤      ├───────────────┤      ├───────────────┤      ├───────────────┤      ├───────────────┤ 
│   main        │      │   main        │      │   main        │      │   main        │      │   main        │ 
├───────────────┤      ├───────────────┤      ├───────────────┤      ├───────────────┤      ├───────────────┤ 
│   global      │      │   global      │      │   global      │      │   global      │      │   global      │ 
└───────────────┘      └───────────────┘      └───────────────┘      └───────────────┘      └───────────────┘ 


pop foo ⤴              pop main ⤴            done

│               │      │               │      │               │
├───────────────┤      ├───────────────┤      ├───────────────┤
│   foo         │      │               │      │               │
├───────────────┤      ├───────────────┤      ├───────────────┤
│   main        │      │   main        │      │               │
├───────────────┤      ├───────────────┤      ├───────────────┤
│   global      │      │   global      │      │   global      │
└───────────────┘      └───────────────┘      └───────────────┘

```

<img src="https://user-images.githubusercontent.com/37986794/203842836-8fff1c44-5155-433f-9f4d-6ed57a97f486.png" width="700px" />






<br>
<br>

----

<br>

### Resource : 

https://developer.mozilla.org/en-US/docs/Web/API/HTML_DOM_API/Microtask_guide/In_depth#javascript_execution_contexts