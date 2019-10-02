# TOC
* [Window scroll](#Window-scroll)
* [Scrollable div](#Scrollable-div)
* [Iframe](#Iframe)

## Window scroll
```js
$(window).on("scroll", function() {
	var scrollHeight = $(document).height();
	var scrollPosition = $(window).height() + $(window).scrollTop();
	if ((scrollHeight - scrollPosition) / scrollHeight === 0) {
	    // when scroll to bottom of the page
	}
});
```

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

## Iframe
```js
function setupIframeScrollToBottom({ targetIframe, 
    iframeInBootstrapModal = true, 
    bootstrapModalSelector = '.iframed-modal', 
    scrolledToBottomThreshold = 1,
    onScrolledToBottom}){
    
    let $iframe = $(targetIframe);
    let $iframeContentWindow = $(targetIframe.contentWindow);
    
    let iframeVisibleFrameHeight = 0;
    let iframeScrollHeight = 0;
    
    if(iframeInBootstrapModal){
        
        // get iframe container modal
        let $modal = $(bootstrapModalSelector);
        
        if($modal){
            
            // when modal is shown, calculate heights
            $modal.on('shown.bs.modal', function(){
                
                //console.log(bootstrapModalSelector + " is shown");
                
                //iframeContainerDivHeight = $iframeContainerDiv.outerHeight();
                iframeVisibleFrameHeight = $iframe.height();
                //console.log("iframeVisibleFrameHeight => " + iframeVisibleFrameHeight);
                
                iframeScrollHeight = targetIframe.contentDocument.body.scrollHeight;
                //console.log("iframeScrollHeight => " + iframeScrollHeight);
            });
            
            // scroll event listener
            $iframeContentWindow.on('scroll', function(e){

                let scrollTop = $(this).scrollTop();
                //console.log("scrollTop => " + scrollTop);

                let contentSeen = (iframeVisibleFrameHeight + scrollTop);
                //console.log("contentSeen => " + contentSeen);
                
                // scrolled to bottom check
                let distanceToBottom = (iframeScrollHeight - contentSeen);
                if( (contentSeen >= iframeScrollHeight) || (distanceToBottom <= scrolledToBottomThreshold) ){
                    onScrolledToBottom();
                    return;
                }
            });
        }
    } else {
        // normal iframe (iframe not in modal)
    }
}
```

#### Usage
```js
function onLoadFooIframe(iframe){

    setupIframeScrollToBottom({
        targetIframe: iframe, 
        iframeInBootstrapModal: true, 
        bootstrapModalSelector: '#fooModal', 
        scrolledToBottomThreshold: 5,
        onScrolledToBottom: function(){
            //console.log("onScrolledToBottom callback called");
            //enableButton(closeBtnSelector);
        }
    });
}
```
In page
```html
<div class="modal-body">
    <iframe onload="onLoadFooIframe(this);"
            class="form-control mh-450px" 
            id="fooIframe" 
            src="about:blank" 
            srcdoc="<rendered by view engine (i.e. razor, thymeleaf, jsf etc.)>" />
</div>
```
