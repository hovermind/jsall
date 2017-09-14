# <a name="#toc"></a>TOC
- [The Grand Confusion: \_\_`proto`\_\_ vs `prototype`](#proto-vs-prototype)   



# <a name="#proto-vs-prototype"></a>The Grand Confusion: \_\_`proto`\_\_ vs `prototype`

**First of all, every function in JavaScript is (a potential) constructor.**

## prototype
prototype is a property of a Function. It is the blueprint for creating objects by using that (constructor) function with new keyword.

## \_\_proto\_\_
\_\_`proto`\_\_ is used in the lookup chain (to resolve methods/properties). when an object is created using (constructor) function with new keyword, \_\_`proto`\_\_ property set to (Constructor) Function.prototype
```
function Robot(name) {
    this.name = name;
}
var robot = new Robot();

// the following are true   
robot.__proto__ == Robot.prototype
robot.__proto__.__proto__ == Object.prototype
```
## My imaginary explanation
Imagine there is an imaginary class(blueprint/coockie cutter) associated with function. That imaginary class is used to instantiate objects. `prototype` is the extention mechanism (extention method in C#, or Swift Extension) to add things to that imaginary class.      
```
function Robot(name) {
    this.name = name;
}
```
**The above can be imagined as:**     
```
// imaginary class
class Robot extends Object{

	static prototype = Robot.class  // Robot.prototype way to extend Robot class
	
	// since Robot extends Object, therefore Robot.prototype.__proto__ == Robot.class.__proto__ == Object.prototype
	
	var __proto__;
	
	var name = "";
	
	// constructor
	function Robot(name) {
	
		this.__proto__ = prototype;
		prototype = undefined;
		
		this.name = name;
	}

}
```
**So,**    
```
var robot = new Robot();

robot.__proto__ == Robot.prototype
robot.prototype == undefined
robot.__proto__.__proto__ == Object.prototype
```
**Now adding method to the `prototype` of Robot:**
```
Robot.prototype.move(x, y) = function(x, y){ Robot.position.x = x; Robot.position.y = y};
```
The above can be imagined as extension of Robot class:    
```    
// Swift way of extention
extension Robot{
	function move(x, y){    
		Robot.position.x = x; Robot.position.y = y
	}
}
```
**Which in turn,**   
```
// imaginary class
class Robot{

	static prototype = Robot.class // Robot.prototype way to extend Robot class
	var __proto__;
	
	var name = "";
	
	// constructor
	function Robot(name) {
	
		this.__proto__ = prototype;
		prototype = undefined;
		
		this.name = name;
	}
	
	// added by prototype (as like C# extension method)
	function move(x, y){ 
		Robot.position.x = x; Robot.position.y = y
	};
}
```





