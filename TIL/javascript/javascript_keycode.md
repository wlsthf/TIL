# javascript) keycode



keyup, keydown, presskey, change 등 이용

| 백스페이스 | 8    |
| ---------- | ---- |
| tab        | 9    |
| enter      | 13   |
| shift      | 16   |
| ctrl       | 17   |
| alt        | 18   |
| esc        | 27   |



참고 [더 많은 자료](https://blog.naver.com/wizardry0629/222066976020)

```javascript
// 엔터로 작동
$("인풋").keyup(function(){
    if ( event.keyCode==13 ) {
        $('검색버튼').click();
    }
});
```

