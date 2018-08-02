CommonJS modules enables you to include javascript modules within the current scope and effectively keeps the global scope from being polluted. 
This massively reduces the chance of naming collisions and keeps code organised.

That said I think it's pretty safe to say that **AMD modules have now become more popular than CommonJS.**

#### AMD module: `foo.js`
```
define(['jquery'], function ($) {

  let myModule = {
  
    sayHi: (id) => {
    
      let name = $(`#${id}`).val();
      
      console.log(`Hi ${name}`);
    }
  };
  
  return myModule;
});
```

#### CommonJS module: `foo.js`
```
var $ = require('jquery');

let myModule = {

    sayHi: (id) => {
    
      let name = $(`#${id}`).val();
      
      console.log(`Hi ${name}`);
    }
};

// expose
module.exports = myModule;
```

#### OR
```
(function (root, factory) {

  let jquery = require('jquery');
  
  if(typeof module === "object" && module.exports) { // CommonJS support
  
    module.exports = factory(jquery);
    
  } else {
  
    root.myModule = factory(jquery);
  }
  
}(this, function($) {

  let myModule = {

      sayHi: (id) => {

        let name = $(`#${id}`).val();

        console.log(`Hi ${name}`);
      }
  };
  
  return myModule;
  
});
```
