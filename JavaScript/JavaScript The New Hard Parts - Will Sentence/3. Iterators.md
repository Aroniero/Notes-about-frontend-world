```javascript
const numbers = [4,5,6]
for (let i = 0; i < numbers.length; i++){
 console.log(numbers[i])
} 
```

Steps:
1) numbers: [4,5,6]
2) <u>Check this</u>	i < numbers.length
						0 < 3
	<u>Do this</u>		console.log(numbers[i])
						i++				[4,5,6]  [0]



```javascript
function createNewFunction() {
 function add2 (num){
 return num+2;
 }
 return add2;
}
const newFunction = createNewFunction()
const result = newFunction(3)
```

Steps:
1) createNewFunction: *function*;
2) **newFunction: ...;**		<----- something is gonna be stored in newFunction we dont know it yet
	newFunction = createNewFunction()
	Creating a New Execution Context

|      | Memory            |
| ---- | ----------------- |
|      | add2 : *function* |

​													returning function definition and store it in newFunction
​	**newFunction: *function*;**	<--------- now we know what it is, its function definition :D 

3) result = ....; 		<----- something is gonna be stored in result we dont know it yet
	result = newFunction(3)
	Creating a New Execution Context	

|      | Memory  |
| ---- | ------- |
|      | num : 3 |

​															returning 3 + 2
​	result = 5;		<--------- now we know what it is, its value 5 

# We want to create a function that holds both our array, the position we are currently at in our ‘stream’ of elements and has the ability to return the next element

```javascript
function createFunction(array){
     let i = 0
     function inner(){
         const element = array[i]
         i++
         return element
 	}
 	return inner
}
const returnNextElement = createFunction([4,5,6])
const element1 = returnNextElement()
const element2 = returnNextElement()
```

1) createFunction: *function*;
2) returnNextElement: ....: 	<----- something is gonna be stored in **returnNextElement** we dont know it yet
	returnNextElement = createFunction([4,5,6])
														Creating new Execution Context

|      | Memory                                                       |
| ---- | ------------------------------------------------------------ |
|      | array : [4,5,6],<br />i : 0<br />inner : <span style="color: #82b74b">*function*</span> |

​								returning <span style="color: #82b74b">*function*</span> 				Execution Context is disappearing after returning it
​	returnNextElement: <span style="color: #82b74b">*function*</span>			

3)  element1 : ....: 	<----- something is gonna be stored in **element1** we dont know it yet
	 element1 = returnNextElement();
														Creating new Execution Context

|                                                              | Memory                                         |
| ------------------------------------------------------------ | :--------------------------------------------- |
| element =  array    [i]<br />                <span style="color: #82b74b"> [4,5,6]   [0] </span><br />i++ | element: <span style="color: #82b74b">4</span> |

​																						returning <span style="color: #82b74b">4</span>
​	element1 :  <span style="color: #82b74b">4</span>	

3)  element2 : ....: 	<----- something is gonna be stored in **element1** we dont know it yet. At the moment it is undefined 	 element2 = returnNextElement();
				 										Creating new Execution Context

|                                                              | Memory                                         |
| ------------------------------------------------------------ | :--------------------------------------------- |
| element =  array    [i]<br />                <span style="color: #82b74b"> [4,5,6]   [1] </span><br />i++ | element: <span style="color: #82b74b">5</span> |

​																						returning <span style="color: #82b74b">5</span>
​	element1 :  <span style="color: #82b74b">5</span>	























