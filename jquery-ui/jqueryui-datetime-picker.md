# TOC
* [Simple Datetime Picker](#Simple-Datetime-Picker)
* [Datetime picker using utility function](#Datetime-picker-using-utility-function)

## Datetime Picker
* Courtesy: [trentrichardson.com](https://trentrichardson.com/examples/timepicker/#basic_examples)
* JS and CSS (cdnjs):
  * [jquery](https://cdnjs.com/libraries/jquery)
  * [jquery-ui](https://cdnjs.com/libraries/jqueryui)
  * [jquery-ui-timepicker-addon](https://cdnjs.com/libraries/jquery-ui-timepicker-addon)


## Simple Datetime Picker
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
Note:    
`<script src="./datepicker-ja.js"></script>` => create a js file and copy localized script from https://github.com/jquery/jquery-ui/tree/master/ui/i18n

## Localization By Setting
```js
// region japan
$.timepicker.regional['ja'] = {
	timeOnlyTitle: '時間を選択',
	timeText: '時間', // 時間 text is not needed
	hourText: '時',
	minuteText: '分',
	secondText: '秒',
	millisecText: 'ミリ秒',
	microsecText: 'マイクロ秒',
	timezoneText: 'タイムゾーン',
	currentText: '現時刻',
	closeText: '閉じる',
	timeSuffix: '',
	amNames: ['午前', 'AM', 'A'],
	pmNames: ['午後', 'PM', 'P'],
	isRTL: false
};

// set default region (will be applied to all picker in same context)
$.timepicker.setDefaults($.timepicker.regional['ja']);

$picker.datetimepicker({
  ... : ...
});
```

## Datetime picker using utility function
```js
function isEmpty(x){
  return (typeof x === "undefined" || !x);
}

var regionSettingsJapan = {
	timeOnlyTitle: '時間を選択',
	timeText: '時間', // 時間 text is not needed
	hourText: '時',
	minuteText: '分',
	secondText: '秒',
	millisecText: 'ミリ秒',
	microsecText: 'マイクロ秒',
	timezoneText: 'タイムゾーン',
	currentText: '',
	closeText: '閉じる',
	timeSuffix: '',
	amNames: ['午前', 'AM', 'A'],
	pmNames: ['午後', 'PM', 'P'],
	isRTL: false
};
		
function beforeShowCallbackForClearButtonJP(input, obj){
	setTimeout(function() {
	var buttonPane = $( input ).datepicker( "widget" ).find( ".ui-datepicker-buttonpane" );        
	$("#BCL").hide();
	$("#BTDY").hide();
	$("<button>", {
		  text: "クリアする",
		  click: function() {
			$(input).val('');                
		  }
	}).addClass('ui-state-default ui-corner-all').appendTo( buttonPane );
	}, 1);
}


function activateCalenderWidget(fieldSelector, calenderSettings){
	
	'use strict'

	let defaultSelector = '.jq-ui-calendar';
	if(!fieldSelector){
		console.log("using defaultSelector: " + defaultSelector);
		fieldSelector = defaultSelector;
	}
	
	/*
	* get object array
	* for id: $dateInputFields.length = 1
	* for class: $dateInputFields.length >= 1
	*/
	let $dateInputFields =  $(fieldSelector);
	if(!$dateInputFields || $dateInputFields.length < 1){
		console.log("none of the input fields using '" + fieldSelector + "'");
		return;
	}else{
		console.log("nunber of date/datetime input fields: " + $dateInputFields.length);
	}

	// initializing default values
	let dateFormat = 'yy/mm/dd';
	let timeFormat = 'HH:mm';
	let controlType = 'select';
	let numberOfMonths = 3;
	let showCurrentAtPos = 1;
	let showButtonPanel = true;
	let oneLine = true;
	let regionCode = 'ja';
	let regionSettings = regionSettingsJapan;
	let beforeShowCallback = beforeShowCallbackForClearButtonJP;
	
	// normalizing setting values
	if(!calenderSettings || $.isEmptyObject(calenderSettings)){ // when calenderSettings is not set
		console.log("calenderSettings is not set, using default Settings");
	} else {

		// dateFormat
		if( !isEmpty(calenderSettings.dateFormat) ){
			dateFormat = calenderSettings.dateFormat;
		}
		
		// timeFormat
		if( !isEmpty(calenderSettings.timeFormat) ){
			timeFormat = calenderSettings.timeFormat;
		}
		
		// controlType (i.e. 'select')
		if( !isEmpty(calenderSettings.controlType) ){
			controlType = calenderSettings.controlType;
		}
		
		// numberOfMonths (i.e. 1, 3)
		if( !isEmpty(calenderSettings.numberOfMonths) ){
			numberOfMonths = calenderSettings.numberOfMonths;
		}
		
		// showCurrentAtPos (0, 1)
		if( !isEmpty(calenderSettings.showCurrentAtPos) ){
			if(!isEmpty(calenderSettings.numberOfMonths) && numberOfMonths <= 1){
				showCurrentAtPos = 0;
			}else{
				showCurrentAtPos = calenderSettings.showCurrentAtPos;
			}
		}

		// showButtonPanel
		if( !isEmpty(calenderSettings.showButtonPanel) ){
			showButtonPanel = calenderSettings.showButtonPanel;
		}
		
		// oneLine
		if( !isEmpty(calenderSettings.oneLine) ){
			oneLine = calenderSettings.oneLine;
		}

		// region
		if( !isEmpty(calenderSettings.region) ){
		
			// region code
			if( !isEmpty(calenderSettings.region.regionCode) ){
				regionCode = calenderSettings.region.regionCode;
			}
			
			// regional text settings
			if( !isEmpty(calenderSettings.region.regionSettings) ){
				regionSettings = calenderSettings.region.regionSettings;
			}
		}

		// beforeShowCallback
		if( !isEmpty(calenderSettings.beforeShowCallback) ){
			beforeShowCallback = calenderSettings.beforeShowCallback;
		}
	}
	
	// set default region for calender
	$.timepicker.regional[regionCode] = regionSettings;
	$.timepicker.setDefaults($.timepicker.regional[regionCode]);
	
	let calenderSettingsToApply = {
		dateFormat: dateFormat,
		timeFormat: timeFormat,
		controlType: controlType, // for time
		numberOfMonths: numberOfMonths,
		showCurrentAtPos: showCurrentAtPos,
		changeYear: true,
		changeMonth: true,
		showButtonPanel: showButtonPanel,
		oneLine: oneLine,
		beforeShow: beforeShowCallback,
	};
	
	console.log("calenderSettingsToApply : " + JSON.stringify(calenderSettingsToApply, null, 2));
	
	$dateInputFields.datetimepicker(calenderSettingsToApply);
}

// using activateCalenderWidget
$(function(){
	activateCalenderWidget('', {});
});
```
