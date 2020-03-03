## javascript ) 페이지 벗어날때 확인창

### jquery

```javascript
var checkUnload = true;
    $(window).on("beforeunload", function(){
        if(checkUnload) return "이 페이지를 벗어나면 작성된 내용은 저장되지 않습니다.";
    });
```





### submit 부분

```javascript
$("#saveBtn").on("click", function(){
    checkUnload = false;
    $("#saveForm").submit();
});
```





출처:  [스토브 훌로구](https://stove99.tistory.com/128?category=360125)

