## JS Code for Opening Mutiple Tabs
```js
function openLink(link, i) {

	console.log(`Tab-${i}: ${link}`);

	if (i > 0) {
		window.open(link, "Tab-" + i, "");
	} else {
		window.open(link, "_new", "");
	}

}

$( document ).ready(function() {

	$('#btn-link-check').click((e) => {

		e.preventDefault();

		console.log("link checking...");

		// get links
		let linkString = $('#btn-link-check').data("links");
		console.log(linkString);

		if(linkString === null || linkString.length < 1){
			return;
		}

		let linkArray = linkString.split("|");
		// open tabs
		for(i = 0; i < linkArray.length; i++){
			openLink(linkArray[i], i);
		}

	});
});

```

## Test Html
* Using HTML 5 `data-*` attribute in button to get link list: `data-links='["https://hovermind.com", ...]'`
* Use [htmlshell.com](http://htmlshell.com/) for HTML boilerplate
```html
<!DOCTYPE html>
<!--[if lte IE 6]><html class="preIE7 preIE8 preIE9"><![endif]-->
<!--[if IE 7]><html class="preIE8 preIE9"><![endif]-->
<!--[if IE 8]><html class="preIE9"><![endif]-->
<!--[if gte IE 9]><!--><html><!--<![endif]-->
  <head>
    <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
  <meta name="viewport" content="width=device-width,initial-scale=1">
    <title>title</title>
  <meta name="author" content="name">
  <meta name="description" content="description here">
  <meta name="keywords" content="keywords,here">
  </head>
  <body>
  
  <button action="#" id="btn-link-check" data-links="https://hovermind.com|https://github.com|https://stackoverflow.com">Link Check</button>
  
  <script src="jquery-3.3.1.js" type="text/javascript"></script>
  <script type="text/javascript">
  

	function openLink(link, i) {

		console.log(`Tab-${i}: ${link}`);

		if (i > 0) {
			window.open(link, "Tab-" + i, "");
		} else {
			window.open(link, "_new", "");
		}
	}
  
	$( document ).ready(function() {
		

		$('#btn-link-check').click((e) => {
		
			e.preventDefault();
			
			console.log("link checking...");
			
			// get links
			let linkString = $('#btn-link-check').data("links");
			console.log(linkString);
				
			if(linkString === null || linkString.length < 1){
				return;
			}
			 
			let linkArray = linkString.split("|");
			// open tabs
			for(i = 0; i < linkArray.length; i++){
				openLink(linkArray[i], i);
			}
			
		});
	});
  </script>
  </body>
</html>
```
