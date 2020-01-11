# What happens when javascript executes (runs) my code?

```javascript
const num = 3; 
function multiplyBy2 (inputNumber){ 
    const result = inputNumber*2; 
    return result; } 
const name = "Will" 
```

As soon as we start running our code, we create a global execution context 

- Thread of execution (parsing and executing the code line after line) 
- Live memory of variables with data (known as a Global Variable Environment)

# Running/calling/invoking a function

This is not the same as defining a function

```javascript
const num = 3; 
function multiplyBy2 (inputNumber){ 
    const result = inputNumber*2; 
    return result; } 
const output = multiplyBy2(4);
const newOutput = multiplyBy2(10);
```

When you execute a function you create a new execution context comprising: 

- The thread of execution (we go through the code in the function line by line) 
- A local memory ('Variable environment') where anything defined in the function is stored

## STEPS whats happening:

1. output = multiplyBy2(4);
   	Creating Execution Context:

|      | Local Memory                    |
| ---- | ------------------------------- |
|      | inputNumber : 4<br />result : 8 |

​							return : 8 to the Global Execution Context

2. **newOutput = multiplyBy2(10)**

   ​	Creating Execution Context:

|      | Local Memory                      |
| ---- | --------------------------------- |
|      | inputNumber : 10<br />result : 20 |

​							return : 20 to the Global Execution Context

































