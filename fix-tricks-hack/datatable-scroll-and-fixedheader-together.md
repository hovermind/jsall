## JS
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

## CSS
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
