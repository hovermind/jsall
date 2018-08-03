## Define AMD module
Each module you make will be in a separate file; besides simplifying your development process, you'll see that module loaders such as RequireJS use the file name as the module name. Sure, you can hard-code a name for your module inside the file, but this is a bad idea. That's because, after development, you'll want to use an optimization tool to put all your modules into one file for better downloading. The optimization tool will give your modules a name, deriving it from their file name. If you've added a name for the modules within the file, this could cause some confusion.
```
define(id?, dependencies?, factory);
```

#### Factory function that returns an object literal
```
define(['jquery'], function ($) {

  let myModule = {
  
    color : '#0F0',
    
    sayHi: (id) => {
    
      let name = $(`#${id}`).val();
      
      console.log(`Hi ${name}`);
    }
  };
  
  return myModule;
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
`my_script.js`
```
require( ["modules/my_module"], function (MyModule) {

    console.log(MyModule.color);
    
    MyModule.sayHi('name-field');
    
    //.... .... ..... ....
});
```

See [AMD module best practices](#)

## Skipping Dependency
Use `_` in param of factory fucntion
```
require(['jquery', `my_mod`], function($, _){ // _ for my_mod to skip
  // ... ... ...
});
```

## Loading AMD incompatible dependency
If dependency (i.e. Bootstrap) is not amd compatible then skip parameter for it in factory function
```
require(['jquery', `bootstrap`], function($){ // no param for Bootstrap
  // ... ... ...
});
```

## Simplified Define Wrapper
Instead of
```
define([ './a', 'b', './c', './d', './e', './f', './g', './h'...], function(A, B, C, D, E, F, G, H ...) {
    // App logic
});
```
Define can be simplified as below
```
define(function(require) {

    let A = require('./a');
    let B = require('./b');
    // ... ... ...

    // App logic
    
    return function () {};
    // or
    // return {}
});
```
