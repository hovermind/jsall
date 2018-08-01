```
define(["jquery"], function($){
	
	'use strict';
	
	let response = {
		isError : false,
		message : '',
		data : ''
	};

	let ajaxHelper = {
		
		FetchData: ({method = 'GET', uri, payload = '', dataType = 'json', callback}) => {
			
			let $call;
			
			if(method == 'GET'){
				
				$call = $.ajax(uri, {
					type : method,
					contentType : 'application/json', // send as
					dataType : dataType, // return as
				});
				
			} else {
				
				$call = $.ajax(uri, {
					type : method,
					contentType : 'application/json', // send as
					dataType : dataType, // return as
					data : payload
				});
			}

			$call.done(data => {
				//console.log(data);
				
				response.isError = false;
				response.message = 'Data fetched!';
				response.data = data;
				
				callback(response);
				
			}).fail(error => {
				//console.log(error);
				//console.log(error.statusText);
				
				response.isError = true;
				response.message = error.statusText;
				response.data = '';

				callback(response);
			});
		}
	};
	
	return ajaxHelper;
});
```
