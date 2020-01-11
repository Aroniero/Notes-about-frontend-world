# JavaScript uses this proto link to give objects, functions and arrays a bunch of bonus functionality. All objects by default have __proto__

```javascript
const obj = {
 num : 3
}
obj.num // 3
obj.hasOwnProperty("num") // ? Where's this method?
Object.prototype // {hasOwnProperty: FUNCTION}
```

— With Object.create we override the default __proto__ reference to Object.prototype and replace with functionStore 
— But functionStore is an object so it has a __proto__ reference to Object.prototype - we just intercede in the chain

1) obj : { 
			num : 3, 
			_ _ proto_ _ : <span style="color: #82b74b;">Object</span>.prototype		<------- its referring from <span style="color: #82b74b;">Object: </span>*function* which is combo inside JS
}
2) obj.num	// 3
3) obj.hasOwnProperty("num")
		<span style="color: #82b74b;">Object: </span>*function* :		<---- its created in run time of javascript code

```javascript
This stuff is created at the moment we put JS on.
Object: {
    prototype: {
        hasOwnProperty: function
    }
}
Function: {
    prototype: {
        toString: function,
		call: function,
		bind: function,
		apply: function
    }
}
```

# Arrays and functions are also objects so they get access to all the functions in Object.prototype but also more goodies

```javascript
function multiplyBy2(num){
	 return num*2
}
multiplyBy2.toString() //Where is this method?
Function.prototype // {toString : FUNCTION, call : FUNCTION, bind : FUNCTION}
multiplyBy2.hasOwnProperty("score") // Where's this function?
Function.prototype.__proto__ // Object.prototype {hasOwnProperty: FUNCTION}
```

1) multiplyBy2: *function*		<--------- its FUNCTION OBJECT COMBO
						{ 
							prototype: {
							}
							_ _ proto_ _ : 
						}

2) multiplyBy2.toString()
	-- first it looks for multiplyBy2 and it finds it 
	-- we dont see toString() method on this object so it is going to look for this function in Function.prototype object.
3) multiplyBy2. <span style="color: #feb236">hasOwnProperty</span>("score")
	-- first it looks for function multiplyBy2 definition and it finds it 
	-- and it looks for <span style="color: #feb236">hasOwnProperty</span> and it doesnt find it. But  _ _ _proto_ _ _  is refrencing to Function.prototype
		multiplyBy2: { 
			prototype: { }
			_ _ proto_ _ : { }
		}
	-- In Function.prototype we cant find <span style="color: #feb236">hasOwnProperty</span> function so we look in _ _ proto _ _ of Function.prototype
		Function: {
    			prototype: {
    				   toString: function,
						call: function,
						bind: function,
						apply: function,
						_ _ proto _ _:   <----------- this proto is referencing Object.prototype so we find hasOwnProperty here
				 }
		  }

 