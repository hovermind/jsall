## Enum in JS
```js
class Enum {
  constructor(enumObj) {
	const handler = {
	  get(target, name) {
		if (typeof target[name] != 'undefined') {
		  return target[name];
		}
		throw new Error(`No such enumerator: ${name}`);
	  },
	  set() {
		throw new Error('Cannot add/update properties on an Enum instance after it is defined')
	  }
	};

	return new Proxy(enumObj, handler);
  }
}
```

## Using Enum
```js
var Browser = new Enum({"IE": 1, "Chrome": 2, "Firefox": 3, "Safari": 4, "Opera": 5});

if(detectBrowser() === Browser.IE){
	console.log("Detected browser is IE");
}
```
