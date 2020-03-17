# javascript ) 체크박스에서 선택된 값 가져오기

```javascript
//checkbox의 name값이 이름이면서 체크되어 있는 함수를 체크하여 호출함.
 
 
$("input[name=이름]:checked").each(function() {
  var test = $(this).val(); 

  alert("벨류값확인 : " + test);


}
```



출처 : [빛나는 리오a 티스토리](https://rios.tistory.com/entry/Jquery-%EC%B2%B4%ED%81%AC%EB%B0%95%EC%8A%A4%EC%9D%98-%EC%84%A0%ED%83%9D%EB%90%9C-Value-%EA%B0%80%EC%A0%B8%EC%98%A4%EA%B8%B0)