# javascript) 여러라인의 삼항연산자

여러줄의 삼항연산지는 쓸일은 없을 것 같지만 누가 쓴 코드 해석을 위해 정리함

이푸문

```javascript
if ( true ) {
    console.log("참참참");
} else {
    console.log("그짓");
}
```



삼항연산자

```javascript
true? console.log("참참참") : console.log("그짓"); 
```



여러 줄 짜리 삼항 연산자

```javascript
true?
	(console.log("참"), console.log("참참"))
:
	(console.log("그"), console.log("짓"))
```



혹은

```javascript
true?
	function() {
		console.log("참");
		console.log("참");
	}()
:
	function() {
		console.log("그");
		console.log("짓");
	}()
```

