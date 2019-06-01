* Courtesy: [Stackoverflow Answer](https://stackoverflow.com/a/21159946)
* [Github link](https://gist.github.com/raincoat/6062760)
* [JS Fiddle](http://jsfiddle.net/AGEf7/)

Accessing the clipboard with plain JavaScript.
```js
function TrelloClipboard() {
    var me = this;

    var utils = {
        nodeName: function (node, name) {
            return !!(node.nodeName.toLowerCase() === name)
        }
    }
    var textareaId = 'simulate-trello-clipboard',
        containerId = textareaId + '-container',
        container, textarea

    var createTextarea = function () {
        container = document.querySelector('#' + containerId)
        if (!container) {
            container = document.createElement('div')
            container.id = containerId
            container.setAttribute('style', [, 'position: fixed;', 'left: 0px;', 'top: 0px;', 'width: 0px;', 'height: 0px;', 'z-index: 100;', 'opacity: 0;'].join(''))
            document.body.appendChild(container)
        }
        container.style.display = 'block'
        textarea = document.createElement('textarea')
        textarea.setAttribute('style', [, 'width: 1px;', 'height: 1px;', 'padding: 0px;'].join(''))
        textarea.id = textareaId
        container.innerHTML = ''
        container.appendChild(textarea)

        textarea.appendChild(document.createTextNode(me.value))
        textarea.focus()
        textarea.select()
    }

    var keyDownMonitor = function (e) {
        var code = e.keyCode || e.which;
        if (!(e.ctrlKey || e.metaKey)) {
            return
        }
        var target = e.target
        if (utils.nodeName(target, 'textarea') || utils.nodeName(target, 'input')) {
            return
        }
        if (window.getSelection && window.getSelection() && window.getSelection().toString()) {
            return
        }
        if (document.selection && document.selection.createRange().text) {
            return
        }
        setTimeout(createTextarea, 0)
    }

    var keyUpMonitor = function (e) {
        var code = e.keyCode || e.which;
        if (e.target.id !== textareaId || code !== 67) {
            return
        }
        container.style.display = 'none'
    }

    document.addEventListener('keydown', keyDownMonitor)
    document.addEventListener('keyup', keyUpMonitor)
}

TrelloClipboard.prototype.setValue = function (value) {
    this.value = value;
}

var clip = new TrelloClipboard();
clip.setValue("test");
```
