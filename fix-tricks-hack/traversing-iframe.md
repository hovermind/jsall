# Traversing iframe

## iframe ready event: 
See: https://github.com/hovermind/jsall/blob/master/fix-tricks-hack/iframe-ready-event.md

## traverse
For example - get anchor tags and add target = _blank
```js
$(function(e){
    
    $("iframe").iready(function(e){
        
        console.log("iframe is ready");

        // get anchor tags from iframe
        let $iframe = $(this);
        let $anchors = $iframe.contents().find("body a");
        let $a = $();
        for(let i = 0; i < $anchors.length; i++){
            
            $a = $($anchors[i]);
            
            if(!$a.attr('href')){
              //console.log($a.prop('outerHTML') + " does not have href");
              $a.attr('href', '')
            }
            // set target = _blank
            $a.attr('target', '_blank')
        }
    });
});
```
