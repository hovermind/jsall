## Scrollable div
```js
function setupScrollableDivScrolledToBottom({scrollableDivSelector, scrollToBottomThreshold, onScrolledToBottom}){
    
    //console.log("setScrollableDivScrollEvent()");

    let $scrollableDiv = $(scrollableDivSelector);
    if($scrollableDiv){

        $scrollableDiv.scroll(function(e) {
        
            let $scrollDiv = $(this);
            
            // NOTE: 
            // visibleHeight & contentScrollHeight should be calculated outside of scroll callback
            // scrollableDiv is in a modal, that's why calculating inside here
            //
            // Better solution:
            //   1. you can listen to shown.bs.modal => calculate visibleHeight & contentScrollHeight there (effective)
            //   2. call setupScrollableDivScrolledToBottom() from shown.bs.modal event listener 
            //     (use: $scrollableDiv.off('scroll').on('scroll') since every time modal is shown, the event will be registered again and again)
            let visibleHeight = $scrollDiv.outerHeight();
            let contentScrollHeight = $scrollDiv[0].scrollHeight;
            
            let scrollTop = $scrollDiv.scrollTop();
            //console.log("visibleHeight => " + visibleHeight);
            //console.log("contentScrollHeight => " + contentScrollHeight);
            //console.log("scrollTop => " + scrollTop);

            let contentSeen = (visibleHeight + scrollTop);
            //console.log("contentSeen => " + contentSeen);
            
            let distanceToBottom = (contentScrollHeight - contentSeen);
            if((contentSeen >= contentScrollHeight) || (distanceToBottom <= scrollToBottomThreshold)){
               onScrolledToBottom();
               return;
            }
        });
    }
}
```

#### Usage
```js
// close button activation
setupScrollableDivScrolledToBottom({
    scrollableDivSelector: '#fooDiv', 
    scrollToBottomThreshold: 5, 
    onScrolledToBottom: function(){
        //console.log("srolled to bottom");
        enableButton('.close-btn');
    }
});
```
