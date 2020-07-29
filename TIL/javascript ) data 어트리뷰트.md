# javascript ) data 어트리뷰트



```html
<h1>data()를 이용한 어트리뷰트 사용!!</h1>
<ul id="test">
    <li data-aaa="1">내용1</li>
    <li data-aaa-bbb="2">내용2</li>
    <li data-aaa-bbb-ccc="3">내용3</li>
</ul>
```



### 호출

```javascript
$(function() {
    $("#test > li").click(function() {
        var first = $(this).data("aaa"),
            second = $(this).data("aaaBbb"),
            third = $(this).data("aaaBbbCcc");
        
        // 혹은
        var one = $(this).dataset.aaa,
            two = $(this).dataset.aaaBbb,
            three = $(this).dataset.aaaBbbCcc;
    })
});
```





### 수정 

```javascript
$(function() {
    $("#test > li").click(function() {
        $(this).data("aaa", "변경된1");
        $(this).data("aaaBbb", "변경된2"),
        $(this).data("aaaBbbCcc", "변경된2");
        
        
        $(this).dataset.aaa = "변경된1";
        $(this).dataset.aaaBbb = "변경된2";
        $(this).dataset.aaaBbbCcc = "변경된2";
    })
});
```

