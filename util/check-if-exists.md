## jQuery object check
```js
if( $('[selector]').length )
{
  // it exists
}

// example
// use this if you are using id to check
if( $('#foo').length )
{
  // it exists
}
```

Exist check util
```js
function isJqObjectExist(selector){ // selector => '#foo', '.foo' etc.
  return $(selector).length > 0;
}
```

## JS object check
```js
let foo = {};

if($.isEmptyObject(foo)){
  // foo is an empty object
}
```

## Variable check
#### variables that may or may not be declared
```js
if( typeof x !== 'undefined' )
{
  // variable 'x' is defined
}
```

#### value check for declared variables
```js
if( foo ) {
  // foo has value
}

if( !foo ) {
   //foo does have any value ('', empty, blank etc.)
}
```
The `if(foo)` will check:
* null
* undefined
* NaN
* empty string ("")
* 0
* false

#### only null check for declared variables
```js
if (variable == null) { // checks both null and undefined for declared variables
  // do something 
}
```
the above is equivalent to:
```js
if( variable === 'undefined' || variable === null ){
  // do something 
}
```

#### declared and has value check
```js
if (typeof foo !== "undefined" && foo) {
   // foo is defined and it has value 
}
```

#### empty check
```js
function isEmpty(foo){
  return (typeof foo === "undefined" || !foo);
}
```

## Data attribute exist
```js
if ($("#id").data('timer')) {
  //exist
}
```

