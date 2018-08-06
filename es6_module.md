## ES6 Module
An ES6 module is a file containing JS code. There’s no special module keyword; a module mostly reads just like a script.
There are two differences:
* ES6 modules are automatically strict-mode code, even if you don’t write "use strict"; in them.
* You can use import and export in modules.

## `export`
Everything declared inside a module is local to the module, by default. If you want something declared in a module to be public, 
so that other modules can use it, you must export that feature. There are a few ways to do this. The simplest way is to add the export keyword.
```
export function myFunc(){

}

export class myClass{

}
```
#### You can export any top-level function, class, var, let, or const.

