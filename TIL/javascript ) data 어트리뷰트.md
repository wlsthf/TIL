# javascript ) data 어트리뷰트



```html
<h1>data()를 이용한 어트리뷰트 사용!!</h1>
<ul id="test">
    <li data-aaa="1">내용1</li>
    <li data-aaa-bbb="2">내용2</li>
    <li data-aaa-bbb-ccc="3">내용3</li>
</ul>
```



```javascript
$(function() {
    $("#test > li").click(function() {
        var first = data("aaa"),
            second = data("aaaBbb"),
            third = data("aaaBbbCcc");
    })
})
```

