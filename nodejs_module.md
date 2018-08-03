## `Node.js` Module
* a module encapsulates related code into a single unit of code - can be interpreted as moving all related functions into a file.
* modules to be considered same as JavaScript libraries - a set of functions you want to keep togather & include in your application.
* `node.js` has a set of built-in modules which you can use
* `exports` and `module.exports` reference the same object
* `node.js` runtine also has `require()` to lead module as like `require.js`

## Create module
```
let sayHello = function (name) {
    return `Hello ${name}`;
};

exports.greeting = function(name){
    return sayHello(name);
};

// or
exports.greeting = function (name) {
    return `Hello ${name}`;
};

// also
// exports.greeting = {};
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
