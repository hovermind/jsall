## Iframe ready event
* Courtesy: https://stackoverflow.com/a/35317607/4802664

```js
$(function(e){
    
    $("iframe").iready(function(e){
        
       console.log("iframe is ready");

    });
});

/* 
* jQuery extension for iframe ready 
* Courtesy: Jon Freynik
* See: https://stackoverflow.com/a/35317607/4802664
*/
(function($, document, undefined) {
    $.fn["iready"] = function(callback) {
        var ifr = this.filter("iframe"),
            arg = arguments,
            src = this,
            clc = null, // collection
            lng = 50,   // length of time to wait between intervals
            ivl = -1,   // interval id
            chk = function(ifr) {
                try {
                    var cnt = ifr.contents(),
                        doc = cnt[0],
                        src = ifr.attr("src"),
                        url = doc.URL;
                    switch (doc.readyState) {
                        case "complete":
                            if (!src || src === "about:blank") {
                            	// we don't care about empty iframes
                            	ifr.data("ready", "true");
                            } else if (!url || url === "about:blank") {
                            	// empty document still needs loaded
                            	ifr.data("ready", undefined);
                            } else {
                            	// not an empty iframe and not an empty src
                            	// should be loaded
                            	ifr.data("ready", true);
                            }
                            
                            break;
                        case "interactive":
                            ifr.data("ready", "true");
                            break;
                        case "loading":
                        default:
                            // still loading
                            break;   
                    }
                } catch (ignore) {
                    // as far as we're concerned the iframe is ready
                    // since we won't be able to access it cross domain
                    ifr.data("ready", "true");
                }

                return ifr.data("ready") === "true";
            };

        if (ifr.length) {
            ifr.each(function() {
                if (!$(this).data("ready")) {
                    // add to collection
                    clc = (clc) ? clc.add($(this)) : $(this);
                }
            });
            if (clc) {
                ivl = setInterval(function() {
                    var rd = true;
                    clc.each(function() {
                        if (!$(this).data("ready")) {
                            if (!chk($(this))) {
                                rd = false;
                            }
                        }
                    });

                    if (rd) {
                        clearInterval(ivl);
                        clc = null;
                        callback.apply(src, arg);
                    }
                }, lng);
            } else {
                clc = null;
                callback.apply(src, arg);
            }
        } else {
            clc = null;
            callback.apply(this, arguments);
        }
        return this;
    };
}(jQuery, document));
```
