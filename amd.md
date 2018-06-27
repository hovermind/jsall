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
<script data-main="js/main.js" src="require.js"></script>
```
[data-main attribute](http://requirejs.org/docs/api.html#data-main)     
This is the path to your main javascript file that contains configurations. You can think about it as a main entry point into your application.

## RequireJS config `main.js`
```
// config
requirejs.config({
	//baseUri: 'js',
	paths: {
		d3 : ["lib/d3"],
		c3 : ["lib/c3"]
	}
});

// or config with falback
requirejs.config({
	//baseUri: 'js',
	paths: {
		d3 : ["https://cdnjs.cloudflare.com/ajax/libs/d3/4.13.0/d3.min.js", "lib/d3.min"],
		c3 : ["https://cdnjs.cloudflare.com/ajax/libs/c3/0.6.2/c3.min.js", "lib/c3.min"],
	}
});
```
**Note:** If `data-main="js/main.js"` then baseUri is `js`   

#### baseUri
Root folder from where RequireJS will load modules. See [baseUri details](http://requirejs.org/docs/api.html#config-baseUrl)

#### paths
For modules located in sub-dir of baseUri (baseUri will be prepended to path). See [path details](http://requirejs.org/docs/api.html#config-paths)

## Define AMD module
Each module you make will be in a separate file; besides simplifying your development process, you'll see that module loaders such as RequireJS use the file name as the module name. Sure, you can hard-code a name for your module inside the file, but this is a bad idea. That's because, after development, you'll want to use an optimization tool to put all your modules into one file for better downloading. The optimization tool will give your modules a name, deriving it from their file name. If you've added a name for the modules within the file, this could cause some confusion.
```
// define(id?, dependencies?, factory);

// Function that returns an object literal
define([], function() {

    var obj = {
        Color: 'black', // module property
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

    MyModule.Property;
    MyModule.Method();
    
    //.... .... ..... ....
});
```


