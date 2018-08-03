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
