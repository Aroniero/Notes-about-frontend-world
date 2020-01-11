# #Solution 1

```javascript
function display(data){
 console.log(data)
}
const dataFromAPI = fetchAndWait('https://twitter.com/will/tweets/1')
//... user can do NOTHING here !
//... could be 300ms, could be half a second
// they're just clicking and getting nothing
display(dataFromAPI)
console.log(“Me later!”);
```

## Steps whats happenning:

1. **Memory**:

   a) display: function;
   b) dataFromAPI: "hi"
   	(1ms) dataFromAPI = fetchAndWait('https://twitter.com/will/tweets/1')	->  (200ms) "Hi"
   c) (201ms) display('hi);
   
   ​	Creating Execution Context:
   
   |      | Local Memory |
   | ---- | ------------ |
   |      | data: "hi"   |
   
   ​											return "hi"
   d) (202ms) console.log("Me later")

# Solution  2 - Introducing Web Browser APIs/ Node background threads

```javascript
function printHello(){
 console.log(“Hello”);
}
setTimeout(printHello,1000);
console.log(“Me first!”);
```

## Steps whats happenning:

1. **Memory**:

   a) printHello: *function*;
   b) (1ms) setTimeout(printHello *function*, 1000)		<- Its Web Browser Feature [Timer]
   c) (2ms) console.log("Me first!");	-> 	logs Me first
   d) (1001ms) printHello()				-> 	logs Hello

   

   ​		**Web Browser Feature (ITS HAPPENING IN THE WEB):**
   ​		Timer (1000ms) **->** Completed?: No **->** On complition: not running printHello()
   ​				  (1001ms) **->** Completed?: Yes **->** On complition: running printHello()

# We’re interacting with a world outside of JavaScript now - so we need rules

```javascript
function printHello(){
 console.log(“Hello”);
}
function blockFor1Sec(){
 //blocks in the JavaScript thread for 1 second
}
setTimeout(printHello,0);
blockFor1Sec()
console.log(“Me first!”);
```

### Steps whats happenning:

1. **Memory**:

   a) printHello: *function*;
   b) blockFor1Sec: *function*;
   c) (1ms) setTimeout(printHello *function*, 0)		<- Its Web Browser Feature [Timer]
   d) (2ms) blockFor1Sec();
   	Creating Execution Context:

   |      | Local Memory            |
   | ---- | ----------------------- |
   |      | (1000ms) blockFor1Sec() |

   ​						return
   e) (1002ms) console.log(“Me first!”);		-> Logs Me first!
   d) (1003ms) printHello()							-> Logs Hello

   ​	

   ​		**Web Browser Feature (ITS HAPPENING IN THE WEB):**
   ​		Timer (0ms) **->** Completed?: Yes **->** On complition: running printHello()				  

**Fundamental rule:
Javascript has to empty his callstack and finish running all Global Synchronous Code thats why printHello() is showing in d) moment not the c) moment, even if it was immediately finished. Timer is going to "Callback queue". This queue is storing code which is ready to insert the Callstack. This code is checking if it can enter the Callstack and this rule is called *EventLoop* ** 

# Solution 3 - Using two-pronged ‘facade’ functions that both initiate background web browser work and return a placeholder object (promise) immediately in JavaScript

```javascript
function display(data){
 	console.log(data)
}
const futureData = fetch('https://twitter.com/will/tweets/1')
futureData.then(display); // Attaches display functionality
console.log(“Me first!”);
```

## Steps whats happenning:

1. ### **Memory**:

   a) display: *function*;
   b)  futureData: .....	<-  at the very beginning it is undefined

   - JAVASCRIPT SIDE
     (1ms) futureData = fetch('https://twitter.com/will/tweets/1');
     returns immedietly object called Promise {value: ..., onFulfillment: [ ] } 

   - Web Browser Features SIDE:
     Is making xhr 

     | xhr                                               | Complete? | On completion      |
     | ------------------------------------------------- | --------- | ------------------ |
     | https://twitter.com/will/tweets/1<br />GET method | NOPE      | futureData.value = |

   - futureData: {value: ..., onFulfillment: [ ] }          <- now it has this "empty" objectc) 

   c) futureData.then(display *function*)
   d) (2ms) console.log('Me first!");              <---- Logs "Me first"!
   e) (201ms) Respond coming back from WBF

   | xhr                                               | Complete? | On completion           |
   | ------------------------------------------------- | --------- | ----------------------- |
   | https://twitter.com/will/tweets/1<br />GET method | NOPE      | futureData.value =      |
   | after 201ms                                       | YES       | futureData.value = "hi" |

   ​	display("hi");        <---- Logs "Hi"!

2. **Console view:**
   (2ms) Me first!
   


# But we need to know how our promisedeferred functionality gets back into JavaScript to be run

```javascript
function display(data){console.log(data)}
function printHello(){console.log(“Hello”);}
function blockFor300ms(){/* blocks js thread for 300ms with long for loop */}
setTimeout(printHello, 0);
const futureData = fetch('https://twitter.com/will/tweets/1')
futureData.then(display)
blockFor300ms()
// Which will run first?
console.log(“Me first!”);
```











































