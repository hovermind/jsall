## Show datetime picker below input field and inside viewport
```js

$('#date-picker').datepicker({
	... : ...
	beforeShow: function(input, inst){
		// force picker to show below input field and inside viewport
		showCalendarBelowInputField($this, input, inst);
	}
});

function showCalendarBelowInputField($this, input, inst){
    
  // show calendar below the input field and inside view port
  setTimeout( function () {

      let $inputField =  $(input);

      let inputFieldHorizontalOffset = $inputField.offset().left;
      let datePickerWidth = $('#ui-datepicker-div').outerWidth();
      let viewPortWidthWithoutScrollbar = document.body.clientWidth;
      console.log("inputFieldHorizontalOffset => " + inputFieldHorizontalOffset);
      console.log("datePickerWidth => " + datePickerWidth);
      console.log("viewPortWidthWithoutScrollbar => " + viewPortWidthWithoutScrollbar);

      let positionTop = $inputField.offset().top + $inputField.outerHeight(false);
      let positionLeft = inputFieldHorizontalOffset;

      let isDatepickerInsideViewPort = ( (inputFieldHorizontalOffset + datePickerWidth) < viewPortWidthWithoutScrollbar );
      if(!isDatepickerInsideViewPort){
                // force datepicker to reposition inside view port
                positionLeft = viewPortWidthWithoutScrollbar - datePickerWidth;
                console.log("datepicker is outside of viewport");
      }

      console.log("positionLeft => " + positionLeft);
      inst.dpDiv.css({
          top: positionTop,
          left: positionLeft
      });
        
    }, 0);
}
```
