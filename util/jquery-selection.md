## Select by multiple attribute
```js
let list = $('input[type=checkbox][name*="foo"]');
console.log("foo named checkboxes => " + list.length);
```

* `*` means anywhere in the name attribute `'foo'` is present

## Select not checked check boxes
```js
let list = $('input:checkbox:not(:checked)[name*="fooCheckboxList"]');
console.log("not checked => " + list.length);
```

## Exist or not Exist
jQuery object check
```js
if ($(selector).length > 0) {
    // Do something
}
```

Value check
```js
let val = $('#id');
if (val) {
    // Do something
}
```
