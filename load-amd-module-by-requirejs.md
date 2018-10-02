## Create Module
`foo-module.js`
```
define(["jquery"], function($){
	
	'use strict';
	
	const PI = 3.1416;
	let x = 'Circle';

	let thisModule = {
		
		bar: function() => {
			
		},
		
		baz: ({radius}) =>{
		
			thisModule.bar();
		}
	};
	
	return thisModule;
});
```

## Use Module (in page specific js)
`foo.js`
```
require([ 'module/foo-module' ], function(Foo) {

	// code here

	$(document).ready(function() {
	
		// init()

		$('#my-button').click(function(e) {

			e.preventDefault();

			Foo.baz({radius: 15});
		});
	});
});
```

## Load JS File in Page
`foo.html` (in head, put `require.js` & `require-config.js`)
```
<head>
	
	... ... ... ... ... ...

	<script type="text/javascript" th:src="@{/js/libs/require.js}"></script>
	<script th:inline="javascript">
		var contextPathWithSlash = /*[[@{/}]]*/'/';
	</script>
	<script type="text/javascript" th:src="@{/js/require-config.js}"></script>

</head>
```

**`require-config.js` uses `contextPathWithSlash` for `baseUrl`:**
```
requirejs.config({
	baseUrl: contextPathWithSlash + 'js',  // load all module from here
	paths: {                               // sub folders of baseUrl
		'jquery' : ['./libs/jquery'],
		'bootstrap' : ['./libs/bootstrap'],
		d3 : ["./libs/d3"],
		c3 : ["./libs/c3"],
	},
	shim: {                               // nested dependency
		'bootstrap' : { deps : ['jquery'] },
		'c3' : { deps : ['d3'] }
	}
});
```

**Now load `foo.js` at bottom of `foo.html` page**
```
    ... ... ... ...
	
	<script type="text/javascript">
		// load js files from baseUrl (baseUrl is set in require-config.js)
		require([ 'foo' ]);
	</script>

</body>
```
**Note: `foo.js` uses require module `foo-module`, so `require-config.js` must be loaded before `foo.js` and that's why we put `require-config.js` at top and loading `foo.js` at bottom**
