# javascript) 새로고침



```javascript
//일반적인 새로고침
window.location.reload();
--F5 를눌러 새로고침 하는것과 동일
 
//Window 함수가 안먹힐때가 가끔 있어 필자가 주로쓰는 새로고침
location.reload();
--상위동일
 
//강제적인 새로고침
window.location.reload(true);
--캐쉬를 무시하고 서버에서 다시받아와 새로고침
 
 
//현재 자리 새로고침
history.go(0);
--0이 -1일때 이전으로 가기 처럼 현재 위치에서 다시받아옴
 
//일반적인새로고침
refresh();
--사용 범위가다름.
```



출처 : [빛나는 리오a 티스토리](https://rios.tistory.com/entry/JS-%EC%9E%8A%EC%A7%80%EB%A7%90%EA%B3%A0-%EC%93%B0%EC%9E%90-%EA%B0%81%EC%A2%85-%EC%83%88%EB%A1%9C%EA%B3%A0%EC%B9%A8-%EB%AA%A8%EC%9D%8C?category=711004)