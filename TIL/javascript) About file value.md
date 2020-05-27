# javascript) About file value





```javascript
$("input[type=file]").eq(0).val("")	<= 먹히지 않음

$("input[type=file]").eq(0).prop("defaultValue","") <= 먹힘

=> 안됨 자바스크립트 파일 정책!
```

