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

## RequireJS - AMD loader
An AMD loader is code that implements AMD specification. There are multiple implementations.
RequireJS is one of the AMD loaders.

#### Using RequireJS
In site footer
```
<script src="js/lib/require.js" data-main="js/require_config"></script>
```
For synchronous loading (your script `my_script.js` might be loaded before `require_config.js` and that would cause problem)
```
<script src="require.js"></script>
<script src="js/require_config.js"></script>
```
##### [data-main attribute](http://requirejs.org/docs/api.html#data-main)
This is the path to your main javascript file. You can think about it as a main entry point into your application (configuration goes here => `require_config.js` or `main.js`)  

## The Config File
The config file is the entry point to RequireJS.   

`require_config.js`
```
requirejs.config({
    baseUrl: 'js',
    paths: {
        jquery: './lib/jquery',
	d3 : ["./lib/d3"],
	c3 : ["./lib/c3"]
    }
});
```
Or config with fallback
```
requirejs.config({
    baseUrl: 'js',
    paths: {
	jquery: ['https://code.jquery.com/jquery-3.3.1.min', './lib/jquery'],
	d3 : ["https://cdnjs.cloudflare.com/ajax/libs/d3/4.13.0/d3.min.js", "./lib/d3.min"],
	c3 : ["https://cdnjs.cloudflare.com/ajax/libs/c3/0.6.2/c3.min.js", "./lib/c3.min"],
    }
});
```

### `baseUrl: 'js'`
Root folder from where RequireJS will load modules. If `data-main` attribute is used, `baseUrl` will be location of that `config.js` (or `main.js`) file. Example: If `data-main="js/require_config.js"` then `baseUrl` is `/js`

**Note:** 
* `baseUrl` not `baseUri`
* `baseUrl` will be prepended before module paths while loading asynchronously

See [baseUrl details](http://requirejs.org/docs/api.html#config-baseUrl)

### paths
For modules located in sub-dir of baseUri (baseUri will be prepended to path). See [path details](http://requirejs.org/docs/api.html#config-paths)

**See:**
* [Patterns for separating config from the main module](https://github.com/requirejs/requirejs/wiki/Patterns-for-separating-config-from-the-main-module)
* [AMD Config Details](#)

## Define AMD module
Each module you make will be in a separate file; besides simplifying your development process, you'll see that module loaders such as RequireJS use the file name as the module name. Sure, you can hard-code a name for your module inside the file, but this is a bad idea. That's because, after development, you'll want to use an optimization tool to put all your modules into one file for better downloading. The optimization tool will give your modules a name, deriving it from their file name. If you've added a name for the modules within the file, this could cause some confusion.
```
define(id?, dependencies?, factory);
```

#### Factory function that returns an object literal
```
define(["dependency"], function() {

    let obj = {
        Color: 'black', // module property
        Shirt: function(size) { // ctor
            this.size = size; // class property
        }
    };

    return obj;
});
```

#### Factory function that returns another function
```
define(["dependency"], function() {

    let Jacket = function() {
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

See [AMD module best practices](#)
