# javascript) toFixed 소수길이 제한..



```javascript
let num = new Number(1.232323);
alert(num.toFixed());  // string, 1
alert(num.toFixed(1)); // string, 1.2
alert(num.toFixed(2)); // string, 1.23
alert(num.toFixed(3)); // string, 1.232
 
alert(num.toPrecision()); // string, 1.232323
alert(num.toPrecision(1)); // string, 1
alert(num.toPrecision(10)); // string, 1.232323000
```

