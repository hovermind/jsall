## Better than method 1 & 2 : https://stackoverflow.com/a/57750872/4802664

## Method 1
##### JS
```js
$(function () {

	$("#tableId").DataTable({
		... ... : ... ...
		scrollX: true,
		fixedHeader: true,
		"initComplete": function (settings, json) {

			$('.dataTables_scrollBody').on('scroll', function () {
				$('.dataTables_scrollHeadInner').scrollLeft($(this).scrollLeft());
			});

			$(document).on('scroll', function () {

				var scroll_pos = $(this).scrollTop();
				var margin = 74; // Adjust it to your needs
				var cur_pos = $('.dataTables_scrollHeadInner').position();
				var header_pos = cur_pos.top;

				if (scroll_pos < margin)
					var header_pos = margin - scroll_pos;
				else
					header_pos = 0;

				$('.dataTables_scrollHeadInner').css({"top": header_pos});
			});
		}
	});
});
```

Auto margin adjustment
```js
// get initial Y
let yPositionScrollHeadInner = window.scrollY + document.querySelector('.dataTables_scrollHeadInner').getBoundingClientRect().top;
//console.log("adjusment mergin: " + yPositionScrollHeadInner);

// ==>> use yPositionScrollHeadInner
var margin = yPositionScrollHeadInner; // Adjust it to your needs
```

##### CSS
```css
table.dataTable.fixedHeader-floating {
     display: none !important; /* Hide the fixedHeader since we dont need it*/
}
 
.dataTables_scrollHeadInner{
    margin-left: 0px;
    width: 100% !important;
    position: fixed;
    display: block;
    overflow: hidden;
    margin-right: 30px;
    background: white;
    z-index: 1000;
}
 
.dataTables_scrollBody{
    padding-top: 60px;
}
```

## Method 2 - trick by window scroll
If method 1 does not work, use window sroll instead
```js
// on init complete
function onDataTableInitComplete(settings, json) {

    // override width of the table
    let $dataTables = $('.dataTable');
    if($dataTables.length){
      $dataTables.css('width', 'max-content');
    }

    // onscroll window horizontally -> set body with: max-content
    $(window).on('scroll', function() {
        let $body = $('body');
        let horizontalScroll = $(this).scrollLeft();
        //console.log("Horizontally scrolled: " + horizontalScroll);
        if(horizontalScroll > 0){
            $body.css('width', 'max-content'); //$body.css('width', '100%');
        } else {
            $body.css('width', 'auto'); //$body.prop("style").removeProperty("width");
        }
    });
}

// data table
$(function() {
    let dt = $('#example');
    dt.DataTable({
	  fixedHeader: true,
	  //scrollX: true,
	  pageLength: 100,
	  initComplete: onDataTableInitComplete
    });
});
```
