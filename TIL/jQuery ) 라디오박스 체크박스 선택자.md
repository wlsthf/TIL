# jQuery ) 라디오박스/ 체크박스 선택자

### 라디오 버튼

```javascript
var $radio = $("input[name=이름입력]:checked");
var radio = $("input[name=이름입력]:checked").val();

// 라디오 미선택 검사
if ( radio == undefined ) {
    
    alert("라디오 버튼을 선택하지 않았습니다.");
    return false;
    
}
```



### 체크박스

```javascript
var $check = $("input:checkbox[name=act_type]");
var check = $("input:checkbox[name=act_type]").is(":checked");
```

