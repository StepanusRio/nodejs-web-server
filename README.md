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