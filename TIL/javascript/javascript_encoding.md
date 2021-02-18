# javascript) encoding

```javascript
encodeURIComponent(str)
```

톰켓에서 알아서 디코딩 해줌. 디코딩을 직접하고싶다면

```javascript
encodeURIComponent(encodeURIComponent(str))
```

위와같이 두번 하고 디코딩 해준다. 

* 인코딩 할 때  UTF-8로 인코딩 하기 때문에 디코딩할때 설정을 UTF-8로 꼭 해줘야한다. 아님 한글 꺠짐.