# javascript) Object 선언과 활용



```javascript
/* object 선언 방법 */
let obj = new Object();
// let obj = {};

/* object key, value 설정 방법 */
// 방법1
obj = {
    key1: 111,
    key2: 222
}
// 방법2
obj.key3 = 333;
obj['key4'] = 444; 

// 방법3 ( 동적 )
let str = 'key5';
obj[str] = 555;

// 방법4 ( 함수 )
function Fn (key1, key2) {
	this.key1 = key1;
   	this.key2 = key2;
}
let obj2 = new Fn(1111, 2222);

// 키들을 가져오는 방법
let objKeyArr = Object.keys(obj);
console.log('길이: ' + objKeyArr.length); // 길이: 6

for ( let key in obj2 ) {
    console.log('키:' + key + ', 값: ' + obj2[key]);	// 동적으로 값을 가져오는 방법. obj2.key로 하면 오류남!!
}
// 키: key1, 값: 1111
// 키: key2, 값: 2222
```

