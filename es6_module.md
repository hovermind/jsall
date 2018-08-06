## ES6 Module
An ES6 module is a file containing JS code. There’s no special module keyword; a module mostly reads just like a script.
There are two differences:
* ES6 modules are automatically strict-mode code, even if you don’t write `"use strict";` in them.
* You can use `import` and `export` in modules.

## `export`
Everything declared inside a module is local to the module, by default. If you want something declared in a module to be public, 
so that other modules can use it, you must export that feature. There are a few ways to do this. The simplest way is to add the export keyword.   

`my_module.js`
```
export function myMethod(){

}

export class myClass{

}
```
Or
```
export {myMethod, myClass};

function myMethod(){

}

class myClass{

}
```
* you can export any top-level `function`, `class`, `var`, `let`, or `const`
* the code is a module, not a script, all the declarations will be scoped to that module
* the code in a module is pretty much just normal code
* if your module runs in a web browser, it can use document and `XMLHttpRequest`

## `import`
```
import {myMethod} from "my_module.js";

function doSomthing() {

  // ...
  myMethod();
  
}
```
To import multiple names from a module, you would write:
```
import {myMethod, myClass} from "my_module.js";
```
When you run a module containing an import declaration, the modules it imports are loaded first, then each module body is executed in a depth-first traversal of the dependency graph, avoiding cycles by skipping anything already executed.

## Renaming imports and exports
Import
```
import {doSomething as ds1} from "my_module_1.js";
import {doSomething as ds2} from "my_module_2.js";
```
Export
```
function v1() { ... }
function v2() { ... }

export {
  v1 as streamV1,
  v2 as streamV2,
  v2 as streamLatestVersion
};
```

## Importing AMD module to CS6 module
```
import {each, map} from "lodash";

import _ from "lodash";

import colors from "colors/safe";

import * as cows from "cows"; // cows.moo()
```
See: [ES6 Module Details](https://hacks.mozilla.org/2015/08/es6-in-depth-modules/)
