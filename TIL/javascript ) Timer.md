# javascript ) Timer

```javascript
// 1초 뒤 test() 함수 실행
setTimeout("test()", 1000);

// 1초마다 test() 함수 실행
setInterval("test()", 1000);

function test(){
    alert("성공!");
}

```



### 다른 방식

```java
setTimeout(function() {
    alert("성공!");
}, 1000);

setInterval(function() {
    altert("성공");
}, 1000);

```

