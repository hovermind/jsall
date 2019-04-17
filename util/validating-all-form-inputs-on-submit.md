## Common validation of form inputs on submit
```js
function isFormInputValid(){

	let isValid = true;

	// 共通Validation（例えばEmptyとNullチェック）
	// English: Common Validation (i.e. Empty or null check)
	$.each($('form').serializeArray(), function(index, field) {

		console.log(index + ": " + field.name + " => " + field.value);

		if(!field.value){
		  isValid = false;
		}

	});

	/* 
	* Validation論理はいれてください
	* English: Validation logic here
	*/

	//「○○」のValidation
	// English: Validation of [xxx]

	return isValid;
}
```

**Sample**
```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <title>FOO</title>
</head>
<body>

	<form action="/" method="POST">
		<input id="foo-id" name="foo-id" type="text" placeholder="Foo id" />
		<input type="submit" value="Send" />
	</form>

	<script src="https://code.jquery.com/jquery.min.js"></script>
	<link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap.min.css" rel="stylesheet" type="text/css" />
	<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/js/bootstrap.min.js"></script>
	  
	<script type="text/javascript">

		"use strict";

		$(function(){
		  
		  $('body').on('submit', 'form', function(e) {
			
			e.preventDefault(); 
			
			$.each($(this).serializeArray(), function(index, field) {
			  
			  console.log(field.name + " => " + field.value);
			  
			  // common validation here
			  
			});
		  });
		});
		
	</script>
	  
</body>
</html>
```
