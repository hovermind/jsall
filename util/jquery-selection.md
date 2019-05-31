## Select by multiple attribute
```js
let list = $('input[type=checkbox][name*="foo"]');
console.log("foo named checkboxes => " + list.length);
```

* `*` means anywhere in the name attribute `'foo'` is present

## Select not checked check boxes
```js
let list = $('input:checkbox:not(:checked)[name*="checkList"]');
console.log("not checked => " + list.length);
```
