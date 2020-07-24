# javascript) 시작 - 끝 날짜 validation (date에서 날짜 숫자로 바꾸기)



javascript

```javascript
$(function() {
    $("btn").click(function() {
        chkDate();
    }
});

// 날짜 validation
function chkDate() {
    var pre_start	= $("input[name=start_dt]").val(),
        pre_end		= $("input[name=end_dt]").val();
    
    if  ( pre_start != "" && pre_end != "" ) {
        var start	= Number(pre_start.replace(/-/g,"")),
            end		= Number(pre_end.replace(/-/g,""));
    
        if ( start > end ) {

            alert("종료일은 시작일과 같거나 이후로 선택하시기 바랍니다.");
            return false;

        } else {

            return true;

        }
        
    } else if ( pre_start == "" || pre_end == "" ) {

        alert("시작일과 종료일을 모두 입력해 주시기 바랍니다.");
        return false;
        
    }
    
    return true;
    
}
```

모든 - 를 지우고 싶을땐 정규식으로!





html

```html
<input type="date" name="start" max="9999-12-31">
<span class="input-group-text">~</span>
<input type="date" name="end" max="9999-12-31">
```

