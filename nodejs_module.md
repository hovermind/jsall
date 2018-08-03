## `Node.js` Module
* modules to be considered same as JavaScript libraries - a set of functions you want to keep togather & include in your application.
* `node.js` has a set of built-in modules which you can use

#### Create module
```
let sayHi = function (name) {
    console.log(`Hi ${name}`);
};
exports.sayHi = sayHi;

// or
exports.sayHi = function (name) {
    console.log(`Hi ${name}`);
};
```

## Load Module
Use the `require()` function with the name of the module
```
var http = require('http'); // built-in node.js module

http.createServer(function (req, res) {
    res.writeHead(200, {'Content-Type': 'text/html'});
    res.end('Hello World!');
}).listen(8080);
```
