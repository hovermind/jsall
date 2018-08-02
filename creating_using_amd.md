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
