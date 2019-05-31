* [Sample in Online Editor](https://playcode.io/329516?tabs=console&script.js&output)
* Courtesy: [Stackoverflow Answer](https://stackoverflow.com/a/46118025)

## From Data Attribute
**JSF xhtml**
```xhtml
<input id="btnCopy#{stat.index}" data-tocopy="#{templateInfo.content}" onclick="processCopyAction(this.id);" type="button" class="table-approval-btn" value="本文をコピー" />
```

**js**
```js
function copyToClipboard(text) {
    var dummy = document.createElement("textarea");
    // to avoid breaking orgain page when copying more words
    // cant copy when adding below this code
    // dummy.style.display = 'none'
    document.body.appendChild(dummy);
    dummy.value = text;
    dummy.select();
    document.execCommand("copy");
    document.body.removeChild(dummy);
}
function processCopyAction(buttonId){
  // add # for jquery
  buttonId = '#' + buttonId;
  console.log("Clicked button id => " + buttonId);
  
  let textToCopy = $(buttonId).attr('data-tocopy');
  console.log("Text to copy => " + textToCopy);
  copyToClipboard(textToCopy);
}
```

## From onclick of button
**html**
```html
<div>
  <h1 id="title">ハッサン</h1>
  <button id="copyCommandBtn" type="button" style="display:block;font-size:2em;">Copy to Clip Borad</button>
  <textarea name="content" id="source" rows="10" cols="50" >
    --------ハッサン--------ハッサン--------
    text content
    
    
    with space 
    
    
    and new line
  </textarea>

  <textarea name="target" id="target" rows="10" cols="50" placeholder="paste here"></textarea>
  
</div>
```

**js**
```js
// Try edit msg
function copyToClipboard(text) {
    var dummy = document.createElement("textarea");
    // to avoid breaking orgain page when copying more words
    // cant copy when adding below this code
    // dummy.style.display = 'none'
    document.body.appendChild(dummy);
    dummy.value = text;
    dummy.select();
    document.execCommand("copy");
    document.body.removeChild(dummy);
}

let $command = $('#copyCommandBtn');
let $source = $('#source');
let $target = $('#target');
$command.click(function(){
  let textToCopy = $source.val();
  copyToClipboard(textToCopy);
});
```
