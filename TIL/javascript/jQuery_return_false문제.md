# Javascript ) return false문제

###### 제이쿼리를 click 이벤트 안에 each문에서 return false 로 빠져 나가지지 않는 문제



### each문 사용

```javascript
$("#아이디").click(function() {
    var booleanResult = true;
    
    $(".여러개").each(function(i) {
    	var resultCnt = $(this).val();
        var maxCnt = $(this).attr("maxCnt")
        var minCnt = $(this).attr("minCnt")
        if(resultCnt.length > maxCnt) {
            alsert("글자 수를 초과하였습니다.");
            $(this).focus();
            booleanResult = false;
            return false;
        } else if(resultCnt.length == 0 || resultCnt.length == "") {
            alsert("글을 입력해주세요.");
            $(this).focus();
            booleanResult = false;
            return false;
        } else if(resultCnt.length < 50) {
            alsert("50자이상 입력해주세요");
            $(this).focus();
            booleanResult = false;
            return false;
        }
    });
    
    if(!booleanResult) retrun false;
    
});
```

###### each도 function이기 때문에 each문 안에서 return false를 하면 each문 만 빠져나가 click이벤트가 끝나지 않는다!!!!





### for문 사용

```javascript
$("#아이디").click(function() {
    var resultCnt = $(".여러개").length;
    
    for(var i = 0; i < resultCnt; i++) {
        var $this = $(".여러개").eq(i);
       	var resultCnt = $(this).val();
        var maxCnt = $this.attr("maxCnt")
        var minCnt = $this.attr("minCnt")
        if(resultCnt.length > maxCnt) {
            alsert("글자 수를 초과하였습니다.");
            $(this).focus();
            return false;
        } else if(resultCnt.length == 0 || resultCnt.length == "") {
            alsert("글을 입력해주세요.");
            $(this).focus();
            return false;
        } else if(resultCnt.length < 50) {
            alsert("50자이상 입력해주세요");
            $(this).focus();
            return false;
        }
    }    
});
```

###### each와 다르게 retrun false하면 바로 빠져 나가진다.



###### $this를 선언해서 $(this) 처럼 사용하면 덜 헷깔린다.  => 선택자는 $붙여서 구분해보자