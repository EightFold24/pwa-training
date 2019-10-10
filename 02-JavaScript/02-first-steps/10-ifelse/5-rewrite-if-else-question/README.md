# Rewrite 'if..else' into '?'
_`Importance: 3`_

Rewrite `if..else` using multiple ternary operators `'?'`.

For readability, it's recommended to split the code into multiple lines.

```js
let message;

if (login == 'Employee') {
  message = 'Hello';
} else if (login == 'Director') {
  message = 'Greetings';
} else if (login == '') {
  message = 'No login';
} else {
  message = '';
}
```
