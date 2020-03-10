# javascript ) 대화상자



### alert()

```javascript
alert("alert test");
```

###### 단순 알림 기능



### prompt()

```javascript
prompt("promp test", "입력해주세요"); // "문구", "placholder"
```

###### 입력받을 때 사용



### confirm()

```javascript
function comfrimTest() {
    var confirmFlag = comfrim("confirm test");
    if(confirmFlag) {
        alert("확인을 선택하셨습니다.") ;
    } else {
        prompt("취소를 선택하셨습니다.","취소를 선택하신 이유를 입력해 주세요.")
    }
}
```

###### 확인 : true / 취소 : false

###### 다른 대화상자도 이런식으로 사용 가능