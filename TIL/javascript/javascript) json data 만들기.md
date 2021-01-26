# javascript) json data 만들기

```javascript
var list = new Array();
var idx = 0;
선택자.each(function() {
    var data = new Object();
    data.idx = idx;
    data.somethig = $(this).val();
    list.push(data);
    idx++;
});

jsonData = JSON.stringify(data);
console.log(jsonData)
```

