## AMD, CommonJS and Browser Support
Writing code in such way that it will work in all environment (AMD, CommonJS or plain js in browser)
```
(function (root, factory) {

  if(typeof define === "function" && define.amd) { // AMD support
  
    define(["jquery"], factory);
    
  } else if(typeof module === "object" && module.exports) { // CommonJS support
  
    let jquery = require('jquery');
    
    module.exports = factory(jquery);
    
  } else { // plain js
  
    let jquery = require('jquery');
    
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
  
}));
```
