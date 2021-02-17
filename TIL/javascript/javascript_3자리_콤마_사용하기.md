# javascript ) 3자리 콤마 사용하기



### javascript 이용

```javascript
function comma(num) {
    var len, point, str; 
       
    num = num + ""; 
    point = num.length % 3 ;
    len = num.length; 
   
    str = num.substring(0, point); 
    while (point < len) { 
        if (str != "") str += ","; 
        str += num.substring(point, point + 3); 
        point += 3; 
    } 
     
    return str;
 
}
```





### 정규식 이용

```javascript
function numberWithCommas(x) {
    return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
}
```



[출처 : 물고기 개발자의 블로그]([https://epthffh.tistory.com/entry/%ED%86%B5%ED%99%94%ED%98%95%EC%8B%9D-3%EC%9E%90%EB%A6%AC-%EC%BD%A4%EB%A7%88-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0-%EC%98%88%EC%A0%9C?category=687610](https://epthffh.tistory.com/entry/통화형식-3자리-콤마-사용하기-예제?category=687610))