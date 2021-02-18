# javascript) 반응형 javascript

```javascript
var mql = window.matchMedia("screen and (max-width: 1280px)");

mql.addListener(function(event) {
    if(event.matches) {
        console.log('1280px보다 화면이 작아졌습니다.');
    } else {
        console.log('1280px보다 화면이 커졌습니다.');
    }
});
```

