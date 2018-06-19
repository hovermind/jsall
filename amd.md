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
```
// define(id?, dependencies?, factory);

define( 'MyApp', ["marionette"], function (Marionette) {
 
    // set up the app instance
    var MyApp = new Marionette.Application();
 
    MyApp.on("initialize:after", function(){
      alert("Application has started!");
    });
 
    // export the app from this module
    return MyApp;
});
```

## Load AMD module using RequireJS
```
// Fetch and execute Marionette App
require( ["MyApp"], function (MyApp) {
    // Execute App
    MyApp.start();
});
```


