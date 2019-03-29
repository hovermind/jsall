## Detecting browser
```js
var Browser = {"IE": 1, "Edge": 2, "Chrome": 3, "Firefox": 4, "Safari": 5, "Opera": 6, "Unknown": 7};

function detectBrowser() {

	//IE
	if (navigator.userAgent.search("MSIE") >= 0 || navigator.userAgent.search("Trident") >= 0) {
		return Browser.IE;
	}
	
	//Edge
	else if (navigator.userAgent.search("Edge") >= 0) {
		return Browser.Edge;
	}
	
	//Chrome
	else if (navigator.userAgent.search("Chrome") >= 0) {
		return Browser.Chrome;
	}
	
	//Firefox 
	else if (navigator.userAgent.search("Firefox") >= 0) {
		return Browser.Firefox;
	}
	
	//Safari
	else if (navigator.userAgent.search("Safari") >= 0 && navigator.userAgent.search("Chrome") < 0) {
		return Browser.Safari;
	}
	
	//Opera
	else if (navigator.userAgent.search("Opera") >= 0) {
		return Browser.Opera;
	}
	
	// could not detect
	return Browser.Unknown;
}
```

* Code Courtesy (copied & modified): [learningjquery.com - How to Use JavaScript to Detect Browser](https://www.learningjquery.com/2017/05/how-to-use-javascript-to-detect-browser)
* [Get user agent string of a browser](http://www.useragentstring.com/pages/useragentstring.php)
