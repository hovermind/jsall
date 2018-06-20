## AMD
Asynchronous module definition (AMD) is a specification for the programming language JavaScript. It defines an application programming interface (API) that defines code module and their dependencies, 
and loads them asynchronously if desired.    

Whole API consists of a single function. Brilliant! The signature of the function is:
```
define(id?, dependencies?, factory);
```
First, two arguments id and dependencies are optional. Third factory is a function that is executed to instantiate a module. 
If id is not specified then the module name is its file location. 
If dependencies argument is not specified it means (don’t screw this up!) that the module has no dependencies.

## RequireJS
An AMD loader is code that implements AMD specification. There are multiple implementations.
RequireJS is one of the AMD loaders.

**Loading RequireJS**    
`index.html`
```
<script data-main="app.js" src="require.js"></script>
```
**data-main attribute of the script tag:** This is the path to your main javascript file that contains configuration. You can think about it as a main entry point into your application.    

`app.js`
```
// config
require.config({
  baseUri: "path/to/scripts/folder"
  paths: {
     "jquery": "libs/jquery",
     "jquery.cookie": "plugins/jquery.cookie"
  }
});

// or config with falback
require.config({
  baseUri: "path/to/scripts/folder"
  paths: {
     "jquery": [
        "cdn",
        "libs/jquery"
      ],
     "jquery.cookie": "plugins/jquery.cookie"
  }
});
```
## Define AMD module
Each module you make will be in a separate file; besides simplifying your development process, you'll see that module loaders such as RequireJS use the file name as the module name. Sure, you can hard-code a name for your module inside the file, but this is a bad idea. That's because, after development, you'll want to use an optimization tool to put all your modules into one file for better downloading. The optimization tool will give your modules a name, deriving it from their file name. If you've added a name for the modules within the file, this could cause some confusion.
```
// define(id?, dependencies?, factory);

// Function that returns an object literal
define([], function() {

    var obj = {
        color: 'black', // module property
        Shirt: function(size) { // ctor
            this.size = size; // class property
        }
    };

    return obj;
});

// Function that returns another function
define([], function() {

    var Jacket = function() {
        // ...
    };

    Jacket.prototype.zip = function() {     // Zip up the jacket
        // ...
    };

    return Jacket;
});
```

## Load AMD module using RequireJS
```
// Fetch and execute Marionette App
require( ["my/module"], function (MyModule) {

    MyModule.start();
});
```


