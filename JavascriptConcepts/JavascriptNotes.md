Everything in javascript happens inside an execution context

Javascript is weakly typed, synchronous single threaded language


==Execution Context==  has two components

|Memory | Code|
|----|---|
|key : value| - code execution
|a : 10| - code execution
|fn : {....}| - code execution





 Memory Component - Variable environment 

code component - thread of execution


What happens when you run Javascript Code ?


Everything in Javascript happens inside an execution context.



```js
var n = 2;
function square (num) {
    var ans = num * num;
    return ans;
}

var square2 = square(2)
var square4 = square(4)
```


When you run the code a execution context is created with memory component and code component. It is created in two phase 

1 Memory creation phase : Javascript will allocate memory to all the variable and functions

| Memory |
|---|
|n : undefined|
|square : {...}|
|square2 : undefined|
|square4 : undefined|


2. Code execution phase : 

Memory| Code execution |
|----|---|
|n : undefined|executing n = 2
|n : 2|
||new execution context created for invoking square function for 2 |


-     execution context for invoking square function for 2 
 
    |Memory| 
    |---|
    |num : undefined|
    |ans : undefined|

    |Code execution|
    |---|
    |executing square(n) where n = 2|

    |Memory| 
    |---|
    |num : 2|
    |ans : undefined|

    |Code execution|
    |---|
    |executing ans = num * num|

    |Memory| 
    |---|
    |num : 2|
    |ans : 4|

    |Code execution|
    |---|
    |return ans which finds ans from current memory <br> and return back to the execution context where it is invoked|

| Memory | Code |
|----| ---- |
|n : 2||
|square : {...}|
|square2 : 4 - entire execution context for function invocation will be deleted|
||new execution context created for invoking square function for 4|



-     execution context for invoking square function for 4
 
    |Memory| 
    |---|
    |num : undefined|
    |ans : undefined|

    |Code execution|
    |---|
    |executing square(n) where n = 4|

    |Memory| 
    |---|
    |num : 4|
    |ans : undefined|

    |Code execution|
    |---|
    |executing ans = num * num|

    |Memory| 
    |---|
    |num : 2|
    |ans : 16|

    |Code execution|
    |---|
    |return ans which finds ans from current memory <br> and return back to the execution context where it is invoked|

| Memory | Code |
|----| ---- |
|n : 2||
|square : {...}|
|square2 : 4 - entire execution context for function invocation will be deleted|
|square4 : 16 - entire execution context for function invocation will be deleted|


JS Engine handles everything to manage everything this creation and deletion of execution context through call stack

|Call stack|
|---|
|Execution Context for 2|
|Global Execution Context|



|Call stack|
|---|
|Execution Context for 4|
|Global Execution Context|


When execution context is created it will be pushed into the stack and when it is completed it will be deleted from the stack. After the whole program is executed the call stack becomes empty.


Call Stack maintains the order of execution of execution contexts


Call stack is also known by 

0. Call stack
1. Execution Context Stack
2. Program Stack
3. Control Stack
4. Runtime Stack
5. Machine stack




Hoisting in Javascript : Hoisting is JavaScript's default behavior of moving declarations to the top.

```js
var x = 7;

function getName(){
    console.log("Namaste Javascript");
}

getName();
console.log(x);

```

```
Namaste Javascript
7
```

```js
var x = 7;

getName();
console.log(x);

function getName(){
    console.log("Namaste Javascript");
}
```

```
Namaste Javascript
undefined
```

```js

getName();
console.log(x);

function getName(){
    console.log("Namaste Javascript");
}
```

```
Namaste Javascript
Uncaught ReferenceError: x is not defined at index.js:3
```


```js

console.log(getName);

function getName(){
    console.log("Namaste Javascript");
}
```

```
f getName(){
    console.log("Namaste Javascript");
}
```


```js

var getName1 = () => {
    console.log("Namaste Javascript")
}

var getName2 = function(){
    console.log("Namaste Javascript")
}


// getName will behave like a variable and will be initialized with undefined

```


**Functions in Javascript**

```js

var x = 1;

a();
b();

console.log(x)

function a (){
    var x = 10;
    console.log(x);
}

function b (){
    var x = 100;
    console.log(x)
}

```


```
10
100
1

```


|Memory| Code|
|-|-|
|x : undefined||
|a : {...} |
|b : {...} |
||x = 10;
|x: 10|
||new execution context created for invoking a ( )|

- Execution Context for a ( )

    |Memory|Code|
    |-|-|
    |x : undefined||
    ||x=10|
    |x : 10|
    ||console.log(x)|

|Memory| Code|
|-|-|
|x : undefined||
|a : {...} |
|b : {...} |
||x = 10;
|x: 10|
||new execution context create for invoking b ( ) |


- Execution Context for b ( )

    |Memory|Code|
    |-|-|
    |x : undefined||
    ||x=100|
    |x : 100|
    ||console.log(x)|

|Memory| Code|
|-|-|
|x : undefined||
|a : {...} |
|b : {...} |
||x = 1;
|x: 1|
||console.log(1)|

Global Execution Context deleted




**Shortest Javascript Program**


index.js 
```js


```


windown - is global object which is created with gec along with gec this is created.


this === window > true in global execution context 


so does that mean this and window is same ?

this and window are not the same thing. Depending on context, this can refer to any number of elements, while window always means window.


```js
var a = 10;

console.log(window.a);
console.log(a);
console.log(this.a);

```

**undefined and not defined**

> var a = undefined (fine but not a good practice)


**The scope chain, Scope and Lexical Environment**

Lexical Environment is created when EC is created
Lexical Environment = Local Memory + Lexical Environment of Parent

Whole chain of Lexical Environment is SCOPE CHAIN

![alt text](scope_chain.png)



```js
function a(){
    c();

    function c(){
        console.log(b)
    }
}


var b = 10;
a();

```

