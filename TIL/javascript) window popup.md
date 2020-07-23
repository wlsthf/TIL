# javascript) window popup



#### 부모 창에서

```javascript
// 팝업 열기
$("#btn_팝업").click(function() {		
    // 팝업의 주소
    var url = "/팝업의 주소";
    //팝업의 고유 식별 이름 ( 두개의 팝업창이 열리지 않도록 / 중복된 팝업창 이름x)
    var name = "popup_팝업";
    //팝업 옵션 지정
    var option = "width = 1200, height = 700, top = 100, left = 200, location = no"
    //팝업 오픈
    window.open(url, name, option);			
});
```





#### 팝업창에서

```javascript
// 닫기버튼 클릭
$("#btn_닫기").click(function() {
    // 팝업 close
    window.close();		

    // 자신의 팝업을 오픈한 부모 도큐먼트에 접근 -> $(opener.document).find("#")
    $(opener.document).find("#아이디").html("블라블라");
});
```

