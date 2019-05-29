## jQuery code to remove wildcard css class
```js
/**
* /pattern/flags
* new RegExp(pattern[, flags])
* new RegExp(/ab+c/, 'i');
* new RegExp('ab+c', 'i');
*
* A regular expression in js might be var pattern = /\d{1}/ , no quotations needed,
* but once you convert to string, it would become var patternString = "\\d{1}"
* https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp
* https://stackoverflow.com/questions/1695633/how-to-pass-a-variable-into-regex-in-jquery-javascript
* https://stackoverflow.com/questions/5172183/javascript-new-regexp-from-string
*/
function removeWildcardClass($element, mword){
	let pattern = mword + '-\\b\\S+';
	$element.removeClass(function (index, className) {
		return (className.match(pattern, 'gi') || []).join(' ');
	});
}
```
