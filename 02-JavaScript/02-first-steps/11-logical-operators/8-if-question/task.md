# A question about "if"
_`Importance: 5`_

Which of these `alert`s are going to execute?

What will the results of the expressions be inside `if(...)`?

```js
if (-1 || 0) alert( 'first' );
if (-1 && 0) alert( 'second' );
if (null || -1 && 1) alert( 'third' );
```

