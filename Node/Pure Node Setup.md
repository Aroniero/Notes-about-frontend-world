# Setup

Go to official site of node and [download it](https://nodejs.org/en/). If u have already node installed you can check your version by typiing this command 

```
node -v
```

# Module & require

```
const xyz = require('./people'); 

const os = require('os');   //Its module build in Node. It gives you information about operating system (os)
console.log(os.platform(), os.homedir()); 		//win32  C:/Users/Shaun
```

# File system

To interact with file system you need to import fs module build in Node

```javascript
const fs = require('fs')
```

## Reading files:

```javascript
fs.readFile('./docs/blog1.txt', (err, data) => {
	if (err) {
        console.log(err)
    }
    console.log(data) //output: <Buffer .......>
    console.log(data.toString());  //output: hello, ninjas
})
```

## Writing files:

```javascript
fs.writeFile('./docs/blog1.txt', 'hello world', () => {
    console.log('file was written')
})      
// If we run this code the blog1.txt will be updated with "hello world"
```

in case we run this code and the `blog1` Node will create this file for us.

## directories

```javascript
fs.mkdir('./assets', (err) => {
	if(err){
		console.log(err)
	}
    console.log('folder created') 
})
//It will create assets folder in current directory.
```

If we will use the same code again. We will get error which says "file already exists", so you cannot remake existing folder. So firstable you should check if this folder already exists:

```javascript
if(!fs.existsSync('./assets')){
    fs.mkdir('./assets', (err) => {
        if(err){
            console.log(err)
        }
        console.log('folder created')
	})
} else {
    fs.rmdir('./assets', (err) => {
        if(err) {
            console.log(err)
        }
        console.log('folder deleted')
    })
}
```

## deleting files

```javascript
if(fs.existsSync('./docs/deleteme.txt')){
	fs.unlink('./docs/deleteme.txt', (err) => {
        if(err){
            console.log(err)
        }
        console.log('file deleted')
    })
}
```

# Streams & Buffers

## Streams

Start using data, before it has finished loading.

### Readstream

```javascript
const fs = require('fs')
const readStream = fs.createReadStream('./docs/blog3.txt');

readStream.on('data', (chunk) = {
    console.log('New chunk')
    console.log(chunk)
})
```

If we run our file we should get something like this

```
<Buffer .......>
New chunk
<Buffer .......>
New chunk
<Buffer .......>
New chunk
```

To turn `<Buffer ..>` into readable format we can use `toString()` on our `chunk` data

```javascript
const fs = require('fs')
const readStream = fs.createReadStream('./docs/blog3.txt');

readStream.on('data', (chunk) = {
    console.log('New chunk')
    console.log(chunk.toString())
})
```

Instead we can pass object in second argument of `createReadStream()` method. So we dont have to write `toString()` method

```javascript
const fs = require('fs')
const readStream = fs.createReadStream('./docs/blog3.txt', {encoding: 'utf8'});

readStream.on('data', (chunk) = {
    console.log('New chunk')
    console.log(chunk)
})
```

### Write Stream

To create write stream we can use `createWriteStream()` method:

```javascript
const fs = require('fs')
const readStream = fs.createReadStream('./docs/blog3.txt', {encoding: 'utf8'});
const writeStream = fs.createWriteStream('./docs/blog4.txt');

readStream.on('data', (chunk) = {
    console.log('New chunk')
    console.log(chunk)
	writeStream.write('\n New Chunk \n')
    writeStream.write(chunk)
})
```

We can do all the same thing by using pipe. But it must be from READABLE STREAM to the WRITABLE STREAM

```javascript
readStream.pipe(writeStream);
```

# Creating server

Create file `server.js`

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
	console.log('request made')
});

server.listen(3000, 'localhost', () => {
   console.log('listening port on 3000')
})
```

## Response

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
	console.log('request made')
    
    res.setHeader('Content-type', 'text/html')
    res.write('<p>Hello world</p>');
    res.end()
});

server.listen(3000, 'localhost', () => {
   console.log('listening port on 3000')
})
```

