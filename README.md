# Nodejs Web Server

### TODO
First task is Initialization Node & Github
```
npm init -y
git init
git add .
git commit -m <Message String>
git branch -M <branchName>
git remote add <remote> <url>
git push -u <remote> <branch>
```
Second task Create a server.js
```
touch server.js
```
How to create a Native Server using **Core Module** Nodejs **( http )**
--
-   import a http core module  
```
const http = require('http');
```
-   Create requestListener
```
const requestListener = (request,response)=>{
    response.setHeader('Content-Type','text/html');
    response.statusCode=200;
    response.end('<h1>Hallo Server Http</h1>')
}
```
-   Create instance server
```
const server = http.createServer(requestListener);
```
-   Create Listener
```
const port = 5000; //optional
const host = 'localhost'; //optional
server.listen(port,host,()=>{
    console.log(`Server Running on http://${host}:${port}`);
});
```
-   Update script on Package.json to run node server.js
```
"start" = "node server.js"
```
to run script u can run on terminal 
using
```
npm run start
```
check the server is running using
```
curl -X GET http://localhost:5000
```
Handling Request
--
On requestListener Add logical method to handle the request from client
request method is:
-   GET
-   POST
-   PUT
-   DELETE
---
you can add this logical.
---
Before :
```
const requestListener = (request,response)=>{
    response.setHeader('Content-Type','text/html');
    response.statusCode=200;
    response.end('<h1>Hallo Server Http</h1>')
}
```
After:
```
const requestListener = (request,response)=>{
    response.setHeader('Content-Type','text/html');
    response.statusCode=200;
    const {method} = request;
    if(method == 'GET'){
        response.end('<h1>Hello!</h1>')
    }
    if(method === 'POST') {
        response.end('<h1>Hai!</h1>');
    }
    if(method === 'PUT') {
        response.end('<h1>Bonjour!</h1>');
    }
    if(method === 'DELETE') {
        response.end('<h1>Salam!</h1>');
    }
};
```
Check on Terminal
```
curl -X GET http://localhost:5000
// output: <h1>Hello!</h1>
curl -X POST http://localhost:5000
// output: <h1>Hai!</h1>
curl -X PUT http://localhost:5000
// output: <h1>Bonjour!</h1>
curl -X DELETE http://localhost:5000
// output: <h1>Salam!</h1>
```
**Note:** If you **change** the **server.js** you must restart the server
```
CTRL+C 
npm run start
```
**How to get Body Request**
--
Add Stream Logic on **POST**
```
let body = [];
request.on('data',(chunk)=>{
    body.push(chunk);
});
request.on('body',()=>{
    body = Buffer.concat(body).toString();
    response.end(`<h1>Hai, ${body}!</h1>`);
});
```
Check the Output
```
curl -X POST -H "Content-Type: application/json" http://localhost:5000 -d "{\"name\": \"Dicoding\"}"
```
OUTPUT
```
<h1>Hai, {"name": "Dicoding"}!</h1>
```
The output data 

Solution to given log without Tag HTML like this :
---
Add Stream Logic on **POST**
```
let body = [];
request.on('data',(chunk)=>{
    body.push(chunk);
});
request.on('body',()=>{
    body = Buffer.concat(body).toString();
    const {name} = JSON.parse(body);
    response.end(`<h1>Hai, ${body}!</h1>`);
});
```
Output
```
<h1>Hai, Dicoding!</h1>
```
