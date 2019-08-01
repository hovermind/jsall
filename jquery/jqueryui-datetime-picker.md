## Basic Datetime Picker
* Courtesy: [trentrichardson.com](https://trentrichardson.com/examples/timepicker/#basic_examples)
* JS and CSS (cdnjs):
  * [jquery](https://cdnjs.com/libraries/jquery)
  * [jquery-ui](https://cdnjs.com/libraries/jqueryui)
  * [jquery-ui-timepicker-addon](https://cdnjs.com/libraries/jquery-ui-timepicker-addon)

`foo.html`
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>title</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/4.3.1/css/bootstrap.min.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/jqueryui/1.12.1/jquery-ui.min.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/jqueryui/1.12.1/themes/base/theme.min.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/jquery-ui-timepicker-addon/1.6.3/jquery-ui-timepicker-addon.min.css">
  
    <style type="text/css">
     .row {
       // background: #f8f9fa;
       margin-top: 20px;
     }
    </style>

  </head>
  <body>
  
	<div role="main" class="container">
	  <div class="form-group row">
		<label class="col">Period: </label>
		<div class="col" >
		 <input type="text" id="from" name="from" value=''/> 
		</div>
		<label class="col text-center">～</label>
		<div class="col">
		 <input type="text" id="to" name="to" value=''/>
		</div>
		<div class="col">

		</div>
	  </div>
	</div>
  
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jqueryui/1.12.1/jquery-ui.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery-ui-timepicker-addon/1.6.3/jquery-ui-timepicker-addon.min.js"></script>

  <script type="text/javascript">

  function initDateTimePicker($pickerObj, params){
      $pickerObj.datetimepicker({
      dateFormat: "yy/mm/dd",
      timeFormat: 'HH:mm',
      numberOfMonths: 3,
      showCurrentAtPos: 1,
      showButtonPanel: true,
      changeYear: true,
      changeMonth: true,
      controlType: 'select',
      oneLine: true
    });
  }

  $(function(){
    initDateTimePicker($('#from'), {});
    initDateTimePicker($('#to'), {});
  });
   
  </script>
  </body>
</html>
```
  
## Localization
* can be localized by using scripts or setting
* jquery-ui has region specific scripts that will localize date picker only (need seperate script/setting for time add-on)
* if region specific scripts do not cover all texts, then you can provide your custon text using setting

## Localization By Script
* localizing datepciker: https://stackoverflow.com/questions/494958/how-do-i-localize-the-jquery-ui-datepicker
* localizing timepicker: load localized script (i.e. `jquery-ui-timepicker-addon-ja.js`) after `jquery-ui-timepicker-addon.js`

Scripts
```html
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jqueryui/1.12.1/jquery-ui.min.js"></script>
  <script src="./datepicker-ja.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery-ui-timepicker-addon/1.6.3/jquery-ui-timepicker-addon.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery-ui-timepicker-addon/1.6.3/i18n/jquery-ui-timepicker-ja.js"></script>
```
Note: `<script src="./datepicker-ja.js"></script>` => copy localized script from https://github.com/jquery/jquery-ui/tree/master/ui/i18n and then create a js file

## Localization By Setting