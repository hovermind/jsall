## Java util to convert to json string
```java
import com.fasterxml.jackson.databind.ObjectMapper;


static final ObjectMapper mapper = new ObjectMapper();
public static String convertToJsonString(Lis<T> fooList) {
	String jsonPayload = "";
	try {
		jsonPayload = mapper.writeValueAsString(fooList);
	} catch (JsonProcessingException ex) {
		//Logger.log(...);
	}
	return jsonPayload;
}
```

## Processing json payload
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>JSON Payload Processing</title>
  </head>
  <body>
  
	<button type="button" onclick="processJsonPayloadAndShowModal('thymeleaf/jsf will render json string here')">Process Payload</button>
  
	<script>

		function processJsonPayloadAndShowModal(jsonArrayAsString) {

			//console.log(jsonArrayAsString);
			let $fooDiv = $('#foo-div');
			$fooDiv.empty();

			let jsonArray = JSON.parse(jsonArrayAsString);
			let rowData;
			let tr = "";
			for (i = 0; i < jsonArray.length; i++) {
				rowData = jsonArray[i];
				//console.log(rowData);
				tr += '<tr>' +
						'<td class="td-name">' + rowData['id'] + '</td>' +
						'<td class="td-name">' + rowData['name'] + '</td>' +
						'<td class="td-number">' + rowData['nonce'] + '</td>' +
						'<tr>';
			}
			$fooDiv.html(tr);


			$('#foo-modal').modal('show');
		}
		
	</script>
  
  </body>
</html>


```
