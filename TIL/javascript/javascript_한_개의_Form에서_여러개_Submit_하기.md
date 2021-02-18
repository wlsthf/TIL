# 한 개의 Form에서 여러개 Submit 하기



## 함수생성

```javascript
$("#update").click(function () {
       $("form").attr("action", "/manage/update");
});
 
$("#delete").click(function () {
       $("form").attr("action", "/manage/delete");
});
```



## 함수생성  by if

```javascript
<input type="submit" value="수정" onclick='btn_click("update");'>
<input type="submit" value="삭제" onclick='btn_click("delete");'>
 
<script>
    function btn_click(str){                             
        if(str=="update"){                                 
            frm1.action="/manage/update";      
        } else if(str=="delete"){      
            frm1.action="/manage/delete";      
        }  else {
            //...
        }
    }
</script>
```





## HTML에 작성

```html
<form method="post" name="form">
    <input type="submit" value="update" onclick="javascript: form.action='/manage/update';"/>
    <input type="submit" value="delete" onclick="javascript: form.action='/manage/delete';"/>
</form>
```





## name & value

```html
<input type="submit" name="action" value="update" />
<input type="submit" name="action" value="delete" />
```





## formation 속성사용 (HTML5)

```html
<input type="submit" value="수정" formaction="/manage/update">
<input type="submit" value="삭제" formaction="/manage/delete">
```

